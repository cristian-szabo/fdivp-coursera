# Week 12

### Question 1

Check all the problem(s) that admit sparse solution(s):

- [x] minx∥x∥p subject to Ax=b (p is between 0 and 1)
- [x] minx∥x∥0 subject to Ax=b
- [x] minx∥x∥1 subject to Ax=b
- [ ] minx∥x∥2 subject to Ax=b

### Question 2

Natural image patches (unlike random noise) cannot be sparsely represented over a DCT dictionary.

- [ ] True
- [x] False

### Question 3

In video surveillance applications, background is modeled as a ______ matrix and moving parts are modeled via a ______ matrix.

- [ ] low-rank, low-rank
- [ ] sparse, low-rank
- [ ] sparse, sparse
- [x] low-rank, sparse

### Question 4

Which one of the greedy algorithms discussed in class is designed to solve the following problem?

minA,X∥AX−B∥F subject to ∥X(:,i)∥ 0≤k∀i

- [ ] Orthogonal Matching Pursuit
- [ ] Matching Pursuit
- [x] Method of Optimal Directions
- [ ] This problem has a closed form solution and hence doesn't need to be solved in a greedy fashion.

### Question 5
 
Check all the norms that are convex functions.

- [ ] The Lp norm (f(x)=∥x∥p where p is between 0 and 1.
- [x] The L1 norm (f(x)=∥x∥1)
- [x] The L2 norm (f(x)=∥x∥2)
- [ ] The L0 norm (f(x)=∥x∥0)

### Question 6

Which one of the following statements is true regarding the basis pursuit problem given by x∗=argminx∥x∥1subjecttoAx=b?

- [ ] If one of the columns in A is identical to b≠0, then ∥x∗∥1=1.
- [ ] If b=0 and A is full rank, then the problem has no solution since the constraint set becomes empty.
- [ ] x∗ also minimizes the corresponding LASSO problem given by minx∥Ax−b∥22+λ∥x∥1.
- [x] none of the above.

### Question 7

The singular value decomposition of the n×n square matrix A is given by A=UΣVT. Check all correct statements.

- [ ] Only square matrices (such as A) have singular value decomposition.
- [x] Matrices U and V are orthonormal bases for the n-dimensional space.
- [x] If Σ has only one non-zero entry, then A is definitely a rank-1 matrix.
- [ ] The nuclear norm of A (given by the sum of absolute values of entries on the diagonal of Σ) is an upper bound on the rank of A.

### Question 8

In this MATLAB assignment you will code-up the orthogonal matching pursuit (OMP) algorithm, as discussed in the lecture, to solve the following optimization problem:

minx∥Ax−b∥2subjectto∥x∥0≤S.

In this exercise A=D+I, where Dij=sin(i+j) for 1≤i,j≤10 and I is the 10×10 identity matrix. Use A along with b=[−2,−6,−9,1,8,10,1,−9,−4,−3]T, and S=3 to find the solution to the problem given above.

Your solution x∗ uses three columns of A in order to approximate b. Type in the sum of the indices of these three columns. For example, if you find that your solution uses the first, third, and fifth columns of A then you must enter 9. (Hint: normc(A) normalizes the columns of A to a length of 1 in MATLAB.)

#### Solution

```matlab
function x = omp(A,b,S)

[N,K] = size(A);

x = zeros(K,1);      
r = b;               
omega = zeros(S,1);
A_omega = [];
cnt = 0;

while (cnt < S)
    cnt = cnt+1;
    x_tmp = zeros(K,1);
    inds = setdiff([1:K],omega);
    for i = inds
        x_tmp(i) = A(:,i)' * r / norm(A(:,i));
    end
    [~,ichosen] = max(abs(x_tmp));
    omega(cnt) = ichosen;
    A_omega = [A_omega A(:,ichosen)];
    x_ls = A_omega \ b;
    r = b - A_omega * x_ls;
end

for i = 1:S
    x(omega(i)) = x_ls(i);
end

b = [-2,-6,-9,1,8,10,1,-9,-4,-3];
S = 3;
for i = 1:10
	for j = 1:10
		A(i,j) = sin(i+j);
		if (i==j)
			A(i,j) = A(i,j) +1;
		end
	end
end

omp(A, b, S);

ans =

    16 % <- Answer
```
