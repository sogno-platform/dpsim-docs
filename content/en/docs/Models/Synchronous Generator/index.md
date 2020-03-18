---
title: "Synchronous Generator"
linkTitle: "Synchronous Generator"
date: 2020-03-18
markup: pandoc
---

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

## Basic Equations

The equations of the stator and rotor voltages are

\begin{align}
	\mathbf{v}_{abcs} &= \mathbf{R}_s \mathbf{i}_{abcs} + \frac{d}{dt} \boldsymbol{\lambda}_{abcs} \\
	\mathbf{v}_{dqr} &= \mathbf{R}_r \mathbf{i}_{dqr} + \frac{d}{dt} \boldsymbol{\lambda}_{dqr}
\end{align}

where

\begin{align}
  \mathbf{v}_{abcs} &=
  \begin{pmatrix}
    v_{as} & v_{bs} & v_{cs}
  \end{pmatrix}^T \\
  %
  \mathbf{v}_{dqr} &=
  \begin{pmatrix}
    v_{fd} & v_{kd} & v_{kq1} & v_{kq2}
  \end{pmatrix}^T \\
  %
  \mathbf{i}_{abcs} &=
  \begin{pmatrix}
    i_{as} & i_{bs} & i_{cs}
  \end{pmatrix}^T \\
  %
  \mathbf{i}_{dqr} &=
  \begin{pmatrix}
    i_{fd} & i_{kd} & i_{kq1} & i_{kq2}
  \end{pmatrix}^T \\
  %
  \boldsymbol{\lambda}_{abcs} &=
  \begin{pmatrix}
    \lambda_{as} & \lambda_{bs} & \lambda_{cs}
  \end{pmatrix}^T \\
  %
  \boldsymbol{\lambda}_{dqr} &=
  \begin{pmatrix}
    \lambda_{fd} & \lambda_{kd} & \lambda_{kq1} & \lambda_{kq2}
  \end{pmatrix}^T \\
  %
  \mathbf{R}_s &= diag
  \begin{bmatrix}
    R_s & R_s & R_s
  \end{bmatrix} \\
  %
  \mathbf{R}_r &= diag
  \begin{bmatrix}
    R_{fd} & R_{kd} & R_{kq1} & R_{kq2}
  \end{bmatrix}
\end{align}

The flux linkage equations are defined as

\begin{equation}
	\begin{bmatrix}
		\boldsymbol{\lambda}_{abcs} \\
		\boldsymbol{\lambda}_{dqr}
	\end{bmatrix}
	=
	\begin{bmatrix}
		\mathbf{L}_s & \mathbf{L}_{rs} \\
		{(\mathbf{L}_{rs})}^{T} & \mathbf{L}_r
	\end{bmatrix}
	\begin{bmatrix}
		\mathbf{i}_{abcs} \\
		\mathbf{i}_{dqr}
  \end{bmatrix}
\end{equation}

The inductance matrices are varying with the rotor position $\theta_r$ which varies with time.

The mechanical equations are:

\begin{align}
  \frac{d\theta_r}{dt} &= \omega_r \\
  \frac{d\omega_r}{dt} &= \frac{P}{2J} (T_e-T_m)
\end{align}

where $\theta_r$ is the rotor position, $\omega_r$ is the angular electrical speed, $P$ is the number of poles, $J$ is the moment of inertia, $T_m$ and $T_e$ are the mechanical and electrical torque, respectively. Motor convention is used for all models.
