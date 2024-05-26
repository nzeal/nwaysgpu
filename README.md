# nwaysgpu

This is a basic to advanced tutorial to N ways to offload C code:

- CUDA 
- OpenACC
- OpenMP
- Kakos 
- SYCL

# Building and Running the Application
 - Laplace 

''' bash

while ( error > tol && iter < iter_max ) {
error=0.0;
for( int j = 1; j < n-1; j++) {
for(int i = 1; i < m-1; i++) {
Anew[j][i] = 0.25 * (A[j][i+1] + A[j][i-1] +
A[j-1][i] + A[j+1][i]);
error = max(error, abs(Anew[j][i] - A[j][i]);
}
}
for( int j = 1; j < n-1; j++) {
for( int i = 1; i < m-1; i++ ) {
A[j][i] = Anew[j][i];
}
}
iter++;
}

'''

''' bash
git  clone git@github.com:nzeal/nwaysgpu.git
cd nwaysgpu
git fetch --all
git checkout $NWAYS
make
make run

'''
