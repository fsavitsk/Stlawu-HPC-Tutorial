# Example: R Cars dataset

Create a file named cars.R using your preffered text editor (nano/vim)

```bash
[user@ada ~]$ nano cars.R
```

Paste the following code in the file

```R
# Load the built-in dataset
data(cars)

# (1) Perform Linear Regression: dist = b0 + b1(speed)
model <- lm(dist ~ speed, data = cars)

# Print a summary of the model results
print(summary(model))

# (2) Save the output to a text file for later
saveRDS(model, file = "car_model.rds")

cat("\nAnalysis complete. Model saved to car_model.rds\n")
```

Then exit and save your text editor.

Then create a bash script called cars.slurm again in your preffered editor and paste this code

```bash
[user@ada ~]$ nano cars.slurm
```

Note: make sure to replace the email adress below.

```bash
#!/bin/bash
#SBATCH --job-name=cars		   # Job name
#SBATCH --mail-type=END,FAIL          # Mail events (NONE, BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=fbsavi23@stlawu.edu     # Where to send mail
#SBATCH --ntasks=1		   # Only 1 task
#SBATCH --cpus-per-task=1          # Requesting 1 CPU Core per task
#SBATCH --mem=1G                   # Requesting 1GB of RAM
#SBATCH --time=00:05:00            # Set a 5-minute limit

#SBATCH --output=cars_%j.log       # Standard output and error log

# Load the R environment
module load R/4.5.0

# Run the script
Rscript cars.R
```

To run your job you will execute

```bash
[user@ada ~]$ sbatch cars.slurm
```
If all the nodes are being used, then your job will sit in the queue until space is available for it to run.

Remember you can check on your job using squeue.

Once your job is done running you may get an email.

To check the output run:
```bash
[user@ada ~]$ cat cars_*.log
```
