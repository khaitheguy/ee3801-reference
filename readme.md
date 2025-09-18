# EE3801 Reference Sheet

## Quick Reference
1. [Create cluster](#parallelcluster)
2. [Set up conda env](#ec2-shell)
3. [Manage slurm jobs](#slurm-commands)
4. [Check for missing files](#bash-commands)
5. [Lab links](#links-to-labs)

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

Update compute nodes on the fly:

```bash
pcluster update-compute-fleet --status STOP_REQUESTED -n MyCluster01
```
```bash
pcluster update-cluster -c ~/cluster-config.yaml -n MyCluster01
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

Configure AWS:
```bash
aws configure
```
- Select options
```
AWS Access Key ID [None]:
AWS Secret Access Key [None]:
Default region name [None]: ap-southeast-1
Default output format [None]: json
```
- Get AWS keys:
```bash
cat ~/.aws/credentials
```

Terminate ipython:
```bash
ps -ef | grep ipython
```

```bash
kill -9 12958 # process-id, the 2nd number
```
[Back to Top](#quick-reference)

## Git commands
Configure Git:
```bash
git config --global core.editor "nano"
git config --global user.name "[Name]"
git config --global user.email "[Email]"
```

Check upstream repo:
```bash
git remote -v
```
- Expected result
```
origin		https://github.com/yourusername/PyHipp.git (fetch)
origin		https://github.com/yourusername/PyHipp.git (push)
upstream	https://github.com/shihchengyen/PyHipp.git (fetch)
upstream	https://github.com/shihchengyen/PyHipp.git (push)
```

Set upstream repo:
```bash
git remote add upstream https://github.com/shihchengyen/PyHipp.git
```

*If accidentally cloned wrong repo*
```bash
git remote set-url origin https://github.com/yourusername/PyHipp.git
```
[Back to Top](#quick-reference)

Merge with upstream changes:
```bash
git fetch upstream
```
```bash
git checkout main
```
```bash
git merge upstream/main
```

## Slurm Commands

Submit job:
```bash
sbatch file.sh
```

- *With dependencies*
```bash
sbatch --dependency=afterok:12:13:14:15:16 /data/src/PyHipp/consol_jobs.sh
```

Check job queue:
```bash
squeue
```

Cancel jobs:
- *1 job*
```bash
scancel 2
```

- *Multiple jobs*
```bash
scancel {2,3,4}
```

- *All jobs*
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
Copy file over SSH:
```bash
scp -i ~/MyKeyPair.pem ~/EE3801/PyHipp/slurm.sh ec2-user@xxx:/data/submit.sh
```

Regenerate missing `.hkl` files:
1. Get all channels
```bash
find . -name "channel*" | grep -v -e eye -e mountain | sort > chs.txt
```
2. Get generated channels
```bash
find . -name "rplhighpass*hkl" | grep -v -e eye | sort | cut -d "/" -f 1-4 > hps.txt
```
3. Get missing channels
```bash
comm -23 chs.txt hps.txt
```
4. Generate missing channels
```bash
cwd=`pwd`; for i in `comm -23 chs.txt hps.txt`; do echo $i; cd $i; sbatch /data/src/PyHipp/rplhighpass-sort-slurm.sh; cd $cwd; done
```

Regenerate `firings.mda` files:
1. Get all channels
```bash
find . -name "channel*" | grep -v -e eye -e mountain | sort
```
2. Get generated channels
```bash
find mountains -name "firings.mda" | sort
```
3. Cut both outputs such that only channel dir remains
4. Use `comm` to extract missing channels
5. Use same for loop as above to regenerate files

Get full path of file:
```bash
find . -name "firings.mda" | xargs realpath
```

[Back to Top](#quick-reference)

### Useful keyboard shortcuts
- `Ctrl+R` Reverse search
- `Ctrl+L` Clear terminal
- `Ctrl+D` Exit
- `Ctrl+C` Interrupt command
- `Tab` Autocomplete filename

## Links to labs
- [Lab 1](https://ee3801.github.io/Lab1)
- [Lab 2](https://ee3801.github.io/Lab2)
- [Lab 3](https://ee3801.github.io/Lab3)
- [Lab 4](https://ee3801.github.io/Lab4)
- [Lab 5](https://ee3801.github.io/Lab5)