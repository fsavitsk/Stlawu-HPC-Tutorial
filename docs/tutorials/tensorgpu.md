# Submit a Simple Job using SLURM

## Example TensorFlow (GPU)

Create a file named mnist_cnn.py using your preffered text editor (nano/vim)

```bash
[usr@ada ~]$ nano mnist_cnn.py
```

Paste the following code in the file

```python
"""
Chapter 2 of Deep Learning with Python, Chollet, Manning 2018
"""
from keras.datasets import mnist
from keras import models, layers
from keras.utils import to_categorical

(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

network = models.Sequential()
network.add(layers.Dense(512, activation='relu', input_shape=(28 * 28,)))
network.add(layers.Dense(10, activation='softmax'))

train_images = train_images.reshape((60000, 28 * 28))
train_images = train_images.astype('float32') / 255

network.compile(optimizer='rmsprop',
                loss='categorical_crossentropy',
                metrics=['accuracy'])

test_images = test_images.reshape((10000, 28 * 28))
test_images = test_images.astype('float32') / 255


train_labels = to_categorical(train_labels)
test_labels = to_categorical(test_labels)

network.fit(train_images, train_labels, epochs=5, batch_size=2048, verbose=2)
test_loss, test_acc = network.evaluate(test_images, test_labels)
print('test_acc:', test_acc)
```

Then exit and save your text editor.

Then create a bash script called mnist_job.slurm again in your preffered editor and paste this code

```bash
[usr@ada ~]$ nano mnist_job.slurm
```

Note: make sure to replace the email adress below.

```bash
#!/bin/bash
#SBATCH --job-name=slurm_gpu    # Job name
#SBATCH --mail-type=END,FAIL          # Mail events (NONE, BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=(email address)     # Where to send mail	
#SBATCH --gres=gpu:1                    # Allocate 1 GPU card
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-gpu=4                # Count of CPUs allocated per GPU.
#SBATCH --mem=16G   
#SBATCH --time=00:05:00                 # Time limit hrs:min:sec

#SBATCH --output=slurm_gpu_%j.log       # Standard output and error log

echo "Date              = $(date)"
echo "Hostname          = $(hostname -s)"
echo "Working Directory = $(pwd)"
echo ""
echo "Number of Nodes Allocated      = $SLURM_JOB_NUM_NODES"
echo "Number of Tasks Allocated      = $SLURM_NTASKS"
echo "Number of Cores/Task Allocated = $SLURM_CPUS_PER_TASK"

echo ""
echo -n "Loading module python/anaconda3....   "
module load python/anaconda3
echo "Done!"
echo ""
echo "CUDA_VISIBLE_DEVICES is set to ${CUDA_VISIBLE_DEVICES}"

echo -n "Executing program at: "
date
echo ""
#srun -n1 --gres=gpu:1 mnist_cnn.py
#python mnist_cnn.py
python3 mnist_cnn.py
echo ""
echo -n "Finished program at: "
date
echo ""
```

To run your job you will execute

```bash
[usr@ada ~]$ sbatch mnist_job.slurm
```
If all the GPUs are being used, then your job will sit in the queue until space is available for it to run.

Remember you can check on your job using squeue.

Once your job is done running you may get an email.

To check the output run:
```bash
[usr@ada ~]$ cat slurm_gpu_*.log
```
