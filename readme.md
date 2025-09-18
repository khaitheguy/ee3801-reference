# EE3801 Reference Sheet

## Quick Reference
1. [Create cluster](#parallelcluster)
2. [Set up conda env](#ec2-shell)
3. [Slurm commands](#slurm-commands)
4. [Bash commands](#bash-commands)

## ParallelCluster
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
./update_snapshot.sh data 2 MyCluster01
```

Checking snapshot status:

```bash
aws ec2 describe-snapshots --owner-ids self --query 'Snapshots[]'
```

Deleting a cluster:

```bash
pcluster delete-cluster -n MyCluster01
```
[Back to Top](#quick-reference)

## EC2 Shell
Activate conda:

```bash
/data/miniconda3/bin/conda init
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

**Do all the above using my custom script:**

```bash
source /data/src/PyHipp/auto.sh
```

Configure Git:

```bash
git config --global core.editor "nano"
git config --global user.name "[Name]"
git config --global user.email "[Email]"
```
[Back to Top](#quick-reference)

## Slurm Commands

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

[Back to Top](#quick-reference)

## Misc
Publish a notification through SNS:
```bash
aws sns publish --topic-arn arn:aws:sns:ap-southeast-1:123456789012:awsnotify --message "Message"
```

Fix for Node.js:
```bash
nvm install 16.9.1
```
[Back to Top](#quick-reference)

## General
### Bash Commands
Search through current directory for filename
```bash
find . -name "channel*"
```

Sort output of a command, then save results to a file
```bash
find . -name "channel*" | sort > results1.txt
```

Filter output for specific keyword
```bash
find . -name "channel*" | grep -v -e eye -e mountain
```
[Back to Top](#quick-reference)

### Useful keyboard shortcuts
- `Ctrl+R` Reverse search
- `Ctrl+L` Clear terminal
- `Ctrl+D` Exit
- `Ctrl+C` Interrupt command
- `Tab` Autocomplete filename