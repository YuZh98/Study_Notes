### Casual Inference 10/10/23



<u>**Agenda: The Change-in-Change method**</u>



<u>Repeated Cross-Sectional Design</u>

$(y_i,G_i,T_i)\leftarrow$ observed data from individual $i$

$G_i=\begin{cases}0,\;\text{if the individual is not treated}\\1,\;\text{if the individual is treated}\end{cases}$  $T_i=\begin{cases}0,\;\text{in the pre-treatment}\\1,\;\text{in the post-treatment}\end{cases}$

<u>Potential Outcomes</u> $(y_i(1),y_i(0),G_i,T_i)$

<u>No-anticipation</u> if $T_i=0$, then $y_i(0)=y_i(1)$.
$$
y_i=y_i(1)\cdot G_i\times T_i + y_i(0)\cdot(1-G_i\times T_i)
$$
<u>Campbell's model</u>
$$
y_i=\alpha+\beta G_iT_i+\gamma G_i+\delta T_i+\varepsilon_i
$$

$$
\mathbb E(y_i(1)-y_i(0)|G_i=1,T_i=1)\leftarrow \text{ATT}
$$

Under Campbell's model
$$
\begin{aligned}
\text{ATT}=\beta=&\mathbb E(y_i|G_i=1,T_i=1)-\mathbb E(y_i|G_i=1,T_i=0)\\
& -[\mathbb E(y_i|G_i=0,T_i=1)-\mathbb E(y_i|G_i=0,T_i=0)]
\end{aligned}
$$
$\exist$ $U_i$ correlated with the group indicator $G_i$. $U_i$ is a confounder associated with the potential outcomes.

##### <u>**The Change-in-Change Model**</u>

$$
y_i(0)=h(U_i,T_i) \text{ for some function }h
$$

*This is a generalization of Campbell's model: Take $U_i=\gamma G_i+\varepsilon_i$ and $h(u,t)=u+\alpha+\delta t$.

<u>**Assumptions:**</u> 

1. <u>Monotonicity:</u> $u\to h(u,1)$ and $u\to h(u,0)$ are strictly monotone in $u$
2. <u>Time invariance:</u> $U_i\perp T_i\mid G_i$ (how to relax this assumption can be a final project for this course)

$$
\begin{aligned}
\text{ATT}&=\mathbb E(y_i(1)-y_i(0)|G_i=1,T_i=1)\\
&=\mathbb E(y_i(1)|G_i=1,T_i=1)-\mathbb E(y_i(0)|G_i=1,T_i=1)\\
&=\mathbb E(y_i|G_i=1,T_i=1)-\underbrace{\mathbb E(y_i(0)|G_i=1,T_i=1)}_{?}
\end{aligned}
$$

<u>**Theorem:**</u> Under the change-in-change model, if monotonicity and time invariance are satisfied, then
$$
F_{y_i(0),11}(y)=F_{y_i(0),10}\left(F^{-1}_{y_i(0),00}\left(F_{y_i(0),01}(y)\right)\right)
$$
where $F_{y_i(0),gt}(y)=Pr(y_i(0)\leq y|G_i=g,T_i=t)$.

*proof:* 
$$
\begin{aligned}
F_{y_i(0),gt}(y)&=Pr(y_i(0)\leq y|G_i=g,T_i=t)\\
&= Pr(h(U_i,T_i)\leq y|G_i=g,T_i=t)\\
&=Pr(h(U_i,t)\leq y|G_i=g,T_i=t)\\
&=Pr(h(U_i,t)\leq y|G_i=g)\\
&=Pr(U_i\leq h^{-1}(y;t)|G_i=g)
\end{aligned}
$$

$$
\begin{aligned}
&F_{y_i(0),00}(y)=Pr(U_i\leq h^{-1}(y;0)|G_i=0)\\
\Rightarrow &F_{y_i(0),00}(h(h^{-1}(y;1);0))=Pr(U_i\leq h^{-1}(y;1)|G_i=0)=F_{y_i(0),01}(y)
\end{aligned}
$$

$$
F_{y_0(0),10}(y)=Pr(U_i\leq h^{-1}(y;0)\mid G_i=1)\\
\Rightarrow F_{y_i(0),10}(h(u,0))=Pr(U_i\leq u|G_i=1)
$$

$$
\begin{aligned}
F_{y_i(0),11}(y)&=Pr(U_i\leq h^{-1}(y;1)|G_i=1)\\
&=F_{y_i(0),10}\left(h\left(h^{-1}(y;1);0\right)\right)\\
&=F_{y_i(0),10}\left(F^{-1}_{y_i(0),00}\left(F_{y_i(0),01}(y)\right)\right)
\end{aligned}
$$




$$
F_{y_i(0),00}=F_{y_i,00}\\
F_{y_i(0),01}=F_{y_i,01}\\
F_{y_i(0),10}=F_{y_i,10}
$$




### Casual Inference 10/12/23

<u>**Agenda: (1) Confounding in panel data; (2) Complexities in panel data structure.**</u>



$y_{it}$          $D_{it}$

Unit-specific confounder $U_i$

Time-specific confounder $V_t$



- <u>Unit-Specific Confounder:</u>
  $$
  y_{it}=\alpha + h(U_i) + \beta D_{it} + \varepsilon_{it},\quad i=1,\ldots,N;\;t=1,\ldots,T.
  $$

  $$
  y_{it}-\bar{y}_{i\cdot}=\beta(D_{it}-\bar{D}_{i\cdot})+(\varepsilon_{it}-\bar{\varepsilon}_{i\cdot})
  $$

  $\beta=$ OLS estimate is a causal estimate as long as you have only unit specific confounder and the additive model.

  Equivalently, we can write the model as
  $$
  y_{it}=\alpha + \mu_i + \beta D_{it} + \varepsilon_{it},\quad i=1,\ldots,N;\;t=1,\ldots,T,
  $$
  which is a <u>one-way fixed effect model</u>.

   

- <u>Time-Specific Confounder:</u>
  $$
  y_{it}=\alpha+f(V_t)+\beta D_{it}+\varepsilon_{it}
  $$

  $$
  y_{it}-\bar{y}_{\cdot t}=\beta(D_{it}-\bar{D}_{\cdot t})+(\varepsilon_{it}-\bar\varepsilon_{\cdot t})
  $$

  $$
  \begin{aligned}
  \hat\beta&=\frac{\sum_i\sum_t(y_{it}-\bar{y}_{\cdot t})(D_{it}-\bar{D}_{\cdot t})}{\sum_i\sum_t(D_{it}-\bar{D}_{\cdot t})^2}\\
  &=\frac{\sum_i\sum_t(D_{it}-\bar{D}_{\cdot t})^2\cdot\frac{\sum_t(y_{it}-\bar{y}_{\cdot t})(D_{it}-\bar{D}_{\cdot t})}{\sum_t(D_{it}-\bar{D}_{\cdot t})^2}}{\sum_i\sum_t(D_{it}-\bar{D}_{\cdot t})^2}\\
  &=\frac{\sum_i w_i\hat{\beta}_i}{\sum_iw_i}
  \end{aligned}
  $$

  where $w_i=\sum_t(D_{it}-\bar{D}_{\cdot t})^2$ and $\hat\beta_i=\frac{\sum_t(y_{it}-\bar{y}_{\cdot t})(D_{it}-\bar{D}_{\cdot t})}{\sum_t(D_{it}-\bar{D}_{\cdot t})^2}$. 



Based on the estimator, we have the two notes:

1. One-way fixed effect with only time-specific confounder is practically sensible if we assume that the treatment effect is homogeneous across units (Similar statement holds for the unit-specific one way fixed effect model);
2. The form of the time-specific or unit-specific confounder does not matter.



- <u>Time-specific and unit-specific confounder:</u>
  $$
  \begin{aligned}
  y_{it}&=\alpha+f(V_t)+h(U_i)+\beta D_{it}+\varepsilon_{it}\\
  &=\alpha+\theta_t+\mu_i+\beta D_{it}+\varepsilon_{it}
  \end{aligned}
  $$
  This model is called <u>2-way fixed effect model</u>. (Does not identify any causal quantity)

  If we only had two time periods $t=0,1$, then there is one unknown $\theta_t$.

  Remember Campbell's model
  $$
  y_i=\alpha+\beta G_iT_i+\gamma G_i+\eta T_i+\varepsilon_i
  $$

  |         | $T_i=0$ | $T_i=1$ |
  | :-----: | :-----: | :-----: |
  | $G_i=0$ |    0    |    0    |
  | $G_i=1$ |    0    |    1    |

  The two models share resemblance but the 2-way fixed effect model does not identify any causal quantity as mentioned earlier.

  Potential Outcomes
  $$
  y_{it}(0), \; y_{it}(1),\; y_{it}=y_{it}(0)(1-D_{it})+y_{it}(1)D_{it}
  $$

  $$
  \text{ATT}_t=\mathbb E(y_{it}(1)-y_{it}(0)\mid D_{it}=1)\\
  \text{ATT}=\frac{1}{T}\sum_t\text{ATT}_t
  $$

  $$
  \widehat{\text{ATT}}=\frac{1}{\sum_i\sum_t D_{it}N_{t}}\sum_i\sum_t N_{t}D_{it}(y_{it}-\widehat{y_{it}(0)})\\
  \widehat{y_{it}(0)}=y_{i(t-1)}+\frac{1}{\sum_i1_{(D_{it}=0,\, D_{i(t-1)=0})}}\sum_{i':D_{i't}=0,\,D_{i'(t-1)=0}}(y_{i't}-y_{i'(t-1)})\\
  N_{t}=\begin{cases}
  1,\quad\text{if }\sum_{i'}1_{(D_{i't}=0,\,D_{i'(t-1)=0})}>0,\\
  0,\quad\text{otherwise.}
  \end{cases}
  $$

  $\widehat{\text{ATT}}$ is constant for ATT, under parallel trends.











If only a small number of units (in the extreme case just one unit is treated)



#### <u>**Synthetic Control**</u>

<u>Covariate information</u>

1. Covariates that are affected by the treatment (avoid them)
2. Time varying confounder ($g$-computation & Marginal Structural Model)
3. Loss to follow up (assume ignorable loss to follow up)























































