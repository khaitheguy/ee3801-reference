# EE3801 Reference Sheet

## AWS Commands

### ParallelCluster
Edit the cluster configuration:

```bash
nano ~/cluster-config.yaml
```

Creating a cluster:

```bash
pcluster create-cluster -c ~/cluster-config.yaml -n MyCluster01
```

Check status/IP address of cluster

```bash
pcluster describe-cluster -n MyCluster01
```

Listing down all clusters:

```bash
pcluster list-clusters
```

Logging into a cluster using SSH:

```bash
pcluster ssh -i ~/MyKeyPair.pem -n MyCluster01
```

Taking a snapshot:

```bash
update_snapshot.sh data 2 MyCluster01
```

Checking snapshot status:

```bash
aws ec2 describe-snapshots --owner-ids self --query 'Snapshots[]'
```

Deleting a cluster:

```bash
pcluster delete-cluster -n MyCluster01
```

### EC2 Shell
Activate conda:

```bash
miniconda3/bin/conda init
```

Reload bash:

```bash
source ~/.bashrc
```

Activate env1:

```bash
conda activate env1
```

Copy AWS credentials:

```bash
cp -r /data/aws ~/.aws
```

Submit job:
```bash
sbatch file.sh
```

Check job queue:
```bash
squeue
```

Cancel all jobs:
```bash
scancel --user=ec2-user
```

Run on compute node:
```bash
srun --pty /bin/bash
```

## General
### Useful keyboard shortcuts
- `Ctrl+R` Reverse search
- `Ctrl+L` Clear terminal
- `Ctrl+D` Exit
- `Ctrl+C` Interrupt command
- `Tab` Autocomplete filename