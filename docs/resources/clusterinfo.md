# Node Specs
Last updated Apr 6th, 2026

## CPU

Each node contains one Intel(R) Xeon(R) Gold 5218 CPU @ 2.30GHz
See specs here for further details and supported technologies: [Intel Xeon Gold 5218 Specs](https://www.intel.com/content/www/us/en/products/sku/192444/intel-xeon-gold-5218-processor-22m-cache-2-30-ghz/specifications.html)

## Memory

| Node numbers | Type | Memory (RAM) | GPU |
| :--- | :---: | :---: | :--- |
| ada01-ada02 | High-Mem | 512GB | No |
| ada03-ada16 | Standard | 256GB | No |
| ada17-ada18 | GPU | 128GB | Yes |

## GPU

Each GPU node contains two Nvidia Tesla V100-PCIE-32GB, for a total of four GPUs across the entire HPC cluster
See specs here for further details and supported technologies: [Nvidia Tesla V100 Specs](https://images.nvidia.com/content/technologies/volta/pdf/volta-v100-datasheet-update-us-1165301-r5.pdf)
