# Infrastructure Data Migration Procedure

## Migrating Consul Cluster:

### Step 1: Backup Consul Data
1. Connect to the Consul cluster and take a snapshot.
   ```bash
   consul snapshot save /path/to/your/snapshot

### Step 2: Transfer Snapshot to New Infrastructure
1. Copy the Consul snapshot from the old infrastructure to the new infrastructure.
   ```bash
    scp /path/to/your/snapshot new_server:/path/to/restore/location

### Step 3: Restore Consul Data on New Cluster
1. Install and set up Consul on the new infrastructure.
2. Restore the snapshot on the new Consul cluster.
   ```bash
    consul snapshot restore /path/to/your/snapshot
