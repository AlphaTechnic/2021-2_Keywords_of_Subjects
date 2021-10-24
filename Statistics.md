# 2강

- Random(형용사스러움) = Probablity = Likelihood
- 표본공간 S = outcome들의 집합
  - {(1. 1), .., (6, 6)}
  - {HH, HT, TH, TT}
- 조건부확률
  - 정의 : 표본공간 S를 특정한 event들의 모임으로 제한
  - Bayes' Rule
- 확률변수 is 함수 s.t 표본 공간에서 정의된 실변수 함수 X : S -> R
  - X(HH) = 2
  - P(X = 2) = 1 / 4
  - 확률변수의 정의역에 따라
    - `discrete` if countable -> pmf = P(X = x) = 1/ 4
    - `conti` if uncountable -> pdf = P(a < X < b) = 1 / 4
  - cdf(cummulative)



# 3강

- 적률 (Moment)
  - $E(X)$, $E(X^2)$, ..
- 적률 생성 함수 (Moment generating func)
  - $E(exp(tX))$



- Special 분포 함수
  1. 베르누이 분포 -> 이항 분포
  2. 포아송 분포
  3. Uniform 분포
  4. 정규 분포
  5. 감마 분포
     1. 지수 분포
     2. 카이제곱 분포



# 4강

- Special 분포 함수
  1. 베르누이 분포 -> 이항 분포
  2. 포아송 분포 : **특정한 시간** 사건 발생 횟수
  3. Uniform 분포
  4. 정규 분포
  5. 감마 분포 : 첫 사건 발생까지 걸린 시간
     1. 지수 분포 ($\alpha$ = 1) : 망각 곡선
     2. 카이제곱 분포 ($\alpha$ = $\frac n 2$, $\beta$ = 2 )

- Joint(확률변수 2개) 확률 분포

  - `def` : f(x, y) = P(X = x, Y = y) = P(a < X < b, c < Y < d)

  - Marginal pmf of X

    - $f_X(x)$ = $\sum f(x, y)~ all~y$

  - 조건부 확률 분포

    - f(x | y) = f(x | Y = y) = $\frac {f(x,y)} {f_Y(y)}$

  - 조건부 기댓값 of g(X) given Y = y

    - E(g(X) | y) = E(g(X) | Y = y) =  $\sum g(x)f(x| y)~ all~x$

      (조건부 확률을 곱하는 것에 불과)



- 확률 변수들의 독립
  - f(x, y) a joint pdf X, Y, 확률변수가 서로 독립 $\Longleftrightarrow$ f(x, y) = $f_X(x)f_Y(y)$
  - E(g(X, Y)) = $\sum_{x, y} g(x, y)f(x, y)$



# 5강

- 독립
  - event가 독립 $\Leftrightarrow$ P(A$\cap$B) = P(A)P(B)
  - 확률변수(함수)가 독립 $\Leftrightarrow$ $f(x, y) = f_X(x)f_Y(y)$
  - E(aX+bY) = aE(X) + bE(Y) always
    - E(XY) = E(X)E(Y) if X, Y are independent

- Covariance, Correlation coefficient
  - Cov(X, Y) = E$((X - u_x)(Y - u_y))$
  - $\rho(X, Y) = \rho_{XY} = \frac {Cov(X, Y)} {\sqrt{Var(X)}\sqrt{Var(Y)}}$



- g(X, Y)의 pdf를 구하는 방법?
  1. cdf로 pdf 구하기
  2. diff, monotone인 상황에서 -> 미분(공식)
  3. 변수를 늘리는 방법



# 6강

- `Limit Theorem`
  - `Chebyshev's thm`
  - 
    - $P(|X - u_X| < k \sigma) \ge 1 - \frac 1 {k^2}$
  - `Weak Law of large numbers`
    - $\bar X \rightarrow \mu$ (확률적으로) as n -> $\infty$
  - `Strong Law of large numbers`
    - $\bar X \rightarrow \mu$  as n -> $\infty$
  - `Central limit thm`
    - $Z_n = \frac {\bar X - \mu} {\frac {\sigma} {\sqrt n}}$ -> N(0, 1) as n -> $\infty$



- Sampling Distributions
  - T(통계량) : function of observed random variables s.t unknown parameter가 없다
  - $\bar X = \frac {X_1 + .. +X_n} {n}$
  - $s^2 = \frac {1} {n - 1} \Sigma (X_i - \bar X)^2$
  - `Thm`
    - n이 1이건 2이건 상관 없이 $E(\bar X) = \mu$, $Var(\bar X) = \frac {\sigma ^2} {n}$



# 7강

(생략)



# 8강

- `Def` $\chi ^2 - distrib$ 
  - $X$ ~ $f(x) = \frac {1} {\beta ^ \alpha \Gamma(\alpha)} x^{\alpha - 1} exp(- \frac {x} {\beta})$ (x > 0)
    - E(X) = $\alpha \beta$
    - V(X) = $\alpha \beta ^2$
    - $M_x(t) = (1 - \beta t)^{-\alpha}$, $t < \frac 1 \beta$

- `Thm`
  - $X_1$ ~ $\chi^2(n _1)$, $X_2$ ~ $\chi^2(n _2)$ $\Rightarrow$ $\Sigma X_k$ ~ $\chi^2(n _1 + n_2)$
- `Thm`
  - $X$ ~ $N(0, 1)$ $\Rightarrow$ $X^2$ ~ $\chi^2(1)$
- `Thm`
  - $\Sigma Z^2$ ~ $\chi^2(n)$
- `Thm`
  - $\Sigma \frac {(X_i - \bar X)^2}{\sigma ^2} = \frac {(n-1)s^2}{\sigma ^2}$ ~ $\chi^2(n-1)$
- Student t - distrib (sample size 작들 때, 정규분포 대용으로)
  - T $\equiv$ $\frac {\bar X - \mu} {\frac {s} {\sqrt n}}$ ~ T(n - 1)



# 9강

- F - distrib => 2개의 population이 서로 다른 경우에 사용 (남자grp과 여자grp 라든가)
- U ~ $\chi^2(n _1)$, V ~ $\chi^2(n _2)$ => F $\equiv$ $\frac {\frac {U} {n_1}} {\frac {V} {n_2}}$ ~ F($n_1, n_2$)
- F $\equiv$ $\frac {\sigma_2 ^2 s_1^2} {\sigma_1^2 s_2 ^2}$ ~ F($n_1 - 1, n_2 -1$)



