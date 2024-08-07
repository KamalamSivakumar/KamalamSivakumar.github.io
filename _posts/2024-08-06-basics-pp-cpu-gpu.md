## parallel and distributed learning (part 1)

Covers basics of parallel computing and cpu vs gpu.

**Serial computing**  
Instructions/flows are executed sequentially after one another, only one instruction executed at any moment in time.

**Parallel computing**  
The simultaneous use of multiple resources to solve a computational problem. i.e., solved concurrently.  
An overall control/coordination is employed to orchestrate the flow.  

To enable parallel computing, the problem at hand must be:  
  1. broken down into operations that are discrete and can be done simultaneously.
  2. execute multiple instructions at any moment in time.

Assumption: You own a watch manufacturing company and the components you manufacture include dial, strap and the clasp. When it comes to manufacturing these parts, you have two approaches to consider:  
1. Serial Computing: Manufacture each component one by one. First the dial, then the strap, then the clasp, before assembling the watch. This is slower as each step depends on the previous one.  
2. Parallel Computing: Manufacture all components simultaneously and then assemble them, speeding up production by completing tasks concurrently.

**Parallel processing vs Parallel computing**  
**computing** considers the processor aspect, concerned with the physical architecture and how to use multiple processors effectively.  
**processing** considers the task orchestration aspect, the strategy of executing a task in parallel, focusing more on the software and algorithmic side. (divide-and-conquer strategy)

**Parallel programming model**
1. **data parallelism**: same operation is performed simultaneously on multiple data elements, typically by distributing the data across multiple processors or cores.
2. **process parallelisation**: multiple processes performed simultaneously. (the watch manufacturing example)
3. **master-slave approach**: master process assigns tasks to multiple slave processes, which perform the work and report results back to the master.

In ai/ml, data parallelism and process parallelisation are more prevalent than the 
master-slave approach because they handle redundant data and processes more efficiently, avoiding bottlenecks and enhancing scalability.

**Disadvantage of parallel programming**: more resource requirements, communications overhead, and complexity in developing solutions.

**CPU vs GPU architecture** (high-level overview)

| CPU                                                                                                                                                                                    | GPU                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------|
| relatively lesser no.of cores, each core is capable of executing complex instructions and is designed for high single threaded perfromance, allows each core to handle multiple threads| thousands of simpler and smaller cores, designed to handle operations in parallel                                                 |
| typically larger and complex caches to reduce latency and handle diverse workloads                                                                                                     | high memory bandwidth with a focus on throughput rather than latency, equipped with large memory volume                           |
| CPUs are designed with sophisticated control-logic for executing a broad range of instructions and complex task scheduling                                                             | simpler control-logic, focusing on executing many threads concurrently rather than handling complex control-flows                 |
| better suited for tasks that require complex, low-level control and have limitted parallelism                                                                                          | large datasets, tasks that can be divided into many parallel threads                                                              |

In conclusion,  
Parallel computing speeds things up by running multiple tasks at once, unlike serial computing, 
which does things one step at a time. While parallel computing is all about using hardware efficiently, 
parallel processing focuses on managing tasks. In ai/ml, data parallelism and process parallelization are 
preferred because they handle big tasks more efficiently. CPUs are great for complex, single tasks,
while GPUs are designed to handle lots of tasks at once, making them ideal for different kinds of work.
