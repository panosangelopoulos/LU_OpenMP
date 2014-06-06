LU_OpenMP
=========

Parallel Project


Parallel dense blocked LU factorization

void lu ( long n, long bs )
{
	long i, il, j, jl, k, kl, I, J, K;
	double *A, *B, *C, *D;
	long strI;

	strI = n;
	for ( k=0, K=0; k<n; k+=bs, K++ ) {
		kl = k+bs;
		if ( kl>n ) {
			kl = n;
		}

		/* factor diagonal block */
		A = & ( a[k+k*n] );
		lu0 ( A, kl-k, strI );

		/* divide column k by diagonal block */
		D = & ( a[k+k*n] );
		for ( i=kl, I=K+1; i<n; i+=bs, I++ ) {
			il = i + bs;
			if ( il > n ) {
				il = n;
			}
			A = & ( a[i+k*n] );
			bdiv ( A, D, strI, n, il-i, kl-k );
		}
		/* modify row k by diagonal block */
		for ( j=kl, J=K+1; j<n; j+=bs, J++ ) {
			jl = j+bs;
			if ( jl > n ) {
				jl = n;
			}
			A = & ( a[k+j*n] );
			bmodd ( D, A, kl-k, jl-j, n, strI );
		}

		/* modify subsequent block columns */
		for ( i=kl, I=K+1; i<n; i+=bs, I++ ) {
			il = i+bs;
			if ( il > n ) {
				il = n;
			}
			A = & ( a[i+k*n] );
			for ( j=kl, J=K+1; j<n; j+=bs, J++ ) {
				jl = j + bs;
				if ( jl > n ) {
					jl = n;
				}
				B = & ( a[k+j*n] );
				C = & ( a[i+j*n] );
				bmod ( A, B, C, il-i, jl-j, kl-k, n );
			}
		}
	}
}
