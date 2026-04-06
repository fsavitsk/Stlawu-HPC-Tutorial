# Introduction

Welcome to the High Performance Computing Cluster (HPCC) at St. Lawrence University

# What is High Performance Computing HPC?

At its simplest, High-Performance Computing (HPC) is the practice of aggregating computing power in a way that delivers much higher performance than one could get out of a typical desktop computer or laptop.

While the hardware in your Laptop, Desktop, or even smartphone might have faster single core performance, than an HPC system, it does not posess the raw horsepower needed for intense HPC workflows.

## The "Cluster" Concept

An HPC system is rarely just one giant supercomputer. Instead, it is a cluster of many individual computers (called nodes) connected by a high-speed network.

## Why do we need it?

Standard computers process tasks sequentially (one after another). HPC systems use parallel processing, meaning they break a massive problem into smaller pieces and solve them all at the exact same time.

Common uses for the system you are accessing include:

Deep Learning: Training models like TensorFlow or PyTorch requires billions of mathematical calculations. Using a GPU node can finish in hours what a laptop might take weeks to do.

Simulations: Modeling weather patterns, fluid dynamics, or molecular structures.

Big Data: Analyzing datasets that are too large to even open on a normal computer's memory (RAM).

# Best Practices & Cluster Etiquette

## 1. The "Login Node" Rule

The login node is the shared "lobby." It is meant for editing code, moving files, and submitting jobs—not for running heavy computations.
!!! danger "Don't Run Heavy Code on Login"
Running a python train.py command directly on the login node will slow down the system for everyone. Always use sbatch or srun. (See Documentation section for how to use SLURM commands)

## 2. Be Realistic with Resource Requests

If your job only needs 8GB of RAM, don't request 64GB.
!!! info "Efficiency"
Requesting more resources than you need makes your job stay in the "Pending" queue longer. Accurate requests = faster start times.

## 3. Storage

# Key HPC Terms

| Term | Category | Definition |
| :--- | :--- | :--- |
| **Node** | Hardware | An individual "computer" within the cluster. We have **18** total. |
| **Core (CPU)** | Hardware | A single processing unit inside a node; used for general tasks. |
| **GPU** | Hardware | Specialized hardware for math (Available on **2** nodes). |
| **Partition** | Slurm | A logical grouping of nodes (e.g., `compute`, `gpu`, or `high-mem`). |
| **Job** | Slurm | A specific task or script submitted to the cluster for execution. |
| **sbatch** | Command | The primary command used to submit a script to the queue. |
| **squeue** | Command | Used to view the status of all running and pending jobs. |
| **Allocation** | Account | Your "budget" of computing time or credits for a project. |
