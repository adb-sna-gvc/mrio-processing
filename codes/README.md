
# Custom functions

The file `functions.py` contain custom functions that aid in the matrix operations performed in the notebooks. The following describes these functions and presents a visual illustration of what they do.

## ind

`ind(s, i=None, G=G, N=N)`

Selects the indices of country $s$ in any $G \times N$ array. Optional argument `i` selects a specific element in the array. With three countries $C$, $J$, and $U$ and two sectors 1 and 2, 

$$
\begin{alignat*}{3}
  & \texttt{Z[ind(0), ind(1)]} \qquad & & \begin{bmatrix}
        z_{(C1,C1)} & z_{(C1,C2)} & \textcolor{blue}{z_{(C1,J1)}} & \textcolor{blue}{z_{(C1,J2)}} & z_{(C1,U1)} & z_{(C1,U2)} \\
        z_{(C2,C1)} & z_{(C2,C2)} & \textcolor{blue}{z_{(C2,J1)}} & \textcolor{blue}{z_{(C2,J2)}} & z_{(C2,U1)} & z_{(C2,U2)} \\
        z_{(J1,C1)} & z_{(J1,C2)} & z_{(J1,J1)} & z_{(J1,J2)} & z_{(J1,U1)} & z_{(J1,U2)} \\
        z_{(J2,C1)} & z_{(J2,C2)} & z_{(J2,J1)} & z_{(J2,J2)} & z_{(J2,U1)} & z_{(J2,U2)} \\
        z_{(U1,C1)} & z_{(U1,C2)} & z_{(U1,J1)} & z_{(U1,J2)} & z_{(U1,U1)} & z_{(U1,U2)} \\
        z_{(U2,C1)} & z_{(U2,C2)} & z_{(U2,J1)} & z_{(U2,J2)} & z_{(U2,U1)} & z_{(U2,U2)} \\
  \end{bmatrix} \\
\end{alignat*}
$$

## asvector

`asvector(matrix)`

Flattens a matrix into a column vector. This uses the so-called Fortran order, meaning it first goes down a column before moving to the next column. 



## zeroout

`zeroout(matrix, row=None, col=None, inverse=False, steps=G)`

Zeroes out a block of arbritrary dimensions in a matrix. Under default arguments, the function zeroes out the block diagonals. If `inverse=True`, everything but the block diagonals is zeroed out. Specifying `row` and `col` lets one zero out a specific block of the matrix.

$$
\begin{alignat*}{3}
  & \texttt{zeroout(.)} \qquad & & \begin{bmatrix}
    0 & 0 & \times & \times & \times & \times \\
    0 & 0 & \times & \times & \times & \times \\
    \times & \times & 0 & 0 & \times & \times \\
    \times & \times & 0 & 0 & \times & \times \\
    \times & \times & \times & \times & 0 & 0 \\
    \times & \times & \times & \times & 0 & 0 \\
  \end{bmatrix} \\ \\
  & \texttt{zeroout(., inverse=True)} \qquad & & \begin{bmatrix}
    \times & \times & 0 & 0 & 0 & 0 \\
    \times & \times & 0 & 0 & 0 & 0 \\
    0 & 0 & \times & \times & 0 & 0 \\
    0 & 0 & \times & \times & 0 & 0\\
    0 & 0 & 0 & 0 & \times & \times \\
    0 & 0 & 0 & 0 & \times & \times \\
  \end{bmatrix} \\ \\
  & \texttt{zeroout(., row=[0,1], col=[2,3])} \qquad & & \begin{bmatrix}
    \times & \times & 0 & 0 & \times & \times \\
    \times & \times & 0 & 0 & \times & \times \\
    \times & \times & \times & \times & \times & \times \\
    \times & \times & \times & \times & \times & \times \\
    \times & \times & \times & \times & \times & \times \\
    \times & \times & \times & \times & \times & \times \\
  \end{bmatrix}
\end{alignat*}
$$