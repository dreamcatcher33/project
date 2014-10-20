# MAFsnp: the score statistic

标签（空格分隔）： MAFsnp

##Outlines:
[TOC]

---
#1. The score statistics
- Parameters: $\theta_{j}= (p_j,e_j)$,
- log-Likelihood function:
\begin{equation}
    l_{j}(\theta_{j};X_{j},N_{j}) = \sum_{i=1}^I ln{Pr(X_{ij},G_{ij}|N_{ij},\theta_{j})}
\end{equation}
with
    $$Pr(X_{ij},G_{ij}|N_{ij},\theta_{j})= p_{j}^2B(X_{ij},N_{ij},1-e_{j})+2p_{j}(1- p_{j})B(X_{ij},N_{ij},0.5) + (1- p_{j})^2B(X_{ij},N_{ij},e_{j}),$$
where
$B(X_{ij},N_{ij},e_{j})=\binom{N_{ij}}{X_{ij}}e_{j}^{X_{ij}}(1-e_{j})^{N_{ij}-X_{ij}}$.

- Omit subscript $j$ in the following.
- Score function/vector $S(\theta) = (S_p,S_e)^{T}$ with $S_p(\theta)=\frac{\partial l(\theta)}{\partial p}$,$S_e(\theta)=\frac{\partial l(\theta)}{\partial e}$.

- Fisher's information matrix $I(\theta)=\begin{pmatrix} I_{11} & I_{12} \\ I_{12} & I_{22} \end{pmatrix}$ with 
- $I_{11} =-\frac{\partial^2 l(\theta)}{\partial p^2} $,$I_{12} =-\frac{\partial^2 l(\theta)}{\partial p \partial e} $,$I_{22} =-\frac{\partial^2 l(\theta)}{\partial e^2} $

- Hypothesis: $H_0: p=0$;
- $\hat{\theta}_0=(0,\hat{e})$ with $\hat{e}=\frac{\sum_i X_i}{\sum_i N_i}$.
- Score statistics: (I)
$$T = S^T(\hat{\theta}_0) I^{-1}(\hat{\theta}_0) S(\hat{\theta}_0) \sim \chi^2_k,k=2$$
- Score statistics: (II. approximation using profile likelihood )

$I^{11}(\theta) = \frac{I_{22}}{I_{11}I_{22}-I_{12}^2}=\frac{1}{I_{11}-\frac{I_{12}^2}{I_{22}}} \ge \frac{1}{I_{11}}$
$$T_{approx}=\frac{S_p(\hat{\theta}_0)^2}{(I^{11}(\hat{\theta}_0))^{-1}} \approx \frac{S_p(\hat{\theta}_0)^2}{I_{11}(\hat{\theta}_0)}$$

---
#2. Numeric representation of 2 score statistic

- Take simulation data $e = 0.01,c = 5,S = 50,p=0/3$ for example.



**Table 1:** $T$
| $\ge 0$ (%)        | $H_0$ data   | $H_1$ data  |
| --------   | -----:  | :----:  |
| $S_p(\hat{\theta}_0)$     | 2.343 |   99.94     |
| $S_e(\hat{\theta}_0)$        |   98.210  |   100   |
| $det(I(\hat{\theta}_0))$        |    97.807    |  2.68  |
| $T$        |   97.807     |  **2.68**  |

Table 2: $T.{approx}$
| $\ge 0$ (%)        | $H_0$ data   | $H_1$ data  |
| --------   | -----:  | :----:  |
| $S_p(\hat{\theta}_0)$     | 2.343 |   99.94     |
| $I_{11}(\hat{\theta}_0))$        |   100    |  100    |
| $T.approx$        |    100    |  100  |


Rk: We then let those score/det(I)<0 to be =0. data OK!

- summary of T:
```R
summary(T0)
#     Min.   1st Qu.    Median      Mean   3rd Qu.      Max.
#    0.000     0.000     0.000     0.258     0.000 17350.000

summary(T0.profile)
#   Min. 1st Qu.  Median    Mean 3rd Qu.    Max.
#0.00000 0.00000 0.00000 0.01054 0.00000 1.51200
```

- The estimation of $a$ and $k$

1. $T:a=0.989,k=0.925$;
2. $T.approx:a=0.977,k=0.692$;
![qqplot](http://ww4.sinaimg.cn/bmiddle/62725321jw1elhnttfwh7j20te0ebq45.jpg)



---
#3. compare with psudo-lrt
$e = 0.01,c = 5,S = 50,p=0,1,2,3$ and 
$e = 0.01,c = 10,S = 50,p=0,1,2,3$.
![c5](http://ww3.sinaimg.cn/mw1024/62725321jw1elhsyfugq8j21he0jxgon.jpg)
![c10](http://ww3.sinaimg.cn/mw1024/62725321jw1elhsye9ft4j21js0jvn03.jpg)




---


  [1]: http://ww1.sinaimg.cn/bmiddle/62725321jw1elhs3movhpj20ha0giaav.jpg