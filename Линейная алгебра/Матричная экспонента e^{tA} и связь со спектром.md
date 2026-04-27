---
topic: Линейная алгебра
subtopic: "Матричная экспонента e^{tA} и связь со спектром"
sources:
  - "Horn, Johnson — Topics in Matrix Analysis (Ch. 6: Matrix Functions)"
  - "Higham — Functions of Matrices: Theory and Computation"
  - "Hall — Lie Groups, Lie Algebras, and Representations (GTM 222)"
  - "Bhatia — Matrix Analysis (GTM 169)"
  - "Bellman — Introduction to Matrix Analysis"
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Moler, Van Loan — Nineteen Dubious Ways to Compute the Exponential of a Matrix (SIAM Review 2003)"
  - "Putzer — Avoiding the Jordan Canonical Form in the Discussion of Linear Systems with Constant Coefficients (AMM 1966)"
  - "Iserles, Nørsett — On the Solution of Linear Differential Equations in Lie Groups (Magnus expansion)"
  - "Tao — Blog: The Golden–Thompson inequality"
  - "Wikipedia — Matrix exponential, Spectral mapping theorem, Baker–Campbell–Hausdorff formula, Lie product formula, Cayley transform, Lyapunov equation"
  - "IMC Compendium"
  - "Putnam Compendium"
problems_referenced:
  - IMC-2000-DAY2-6
  - IMC-2002-6
  - IMC-2004-DAY2-4
  - IMC-2016-10
  - IMC-2019-9
last_updated: 2026-04-27
---

# Матричная экспонента $e^{tA}$ и связь со спектром

## Scope
Матричная экспонента $e^{tA} = \sum_{k \ge 0} (tA)^k / k!$ как функциональное исчисление от $A \in M_n(\mathbb{C})$, её связь со спектром через spectral mapping ($\sigma(e^A) = e^{\sigma(A)}$ с кратностями), $\det e^A = e^{\operatorname{tr} A}$, разложение через Jordan form для вычисления, ODE $x' = Ax$, Lie group ↔ Lie algebra ($e^{\mathfrak{g}} \subset G$ для классических групп), surjectivity на $GL_n(\mathbb{C})$ и failure на $GL_n(\mathbb{R})$, оценки $\|e^{tA}\|$ и $\|A^n\|$ через spectral radius и размер Jordan блоков, Lyapunov equation для устойчивости, Lie product formula (Trotter), BCH-разложение, Fréchet производная $D \exp$ (Daleckii–Krein), Golden–Thompson, Cayley transform, Putzer's algorithm.

## Записи — Core

### E1. Определение $e^A$ и формула на Jordan-блоке

Формулировка. Для $A \in M_n(\mathbb{C})$ ряд
$$e^A := \sum_{k=0}^{\infty} \frac{A^k}{k!}$$
сходится абсолютно в любой нормированной матричной алгебре (так как $\|A^k\| \le \|A\|^k$). Для Jordan-блока $J_m(\lambda) = \lambda I + N$, где $N$ — стандартный nilpotent shift ($N^m = 0$):
$$e^{t J_m(\lambda)} = e^{t\lambda} \sum_{k=0}^{m-1} \frac{t^k}{k!} N^k = e^{t\lambda} \begin{pmatrix} 1 & t & t^2/2! & \cdots & t^{m-1}/(m-1)! \\ 0 & 1 & t & \cdots & t^{m-2}/(m-2)! \\ \vdots & & \ddots & & \vdots \\ 0 & 0 & \cdots & 1 & t \\ 0 & 0 & \cdots & 0 & 1 \end{pmatrix}.$$
Для произвольной $A = S J S^{-1}$: $e^{tA} = S e^{tJ} S^{-1}$, где $e^{tJ} = \bigoplus_k e^{t J_{m_k}(\lambda_k)}$.

Условия применимости. Любая $A \in M_n(\mathbb{F})$ над $\mathbb{F} \in \{\mathbb{R}, \mathbb{C}\}$. Над произвольной полной нормированной алгеброй — тоже.

Идея доказательства. Сходимость ряда — мажорантой $e^{\|A\|}$. На $J_m(\lambda)$: $e^{\lambda I + N} = e^{\lambda} e^{N}$ (коммутируют, см. E4), $e^N$ — конечная сумма из-за нильпотентности.

Варианты и обобщения.
- Альтернативное определение: $e^A = \lim_{n \to \infty} (I + A/n)^n$.
- Riesz–Dunford: $e^A = \frac{1}{2\pi i} \oint_\Gamma e^z (zI - A)^{-1} dz$, $\Gamma$ окружает $\sigma(A)$. Работает для любой $f$ голоморфной в окрестности $\sigma(A)$.
- Для нормальной $A = U \Lambda U^*$: $e^A = U \operatorname{diag}(e^{\lambda_i}) U^*$.

Используется в. Базовое определение для всех ниже. [IMC-2000-DAY2-6 (через $q(e^{AB}) = q(e^{BA}) + AC = q(e^{BA})$ ↔ char polynomials AC и CA через ряд)].

---

### E2. Spectral mapping theorem (теорема о спектральном отображении) для $e^A$

Формулировка. Если $\sigma(A) = \{\lambda_1, \dots, \lambda_n\}$ — спектр $A \in M_n(\mathbb{C})$ с алгебраическими кратностями, то
$$\sigma(e^A) = \{e^{\lambda_1}, \dots, e^{\lambda_n}\}$$
с теми же алгебраическими кратностями. Жорданова структура $e^A$ совпадает с жордановой структурой «полиномиального остатка»: блок $J_m(\lambda)$ для $A$ переходит в блок размера $m$ для собственного значения $e^\lambda$ матрицы $e^A$ (так как $e^{J_m(\lambda)} = e^\lambda(I + N')$, $N'$ нильпотентный с тем же индексом нильпотентности).

Условия применимости. $A \in M_n(\mathbb{C})$, любая. Обобщается на $f(A)$ голоморфную в окрестности $\sigma(A)$: $\sigma(f(A)) = f(\sigma(A))$.

Идея доказательства. Перейти к Jordan: $A = SJS^{-1}$, $e^A = S e^J S^{-1}$. На блоке $J_m(\lambda)$: $e^{J_m(\lambda)} = e^\lambda I + (\text{строго upper-triangular})$, единственное собственное значение $= e^\lambda$ алгебраической кратности $m$. Жорданова структура сохраняется потому, что $e^{N} - I$ имеет тот же ранг, что и $N$ (это даёт совпадение $\dim \ker (e^A - e^\lambda I)^k$ и $\dim \ker (A - \lambda I)^k$).

Варианты и обобщения.
- Для $f$ инъективной на $\sigma(A)$ жорданова структура полностью сохраняется.
- Если $f'(\lambda) = 0$ для какого-то $\lambda \in \sigma(A)$, блоки могут сливаться. Для $\exp$ такого нет ($e^z$ не имеет нулей производной).
- Контрпример «отбрасывания кратностей»: для $A = \operatorname{diag}(0, 2\pi i)$ имеем $\sigma(e^A) = \{1, 1\}$ — кратное собственное значение, хотя $A$ имела простой спектр.

Используется в. Любая задача про спектр $e^A$ или $A^n = e^{n \log A}$. [IMC-2016-10 (поведение $\|A^n\|$ контролируется $\rho(A) = \max |\lambda_i|$)].

---

### E3. $\det e^A = e^{\operatorname{tr} A}$

Формулировка. Для любой $A \in M_n(\mathbb{C})$:
$$\det e^A = e^{\operatorname{tr} A}.$$
В частности $e^A$ всегда обратима (значит $\exp: M_n(\mathbb{C}) \to GL_n(\mathbb{C})$).

Условия применимости. Универсально, $A$ произвольная.

Идея доказательства. (1) Через Jordan: $\det e^A = \prod_i e^{\lambda_i} = e^{\sum \lambda_i} = e^{\operatorname{tr} A}$. (2) Бескоординатно: $\frac{d}{dt} \det e^{tA} = \det e^{tA} \cdot \operatorname{tr}(A)$ (Jacobi formula), $\det e^{0} = 1 \Rightarrow \det e^{tA} = e^{t \operatorname{tr} A}$.

Варианты и обобщения.
- Jacobi formula: $\frac{d}{dt} \det X(t) = \det X(t) \cdot \operatorname{tr}(X(t)^{-1} X'(t))$.
- $A \in \mathfrak{sl}_n$ (бесследовая) $\iff e^A \in SL_n$ — критерий принадлежности Lie-подалгебре.
- Логарифмическая версия: $\log \det e^A = \operatorname{tr} A$ — с правильной ветвью log.

Используется в. Регулярно в задачах про $\det$ и $\operatorname{tr}$ через дифференциальные тождества. Putnam-style: показать $\det e^A > 0$ для real $A$.

---

### E4. $e^{A+B} = e^A e^B \iff AB = BA$ (на коммутирующих)

Формулировка. Если $A, B \in M_n(\mathbb{C})$ коммутируют ($AB = BA$), то $e^{A+B} = e^A e^B = e^B e^A$. В общем случае равенство не верно (контрпример ниже). Точная количественная мера несоответствия — Lie product formula (E10) и BCH (E12).

Условия применимости. Импликация «коммутируют $\Rightarrow$ равенство» — без условий. Обратная импликация ($e^{A+B} = e^A e^B$ для всех малых параметров $\Rightarrow AB = BA$) — требует анализа BCH; для конкретных пар $A, B$ может быть совпадение и без коммутативности.

Идея доказательства. Прямой ряд: $e^{A+B} = \sum (A+B)^k / k!$. При $AB = BA$ биномиальная теорема даёт $(A+B)^k = \sum_j \binom{k}{j} A^j B^{k-j}$, после перегруппировки получим $\bigl(\sum A^j / j!\bigr)\bigl(\sum B^k / k!\bigr) = e^A e^B$.

Варианты и обобщения.
- Контрпример: $A = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}$, $B = \begin{pmatrix} 0 & 0 \\ 1 & 0 \end{pmatrix}$. $A + B$ — involution в $SL_2$ направлении, $e^{A+B}$, $e^A e^B$ можно прямо посчитать и сравнить.
- $e^A e^B = e^B e^A \not\Rightarrow AB = BA$. Например $A = 2\pi i \cdot I, B$ — произвольная: $e^A = I$, коммутирует с любой.
- $e^A B = B e^A$ для всех $A \iff B$ — функция от $A$ (в духе double commutant).

Используется в. [IMC-2000-DAY2-6 (введение $S = e^{AB}, T = e^{BA}$, использует, что $AB \neq BA$ приводит к разным результатам)]. Стандартный приём: упростить вычисление, доказав коммутативность (например, $A$ — функция $B$).

---

### E5. ODE $x' = Ax$ и фундаментальная матрица $e^{tA}$

Формулировка. Решение задачи Коши $x'(t) = A x(t)$, $x(0) = x_0$, в $\mathbb{C}^n$:
$$x(t) = e^{tA} x_0.$$
Фундаментальная матрица системы — $\Phi(t) = e^{tA}$, удовлетворяет $\Phi'(t) = A \Phi(t) = \Phi(t) A$, $\Phi(0) = I$. Решение существует на всём $\mathbb{R}$ и единственно.

Условия применимости. $A$ — постоянная матрица. Для нестационарной $A(t)$ формула $\Phi(t) = e^{\int_0^t A(s) ds}$ работает только при $[A(t), A(s)] = 0$ для всех $t, s$ — иначе нужен Magnus expansion (E13).

Идея доказательства. $\frac{d}{dt} e^{tA} = \frac{d}{dt} \sum t^k A^k / k! = \sum k t^{k-1} A^k / k! = A e^{tA}$. Единственность — линейность ODE.

Варианты и обобщения.
- Неоднородная: $x' = Ax + f(t) \Rightarrow x(t) = e^{tA} x_0 + \int_0^t e^{(t-s)A} f(s) ds$ (Duhamel).
- Связь со спектром: общее решение — линейная комбинация $t^k e^{\lambda t} v$ по жордановым цепочкам $v$, где $A v = \lambda v$ или $(A - \lambda I)^k v = 0$.
- Теорема Floquet: для $T$-периодической $A(t)$ — $\Phi(t) = P(t) e^{tQ}$, $P$ периодическая, $Q$ постоянная.

Используется в. [IMC-2002-6 (анализ $A^n \to L$ через $A = e^B$ и поведение $e^{nB}$, хотя в задаче работают напрямую с $A^n$)], [IMC-2004-DAY2-4 (Lyapunov оператор $L_M(X) = MX + XM^T$ — порождён ODE $X' = MX + XM^T$, решение $X(t) = e^{tM} X(0) e^{tM^T}$, спектр $L_M$ = $\{\lambda_r + \lambda_s\}$)].

---

## Записи — Standard

### E6. Оценки $\|e^{tA}\|$ и $\|A^n\|$ через spectral abscissa и Jordan

Формулировка. Пусть $\rho(A) = \max |\lambda|$ — spectral radius, $\alpha(A) = \max \operatorname{Re} \lambda$ — spectral abscissa, $m$ — размер крупнейшего Jordan-блока для самого «большого» собственного значения. Тогда:
$$\|A^n\| \le C \cdot n^{m-1} \rho(A)^n, \qquad \|e^{tA}\| \le C(1 + t^{m-1}) e^{\alpha(A) t} \quad (t \ge 0),$$
с константой $C = C(A, \|\cdot\|)$. Гельфанд: $\rho(A) = \lim_n \|A^n\|^{1/n}$.

Условия применимости. $A \in M_n(\mathbb{C})$, любая subordinate matrix norm. Для $A$ нормальной $C = 1$, $m = 1$ (диагонализуема): $\|A^n\| = \rho(A)^n$, $\|e^{tA}\| = e^{\alpha(A) t}$ в spectral norm.

Идея доказательства. Schur-форма $A = U(D + N) U^*$, $D$ диагональная, $N$ строго upper-triangular. На Jordan-блоке $\|J_m(\lambda)^n\| \le \binom{n}{m-1} |\lambda|^{n-(m-1)} \cdot \|N\|^{m-1}$, биномиальный коэффициент даёт полиномиальный рост. Для $e^{tA}$ — аналогичный анализ через ряд.

Варианты и обобщения.
- Power-bounded: $\sup_n \|A^n\| < \infty \iff \rho(A) \le 1$ и для каждого $\lambda \in \sigma(A)$ с $|\lambda| = 1$ Jordan-блоки имеют размер $1$ (полупростота в граничных eigenvalues).
- Spectral radius формула Gelfand: верна в любой Banach-алгебре.
- Hile / Kreiss: $\sup_n \|A^n\|$ оценивается через $\sup_{|z| > 1} (|z| - 1) \|(zI - A)^{-1}\|$ (Kreiss matrix theorem).

Используется в. [IMC-2002-6 (доказать $A^n$ сходится в operator norm при определённых условиях на $a_n = \|A^{n+1} - A^n\|$ — здесь и используется power-bounded plus spectral radius $< 1$ в проекции)], [IMC-2016-10 ($\|A^n\| \le (n / \ln 2) \|A\|^{n-1}$ при $\rho(A) \le 1$ — точная константа $n/\ln 2$ через анализ Jordan + биномиальная оценка)].

---

### E7. Putzer's algorithm (алгоритм Путцера)

Формулировка. Пусть $\lambda_1, \dots, \lambda_n$ — собственные значения $A \in M_n(\mathbb{C})$ (с кратностями, в любом порядке). Тогда
$$e^{tA} = \sum_{k=0}^{n-1} r_{k+1}(t) P_k, \qquad P_0 = I, \quad P_k = \prod_{j=1}^{k} (A - \lambda_j I),$$
где $r_k(t)$ — решение треугольной ODE-системы:
$$r_1' = \lambda_1 r_1, \quad r_1(0) = 1; \quad r_k' = \lambda_k r_k + r_{k-1}, \quad r_k(0) = 0 \text{ для } k \ge 2.$$

Условия применимости. Любая $A \in M_n(\mathbb{C})$, не нужна Jordan-форма или диагонализуемость. Особенно удобно при кратном спектре или близких собственных значениях.

Идея доказательства. Cayley–Hamilton: $\prod_{k=1}^n (A - \lambda_k I) = 0$, поэтому $\{P_0, \dots, P_{n-1}\}$ порождают алгебру $\mathbb{C}[A]$. Подстановка ряда для $e^{tA}$ в этот базис и сравнение коэффициентов даёт указанную ODE на $r_k$.

Варианты и обобщения.
- Аналог для $f(A)$ при произвольной $f$ голоморфной — формула Sylvester.
- Полиномиальное выражение: $e^{tA}$ — полином от $A$ степени $\le n - 1$ с коэффициентами зависящими от $t$ (следует из Cayley–Hamilton).

Используется в. Применяется при ручных вычислениях $e^{tA}$ для $n = 2, 3$: для $n = 2$, $\sigma(A) = \{\lambda_1, \lambda_2\}$, $\lambda_1 \neq \lambda_2$:
$$e^{tA} = \frac{\lambda_2 e^{t \lambda_1} - \lambda_1 e^{t \lambda_2}}{\lambda_2 - \lambda_1} I + \frac{e^{t \lambda_1} - e^{t \lambda_2}}{\lambda_1 - \lambda_2} A.$$
В олимпиадных задачах с малой размерностью — экономит чем формула через Jordan.

---

### E8. Lie-группы и образ exp на классических группах

Формулировка. Для классических матричных групп $G \subset GL_n(\mathbb{C})$ и соответствующих Lie-алгебр $\mathfrak{g}$:
- $\exp: M_n(\mathbb{C}) \to GL_n(\mathbb{C})$ сюръективен (E11).
- $\exp: \{A : A^* = -A\} \to U(n)$ сюръективен (любую унитарную можно представить как $e^{iH}$, $H = H^*$).
- $\exp: \{A : A^T = -A, \operatorname{tr} A = 0\} \to SO(n)$ сюръективен (real ортогональные с $\det = 1$).
- $\exp: \mathfrak{sl}_n(\mathbb{C}) \to SL_n(\mathbb{C})$ сюръективен.
- $\exp: M_n(\mathbb{R}) \to GL_n(\mathbb{R})$ — НЕ сюръективен. Образ — $\{A : \det A > 0$ и блок Jordan с отрицательным real eigenvalue имеет чётный размер$\}$.

Условия применимости. Классические Lie-группы. Для произвольной Lie-группы $G$ exp локально диффеоморфизм в окрестности $0 \in \mathfrak{g}$, но глобально может не покрывать всю компоненту единицы.

Идея доказательства. $A^* = -A \Rightarrow iA = (iA)^* \Rightarrow A = -i \cdot$ (эрмитова), $e^A = e^{-i H}$ — унитарная. Обратно: $U \in U(n) \Rightarrow$ спектральная теорема даёт $U = V \operatorname{diag}(e^{i\theta_k}) V^*$, тогда $H = V \operatorname{diag}(\theta_k) V^*$, $U = e^{iH}$.

Варианты и обобщения.
- Контрпример surjectivity на $GL_n(\mathbb{R})$: $A = \operatorname{diag}(-1, -2)$ — нет $B \in M_2(\mathbb{R})$ с $e^B = A$, потому что $e^B$ на двумерных вращениях тематически другая.
- В $GL_n(\mathbb{R})$ всякая $A$ с $\det A > 0$ выражается как $e^{B_1} e^{B_2}$ — экспонент 2 шт хватает.
- Для $A$ с $\det A < 0$ нет real $B$: $\det e^B = e^{\operatorname{tr} B} > 0$.

Используется в. Стандартный аппарат в задачах про подгруппы $GL_n$. Putnam-style: «доказать что данная матрица представима как $e^B$» — проверка через $\det$, спектр, real-аргумент.

---

### E9. Стабильность $e^{tA}$ через спектр и Lyapunov equation

Формулировка. Пусть $\alpha(A) = \max_{\lambda \in \sigma(A)} \operatorname{Re} \lambda$. Тогда:
- $\alpha(A) < 0 \iff \|e^{tA}\| \to 0$ при $t \to \infty$ (асимптотическая устойчивость).
- $\alpha(A) \le 0$ и для $\operatorname{Re} \lambda = 0$ Jordan-блоки размера $1$ $\iff \sup_t \|e^{tA}\| < \infty$ (стабильность).
- $\alpha(A) < 0 \iff \exists ! P \succ 0$: $A^* P + P A = -Q$ для каждой $Q \succ 0$, причём $P = \int_0^\infty e^{tA^*} Q e^{tA} dt$.

Условия применимости. $A \in M_n(\mathbb{C})$. Уравнение Ляпунова разрешимо однозначно $\iff \sigma(A) \cap (-\sigma(A)) = \emptyset$ (Sylvester-критерий — для общего $AX + XB = C$ соответственно $\sigma(A) \cap \sigma(-B) = \emptyset$).

Идея доказательства. Один направление: из E6 при $\alpha(A) < 0$ — экспоненциальное затухание. Обратное: если $\operatorname{Re} \lambda \ge 0$, то $|e^{t\lambda}| \not\to 0$. Lyapunov: $\frac{d}{dt}\bigl(e^{tA^*} Q e^{tA}\bigr) = e^{tA^*} (A^* Q + Q A) e^{tA}$, интегрирование от $0$ до $\infty$ даёт $-Q = A^* P + P A$ при $P = \int_0^\infty e^{tA^*} Q e^{tA} dt$.

Варианты и обобщения.
- Дискретный аналог: $\rho(A) < 1 \iff \exists P \succ 0$ с $A^* P A - P = -Q \prec 0$.
- $\sigma(A) \subset i\mathbb{R}$ и Jordan-блоки чисто мнимых $\lambda$ размера $1$ $\iff e^{tA}$ ограничена и у $A$ есть инвариантная эрмитова форма (фактически — $A$ similar to skew-Hermitian).
- Lyapunov оператор $L_M(X) = MX + XM^T$ имеет спектр $\{\lambda_r(M) + \lambda_s(M)\}_{r,s}$ — см. E5 / E10 в заметке про Jordan, и [IMC-2004-DAY2-4].

Используется в. [IMC-2004-DAY2-4 (спектр $L_M(X) = MX + XM^T$ через собственные пары $v_r v_s^T$ — частный случай tensor structure $L_M = M \otimes I + I \otimes M$, $\sigma(L_M) = \sigma(M) + \sigma(M)$)]. Olympiad-application: оценки $\|A^n\|$ при $\rho(A) < 1$ через дискретный Lyapunov.

---

### E10. Lie product formula (формула Трóттера)

Формулировка. Для любых $A, B \in M_n(\mathbb{C})$ (без коммутативности!):
$$e^{A+B} = \lim_{n \to \infty} \bigl(e^{A/n} e^{B/n}\bigr)^n.$$
Скорость сходимости: $\|e^{A+B} - (e^{A/n} e^{B/n})^n\| = O(1/n)$.

Условия применимости. Конечномерное матричное пространство (универсально). Обобщается на bounded операторы в Banach-алгебрах. Trotter–Kato — на неограниченные генераторы при условиях замкнутости.

Идея доказательства. $e^{A/n} e^{B/n} = I + \frac{A+B}{n} + O(1/n^2)$, поэтому $(e^{A/n} e^{B/n})^n = (I + (A+B)/n + O(1/n^2))^n \to e^{A+B}$ через стандартную оценку $\|X^n - Y^n\| \le n \|X - Y\| \cdot \max(\|X\|, \|Y\|)^{n-1}$.

Варианты и обобщения.
- Симметризованный Trotter (Strang splitting): $e^{A/(2n)} e^{B/n} e^{A/(2n)})^n \to e^{A+B}$ со скоростью $O(1/n^2)$.
- Лотчик-применение: численное решение $\partial_t u = (A + B) u$ через расщепление.
- Связь с BCH: $\log(e^{A/n} e^{B/n}) = (A + B)/n + \frac{1}{2n^2}[A, B] + O(1/n^3)$, поэтому $n \cdot \log(\cdot) = A + B + O(1/n)$.

Используется в. Трюк для тождеств о $e^{A+B}$: переписать через произведения и использовать коммутативные свойства матриц меньшего масштаба. Редко напрямую в IMC, но хороший background для Schweitzer-уровня задач про operator semigroups.

---

## Записи — Exotic

### E11. Matrix logarithm + сюръективность $\exp: M_n(\mathbb{C}) \to GL_n(\mathbb{C})$

Формулировка. Для любой $A \in GL_n(\mathbb{C})$ существует $B \in M_n(\mathbb{C})$ с $e^B = A$. Если $\sigma(A) \subset \mathbb{C} \setminus \mathbb{R}_{\le 0}$ — главная ветвь: $\log A = \frac{1}{2\pi i} \oint_\Gamma \log z \cdot (zI - A)^{-1} dz$ (Riesz–Dunford), $\Gamma$ обходит спектр в правой полуплоскости.

Для real $A \in M_n(\mathbb{R})$ существует real $B \in M_n(\mathbb{R})$ с $e^B = A$ $\iff \det A > 0$ И каждый Jordan-блок $A$ для отрицательного eigenvalue имеет чётный размер.

Условия применимости. Над $\mathbb{C}$ — только обратимость. Над $\mathbb{R}$ — дополнительные ограничения на Jordan-структуру.

Идея доказательства. На Jordan-блоке $J_m(\lambda) = \lambda(I + N/\lambda)$, $N/\lambda$ нильпотент, $\log(I + X) = \sum_{k \ge 1} (-1)^{k+1} X^k / k$ — конечная сумма, всегда сходится для нильпотента. Для блоков с $\lambda = 0$ — нет логарифма (поскольку $A$ обратима, $\lambda = 0$ невозможна).

Варианты и обобщения.
- Над $\mathbb{R}$ для $A \in GL_n^+(\mathbb{R})$ ($\det > 0$): не всегда $A = e^B$, но всегда $A = e^{B_1} e^{B_2}$.
- $\exp: \mathfrak{g} \to G$ сюръективен для компактных связных $G$ (например, $U(n)$), но нет для некомпактных в общем случае ($SL_2(\mathbb{R})$ — есть элементы вне образа exp).
- Многозначность: $e^B = e^{B + 2\pi i k I}$ для целых $k$ — ветвление логарифма.

Используется в. Контрпримеры в задачах «представить $A = e^B$». [IMC-2000-DAY2-6 (использование $e^{AB}$ и $e^{BA}$ как формальный приём, опирается на $e^A$ всегда обратима через E3)].

---

### E12. Baker–Campbell–Hausdorff формула

Формулировка. Существует формальный ряд (сходится для малых $A, B$):
$$\log(e^A e^B) = A + B + \tfrac{1}{2}[A, B] + \tfrac{1}{12}\bigl([A, [A, B]] + [B, [B, A]]\bigr) - \tfrac{1}{24}[B, [A, [A, B]]] + \dots$$
Все слагаемые — итерированные коммутаторы $[X_1, [X_2, [\dots, X_k]]]$ от $A$ и $B$ (Dynkin). Сходимость ряда гарантируется при $\|A\| + \|B\| < \log 2$ (или более тонкие критерии для конкретных норм).

Условия применимости. Конечномерные матричные алгебры — формальный ряд всегда определён. Сходимость — локально в окрестности $0$. Для нильпотентных $A, B$ ряд конечен.

Идея доказательства. Дифференциальное тождество для $Z(t) = \log(e^{tA} e^B)$ с использованием $\frac{d}{dt}\log e^{tA} = (\operatorname{ad}_A / (e^{\operatorname{ad}_A} - I)) \cdot A$, где $\operatorname{ad}_A B = [A, B]$. Получается ODE с правой частью в виде ряда от $\operatorname{ad}_A, \operatorname{ad}_B$.

Варианты и обобщения.
- Если $[A, B] = c \cdot I$ (центральное расширение, например, Heisenberg алгебра) — BCH обрывается: $e^A e^B = e^{A + B + c/2}$.
- Если $[A, [A, B]] = [B, [A, B]] = 0$ — обрывается на первом коммутаторе: $e^A e^B = e^{A + B + [A,B]/2}$.
- Zassenhaus формула (обратная к BCH): $e^{A+B} = e^A e^B e^{-[A,B]/2} e^{(\dots)} \dots$ — поэлементное расщепление.

Используется в. На IMC напрямую редко, но для Schweitzer уровня и «хитрых» Putnam-style задач: оценки $e^A e^B - e^{A+B}$ через коммутаторы. Полезно как «концептуальная» причина почему $e^{A+B} \neq e^A e^B$ — отслеживается порядком коммутатора.

---

### E13. Fréchet производная $\exp$ — формула Daleckii–Krein

Формулировка. Дифференциал $\exp$ в точке $A$ на касательном векторе $B$:
$$D \exp(A)[B] = \frac{d}{dt}\bigg|_{t=0} e^{A + tB} = \int_0^1 e^{(1-s)A} B \, e^{sA} ds = e^A \cdot \frac{I - e^{-\operatorname{ad}_A}}{\operatorname{ad}_A} B,$$
где $\operatorname{ad}_A X = [A, X]$, а функция $\frac{1 - e^{-z}}{z}$ применяется к оператору $\operatorname{ad}_A: M_n \to M_n$ через ряд.

В диагональном базисе для нормальной $A = U \Lambda U^*$ с $\Lambda = \operatorname{diag}(\lambda_i)$:
$$U^* (D \exp(A)[B]) U = \tilde B \odot \Phi, \quad \tilde B = U^* B U, \quad \Phi_{ij} = \frac{e^{\lambda_i} - e^{\lambda_j}}{\lambda_i - \lambda_j} \text{ (или } e^{\lambda_i} \text{ при } i = j\text{)}.$$
Это «divided difference» матрица; $\odot$ — Hadamard product.

Условия применимости. Любая $A \in M_n(\mathbb{C})$, $B$ — произвольная.

Идея доказательства. Прямое: $\frac{d}{dt} e^{A + tB} = $ продифференцировать ряд почленно, использовать $A B \neq B A$ (нельзя коммутировать), получится $\sum_{k} \sum_{j} A^j B A^{k-1-j} / k!$, после симметризации — интеграл.

Варианты и обобщения.
- Daleckii–Krein 1965: общая формула для $D f(A)[B]$ через divided differences $f[\lambda_i, \lambda_j]$ при нормальной $A$.
- Для не-нормальной — формула с Schur-формой или Frechet-Cauchy интеграл $D f(A)[B] = \frac{1}{2\pi i} \oint_\Gamma f(z) (zI - A)^{-1} B (zI - A)^{-1} dz$.
- Hessian: $D^2 \exp(A)[B, C] = \int_{0 \le s + r \le 1} e^{(1 - s - r)A} \bigl(B e^{sA} C + C e^{sA} B\bigr) e^{rA} dr ds$.

Используется в. Schweitzer и продвинутые задачи на дифференцирование матричных функций. Полезно при анализе perturbation $\sigma(e^{A + \epsilon B}) - \sigma(e^A) = O(\epsilon)$.

---

### E14. Golden–Thompson inequality

Формулировка. Для эрмитовых $A, B \in M_n(\mathbb{C})$:
$$\operatorname{tr} e^{A + B} \le \operatorname{tr}(e^A e^B).$$
Равенство $\iff AB = BA$.

Условия применимости. $A, B$ обязательно эрмитовы. Без эрмитовости — может нарушаться.

Идея доказательства. Lie product (E10): $e^{A+B} = \lim_n (e^{A/n} e^{B/n})^n$. Применить $\operatorname{tr} (X^*)^n \le \operatorname{tr}(X X^*)^{n/2}$ (Schwarz) к $X = e^{A/n} e^{B/n}$ и предельный переход. Альтернативно — через Lie–Trotter и concavity.

Варианты и обобщения.
- Не верно для трёх и более матриц: $\operatorname{tr} e^{A+B+C} \not\le \operatorname{tr}(e^A e^B e^C)$ в общем случае (контрпример).
- Lieb's triple matrix inequality (1973): $\operatorname{tr} e^{\log A - \log B + \log C} \le \int_0^\infty \operatorname{tr}\bigl(A (B + tI)^{-1} C (B + tI)^{-1}\bigr) dt$ для PSD $A, B, C$.
- Sutter–Berta–Tomamichel (2017): «multivariate Golden–Thompson» с интегральными представлениями.

Используется в. Inequality-задачи с trace и matrix exponential, особенно Schweitzer и квантовая информация. На IMC не встречается напрямую, но идея «trace полиномов от exp» пересекается с trace-аргументами на нормальных матрицах.

---

### E15. Cayley transform (преобразование Кэли)

Формулировка. Для $A$ с $-1 \notin \sigma(A)$:
$$\Phi(A) = (I - A)(I + A)^{-1} = (I + A)^{-1}(I - A).$$
Свойства:
- $\Phi$ — инволюция: $\Phi(\Phi(A)) = A$.
- $A$ skew-Hermitian ($A^* = -A$) $\iff \Phi(A)$ unitary с $-1 \notin \sigma(\Phi(A))$.
- $A$ skew-symmetric real ($A^T = -A$) $\iff \Phi(A) \in SO(n)$ с $-1 \notin \sigma(\Phi(A))$.
- Real часть: для эрмитовой $A$ имеем $\Phi(A)$ unitary $\iff A$ эрмитова и spectrum в $i\mathbb{R}$ — нет, не сходится. Точно: эрмитова $A$ даёт $\Phi(A)$ с unitary $\iff i A$ skew-Hermitian.

Связь с exp: $\Phi$ — рациональная Padé-аппроксимация $[1/1]$ к $e^{2A}$ (конформное отображение в правую полуплоскость аналог).

Условия применимости. $-1 \notin \sigma(A)$. Для skew-Hermitian — почти всегда выполнено.

Идея доказательства. $A^* = -A \Rightarrow \Phi(A)^* \Phi(A) = (I + A)^{-T} (I - A)^T (I - A)(I + A)^{-1} = (I - A)^{-1}(I + A)(I - A)(I + A)^{-1} = (I-A)^{-1}(I-A^2)(I+A)^{-1}$ (использовали $(I+A)(I-A) = (I-A)(I+A) = I - A^2$). Дальше упрощается до $I$ при $A^* = -A$.

Варианты и обобщения.
- Cayley parametrization: $SO(n) \setminus \{$матриц с $-1$ в спектре$\}$ параметризуется skew-symmetric матрицами через $\Phi$, открытое плотное подмножество.
- Аналог в matrix Lie groups: для каждой матричной Lie-группы есть ratiональная параметризация Cayley-типа в окрестности единицы.
- Discrete-time stability: $\rho(A) < 1 \iff (I - A)(I + A)^{-1}$ — устойчивая в continuous-time смысле, $\alpha < 0$.

Используется в. Параметризации $SO(n)$ и $U(n)$ через линейное (skew) пространство. Putnam / IMC: показать что определённое подмножество $O(n)$ открыто / связно через exp / Cayley-параметризации.

---

## Self-test

1. Найти $e^{tA}$ для $A = \begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix}$ и описать орбиты ODE $x' = Ax$ в $\mathbb{R}^2$.

2. Доказать, что для любой $A \in M_n(\mathbb{C})$ имеет место $\det e^A \neq 0$, и более точно $|\det e^A| = e^{\operatorname{Re} \operatorname{tr} A}$.

3. Пусть $A \in M_n(\mathbb{R})$ — кососимметричная ($A^T = -A$). Показать, что $e^A \in SO(n)$.

4. Существует ли $B \in M_2(\mathbb{R})$ такая, что $e^B = \begin{pmatrix} -1 & 0 \\ 0 & -2 \end{pmatrix}$?

5. Доказать, что если $\rho(A) < 1$, то $\sum_{k=0}^\infty A^k = (I - A)^{-1}$, причём ряд сходится в operator norm.

6. Пусть $A \in M_n(\mathbb{C})$ удовлетворяет $A^k \to 0$ при $k \to \infty$ в operator norm. Доказать, что $\rho(A) < 1$.

7. Пусть $A, B \in M_n(\mathbb{C})$ — эрмитовы и коммутируют. Показать, что $e^{A+B} = e^A e^B$ и что $e^A e^B$ эрмитова и положительно определённая.

8. Пусть $M \in M_n(\mathbb{R})$ имеет собственные значения $\lambda_1, \dots, \lambda_n$ (с кратностями). Найти спектр оператора $L_M: M_n(\mathbb{R}) \to M_n(\mathbb{R})$, $L_M(X) = MX + XM^T$.

9. Пусть $A \in M_n(\mathbb{C})$ с $\sigma(A) \subset \{\operatorname{Re} z < 0\}$, $Q \succ 0$. Показать, что $P = \int_0^\infty e^{tA^*} Q e^{tA} dt$ корректно определён, $P \succ 0$, и $A^* P + P A = -Q$.

10. Доказать, что $\operatorname{tr}((AB - BA)^k) = 0$ для всех нечётных $k \ge 1$, если $A, B \in M_n(\mathbb{R})$ — симметричные. (Указание: использовать spectral mapping и antisymmetry $(AB - BA)^T = BA - AB = -(AB - BA)$.)

---

## Решения

1. $A^2 = -I$ (т.е. $A$ — мнимая единица в матричном виде). $e^{tA} = \cos t \cdot I + \sin t \cdot A = \begin{pmatrix} \cos t & -\sin t \\ \sin t & \cos t \end{pmatrix}$ — стандартное вращение. ODE-орбиты — окружности с центром в $0$. По E3: $\det e^{tA} = e^{t \cdot 0} = 1$ — согласовано с $\det R_t = 1$.

2. $\det e^A = e^{\operatorname{tr} A}$ (E3) над $\mathbb{C}$. $|\det e^A| = |e^{\operatorname{tr} A}| = e^{\operatorname{Re}(\operatorname{tr} A)}$ — стандартная формула $|e^z| = e^{\operatorname{Re} z}$. $\det e^A \neq 0$ потому что $e^A \cdot e^{-A} = I$ (E4: $A$ и $-A$ коммутируют).

3. $A^T = -A \Rightarrow (e^A)^T = e^{A^T} = e^{-A}$. $(e^A)^T e^A = e^{-A} e^A = I$ (E4 на коммутирующих $-A, A$), значит $e^A$ ортогональная. $\det e^A = e^{\operatorname{tr} A} = e^0 = 1$ ($\operatorname{tr}$ skew-symmetric $= 0$), значит $e^A \in SO(n)$.

4. Нет такой $B$. По E2 спектр $e^B = \{e^{\lambda_1}, e^{\lambda_2}\}$, должен совпасть с $\{-1, -2\}$. Для real $B$ собственные значения либо real, либо пары комплексно-сопряжённых. Случай 1: real $\lambda_i \Rightarrow e^{\lambda_i} > 0$ — не покрывает $\{-1, -2\}$. Случай 2: $\lambda_{1,2} = a \pm ib$, $b > 0$, $e^{\lambda_{1,2}} = e^a (\cos b \pm i \sin b)$ — комплексно-сопряжённые. $\{-1, -2\}$ — оба real, не комплексно-сопряжённая пара (если бы хотя бы один не-real). Получается, что нужны два разных real eigenvalues, оба отрицательные — но Jordan-блок чётного размера для $-1$ не подходит, размер блока $1$. По E11 такого $B$ нет (блок размера 1 для отрицательного eigenvalue запрещён).

5. Для $\rho(A) < 1$ выберем norm так, что $\|A\| < 1$ (existence — по Gelfand: $\|A\|_\epsilon := \sup_n \|A^n\|^{1/n} \cdot (1 + \epsilon)$). Тогда $\sum \|A^k\| \le \sum \|A\|^k < \infty$, ряд абсолютно сходится. $(I - A)\sum_{k=0}^N A^k = I - A^{N+1} \to I$ (E6: $A^k \to 0$). Получаем $(I - A)^{-1} = \sum A^k$.

6. $\|A^k\|^{1/k} \to \rho(A)$ (Gelfand). $\|A^k\| \to 0 \Rightarrow$ в частности $\|A^k\|^{1/k} \to 0 \le \rho(A)$. С другой стороны, $\|A^k\| \ge |\lambda|^k$ для каждого собственного $\lambda$ (через собственный вектор), значит $|\lambda| < 1$. Это даёт $\rho(A) < 1$ строго (нужно ещё выкрутить полиномиальный множитель — для $|\lambda| = 1$ имеем $|\lambda|^k = 1 \not\to 0$, противоречие; значит $|\lambda| < 1$ для всех $\lambda$, и $\rho(A) < 1$).

7. $AB = BA \Rightarrow e^{A+B} = e^A e^B$ (E4). $e^A e^B = (e^A)(e^B)$ — произведение двух эрмитовых положительно-определённых (по E3 спектр $e^A = e^{\sigma(A)} \subset \mathbb{R}_{> 0}$, и $e^A$ эрмитова потому что $A$ эрмитова: $(e^A)^* = e^{A^*} = e^A$). При коммутативности $A, B$ — также $e^A, e^B$ коммутируют, тогда $e^A e^B = (e^A)^{1/2} e^B (e^A)^{1/2}$ (через коммутативность) — congruence сохраняет PSD. Итого $e^{A+B} = e^A e^B \succ 0$, эрмитова.

8. Через E5 / E9: $L_M = M \otimes I + I \otimes M$ как оператор на $M_n \cong \mathbb{R}^{n^2}$ (если транспонирование убрать через изоморфизм). Точнее с транспонированием: $L_M(X) = MX + XM^T$ имеет собственные пары $X = v_r v_s^T$ (где $M v_r = \lambda_r v_r$, $M^T u_s = \lambda_s u_s$), $L_M(v_r u_s^T) = (\lambda_r + \lambda_s)(v_r u_s^T)$. Спектр $L_M = \{\lambda_r + \lambda_s : r, s = 1, \dots, n\}$ с кратностями (общий случай по непрерывности от диагонализуемых). Это — IMC-2004-DAY2-4.

9. Сходимость: $\|e^{tA}\| \le C(1 + t^{m-1}) e^{\alpha(A) t}$ (E6) с $\alpha(A) < 0$, поэтому $\|e^{tA^*} Q e^{tA}\| \le \|Q\| \cdot C^2 (1 + t^{m-1})^2 e^{2\alpha(A) t}$ — экспоненциальное затухание. Интеграл сходится. $P^* = \int_0^\infty (e^{tA^*} Q e^{tA})^* dt = \int e^{tA^*} Q e^{tA} dt = P$ (так как $Q^* = Q$). $P \succ 0$ потому что $x^* P x = \int_0^\infty \|Q^{1/2} e^{tA} x\|^2 dt \ge 0$ с равенством $\iff Q^{1/2} e^{tA} x \equiv 0 \iff x = 0$ (поскольку $e^{tA}$ обратима, $Q^{1/2}$ инъективна). Тождество Lyapunov: $\frac{d}{dt}(e^{tA^*} Q e^{tA}) = e^{tA^*}(A^* Q + Q A) e^{tA}$, интегрирование от $0$ до $\infty$ даёт $0 - Q = A^* P + P A$, т.е. $A^* P + P A = -Q$.

10. $C = AB - BA$. Для real symmetric $A, B$: $C^T = (AB - BA)^T = B^T A^T - A^T B^T = BA - AB = -C$, значит $C$ skew-symmetric. Спектр real skew-symmetric лежит в $i\mathbb{R}$ и состоит из пар $\pm i \mu_k$ (E12 в заметке про Jordan / спектральная теорема). По E2: $\sigma(C^k) = \{(i\mu_j)^k\} \cup \{(-i\mu_j)^k\}$. Для нечётного $k$: $(i\mu)^k + (-i\mu)^k = 2 \operatorname{Re}((i\mu)^k) = 0$ (мнимое число в нечётной степени — снова мнимое). Сумма по парам $= 0$, значит $\operatorname{tr}(C^k) = \sum (i\mu_j)^k + \sum (-i\mu_j)^k = 0$. Дополнительно — нулевые eigenvalues (если $\dim$ нечётная) тоже в нечётной степени дают $0$.
