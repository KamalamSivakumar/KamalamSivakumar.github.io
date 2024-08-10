## parallel and distributed learning (part 2) [ cuda programming using cpp ]

Notes on CUDA programming basics.

**kernel**: a function that a GPU can run.  
add ```__global__``` to the function. This tells the CUDA cpp compiler that the function runs on the GPU, and can be called from the CPU.  
device code: code that runs on the GPU.  
host code: code that runs on the CPU.  
```
__global__ //CUDA kernel; the arrays are initialised as pointers in the function definition.
void add(int n, float *x, float *y){
        for(int i=0;i<n;i++){
                y[i] = x[i] + y[i];
        }
}
```

**unified memory**:  
single memory address space accessible from any processor in a system.  
allows applications to allocate data that can be read or written from code running on either CPUs or GPUs.  
facilitated by **cudaMallocManaged()** (similar to malloc()): allocation function that returns a pointer accessible from any processor.  
cuda managed data: automatically manages data migration between the CPU and GPU memory, allowing both processors to access the same data seamlessly without explicit data transfers, when using cudaMallocManaged()    
**page migrations**:  
shift between CPU and GPU. (e.g., every page in the arrays is written by the CPU, and then accessed by the CUDA kernel on the GPU, causing the kernel to wait on a lot of page migrations)  

**ways to mitigate migration overhead**:
1. Move the data initialization to the GPU in another CUDA kernel.
2. Run the kernel many times and look at the average and minimum run times.
3. Prefetch the data to GPU memory before running the kernel.

**to free data**: pass the pointer to cudaFree()  

```
//memory allocation on unified memory
float *x, *y; //declare pointers
cudaMallocManaged(&x, N*sizeof(float)); //instead of float *x = new float[N];
cudaMallocManaged(&y, N*sizeof(float));
...
...
...
cudaFree(x); //instead of delete[] x;
cudaFree(y);
```

**launch kernel**: basically invoking the function on GPU  
CUDA kernel launches are specified using the triple angle bracket syntax <<< >>>  
e.g., to launch the add kernel  
```
add<<<1, 1>>>(N, x, y);
```
to make the CPU wait until the kernel finishes, before accessing the results from CPU: call **cudaDeviceSynchronize()** before mentioning the CPU block function/code  
cuda files have extension ```.cu```  

**the whole code**:  
```
//introductory program to CUDA
#include <iostream>
#include <math.h>

__global__ //CUDA kernel; the arrays are initialised as pointers in the function definition.
void add(int n, float *x, float *y){
        for(int i=0;i<n;i++){
                y[i] = x[i] + y[i];
        }
}

int main(void)
{
        int N = 1<<20; //1 milion elements

        float *x, *y; //declare pointers
	cudaMallocManaged(&x, N*sizeof(float)); //instead of float *x = new float[N];
	cudaMallocManaged(&y, N*sizeof(float));

        //initialize x and y arrays
        for(int i=0;i<N;i++){
                x[i] = 1.0f;
                y[i] = 2.0f;
        }

        //run on CPU
	add<<<1, 1>>>(N, x, y);

	cudaDeviceSynchronize(); //wait for GPU to finish before accessing on host aka CPU
		
        //error handling
        float maxError=0.0f;
        for(int i=0;i<N;i++){
                maxError = fmax(maxError, fabs(y[i]-3.0f));
        }
        std::cout << "Max Error: " << maxError << std::endl;

        //free memory
        cudaFree(x);
        cudaFree(y);

        return 0;
}
```
(similar to g++ compilation and run)  
compile: nvcc add_kernel.cu -o add_cuda  
run: ./add_cuda 

to work on more on the CUDA cpp programming aspect:  
did not handle [race condition](https://medium.com/@kaushikakshat/race-conditions-d0298dfb99fe); written for a single thread i.e., every thread spawned will work on the whole array.  

**nuances with respect to using CUDA with python**:  
**options**: pycuda --> python toolkit from nvidia for cuda programming | torch | tensorflow  
personally learning torch and tensorflow would make so much sense, even jax  
**torch**: [torch.cuda](https://pytorch.org/docs/stable/cuda.html)  
This package adds support for CUDA tensor types.  
It implements the same function as CPU tensors, but they utilize GPUs for computation.  
**tensorflow**: [tf.device("/GPU:0")](https://www.tensorflow.org/guide/gpu)  
**jax**: a dedicated post, soon  

**next notes**: race condition, other cuda programming hurdles, and implementing parallelism

**References**:  
[cuda intro](https://developer.nvidia.com/blog/even-easier-introduction-cuda/)  
[unified memory](https://developer.nvidia.com/blog/unified-memory-cuda-beginners/)  
p.s wrote the cpp program using vim as I'm working on mastering it too.
