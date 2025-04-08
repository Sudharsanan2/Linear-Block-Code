
# LINEAR BLOCK CODE
# AIM:
To perform linear block code using python.

# TOOLS REQUIRED:
IDE python with scipy and numpy

# PROGRAM:
import numpy as np

pb = []     
h_dis = [] 
r_code = []  
err = []     

col = int(input("Enter the Parity bits (n-k): "))
row = int(input("Enter the Message bits (k): "))

for i in range(row):
    p = list(map(int, input(f"Enter the row values {i+1} (Separated by space): ").split()))
    if len(p) != col:
        print("Error: Number of columns doesn't match the entered parity bit count.")
        exit()
    pb.append(p)

p_mat = np.array(pb, dtype=int)
Ik = np.eye(row, dtype=int)
g_mat = np.hstack((p_mat, Ik))  # G = [P | I]

n, k = g_mat.shape[1], g_mat.shape[0]

m = np.array([[1 if (i >> (k - j - 1)) & 1 else 0 for j in range(k)] for i in range(2 ** k)])

c = np.mod(np.dot(m, g_mat), 2)

for row in c:
    h_dis.append(np.sum(row))
h_mat = np.array(h_dis).reshape(-1, 1)

d_min = np.min(np.sum(c[1:], axis=1))

h = p_mat[:, :col]
hp = np.hstack((np.eye(col, dtype=int), h.T))
ht = hp.T  # H transpose

zero_row = np.zeros((1, ht.shape[1]), dtype=int)
hp1 = np.vstack((zero_row, ht))
 G = [P | I]:')
for r in g_mat:
    print(" ".join(map(str, r)))


print('\nMessage Bits  Codeword           Hamming Weight')
code_word = np.hstack((m, c, h_mat))
for r in range(code_word.shape[0]):
    message = " ".join(map(str, code_word[r, :k]))
    code = " ".join(map(str, code_word[r, k:k+n]))
    weight = str(code_word[r, -1])
    print(f'{message}\t{code}\t{weight}')

print(f'\nMinimum Hamming Distance (d_min): {d_min}')
print('\nParity Check Matrix H = [I | P^T]:')
for r in hp:
    print(" ".join(map(str, r)))

print('\nParity Check Matrix Transpose (H^T):')
for r in hp1:
    print(" ".join(map(str, r)))

rc = list(map(int, input(f"\nEnter the received codeword (space separated {n} bits): ").split()))
if len(rc) != n:
    print("Error: Length of received codeword must match the codeword length.")
    exit()

r_code.append(rc)
r_c = np.array(r_code)

e = np.mod(np.dot(r_c, ht), 2)
print(f"\nSyndrome of received codeword: {' '.join(map(str, e[0]))}")

for i in range(n):
    if np.array_equal(e[0], ht[i, :]):
        err = np.eye(n, dtype=int)[i, :]
        break
else:
    err = np.zeros(n, dtype=int)  # No error detected

print(f"Error position vector: {' '.join(map(str, err))}")

print('\nSyndrome Table:')
n1 = hp1.shape[0]
for i in range(n1):
    combined_row = np.concatenate((hp1[i, :], np.eye(n1, dtype=int)[i, :]))
    formatted_row = " ".join(map(str, combined_row[:hp1.shape[1]])) + '\t' + " ".join(map(str, combined_row[hp1.shape[1]:]))
    print(formatted_row)

corrected = (np.array(rc) + err) % 2
print(f"\nCorrected codeword: {' '.join(map(str, corrected))}")
OUTPUT:
lcb 1 lcb 2

# OUTPUT

![c](https://github.com/user-attachments/assets/837e2fc2-a4c3-45e2-bc55-3ed0c8b9b9f8)
![b](https://github.com/user-attachments/assets/c8b96138-b1e2-44ec-a3f0-bf88a8e2dfc4)



# RESULT:
Thus ,The linear block code was successfully implemented for error detection and single-bit error correction.

