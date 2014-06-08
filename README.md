LU_OpenMP
=========

Parallel Project


Parallel dense blocked LU factorization.

The implementations of this project includes: 
 - A serial version name **lu.c**
 - A paraller with OpenMP directives **lu_par.c**
 - A paraller combined with SIMD (SSE) **lu_simd.c**
 - A paraller combined with SIMD (AVX) **lu_simd_avx.c**


Compile with
--------------
* #### Main: 

```sh
make //extra here
```
* #### SIMD: 


```
 gcc lu_simd.c -o simd -fopenmp -O0 -msse4.2
 gcc lu_simd.c -o simd3 -fopenmp -O3 -msse4.2
 gcc lu_simd_avx.c -o avx -fopenmp -O0 -mavx
 gcc lu_simd_avx.c -o avx3 -fopenmp -O3 -mavx
```


Current Version
----

0.2
