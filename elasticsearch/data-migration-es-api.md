# Infrastructure Data Migration Procedure

## Migrating Elasticsearch Cluster:

### Step 1: Backup Elasticsearch Data
1. Stop writes to the Elasticsearch cluster.
2. Use Elasticsearch's Snapshot and Restore feature to create a backup.
   ```bash
   curl -X PUT "localhost:9200/_snapshot/my_backup" -H 'Content-Type: application/json' -d'
   {
     "type": "fs",
     "settings": {
       "location": "/path/to/your/backup/location"
     }
   }'

### Step 2: Transfer Backup to New Infrastructure
1. Copy the backup data from the old infrastructure to the new infrastructure.
    ```bash
    scp -r /path/to/your/backup/location new_server:/path/to/restore/location

### Step 3: Restore Elasticsearch Data on New Cluster
1. Install and set up Elasticsearch on the new infrastructure.
2. Restore the backup on the new Elasticsearch cluster.
    ```bash
    curl -X POST "localhost:9200/_snapshot/my_backup/snapshot_1/_restore"