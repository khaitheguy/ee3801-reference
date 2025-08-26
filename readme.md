# EE3801 Reference Sheet

## AWS Commands

### ParallelCluster
Edit the cluster configuration:

`nano ~/cluster-config.yaml`

Creating a cluster:

`pcluster create-cluster -c ~/cluster-config.yaml -n MyCluster01`

Listing down all clusters:

`pcluster list-clusters`

Logging into a cluster using SSH:

`pcluster ssh -i ~/MyKeyPair.pem -n MyCluster01`

Taking a snapshot:

`update_snapshot.sh data 2 MyCluster01`

Checking snapshot status:

`aws ec2 describe-snapshots --owner-ids self --query 'Snapshots[]`

Deleting a cluster:

`pcluster delete-cluster -n MyCluster01`