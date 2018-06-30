:tocdepth: 3


Process Noise Covariance Matrix
********************************


The process covariance acts as a weighting matrix for the system process.  It relates the covariance
between the :math:`i^{th}` and :math:`j^{th}` element of each process-noise vector.  It is defined
as:

.. math::

    \Sigma_{ij} = cov{ \begin{pmatrix} {
                                         \vec{x}_{i},\vec{x}_{j}
                       } \end{pmatrix}
                     }
                = E{ \begin{bmatrix} {
                                       { \begin{pmatrix} { \vec{x}_{i}-\mu_{i} } \end{pmatrix} }
                                       \cdot
                                       { \begin{pmatrix} { \vec{x}_{j}-\mu_{j} } \end{pmatrix} }
                     } \end{bmatrix}
                   }


A Kalman Filter essentially multiplies Gaussians to form state estimates.  :math:`Q` is a measure of
the width of the Gaussian distribution for each state.  The wider the distribution, the more
uncertainty exists in the process model.  This leads to a state-update that affects the state more
than if the model had a tighter distribution, which results in an update having less influence on
the particular state.


Based on the state process-noise vectors, :math:`\vec{w}_{k}` (found above), the Process Noise
Covariance Matrix is:

.. math::

    Q_{k} =  { \begin{bmatrix} { { \Sigma_{r} \\
                                       0_{3} \\
                                       0_{4 \times 3} \\
                                       0_{3} \\
                                       0_{3}
                                     } \hspace{5mm}
                                     { 0_{3} \\
                                       \Sigma_{v} \\
                                       0_{4 \times 3} \\
                                       0_{3} \\
                                       0_{3}
                                     } \hspace{5mm}
                                     { 0_{3 \times 4} \\
                                       0_{3 \times 4} \\
                                       \Sigma_{q} \\
                                       0_{3 \times 4} \\
                                       0_{3 \times 4}
                                     } \hspace{5mm}
                                     { 0_{3} \\
                                       0_{3} \\
                                       0_{4 \times 3} \\
                                       \Sigma_{\omega b} \\
                                       0_{3}
                                     } \hspace{5mm}
                                     { 0_{3} \\
                                       0_{3} \\
                                       0_{4 \times 3} \\
                                       0_{3} \\
                                       \Sigma_{ab}
                                     }
                     } \end{bmatrix}
                   }



The individual process covariance (derived in the sections above) are repeated here:

.. math::

    \Sigma_{r} = {\begin{pmatrix} { \sigma_{a} \cdot {dt}^{2} } \end{pmatrix}}^{2} \cdot I_3

.. math::

    \Sigma_{v} = {\begin{pmatrix} { \sigma_{a} \cdot dt } \end{pmatrix}}^{2} \cdot I_3

.. math::

    \Sigma_{q} = {\begin{pmatrix} {{\sigma_{\omega} \cdot dt } \over {2}} \end{pmatrix}}^{2}
                 \cdot
                 \begin{bmatrix} { { {1 - q_0^2}\\
                                     -{q_0 \cdot q_1}\\
                                     -{q_0 \cdot q_2}\\
                                     -{q_0 \cdot q_3}
                                   } \hspace{5mm}
                                   { -{q_0 \cdot q_1}\\
                                     {1 - q_1^2}\\
                                     -{q_1 \cdot q_2}\\
                                     -{q_1 \cdot q_3}
                                   } \hspace{5mm}
								   { -{q_0 \cdot q_2}\\
                                     -{q_1 \cdot q_2}\\
                                     {1 - q_2^2}\\
                                     -{q_2 \cdot q_3}
                                   } \hspace{5mm}
								   { -{q_0 \cdot q_3}\\
                                     -{q_1 \cdot q_3}\\
                                     -{q_2 \cdot q_3}\\
                                     {1 - q_3^2}
                                   }
                 } \end{bmatrix}

.. math::

    \Sigma_{\omega b} = {\begin{pmatrix} { \sigma_{dd,\omega} \cdot dt } \end{pmatrix}}^{2} \cdot I_3

.. math::

    \Sigma_{ab} = {\begin{pmatrix} { \sigma_{dd,a} \cdot dt } \end{pmatrix}}^{2} \cdot I_3