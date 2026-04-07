# Submit a Simple Job using SLURM

## Example Factor.py

Create a file named factor.py using your preffered text editor (nano/vim/vi)

```bash
[usr@ada]$ nano factor.py
```

Paste the following code in the file

```python
import sys, os
from math import ceil,sqrt

# A naive factoring algorithm for HPC demo purposes.
if __name__ == '__main__':

    # info about the array of jobs numbered  sequenially
    # from SLURM_ARRAY_TASK_MIN to SLURM_ARRAY_TASK_MAX
    print(f"JOB_ID = {os.environ['SLURM_ARRAY_JOB_ID']}")
    print(f"TASK_ID = {os.environ['SLURM_ARRAY_TASK_ID']}")
    print(f"TASK_COUNT = {os.environ['SLURM_ARRAY_TASK_COUNT']}")
    print(f"TASK_MAX = {os.environ['SLURM_ARRAY_TASK_MAX']}")
    print(f"TASK_MIN = {os.environ['SLURM_ARRAY_TASK_MIN']}")


    # make sure a number was provided on the command line    
    if len(sys.argv) < 2:
        print("Provide a number to factor")
        sys.exit(0)

    n = int(sys.argv[1])  # n is the number we are trying to factor
    
    # get the TASK ID as an integer
    TASK_ID = int(os.environ['SLURM_ARRAY_TASK_ID'])

    # get the number of tasks TASK_COUNT as an integer
    TASK_COUNT = int(os.environ['SLURM_ARRAY_TASK_COUNT'])
    
    # checking spread numbers in this task
    spread = int(ceil(sqrt(n) / TASK_COUNT))

    start = TASK_ID * spread + 3 

    # make sure to never start loop on an even number
    if start & 0:  # same as start % 2 == 0
        start = start - 1

    end = start + spread

    print(f"start = {start}, end = {end}")

    for i in range(start, end, 2): 
        if n % i == 0:
            print("Factor: {0}".format(i))
            exit()

    print(f"No factor found between {start} and {end}")

```

Then exit and save your text editor.

Then create a bash script called factor.run again in your preffered editor and paste this code
```bash
[usr@ada]$ nano factor.run
```

```bash
#!/bin/bash
#SBATCH --job-name=slurm_factor       # Job name
#SBATCH --mail-type=END,FAIL          # Mail events (NONE, BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=ehar@stlawu.edu  # Where to send mail	
#SBATCH --ntasks=64
#SBATCH --mem=1gb                     # Job memory request
#SBATCH --time=00:30:00               # Time limit hrs:min:sec
#SBATCH --output=factor_%j.log   # Standard output and error log

echo "Date              = $(date)"
echo "Hostname          = $(hostname -s)"
echo "Working Directory = $(pwd)"
echo ""
echo "Number of Nodes Allocated      = $SLURM_JOB_NUM_NODES"
echo "Number of Tasks Allocated      = $SLURM_NTASKS"
echo "Number of Cores/Task Allocated = $SLURM_CPUS_PER_TASK"

module load python/anaconda3
#python ./factor.py 944871836856449473 3
#python ./factor.py 10000007022601232909773 3 60691391499078479
#python ./factor.py 60691391499078479 
#python ./factor.py 97 
python ./factor.py 10000007022601232909773

```

Create a new file called factor.run

You will likely need to give any bash scripts executing permission in order to run a job.
```bash
[usr@ada]$ chmod +x factor.run
```
To run your job you will execute
```bash
[usr@ada]$ sbatch --array=0-0 factor.run
```
Note, using the array flag will run multiple copies of your job, 0-0 will run 1, 0-1 will run 2, 0-2 will run 3 and so on. If you have more jobs than available space then some will sit in the queue until space is available for them to run.

If you wish to run a single job and not an array of them then small modifications are needed to the python file above so it won't crash without the array flag.

Remember you can check on your job using squeue -user
