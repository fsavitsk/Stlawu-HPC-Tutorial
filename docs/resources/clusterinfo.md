| Node Count | Type | Memory (RAM) | Primary Use Case |
| :--- | :---: | :---: | :--- |
| **16** | Standard | 64GB - 128GB | Data cleaning, CPU-based simulations, and scripting. |
| **2** | **GPU** | 256GB | **Deep Learning (TensorFlow/PyTorch) & GPU-accel math.** |
| **4*** | High-Mem | 512GB+ | Processing massive datasets that exceed standard RAM. |

<br>

!!! note "Note on High-Mem"
    *High-memory capabilities are distributed across 4 of our 16 standard nodes. Use the `--mem` flag in Slurm to target these specifically.*
