import numpy as np

# --- Input vectors ---
n = int(input("Enter number of vectors: "))
m = int(input("Enter dimension of each vector: "))
vecs = [list(map(float, input(f"Vector {i+1}: ").split())) for i in range(n)]
A = np.column_stack(vecs)
print("\nMatrix A:\n", A)

# --- Check Linear Dependence ---
r = np.linalg.matrix_rank(A)
print("\nRank =", r)
print("Linearly Independent" if r == A.shape[1] else "Linearly Dependent")

# --- Linear Combination ---
coef = list(map(float, input("\nEnter coefficients: ").split()))
print("Linear combination =", np.sum([coef[i] * A[:, i] for i in range(n)], axis=0))

# --- Transition Matrix ---
s = int(input("\nEnter size of square matrices: "))
print("\nEnter B1:")
B1 = np.array([list(map(float, input().split())) for _ in range(s)])
print("Enter B2:")
B2 = np.array([list(map(float, input().split())) for _ in range(s)])

try:
    P = np.linalg.inv(B2) @ B1
    print("\nTransition Matrix:\n", P)
except np.linalg.LinAlgError:
    print("\nB2 is not invertible.")
