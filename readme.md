# EE3801 Reference Sheet

## AWS Commands

### ParallelCluster
Edit the cluster configuration:

`nano ~/cluster-config.yaml`

Creating a cluster:

```bash
pcluster create-cluster -c ~/cluster-config.yaml -n MyCluster01
```

Check status/IP address of cluster

`pcluster describe-cluster -n MyCluster01`

Listing down all clusters:

`pcluster list-clusters`

Logging into a cluster using SSH:

`pcluster ssh -i ~/MyKeyPair.pem -n MyCluster01`

Taking a snapshot:

`update_snapshot.sh data 2 MyCluster01`

Checking snapshot status:

`aws ec2 describe-snapshots --owner-ids self --query 'Snapshots[]'`

Deleting a cluster:

`pcluster delete-cluster -n MyCluster01`

### EC2 Shell
Activate conda:

`miniconda3/bin/conda init`

Reload bash:

`source ~/.bashrc`

Activate env1:

`conda activate env1`

Copy AWS credentials:

`cp -r /data/aws ~/.aws`

## General
### Useful keyboard shortcuts
- `Ctrl+L` Clear terminal
- `Ctrl+D` Exit
- `Ctrl+C` Interrupt command
- `Tab` Autocomplete filename