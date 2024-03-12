# elasticsearch-data-migration
elasticsearch data migration steps and tools


We can use elasticdump to take the backup and restore it, We can move data from one server/cluster to another server/cluster.

1. Commands to move one index data from one server/cluster to another using elasticdump.

# Copy an index from production to staging with analyzer and mapping:
```console
elasticdump \
  --input=http://production.es.com:9200/my_index \
  --output=http://staging.es.com:9200/my_index \
  --type=analyzer
elasticdump \
  --input=http://production.es.com:9200/my_index \
  --output=http://staging.es.com:9200/my_index \
  --type=mapping
elasticdump \
  --input=http://production.es.com:9200/my_index \
  --output=http://staging.es.com:9200/my_index \
  --type=data
```

2. Commands to move all indices data from one server/cluster to another using multielasticdump.

Backup
```console
multielasticdump \
  --direction=dump \
  --match='^.*$' \
  --limit=10000 \
  --input=http://production.es.com:9200 \
  --output=/tmp
```

Restore
```console
multielasticdump \
  --direction=load \
  --match='^.*$' \
  --limit=10000 \
  --input=/tmp \
  --output=http://staging.es.com:9200
```

Note:

If the --direction is dump, which is the default, --input MUST be a URL for the base location of an ElasticSearch server (i.e. http://localhost:9200) and --output MUST be a directory. Each index that does match will have a data, mapping, and analyzer file created.

For loading files that you have dumped from multi-elasticsearch, --direction should be set to load, --input MUST be a directory of a multielasticsearch dump and --output MUST be a Elasticsearch server URL.

The 2nd command will take a backup of settings, mappings, template and data itself as JSON files.

The --limit should not be more than 10000 otherwise, it will give an exception.

Get more details [here](https://github.com/elasticsearch-dump/elasticsearch-dump).
