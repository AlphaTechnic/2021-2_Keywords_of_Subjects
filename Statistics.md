# 1강

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



# 2강

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



# 3강

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



