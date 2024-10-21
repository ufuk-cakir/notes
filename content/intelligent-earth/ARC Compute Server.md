---
title: 📝  ARC Compute Server
---
# ARC Compute Server (Oxford)

## **Login**

To connect to the ARC server, use the SSH command with X11 forwarding to enable graphical output:
```bash
ssh -Y name@arc-login.arc.ox.ac.uk
```

X11 forwarding allows for graphical applications to be displayed on your local machine.

---
## **Job Scheduling with SLURM**
ARC uses the SLURM workload manager to handle job submissions. You can submit jobs, check their status, cancel them, or run interactive sessions.
### **Submit a Job**
To submit a job, use the `sbatch` command:
```bash
sbatch example-job.sh
```
### **Check Queue Status**
To check the status of your queued jobs:

```bash
squeue -u yourUsername
```
### **Customize Job**
You can customize job submissions with the following options:
- **Job Name:**
_In your job script:_
```bash
#SBATCH -J jobName
```
- **Resource Requests:**
- Number of tasks (CPUs):
```bash
--ntasks=<ntasks> # or -n <ntasks>
```

- Time limit:

```bash
--time <days-hours:minutes:seconds> # or -t <days-hours:minutes:seconds>
```

- Memory:

```bash
--mem=<megabytes>
# Example for 5 GB
--mem=5g
```

- Number of nodes:

```bash
--nodes=<nnodes> # or -N <nnodes>
```
### **Cancel Jobs**
- Cancel all jobs under your username:

```bash
scancel -u yourUsername
```
- Cancel a specific job:

```bash
scancel JOBID
```
### **Run Single Commands**
Use `srun` to run a command directly on the cluster:

```bash
srun -n 2 echo "This job will use 2 CPUs."
```

You can cancel the job with `Ctrl+C`.
### **Interactive Sessions**

To start an interactive session, run:

```bash
srun --pty bash
```

---
## **Module System**
The module system allows you to load specific software environments.
### **List Available Modules**
```bash
module avail
```
### **Load a Module**
```bash
module load python # Example for loading Python
```
Use `module avail` to find the exact versions available.
### **Unload Modules**
- Unload a specific module:

```bash
module unload python
```

- Unload all modules:

```bash
module purge
```
### **Check Loaded Modules**
To see which modules are currently loaded:

```bash
module list
```
---
## **File Transfer**
You can transfer files between your local machine and the ARC server using `scp` or `rsync`.
### **Copy Files with SCP** 

Run this locally to copy a file to the ARC server:
```bash
scp local_file user@arc-login.arc.ox.ac.uk:remote_destination
```
To recursively copy a folder, use the `-r` flag:

```bash
scp -r local_folder user@arc-login.arc.ox.ac.uk:remote_destination
```
### **Sync Files with Rsync**
Rsync is useful for monitoring transfer progress and resuming partial transfers:

```bash
rsync -avP local_file user@arc-login.arc.ox.ac.uk:remote_destination
```

Options:
- `-a`: Archive mode, preserves file attributes.
- `-v`: Verbose mode, shows transfer details.
- `-P`: Partial transfer support and shows progress.


>[!info] 
>Questions or suggestions on how to improve this note? 
>[Raise an issue on GitHub!](https://github.com/ufuk-cakir/notes/blob/v4/content/intelligent-earth/ARC%20Compute%20Server.md)
