---
topic: Многочлены, кольца и поля
subtopic: "Vieta, симметрические многочлены, тождества Newton"
sources:
  - "Engel — Problem-Solving Strategies (гл. Polynomials, Inequalities)"
  - "Polya, Szegő — Problems and Theorems in Analysis II (отдел V: symmetric functions, Newton's inequalities)"
  - "Prasolov — Polynomials"
  - "Macdonald — Symmetric Functions and Hall Polynomials (гл. I)"
  - "Mildorf — Olympiad Inequalities (AoPS, 2006)"
  - "K. Conrad — Newton's Identities (expository)"
  - "M. Mossé — Newton's Identities (Stanford, 2019)"
  - "Hardy, Littlewood, Pólya — Inequalities (Newton, Maclaurin)"
  - "Niven — Maxima and Minima Without Calculus (sym. fns)"
  - "AoPS Wiki — Newton's Sums / Vieta's Formulas / Maclaurin's Inequality"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "Wikipedia — Newton's identities / Newton's inequalities / Faulhaber's formula / Hermite–Biehler theorem / Schur-convex"
problems_referenced:
  - IMC-1996-DAY2-2
  - IMC-1998-5
  - IMC-1998-DAY2-2
  - IMC-2000-2
  - IMC-2000-DAY2-3
  - IMC-2002-3
  - IMC-2005-4
  - IMC-2006-DAY2-5
  - IMC-2009-DAY2-3
  - IMC-2014-3
  - IMC-2017-7
  - IMC-2020-4
  - IMC-2024-7
  - Putnam-2003-A4
  - Putnam-1973-A4
last_updated: 2026-04-27
---

# Vieta, симметрические многочлены, тождества Newton

## Scope
Связь между корнями и коэффициентами многочлена через elementary symmetric polynomials $e_k$ (Vieta), мост к power sums $p_k$ через Newton–Girard identities, fundamental theorem of symmetric polynomials, log-derivative $P'/P$ как генератор power sums, дискриминант через Vandermonde, Newton / Maclaurin неравенства как тест real-rootedness, Descartes / Cauchy / Eneström–Kakeya для контроля корней, типовые олимпиадные приёмы — power sums к eigenvalues матриц, Faulhaber через Bernoulli, divided differences $\frac{P(x)-P(y)}{x-y}$, AM-GM на Vieta для оценки степени. Exotic — Muirhead / Schur convexity, Hermite–Biehler interlacing, Newton–Girard в положительной характеристике.

## Записи — Core

### E1. Vieta's formulas (формулы Виета)

Формулировка. Пусть $f(x) = a_n x^n + a_{n-1} x^{n-1} + \dots + a_0 \in K[x]$, $a_n \ne 0$, и $\alpha_1, \dots, \alpha_n$ — все корни в алгебраическом замыкании (с кратностями). Тогда $k$-й elementary symmetric polynomial корней
$$e_k(\alpha_1, \dots, \alpha_n) = \sum_{i_1 < \dots < i_k} \alpha_{i_1} \cdots \alpha_{i_k} = (-1)^k \frac{a_{n-k}}{a_n}.$$
В частности, $\sum \alpha_i = -a_{n-1}/a_n$ и $\prod \alpha_i = (-1)^n a_0/a_n$.

Условия применимости. Любое поле $K$. Корни считаются с кратностями в $\bar K$.

Идея доказательства. Раскрыть $a_n \prod (x - \alpha_i)$ и сравнить коэффициенты.

Используется в. Везде, где задача про корни. [IMC-2000-2, IMC-2005-4, IMC-2006-DAY2-5, IMC-2024-7].

---

### E2. Newton–Girard identities (тождества Ньютона–Жирара)

Формулировка. Для $p_k = \alpha_1^k + \dots + \alpha_n^k$ ($k \ge 1$) и elementary $e_k$:
$$p_k - e_1 p_{k-1} + e_2 p_{k-2} - \dots + (-1)^{k-1} e_{k-1} p_1 + (-1)^k k\, e_k = 0, \quad 1 \le k \le n,$$
$$p_k - e_1 p_{k-1} + e_2 p_{k-2} - \dots + (-1)^n e_n p_{k-n} = 0, \quad k > n.$$
По соглашению $p_0 = n$, $e_0 = 1$, $e_k = 0$ при $k > n$.

Условия применимости. $\operatorname{char}(K) = 0$ или $\operatorname{char}(K) > k$ для $1 \le k \le n$ — иначе $k$ может быть нулём в $K$ (см. exotic E18). Над $\mathbb{Z}$ всё работает.

Идея доказательства. Логарифмическая производная: $\sum \frac{1}{x - \alpha_i} = \frac{f'(x)}{f(x)}$. Разложение в ряд по $1/x$: $\frac{f'(x)}{f(x)} = \sum_k \frac{p_k}{x^{k+1}}$, и $f(x) = a_n \prod(x - \alpha_i)$, перемножение даёт рекуррентность. Альтернатива — генерирующая функция $E(t) = \prod(1+\alpha_i t) = \sum e_k t^k$, $P(t) = \sum p_k t^{k-1}$, тождество $E'(t)/E(t) = P(-t)$.

Варианты и обобщения.
- В обратную сторону: $e_k$ через $p_1, \dots, p_k$ — формула Бринта / детерминантная (см. также Jacobi–Trudi).
- Complete homogeneous $h_k$ удовлетворяют аналогичному тождеству $k h_k = \sum_{i=1}^k p_i h_{k-i}$ (без знаков).

Используется в. Стандартный мост между «коэффициенты ↔ степенные суммы». [IMC-1998-5, IMC-2009-DAY2-3, IMC-2002-3 (косвенно)].

---

### E3. Fundamental theorem of symmetric polynomials (основная теорема о симметрических многочленах)

Формулировка. Любой симметрический многочлен $\Phi \in R[x_1, \dots, x_n]$ единственным образом представляется как $\Phi = \Psi(e_1, \dots, e_n)$ для некоторого $\Psi \in R[y_1, \dots, y_n]$. Если $R \supseteq \mathbb{Q}$, то аналогично для $\Psi(p_1, \dots, p_n)$ и $\Psi(h_1, \dots, h_n)$.

Условия применимости. Любое коммутативное кольцо $R$ для $e$-базиса. Для $p$-базиса — нужно деление на $1, 2, \dots, n$, т.е. $R \supseteq \mathbb{Q}$ (или $\operatorname{char}$ больше $n$).

Идея доказательства. Лексикографический алгоритм: старший моном $x_1^{a_1} \cdots x_n^{a_n}$ с $a_1 \ge \dots \ge a_n$ убивается вычитанием $c \cdot e_1^{a_1 - a_2} e_2^{a_2 - a_3} \cdots e_n^{a_n}$ — индукция по лексикографическому старшему моному.

Используется в. Каждый раз, когда симметрическая функция от корней редуцируется к функции от коэффициентов, при отсутствии явных корней. [IMC-2024-7] косвенно через симметрию по eigenvalues.

---

### E4. Power sums determine roots up to permutation (степенные суммы определяют мультимножество корней)

Формулировка. Пусть $\alpha_1, \dots, \alpha_n$ и $\beta_1, \dots, \beta_n$ — два мультимножества элементов поля $K$ характеристики $0$ (или $\operatorname{char} K > n$). Если $\sum \alpha_i^k = \sum \beta_i^k$ для $k = 1, 2, \dots, n$, то мультимножества совпадают.

Условия применимости. $\operatorname{char} K = 0$ или $> n$. Для $\operatorname{char} K = p \le n$ контрпример: $1^p + \dots = $ может совпадать без совпадения мультимножеств.

Идея доказательства. По Newton (E2) $p_1, \dots, p_n$ определяют $e_1, \dots, e_n$ (рекуррентно, нужно делить на $1, 2, \dots, n$). Значит характеристический многочлен $\prod (x - \alpha_i)$ совпадает с $\prod(x - \beta_i)$, и корни — те же с кратностями.

Варианты и обобщения.
- Достаточно $p_k$ для $k = 1, \dots, n$; больших $k$ не нужно.
- В $\operatorname{char} p$ срабатывает «Frobenius»: $\sum \alpha_i^p = (\sum \alpha_i)^p$.

Используется в. [IMC-2009-DAY2-3: $\operatorname{tr}(X^k) = 0$ для $k = 1, \dots, n$ ⇒ все eigenvalues $X$ нулевые ⇒ $X$ nilpotent], [Putnam-2003-A4].

---

### E5. Logarithmic derivative identity $f'/f = \sum 1/(x-\alpha_i)$ (логпроизводная и SOS)

Формулировка. Для $f(x) = a_n \prod(x - \alpha_i)$ имеем $\frac{f'(x)}{f(x)} = \sum_i \frac{1}{x - \alpha_i}$. Дифференцируя ещё раз:
$$\left(\frac{f'}{f}\right)^2 - \frac{f'^2 - f f''}{f^2} = -\frac{f''}{f} + 2 \frac{f'^2}{f^2} - \frac{f'^2}{f^2} \Rightarrow \frac{(f')^2 - f f''}{f^2} = \sum_i \frac{1}{(x-\alpha_i)^2}.$$
Алгебраическая форма (IMC-1998-5):
$$(n-1)\left(\frac{f'}{f}\right)^2 - n \cdot \frac{f''}{f} = \sum_{i < j} \left(\frac{1}{x-\alpha_i} - \frac{1}{x-\alpha_j}\right)^2 \ge 0.$$

Условия применимости. $f \in \mathbb{R}[x]$ или $\mathbb{C}[x]$ с любыми (возможно комплексными) корнями; SOS-форма $\ge 0$ имеет смысл при $x \in \mathbb{R}$ и $\alpha_i \in \mathbb{R}$. Равенство $\iff$ все корни совпадают.

Идея доказательства. Раскрыть $\sum_{i<j}(\cdot)^2 = (n-1) \sum_i 1/(x-\alpha_i)^2 - 2\sum_{i<j} 1/((x-\alpha_i)(x-\alpha_j))$, далее $\sum 1/(x-\alpha_i)^2 = (f'/f)^2 - f''/f$ и $\sum_{i<j}1/((x-\alpha_i)(x-\alpha_j)) = \frac12((f'/f)^2 - \sum 1/(x-\alpha_i)^2)$.

Варианты и обобщения.
- Следствие: $(n-1)(f')^2 \ge n f f''$ для вещественных корней $f$ (Newton inequality в дифференциальной форме).
- $\sum 1/(x - \alpha_i)^k = $ детерминантная формула через power sums (генерирующая функция).

Используется в. [IMC-1998-5], а также в задачах на оценку дискриминанта через коэффициенты. Newton inequality (E7) выводится отсюда подстановкой $x \to \infty$ и анализом коэффициентов.

---

### E6. Discriminant через Vandermonde и power sums

Формулировка. Дискриминант многочлена $f(x) = a_n \prod(x - \alpha_i)$:
$$\Delta(f) = a_n^{2n-2} \prod_{i<j} (\alpha_i - \alpha_j)^2 = a_n^{2n-2} \det\left(p_{i+j-2}\right)_{i,j=1}^n,$$
где $p_0 = n, p_1, \dots, p_{2n-2}$ — power sums корней. Вторая форма — определитель Грамма от $1, \alpha, \alpha^2, \dots$.

Условия применимости. Любое поле, $a_n \ne 0$. $\Delta(f) = 0 \iff$ есть кратный корень.

Идея доказательства. $V = (\alpha_i^{j-1})_{i,j}$ — Vandermonde; $\det V = \prod_{i<j}(\alpha_j - \alpha_i)$. Тогда $V V^T = (\sum_i \alpha_i^{j+k-2})_{j,k} = (p_{j+k-2})_{j,k}$, откуда $(\det V)^2 = \det(p_{j+k-2})$. Множитель $a_n^{2n-2}$ возникает из нормировки $\Delta$.

Варианты и обобщения.
- Для $f(x) = x^3 + px + q$: $\Delta = -4p^3 - 27q^2$. Знак $\Delta$ для $f \in \mathbb{R}[x]$ кубического: $\Delta > 0 \iff$ три различных вещественных корня.
- Resultant: $\Delta(f) = (-1)^{n(n-1)/2} a_n^{-1} \operatorname{Res}(f, f')$ — связь с подтемой Resultant.

Используется в. Связующее звено между «есть ли кратный корень» и явной алгеброй коэффициентов; приходит в задачах на параметризацию (когда коэффициенты зависят от параметра, $\Delta$ как многочлен).

---

### E7. Newton's inequalities (неравенства Ньютона) и log-concavity

Формулировка. Для $f(x) = \prod (x + \alpha_i)$ с $\alpha_i \in \mathbb{R}$ (т.е. $f$ real-rooted) и $E_k = e_k/\binom{n}{k}$ — нормированные элементарные:
$$E_k^2 \ge E_{k-1} E_{k+1}, \quad 1 \le k \le n-1.$$
Эквивалентно: коэффициенты real-rooted многочлена с положительными $\alpha_i$ образуют log-concave последовательность $a_k^2 \ge a_{k-1} a_{k+1} \cdot \frac{(k+1)(n-k+1)}{k(n-k)}$.

Условия применимости. Необходимость — все корни вещественны (знак не важен, но классическая форма для $\alpha_i \ge 0$). Обратное, в общем, неверно: log-concavity не гарантирует real-rootedness.

Идея доказательства. Индукция по $n$ + операция «деления на $(x + \alpha_n)$» + теорема Ролля сохраняет real-rootedness и нужные неравенства. Альтернатива: $\sum 1/(x - \alpha_i)^2 \ge 0$ для вещественных корней + анализ коэффициентов.

Варианты и обобщения.
- **Maclaurin** (см. E8) выводится из Newton цепочкой.
- Log-concavity для real-rooted влечёт unimodality.
- В обратную сторону, real-stable polynomials (Borcea–Brändén): большая теория.

Используется в. [IMC-2017-7] косвенно через анализ числа смен знаков, [IMC-2016-9: log-concavity multidim], олимпиадные неравенства между $e_k$ при заданных $\sum, \sum^2$ и т.п.

---

## Записи — Standard

### E8. Maclaurin's inequality (неравенство Маклорена)

Формулировка. Для $\alpha_1, \dots, \alpha_n > 0$ и $S_k = \binom{n}{k}^{-1} e_k(\alpha_1, \dots, \alpha_n)$:
$$S_1 \ge S_2^{1/2} \ge S_3^{1/3} \ge \dots \ge S_n^{1/n},$$
с равенством $\iff$ $\alpha_1 = \dots = \alpha_n$. Левый край $S_1 = $ AM, правый $S_n^{1/n} = $ GM, поэтому AM-GM — частный случай.

Условия применимости. Все $\alpha_i > 0$. Без положительности $S_k^{1/k}$ может не быть определено.

Идея доказательства. Чейн из Newton (E7): из $S_k^2 \ge S_{k-1} S_{k+1}$ и $S_0 = 1$ телескопически получаем $S_k^{1/k} \ge S_{k+1}^{1/(k+1)}$.

Варианты и обобщения.
- **Schur-Маклорен**: можно усилить до интегральных версий.
- Для general real-rooted $f$ с положительными коэффициентами — те же оценки с заменой $\alpha_i \to -\alpha_i$.

Используется в. Стандартный молот для симметрических неравенств. На IMC прямого появления почти нет, но оно неявно за каждым неравенством на симметрии $e_k$.

---

### E9. Descartes' rule of signs (правило знаков Декарта)

Формулировка. Пусть $f(x) = a_n x^n + \dots + a_0 \in \mathbb{R}[x]$ со всеми ненулевыми коэффициентами по своему списку. Число положительных вещественных корней (с кратностями) равно числу смен знака в последовательности $a_n, a_{n-1}, \dots, a_0$ или меньше его на чётное число. Аналогично для отрицательных корней — через $f(-x)$.

Условия применимости. $f \in \mathbb{R}[x]$. Нулевые коэффициенты пропускаются при подсчёте смен знака.

Идея доказательства. Индукция: операция «домножить на $(x - r)$» с $r > 0$ увеличивает число смен знака на нечётное число. Альтернатива через теорему Ролля.

Варианты и обобщения.
- **Budan–Fourier** — обобщение для интервала $[a, b]$.
- **Sturm's theorem** — точное число вещественных корней на $[a, b]$.

Используется в. [IMC-2014-3: $a_k = q^{k(k-1)/2}$ — лакунарный многочлен; число смен знака $= n$ для подходящих $\pm$, значит $n$ различных вещественных корней], [IMC-2017-7: запрет real-rootedness через анализ числа смен знака]. Часто в Putnam и национальных олимпиадах.

---

### E10. Symmetric reduction $\frac{P(x) - P(y)}{x - y}$ (divided differences для симметризации)

Формулировка. Для $P \in K[t]$ и $x \ne y$ выражение $\frac{P(x) - P(y)}{x - y}$ — многочлен от $x, y$, симметрический в обмен $x \leftrightarrow y$ (после симметризации). Любой такой полином представим как $\sum c_{ij}(x+y)^i(xy)^j$, т.е. через $e_1 = x+y$, $e_2 = xy$.

Условия применимости. Любое поле. Применимо когда у задачи есть «$P(x) - P(y)$ кратно $x - y$» структура, или когда нужно симметрически закодировать пару корней.

Идея доказательства. $\frac{x^k - y^k}{x - y} = \sum_{i+j=k-1} x^i y^j$ — симметрично, выражается через $e_1, e_2$ (Гаусс). Линейность по $P$ распространяет это на любой $P$.

Варианты и обобщения.
- Аналогично для трёх переменных: $\frac{P(x)(y-z) + P(y)(z-x) + P(z)(x-y)}{(x-y)(y-z)(z-x)}$ — симметрический (divided differences второго порядка).
- Связь с Lagrange interpolation: коэффициенты $P$ при $\binom{x}{k}$-базисе суть divided differences.

Используется в. [IMC-2000-2: $P(w,z) = \frac{p(x) - p(y)}{x - y}$ + аналог $Q$, разность $P - Q = 0$ даёт $w + z = 1$, далее Vieta для $c = wz$].

---

### E11. Trace power sums of matrix → spectrum (Newton + Cayley–Hamilton)

Формулировка. Пусть $A \in M_n(K)$, $\operatorname{char} K = 0$. Power sums $\operatorname{tr}(A^k)$ для $k = 1, \dots, n$ полностью определяют характеристический многочлен $\chi_A(x) = \prod(x - \lambda_i)$, поскольку Newton (E2, E4) выражает $e_k(\lambda_1, \dots, \lambda_n)$ через $p_k$. В частности, $\operatorname{tr}(A^k) = 0$ для $k = 1, \dots, n$ $\iff$ $A$ nilpotent.

Условия применимости. $\operatorname{char} K = 0$ или $\operatorname{char} K > n$. В $\operatorname{char} p$ для $n \ge p$ нужно более тонкое утверждение.

Идея доказательства. По Newton: $p_k = 0$ для $k = 1, \dots, n$ ⇒ $e_k = 0$ для $k = 1, \dots, n$ ⇒ $\chi_A(x) = x^n$. По Cayley–Hamilton $A^n = 0$.

Варианты и обобщения.
- Иногда удобнее: $\operatorname{tr}(A^k) = 0$ для $k = 1, \dots, m$ ($m < n$) даёт оценку количества ненулевых eigenvalues.
- В обратную сторону: задавать $A$ через $\chi_A$ и восстанавливать $\operatorname{tr}(A^k)$ для всех $k$ (включая $k > n$) через Cayley–Hamilton.

Используется в. [IMC-2009-DAY2-3: $X = AB - BA$ коммутирует с $A$, $\operatorname{tr}(X^{m+1}) = \operatorname{tr}(A X^m B - X^m B A) = 0$ ⇒ все $p_k(X) = 0$ ⇒ $X$ nilpotent], [Putnam-1973-A4 и др.].

---

### E12. AM-GM/AM-HM на Vieta — bound на степень или коэффициенты

Формулировка. Если все корни $\alpha_i$ многочлена $f \in \mathbb{R}[x]$ имеют известный знак (скажем, $\le 0$), то $|\alpha_i|$ — положительные вещественные, и AM-GM/AM-HM применимы к Vieta: $e_1/n \ge (e_n)^{1/n}$, $e_{n-1}/(n e_n) \ge \frac{n}{e_1}$ (HM ≤ AM на $|\alpha_i|$). Это даёт жёсткие неравенства между коэффициентами.

Условия применимости. Все корни одного знака (или вещественны). Неравенства должны быть нетривиальны — обычно проявляются как «при заданной перестановке коэффициентов степень $n$ ограничена сверху».

Идея доказательства. Прямое применение AM-GM/AM-HM к $|\alpha_i|$. Vieta переписывает в коэффициенты.

Используется в. [IMC-2005-4: коэффициенты $(a_0, \dots, a_n)$ — перестановка $(0, \dots, n)$, корни $\le 0$. $a_0 = 0 \Rightarrow$ есть нулевой корень $\alpha_n$; для остальных $\alpha_1, \dots, \alpha_{n-1} < 0$ AM-HM даёт $a_{n-1}/((n-1) a_n) \ge (n-1) a_1 / a_2$, итого $n^2 \ge (n-1)^2 \cdot (\text{что-то}) \Rightarrow n \le 3$]. Аналогичные degree bounds — стандарт IMC/Putnam.

---

### E13. Lagrange interpolation: derivatives через значения + Chebyshev extremal

Формулировка. Если $f \in \mathbb{R}[x]$ степени $< n$ задан значениями $f(x_1), \dots, f(x_n)$ в различных $x_k$, то $f^{(j)}(x_0) = \sum_k \ell_k^{(j)}(x_0) f(x_k)$, где $\ell_k(x) = \prod_{j \ne k} (x - x_j)/(x_k - x_j)$ — базис Лагранжа. Экстремум $|f^{(j)}(x_0)|$ при $|f(x_k)| \le 1$ достигается на $f(x_k) = \operatorname{sign}(\ell_k^{(j)}(x_0))$, и оптимальный $f$ — Chebyshev $T_n$ для специальных узлов и точки $x_0$ снаружи $[-1, 1]$.

Условия применимости. Различные узлы $x_k$. Степень $f$ строго меньше числа узлов.

Идея доказательства. Lagrange формула — прямой подсчёт. Экстремум — линейная задача в $f(x_k)$, оптимум на вершинах куба $[-1,1]^n$, дальше характеризация Chebyshev.

Варианты и обобщения.
- Newton form: $f(x) = \sum_k [x_0, \dots, x_k]_f \cdot \prod_{j<k}(x - x_j)$, где $[x_0, \dots, x_k]_f$ — divided differences.
- $T_n(\cos\theta) = \cos(n\theta)$, $T_n$ имеет максимум $1$ на $[-1, 1]$ и минимально-возможный максимум на $[-1,1]$ среди монических до константы.

Используется в. [IMC-1998-DAY2-2: $|f''(1)| \le ?$ при $|f(x_k)| \le 1$ для трёх узлов из $[-1,1]$, оптимум на $T_3 = 4x^3 - 3x$ с $f''(1) = 24$].

---

### E14. Faulhaber / Bernoulli polynomials — структура $\sum k^p$

Формулировка. Для целых $p \ge 0$ существует единственный многочлен $S_p \in \mathbb{Q}[n]$ степени $p+1$ такой, что $S_p(n) = \sum_{k=1}^n k^p$. Через Bernoulli polynomials $B_p(x)$ (определены $B_p(x+1) - B_p(x) = p x^{p-1}$):
$$\sum_{k=1}^n k^p = \frac{B_{p+1}(n+1) - B_{p+1}(1)}{p+1}.$$
$S_p(n)$ симметричен: для нечётного $p$ $S_p$ — многочлен от $n(n+1)/2$ (Faulhaber).

Условия применимости. Любые $p \ge 0$, $n \in \mathbb{Z}_{\ge 0}$.

Идея доказательства. Существование/единственность $S_p$ — индукция: $\sum k^p$ как разность $S_p(n) - S_p(n-1) = n^p$, далее любой polynomial $\Delta$-уравнение однозначно решается. $S_p(n) - S_p(-1-n) \cdot (\pm 1)$ — функциональное уравнение Bernoulli даёт симметрию.

Варианты и обобщения.
- $B_n(1-x) = (-1)^n B_n(x)$, $B_n(0) = B_n$, Riemann-style $\sum 1/k^{2m} = (-1)^{m+1} (2\pi)^{2m} B_{2m}/(2(2m)!)$.
- Для $p$ любого многочлена: $\sum_{k=1}^n p(k)$ — многочлен от $n$ степени $\deg p + 1$.

Используется в. [IMC-2020-4: $p(x+1) - p(x) = x^{100}$, ответ — многочлен степени $101$, $p(x) = B_{101}(x)/101 + C$; функциональная симметрия + положительность].

---

### E15. Cauchy / Lagrange / Eneström–Kakeya bounds на корни (root location)

Формулировка. Для $f(x) = a_n x^n + \dots + a_0$ монического (или $a_n \ne 0$):
1. **Cauchy bound**: все корни $|\alpha| \le 1 + \max_{0 \le k < n} |a_k/a_n|$.
2. **Lagrange bound**: все корни $|\alpha| \le \max(1, \sum_{k=0}^{n-1} |a_k/a_n|)$.
3. **Eneström–Kakeya**: при $0 < a_0 \le a_1 \le \dots \le a_n$ все корни лежат в $|z| \le 1$. При $a_0 \ge a_1 \ge \dots \ge a_n > 0$ — в $|z| \ge 1$.

Условия применимости. (1)–(2) — любые $a_k$. (3) — монотонные положительные коэффициенты.

Идея доказательства. (1): если $|\alpha| > C$, то $|a_n \alpha^n| > \sum_{k<n} |a_k \alpha^k|$ — противоречит $f(\alpha) = 0$. (3): $f(z)(1 - z) = a_0 + \sum (a_k - a_{k-1}) z^k - a_n z^{n+1}$, на $|z| = 1$ оценка через треугольник.

Варианты и обобщения. **Lehmer / Mahler measures**: $M(f) = |a_n| \prod_{|\alpha_i|>1} |\alpha_i|$ — связь с высотой многочлена. **Smyth-bound**: $M(f) \ge $ некоторое для не-цикломатических $f \in \mathbb{Z}[x]$.

Используется в. [IMC-2014-3] косвенно для контроля множества корней лакунарного многочлена. Фундамент для Perron / Cohn критериев неприводимости (см. [Факторизация и неприводимость]).

---

### E16. Multiplicity counting via $f'$ (счёт корней с кратностями через производную)

Формулировка. Для $f \in \mathbb{R}[x]$ с корнями $\alpha_1, \dots, \alpha_m$ кратностей $\mu_1, \dots, \mu_m$: $\sum \mu_i = n = \deg f$. Производная $f'$ имеет в каждом $\alpha_i$ корень кратности $\mu_i - 1$, плюс $m - 1$ корней между ними (Rolle). Итого: $\sum (\mu_i - 1) + (m - 1) = (n - m) + (m - 1) = n - 1 = \deg f'$.

Точная учётная формула. Если $\mu(f, c)$ — кратность $c$ как корня $f$, то
$$\sum_c \mu(f, c) - \mu(f', c) = \#\{c : f(c) = 0, c \text{ простой}\} \le n - \deg(\gcd(f, f')).$$

Условия применимости. $f \in \mathbb{R}[x]$ или $\mathbb{C}[x]$. Над $\mathbb{R}$ можно делать оценки $|\{$простые корни$\}|$ через $\deg(\gcd(f, f'))$.

Идея доказательства. $f = (x - c)^\mu g$, $g(c) \ne 0$ ⇒ $f' = (x-c)^{\mu-1}((\mu) g + (x-c) g')$, зануление в $c$ кратности ровно $\mu - 1$.

Используется в. [IMC-2000-DAY2-3]: $|S_0| + |S_1| \ge \sum (\mu(p, c) - \mu(p', c)) + \sum (\mu(p-1, c) - \mu(p', c)) \ge n + n - (n-1) = n+1$, используя $\deg p' = n - 1$.

---

## Записи — Exotic

### E17. Muirhead's inequality / Schur convexity (Muirhead и Schur-выпуклость)

Формулировка (Muirhead). Пусть $a = (a_1 \ge a_2 \ge \dots \ge a_n) \succeq b = (b_1 \ge \dots \ge b_n)$ в смысле majorization (т.е. $\sum a_i = \sum b_i$ и $\sum_{i \le k} a_i \ge \sum_{i \le k} b_i$ для всех $k$). Тогда для $x_i > 0$:
$$\sum_{\sigma \in S_n} x_{\sigma(1)}^{a_1} \cdots x_{\sigma(n)}^{a_n} \ge \sum_{\sigma \in S_n} x_{\sigma(1)}^{b_1} \cdots x_{\sigma(n)}^{b_n}.$$

Schur convexity. Симметрический $f$, дифференцируемый, Schur-выпуклый $\iff$ $(x_i - x_j)(\partial_i f - \partial_j f) \ge 0$ для всех $i, j$. Schur-выпуклые функции монотонны по majorization: $a \succeq b \Rightarrow f(a) \ge f(b)$.

Условия применимости. Положительные $x_i$. Muirhead — частный случай: $f(x) = \sum_\sigma \prod x_{\sigma(i)}^{a_i}$ — Schur-выпукла как функция от $a$.

Идея доказательства. Muirhead — индукция через AM-GM на двух переменных. Schur — прямой mean value на «парном перетоке».

Используется в. Стандартный инструмент из «олимпиадных неравенств». На IMC прямой Muirhead встречается редко (предпочитают SOS / Cauchy–Schwarz), но он за многими стандартными неравенствами на $e_k, p_k$.

---

### E18. Newton–Girard в положительной характеристике

Формулировка. Над полем $\operatorname{char} K = p$ Newton-формула $p_k = e_1 p_{k-1} - \dots + (-1)^{k-1}(k) e_k$ ломается при $k = p$, поскольку $k \cdot e_k = 0$ — теряется информация. Симметрические $\Lambda_K = K[e_1, e_2, \dots]$ строится на $e$- (или $h$-) базисе, но $p$-базис не порождает: $p_p = e_1^p$ (Frobenius), и $e_p$ не выразим через $p_1, \dots, p_p$.

Условия применимости. $\operatorname{char} K = p > 0$. Иерархия: $K[e_k] = K[h_k] \supsetneq K[p_k]$.

Идея доказательства. $p_k$ как функционал на $\Lambda$ — линейная комбинация мономов $e_\lambda$; в $\operatorname{char} p$ часть коэффициентов аннулируется. Frobenius $\phi(x) = x^p$ удовлетворяет $\sum \alpha_i^p = (\sum \alpha_i)^p$ — линейное вырождение.

Используется в. На IMC напрямую почти не приходит. Существенно при работе над $\mathbb{F}_p[x]$ — для подтемы «Многочлены над $\mathbb{F}_p$».

---

### E19. Hermite–Biehler / interlacing real roots criterion

Формулировка. Многочлен $f(z) = p(z^2) + z q(z^2) \in \mathbb{R}[z]$ Гурвицев (все корни $\operatorname{Re} < 0$) $\iff$ $p$ и $q$ имеют простые отрицательные корни $\xi_1 < \dots < \xi_m$, $\eta_1 < \dots < \eta_m$ или $\eta_m \pm 1$, причём они interlace: $\xi_1 < \eta_1 < \xi_2 < \dots$ Эквивалентная формулировка через комплексный многочлен $s = p + i q$: $s$ имеет все корни в верхней полуплоскости $\iff$ $p, q \in \mathbb{R}[x]$ degrees $k$, $k-1$ или $k$, имеют простые вещественные корни и interlace.

Условия применимости. $f \in \mathbb{R}[z]$.

Идея доказательства. На вертикальной прямой $\operatorname{Re} z = 0$ argument principle / Cauchy: число знаков смен $p(t^2)/q(t^2)$ при $t \in (-\infty, +\infty)$ = число корней $f$ в правой полуплоскости.

Варианты и обобщения. **Routh–Hurwitz** — алгоритмический критерий через цепные дроби. **Real-stable polynomials** многомерные (Borcea–Brändén, конец 2000-х).

Используется в. На олимпиадах напрямую не встречается, но даёт «правильные интуиции» — interlacing корней $f$ и $f'$ (Rolle), $f$ и $f - cf'$ (Hermite).

---

### E20. Parametric Vieta (параметризация решений Vieta в малых случаях)

Формулировка. Для уравнения $\alpha + \beta + \gamma = 0$, $\alpha \beta \gamma = -mn$, $\alpha\beta + \beta\gamma + \gamma\alpha = -n$ (cubic с заданными $e_1 = 0$, $e_2 = -n$, $e_3 = -mn$) общее семейство решений в $\mathbb{Z}$ параметризуется так: $\alpha = p^3, \beta = q^3, \gamma = -(p+q)^3$ при $n = (p^2 + pq + q^2)^3$, $m = p^2 q + p q^2$ (т.е. $n$ — куб некоторого $\mathbb{Z}$-формы).

Условия применимости. Заданы symmetric constraints на корни; ищется параметрическое семейство.

Идея доказательства. Подстановка $\alpha = u, \beta = v, \gamma = -(u+v)$ даёт $u^2 + uv + v^2 = n$, $uv(u+v) = mn$. Берём $u = kp, v = kq$, $k = p^2 + pq + q^2$, и подбираем нормировки.

Используется в. [IMC-2006-DAY2-5: cubic roots configurations, параметризация всех целочисленных решений].

---

## Self-test

1. Пусть $f(x) = x^n - n x + n - 1$. Найти $\sum_{i=1}^n \alpha_i^k$ для $k = 1, 2, 3$.
2. Показать: если $A, B \in M_n(\mathbb{R})$ и $\operatorname{tr}((AB - BA)^k) = 0$ для $k = 1, \dots, n$, то $AB - BA$ нильпотентна.
3. Найти все целые $n \ge 2$, для которых существует многочлен $f(x) \in \mathbb{Z}[x]$ степени $n$ с неотрицательными корнями, чьи коэффициенты $a_0, a_1, \dots, a_n$ — перестановка чисел $0, 1, \dots, n$.
4. Пусть $f \in \mathbb{R}[x]$ имеет все корни вещественные. Доказать, что $(n-1)(f'(x))^2 \ge n f(x) f''(x)$ для всех $x \in \mathbb{R}$.
5. Доказать: если коэффициенты $a_0, a_1, \dots, a_n$ многочлена $f$ положительны и $f$ имеет все корни вещественные, то $a_k^2 \ge a_{k-1} a_{k+1} \cdot (1 + 1/k)(1 + 1/(n-k))$ для $1 \le k \le n-1$.
6. Многочлен $p \in \mathbb{R}[x]$ степени $n$ удовлетворяет $p(x+1) - p(x) = x^m$ для фиксированного $m \ge 1$. Найти $\deg p$ и доказать, что $p$ — единственный с точностью до константы.
7. Дано $\alpha + \beta + \gamma = 1$, $\alpha^2 + \beta^2 + \gamma^2 = 2$, $\alpha^3 + \beta^3 + \gamma^3 = 3$. Найти $\alpha^4 + \beta^4 + \gamma^4$ и $\alpha^5 + \beta^5 + \gamma^5$.
8. $f \in \mathbb{R}[x]$ степени $n \ge 2$ имеет $n$ различных вещественных корней. Доказать, что $f''$ имеет не менее $n - 2$ различных вещественных корней (точная оценка) — и явно описать ситуации с равенством.
9. Найти все $f \in \mathbb{R}[x]$ степени $\le n$ такие, что $|f(x_k)| \le 1$ для $k = 0, 1, \dots, n$, где $x_k = \cos(k\pi/n)$, и максимизирующие $|f(x_0)|$ для $|x_0| > 1$.
10. Многочлен $f(x) = \sum_{k=0}^n a_k x^k \in \mathbb{R}[x]$ имеет $a_k = q^{k(k-1)/2}$, $q > 0$ достаточно большое. Доказать, что для любого выбора знаков $\varepsilon_k \in \{\pm 1\}$ многочлен $\sum \varepsilon_k a_k x^k$ имеет $n$ различных вещественных корней.

## Решения

1. По Vieta: $e_1 = 0$, $e_{n-1} = (-1)^{n-1} \cdot (-n) = (-1)^n n$ (коэффициент при $x$ равен $-n$, $e_{n-1} = -(-n)/1 = n$), $e_n = (-1)^n (n-1)$. По Newton (E2): $p_1 = e_1 = 0$. $p_2 = e_1 p_1 - 2 e_2 = 0$ (т.к. $e_2 = 0$ в $f$, при $n \ge 3$). $p_3 = e_1 p_2 - e_2 p_1 + 3 e_3 = 0$ для $n \ge 4$. Для $n = 2$: $f = x^2 - 2x + 1 = (x-1)^2$, $p_k = 2$. Для $n = 3$: $f = x^3 - 3x + 2 = (x-1)^2(x+2)$, $p_1 = 0$, $p_2 = 6$, $p_3 = -6$.

2. См. E11. По Newton $p_k(X) = 0$ для $k = 1, \dots, n$ ⇒ $e_k(\lambda_1, \dots, \lambda_n) = 0$ ⇒ $\chi_X(t) = t^n$. По Cayley–Hamilton $X^n = 0$.

3. См. E12 / [IMC-2005-4]. $a_0 = 0$ ⇒ есть нулевой корень. Остальные $\alpha_1, \dots, \alpha_{n-1} \le 0$, ставлю $\beta_i = -\alpha_i \ge 0$. По Vieta $a_{n-1}/a_n = e_1(\beta) = \sum \beta_i$, $a_1/a_n = e_{n-1}(\beta)$. AM-HM: $\sum \beta_i \cdot \sum 1/\beta_i \ge (n-1)^2$. $\sum 1/\beta_i = e_{n-2}(\beta)/e_{n-1}(\beta) = a_2/a_1$. Итого $(a_{n-1}/a_n)(a_2/a_1) \ge (n-1)^2$. Среди $\{0, 1, \dots, n\}$ значения $a_n \ge 1$, $a_1 \ge 1$, $a_2 \le n$, $a_{n-1} \le n$, поэтому $n^2 \ge (n-1)^2 a_n a_1 \ge (n-1)^2$, т.е. $n \ge n - 1$ — мало даёт. Нужен более тонкий учёт + ограничение $\sum a_k = n(n+1)/2$. Дальнейшее: $n \le 3$, явные примеры $n = 1, 2, 3$.

4. См. E5. Из $\sum_i 1/(x - \alpha_i)^2 = (f'/f)^2 - f''/f \ge 0$ и Cauchy–Schwarz: $\left(\sum 1/(x-\alpha_i)\right)^2 \le n \sum 1/(x-\alpha_i)^2$, т.е. $(f'/f)^2 \le n((f'/f)^2 - f''/f)$, откуда $(n-1)(f')^2 \ge n f f''$.

5. См. E7 (Newton's inequalities). $E_k = a_{n-k}/(\binom{n}{k} \cdot a_n)$ (нормирование). $E_k^2 \ge E_{k-1} E_{k+1}$ ⇒ $(a_{n-k}/\binom{n}{k})^2 \ge (a_{n-k+1}/\binom{n}{k-1})(a_{n-k-1}/\binom{n}{k+1})$. Пере-маркировка $j = n - k$ даёт нужное.

6. См. E14. $\deg p = m + 1$. Существует ровно один с точностью до константы: разностный оператор $\Delta p = p(x+1) - p(x)$ — линейный, $\Delta : \mathbb{R}[x]_{\le m+1} \to \mathbb{R}[x]_{\le m}$ имеет ядро $\mathbb{R}$ (константы) и сюръективен (по индукции на $\deg$, базис $\binom{x}{k}$ ↔ $\binom{x}{k-1}$ через $\Delta$).

7. По Newton (E2): $e_1 = p_1 = 1$. $p_2 = e_1 p_1 - 2 e_2 \Rightarrow 2 = 1 - 2 e_2 \Rightarrow e_2 = -1/2$. $p_3 = e_1 p_2 - e_2 p_1 + 3 e_3 \Rightarrow 3 = 2 + 1/2 + 3 e_3 \Rightarrow e_3 = 1/6$. $p_4 = e_1 p_3 - e_2 p_2 + e_3 p_1 = 3 + 1 + 1/6 = 25/6$. $p_5 = e_1 p_4 - e_2 p_3 + e_3 p_2 = 25/6 + 3/2 + 1/3 = 25/6 + 9/6 + 2/6 = 36/6 = 6$.

8. Между $n$ корнями $f$ есть $n - 1$ корень $f'$ (Rolle). Между $n - 1$ корнями $f'$ есть $n - 2$ корня $f''$. Все различны, если $f$ имел $n$ простых вещественных корней. Равенство — когда $f$ имеет ровно $n$ простых корней и все корни $f'$ простые (общий случай).

9. См. E13. Lagrange + Chebyshev: $f^*(x) = T_n(x)$ — Chebyshev на узлах $x_k = \cos(k\pi/n)$ принимает значения $\pm 1$, и для любого $|x_0| > 1$ верно $|f(x_0)| \le |T_n(x_0)|$ для всех $f$ с $|f(x_k)| \le 1$ — это классическая extremal characterization Chebyshev (Markov–Bernstein).

10. См. E9 (Descartes). При $q$ большом $a_k = q^{k(k-1)/2}$ растёт сверхэкспоненциально. Для любых $\varepsilon_k$ многочлен $\sum \varepsilon_k a_k x^k$ имеет $n$ смен знака на $(0, \infty)$ либо $n$ смен на $(-\infty, 0)$ (через $f(-x)$) — суммарно учитывая (Descartes — оценка сверху, реальное число корней может быть меньше на чётное). Для строгого неравенства нужен анализ $f(x_k)$ в ${q^j}$-промежуточных точках: на каждом интервале $f$ доминируется одним мономом, сменяющим знак — $n$ интервалов = $n$ корней.
