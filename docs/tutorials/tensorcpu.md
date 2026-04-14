# HPC Machine Learning Guide

## TensorFlow Example Job

Create a python file for your TensorFlow code

```bash
[usr@ada ~]$ 
```

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

network.fit(train_images, train_labels, epochs=5, batch_size=128)
test_loss, test_acc = network.evaluate(test_images, test_labels)
print('test_acc:', test_acc)
```

## 4. Submitting a Job

```bash
#!/bin/bash
#SBATCH --job-name=slurm_gpu    # Job name
#SBATCH --mail-type=END,FAIL          # Mail events (NONE, BEGIN, END, FAIL, ALL)
#SBATCH --mail-user=ehar@stlawu.edu     # Where to send mail	
#SBATCH --mem=32G                       # Job memory request
#SBATCH --time=05:00:00                 # Time limit hrs:min:sec
#SBATCH --output=slurm_gpu_%j.log       # Standard output and error log
#SBATCH --cpus-per-gpu=1		# Count of CPUs allocated per GPU.
#SBATCH --gres=gpu:1			# Allocate 1 GPU card
#SBATCH -n 1				# Allocate one node


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
#srun -n1 --gres=gpu:1 examples/mnist_cnn.py
#python examples/mnist_cnn.py
python3 examples/mnist_cnn.py
echo ""
echo -n "Finished program at: "
date
echo ""
```

## 5. Monitoring your Jobs
```bash
[usr@ada]$ squeue
```
