## parallel and distributed learning (part 2.1) [cuda programming using torch]

This covers the notes, implementation will be on the next post.

firstly, determine if there is a need to use gpu.

[torch.cuda.device](https://pytorch.org/docs/stable/generated/torch.cuda.device.html#torch.cuda.device): context manager that changes the selected device (torch.device('cuda'))  

-- cross-gpu operations are not allowed by default. i.e, device specific operations.  
-- manage tensors on specific devices using methods like:  
[to](https://pytorch.org/docs/stable/generated/torch.Tensor.to.html)(tensor dtype/device conversion),  
[cuda](https://pytorch.org/docs/stable/cuda.html)(transfer models from cpu to gpu, enabling the use of gpu acceleration for faster computation)  
-- upon calling just "cuda()" transfers tensor to "cuda(cuda:0)" (specify different gpu's based on your available devices)  
-- always better to check if the gpu is available before switching using "torch.cuda.is_available()"  
.copy() --> copies the content of one tensor to another. It can handle copying between different devices.  '

-- cannot perform operations on tensors located in different devices, torch raises error to bring the tensors to the same device.  
**peer-to-peer memory access**: enables gpu(s) to access other gpu's memory without copying, not by default, must be specified explicitly. (requires specific hardware support and configuration)  
without peer-to-peer memory access, there's a need to copy onto the same device.  

better to avoid data transfers (obviously an overhead)  

-- by default gpu operations are async. i.e., each devices executes operations in the order they are queued.  
-- torch performs necessary data transfer i.e., (copying) between cpu and gpu, to make it "seem" sync.  
-- force synchronous computation by setting environment variable CUDA_LAUNCH_BLOCKING=1. (to check for errors as and when, because with async, only after the queue's done, error's got. stack trace does not show where it was requested.)  
-- async allows us to execute more computations in parallel. consequence: hard to keep track of time.  
-- either call "torch.cuda.synchronize()" before measuring, or use "torch.cuda.Event" to record times.  

**cuda streams**: linear sequence of execution that belongs to a specific device  
-- each device uses its own “default” stream.  
-- Operations inside each stream are serialized in the order they are created, but operations from different streams can execute concurrently in any relative order, unless explicit synchronization functions (such as synchronize() or wait_stream()) are used.  
-- when using non-default streams, it is the user’s responsibility to ensure proper synchronization.  
-- synchronization is necessary even when there is no read dependency, ensure that all operations dependent on deallocated memory are completed before reallocating or reusing that memory, cuda cache may be still with the other stream.  

-- Each backward cuda pass runs on the same stream that was used for its corresponding forward pass.  
-- If the forward pass runs independent operations in parallel on different streams, this helps the backward pass exploit that same parallelism.

caching memory allocator to speed up memory allocations.  
**memory management calls**:  
-- memory_allocated() and max_memory_allocated() to monitor memory occupied by tensors  
-- memory_reserved() and max_memory_reserved() to monitor the total amount of memory managed by the caching allocator  
-- empty_cache() releases all unused cached memory from PyTorch so that those can be used by other gpu applications  
-- more memory management information on: [Understanding CUDA Memory Usage](https://pytorch.org/docs/stable/torch_cuda_memory.html#torch-cuda-memory)    

reference: [CUDA Semantics](https://pytorch.org/docs/stable/notes/cuda.html#)
