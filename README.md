# 2024-MIT6.5940-TinyML-and-Efficient-Deep-Learning-Computing
+ Course website : https://hanlab.mit.edu/courses/2024-fall-65940

## Simple Notes (in Chinese)
(updating...)
+ Lecture 3 - Pruning I : https://hackmd.io/@unshun0120/Sy4aQi8tfe
+ Lecture 4 - Pruning II : https://hackmd.io/@unshun0120/BJj_HJOFzx
+ Lecture 5 - Quantization I : https://hackmd.io/@unshun0120/HkiVpg_tfe
+ Lecture 6 - Quantization II : https://hackmd.io/@unshun0120/HkkYoEFKze
+ Lecture 7 - Network Architecture Search I : https://hackmd.io/@unshun0120/rym85StKzl
 
## Lab5 Debug
### 1. 執行./evaluate.sh reference 如果出現以下錯誤 :   
PS D:\github\mit6.5940\lab\lab5\tinychat-tutorial\transformer> bash ./evaluate.sh reference
./evaluate.sh: line 2: $'\r': command not found  
./evaluate.sh: line 12: $'\r': command not found  
./evaluate.sh: line 16: syntax error near unexpected token `$'do\r''  
'/evaluate.sh: line 16: `    for i in "${!keys[@]}"; do  

**Solve** : 在terminal輸入bash -c "sed -i 's/\r$//' evaluate.sh"把換行符號換掉  

### 2. 執行./evaluate.sh reference 如果出現以下錯誤 :  
../kernels/quantizer.cc:57:38: error: 'int8_t' has not been declared  
   57 | void quantize_fp32_to_int8(float* A, int8_t* qA, float* sA, int size, int block_size) {
      |                                      ^~~~~~  
../kernels/quantizer.cc:57:1: note: 'int8_t' is defined in header '<cstdint>'; this is probably fixable by adding '#include <cstdint>'  
   56 | #include <immintrin.h>  
  +++ |+#include <cstdint>  
   57 | void quantize_fp32_to_int8(float* A, int8_t* qA, float* sA, int size, int block_size) {  
make: *** [Makefile:61: build/transformer/../kernels/quantizer.o] Error 1  
make: *** Waiting for unfinished jobs....  
make: *** wait: No child processes.  Stop.  
Compilation failed!  

**Solve** : 到tinychat-tutorial/kernels/quantizer.cc加上#include \<cstdint>  

### 3. 如果跑bash ./evaluate.sh loop_unrolling之類的卡住 :  

**Solve** : 到./evaluate.sh把make chat test_linear -j IMP="\$\arg"改成make chat test_linear -j1 IMP="$arg"



