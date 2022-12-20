# HPC infrastructure

It is important to consider which HPC provider you use for your simulations in order to obtain your results most efficiently.
A summary of all of the resources available to our group is provided on this page.

The size and scale of the computing infrastructure is divided into *tiers*.
Tiers 3, 2, 1 are categorised as *local*, *regional* and *national*.
The tier that a machine belongs to determines its scale and availability.
On tier 3 machines you will be sharing resources with others at the University,
whereas tier 1 resources are shared by users across the whole country.
For tier 2 and 3 machines it is usually necessary to submit applications for resource allocations.

## Tier 3

| Computing Architecture | Description | Use case |
|---------|---------|--------|
| [Taskfarm](https://wiki.csc.warwick.ac.uk/wiki/Desktop2018/TaskfarmUserGuide?validation_key=b7dd301113983475b4635ac67d9a95ec) | The taskfarm is a compute node extension to the SCRTP-managed Linux desktop. It provides a Slurm batch system, enabling jobs to be submitted directly to the taskfarm nodes from the desktop. The taskfarm is intended for small-scale workloads, test/development jobs and/or workloads not generally needing a large-scale HPC cluster. The taskfarm does not have a high performance cluster network (e.g. InfiniBand) so is best suited to single-node jobs. Distributed-memory parallel work should usually be run on an HPC cluster rather than on the taskfarm. | Small, single-node jobs |
| [Avon](https://warwick.ac.uk/research/rtp/sc/hpc/#avon) | Avon is the successor to Tinis and resides within new data centre space, dedicated to HPC, on the University's Science Park. Through its high core count (9528 cores) and enhanced number of GPU nodes (16 multi-GPU nodes), Avon provides a significant increase in computational power over previous systems and enables the support of new workloads, especially those which use GPUs. | medium-sized jobs, CASTEP and FHI-aims, also ML training|

## Tier 2

| Computing Architecture | Description | Use case |
|---------|---------|--------|
| [Sulis HPC Midlands+](https://warwick.ac.uk/research/rtp/sc/sulis/) | Sulis uses CPU and GPU hardware, configured to support research applications that rely on large ensembles of small scale calculations to enable greater quantities of data sampling, and hence accurate estimation of the uncertainty in predictive models. By running thousands of simulations concurrently in high-throughput mode, time is dramatically reduced, increasing the scope and ambition of research of research that can be accomplished in a given time. | FHIaims and CASTEP. Very good for Machine Learning projects. |
| [MMM Hub Young](https://www.rc.ucl.ac.uk/docs/Clusters/Young/) | Young is built on HPE dual 20 core Intel x86-64 nodes, with 576 nodes with 192GB per node. Uses PBS. | Good for small to medium-sized jobs, target job sizes are between 2-5 nodes. |
| [NI-HPC Kelvin2](https://www.ni-hpc.ac.uk/Kelvin2/) | Kelvin2 is a scalable High Performance Computing (HPC) and Research Data Storage environment. This is the second iteration of the cluster, replacing the previous "Kelvin" system. <p> - 84 x 128 core Dell PowerEdge R6525 compute nodes with AMD EPYC 7702 dual 64-Core Processors (786GB RAM). <p> - 4 High memory nodes (2TB RAM). <p> - 32 x NVIDIA Tesla v100 GPUs. <p> - 16 x NVIDIA Tesla A100 GPUs <p> - 2PB of lustre parallel file system for scratch storage. <p> - All compute nodes and storage are connected by EDR Infiniband fabric. <p> - Compute nodes run CENTOS7 operating system. | FHIaims and CASTEP. Jobs can use up to 27 nodes (756 cores). Also good for GPU ML training |

## Tier 1

| Computing Architecture | Description | Use case |
|---------|---------|--------|
| [ARCHER2](https://www.archer2.ac.uk/) | The full ARCHER2 system is an HPE Cray EX supercomputing system with an estimated peak performance of 28 Pflop/s. The machine has 5,860 compute nodes, each with dual AMD EPYCTM 7742 64-core processors at 2.25GHz, giving 750,080 cores in total. | Very large jobs or many very long ab-initio MD simulations. |
