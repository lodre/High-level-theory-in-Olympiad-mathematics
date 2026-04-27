---
topic: Линейная алгебра
subtopic: "Positive (semi)definite матрицы: A=B^TB, корни, критерии; singular values (базово)"
sources:
  - "Horn, Johnson — Matrix Analysis (главы 4, 7)"
  - "Horn, Johnson — Topics in Matrix Analysis"
  - "Bhatia — Matrix Analysis (Springer GTM 169)"
  - "Bhatia — Positive Definite Matrices"
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Polya, Szegő — Problems and Theorems in Analysis II"
  - "Engel — Problem-Solving Strategies"
  - "IMC Compendium"
  - "Putnam Compendium / Kedlaya–Poonen–Vakil archive"
  - "Yufei Zhao — Linear Algebra Tricks for the Putnam"
  - "Barry Simon — Loewner's Theorem on Monotone Matrix Functions"
  - "Barbeau — Putnam Problems in Matrices, Determinants and Vector Spaces"
problems_referenced:
  - IMC-2006-DAY2-4
  - IMC-2007-DAY2-4
  - IMC-2010-5
  - IMC-2018-3
  - IMC-2024-3
  - Putnam-1999-A5
  - Putnam-2005-A4
  - Putnam-2008-A6
  - Putnam-2014-A2
last_updated: 2026-04-27
---

# Positive (semi)definite матрицы: $A=B^TB$, корни, критерии; singular values (базово)

## Scope
Класс symmetric / Hermitian PSD-матриц и их инвариантов. Эквивалентные критерии positivity (spectrum, Gram, leading minors), факторизации (Cholesky, square root, polar, SVD), вариационные характеристики собственных и сингулярных чисел (Courant–Fischer, Weyl, Cauchy interlacing), частичный порядок Loewner-а, неравенства уровня IMC / Putnam (Hadamard / Fischer / Minkowski / Schur product / Loewner–Heinz). Singular values рассматриваются как «PSD-проекция» произвольной матрицы через $A^*A$, $AA^*$.

## Записи — Core

### E1. Spectral theorem (спектральная теорема для symmetric / Hermitian) и 4 эквивалентных критерия PSD

Формулировка. Для $A \in \mathbb{C}^{n \times n}$ Hermitian (т. е. $A^* = A$) существует унитарная $U$ и вещественная диагональная $\Lambda = \operatorname{diag}(\lambda_1, \dots, \lambda_n)$ с $A = U \Lambda U^*$. Для real symmetric — то же с ортогональной $Q$. Эквиваленты для PSD ($A \succeq 0$):
1. $x^* A x \ge 0$ для всех $x \in \mathbb{C}^n$;
2. все $\lambda_i(A) \ge 0$;
3. $A = B^* B$ для некоторой $B$ (см. E2);
4. все главные миноры (principal minors) $\ge 0$.
Для PD ($A \succ 0$) во всех пунктах строгие неравенства, и в (4) достаточно ведущих главных миноров (Sylvester, E3).

Условия применимости. Hermitian обязательно для (1)–(4): без неё пункт (1) перестаёт совпадать с (2) (eigenvalues могут быть комплексными). В real-случае нужен symmetric + работать с $x \in \mathbb{R}^n$.

Идея доказательства. (2) $\Leftrightarrow$ (1): диагонализация $A = U \Lambda U^*$ даёт $x^* A x = \sum \lambda_i |y_i|^2$, $y = U^* x$. (3) $\Rightarrow$ (1): $x^* B^* B x = \|Bx\|^2 \ge 0$. (1) $\Rightarrow$ (3): через $A = U \Lambda U^*$ положить $B = \Lambda^{1/2} U^*$.

Используется в. [IMC-2010-5 (PSD-критерий через $A = B^T B$ + tensor power)], [IMC-2018-3 (PD ⇒ существование квадратного корня)], база для всех остальных записей.

---

### E2. Gram representation (Gram-разложение): $A = B^* B$

Формулировка. $A \in \mathbb{C}^{n \times n}$ Hermitian PSD $\iff$ $A = B^* B$ для некоторой $B \in \mathbb{C}^{m \times n}$. Минимальный $m$ равен $r := \operatorname{rank}(A)$, и при $m = r$ строки $B$ — линейно независимы. Эквивалентно: $A_{ij} = \langle v_i, v_j \rangle$ для некоторой системы векторов $v_1, \dots, v_n \in \mathbb{C}^m$.
$$\operatorname{rank}(A) = \dim \operatorname{span}(v_1, \dots, v_n).$$
$\det A = $ объём$^2$ параллелепипеда, натянутого на $\{v_i\}$ (Gram-определитель).

Условия применимости. Любое поле с инволюцией ($\mathbb{R}, \mathbb{C}$). Для PD дополнительно $B$ имеет полный столбцовый ранг.

Идея доказательства. Через спектральное разложение $A = U \Lambda U^*$, $\Lambda \succeq 0$: $B = \Lambda^{1/2} U^*$. Альтернатива — Cholesky (E4) при PD; при PSD — pivoted Cholesky.

Варианты и обобщения.
- Gram-определитель: $\det(\langle v_i, v_j \rangle) \ge 0$, $= 0 \iff$ векторы линейно зависимы. Это и Cauchy–Schwarz при $n = 2$.
- Над $\mathbb{R}$: $A$ symmetric PSD $\iff$ $A = B^T B$, причём можно взять $B$ квадратной.
- Любое $A$ с $A^* A$ эрмитово PSD ⇒ singular values $A$ — корни из eigenvalues $A^* A$ (см. E7).

Используется в. [IMC-2006-DAY2-4 (рациональность $\langle v_i, v_j \rangle$ ⇒ рациональность решения через обращение Gram-матрицы)], [IMC-2010-5 (взять $B$ со столбцами $x, y, z$, длины 1, и применить тензорную степень $\otimes^n$, чтобы получить степенную версию)], стандартный приём «PSD ⇒ можно взять корень / Gram-форму».

---

### E3. Sylvester's criterion (критерий Сильвестра)

Формулировка. Для Hermitian $A \in \mathbb{C}^{n \times n}$:
- $A \succ 0 \iff$ все ведущие главные миноры $\Delta_k = \det(A_{[1:k], [1:k]}) > 0$, $k = 1, \dots, n$.
- $A \succeq 0$ $\iff$ все $2^n - 1$ главных миноров (по любым подмножествам индексов) $\ge 0$. Только ведущих — НЕ достаточно для PSD: контрпример $A = \operatorname{diag}(0, -1)$ имеет $\Delta_1 = \Delta_2 = 0$.

Условия применимости. Hermitian (для real — symmetric). Без эрмитовости критерий бессмыслен.

Идея доказательства. Индукция по $n$. Шаг через Schur complement (E11): если $\Delta_{n-1} > 0$, то $A$ блочно-разложима как
$$A = \begin{pmatrix} A_{n-1} & b \\ b^* & a_{nn} \end{pmatrix}, \quad \det A = \Delta_{n-1} \cdot (a_{nn} - b^* A_{n-1}^{-1} b).$$
Множитель $a_{nn} - b^* A_{n-1}^{-1} b > 0$ $\iff$ $A \succ 0$ при $A_{n-1} \succ 0$.

Варианты и обобщения.
- $A \succ 0$ $\iff$ существует Cholesky $A = L L^*$ с $L$ нижнетреугольной с $\operatorname{diag}(L) > 0$ (E4).
- $A \succ 0 \iff a_{ii} > 0$ и $|a_{ij}|^2 < a_{ii} a_{jj}$ для всех $i \neq j$ — необходимо, но НЕ достаточно (только при $n = 2$).
- Для PSD проверка $2^n - 1$ миноров неэффективна; на практике — спектральная проверка.

Используется в. [IMC-2010-5 (PSD-проверка $3 \times 3$ матрицы через $\det \ge 0$ и $2 \times 2$ миноры $\ge 0$)], стандартный rapid-test на IMC / Putnam, особенно для $2 \times 2$ и $3 \times 3$ блочных конструкций.

---

### E4. Cholesky decomposition (разложение Холецкого)

Формулировка. $A \succ 0$ Hermitian $\iff$ существует единственная нижнетреугольная $L$ с $L_{ii} > 0$, такая что
$$A = L L^*.$$
Эквивалентная форма $L D L^*$ с диагональной $D \succ 0$ и unit-нижнетреугольной $L$ — даёт single-pass алгоритм без квадратных корней. Для PSD-случая: разложение существует, но без гарантии единственности (требуется pivoting); $\operatorname{rank}(A) = $ число положительных $D_{ii}$.

Условия применимости. PD (для строгой версии). Над $\mathbb{R}$ и $\mathbb{C}$. Над общим полем — нужно $\sqrt{\Delta_k / \Delta_{k-1}} \in \mathbb{F}$, иначе только $LDL^*$.

Идея доказательства. Индуктивно: после выделения первой строки / столбца через $A_{11} = \ell_{11}^2$, $\ell_{i1} = a_{i1}/\ell_{11}$, остаток — Schur complement $A' = A_{[2:n]} - \ell \ell^*$, и $A' \succ 0$ (при $A \succ 0$).

Варианты и обобщения.
- Связь с Sylvester (E3): $\det L = \prod \ell_{ii} = \prod \sqrt{\Delta_k / \Delta_{k-1}} > 0$.
- $\det A = (\det L)^2 = \prod \ell_{ii}^2$ — даёт явную positivity.
- Для general (не эрмитовой) PD-формы $A$ — LU-разложение (без $L L^*$); Cholesky — special case.

Используется в. Конструктивная сторона $A = B^* B$ (E2). Решение $A x = b$ для PSD-систем (back-substitution за $O(n^2)$ после $O(n^3)$ факторизации). На олимпиадах — как способ получить «треугольный» $B$ из PSD $A$.

---

### E5. Square root (квадратный корень) PSD-матрицы

Формулировка. Любая PSD $A$ имеет единственный PSD корень $A^{1/2}$: $A^{1/2} \succeq 0$, $(A^{1/2})^2 = A$. Через спектральное разложение $A = U \Lambda U^*$:
$$A^{1/2} = U \Lambda^{1/2} U^*, \quad \Lambda^{1/2} = \operatorname{diag}(\sqrt{\lambda_i}).$$
Квадратные корни общего вида (любая $X$ с $X^2 = A$) при PD-$A$ образуют дискретное семейство из $2^r$ элементов (по выбору знаков на $r$ различных eigenvalues), и непрерывное при кратных.

Условия применимости. PSD (Hermitian с $\lambda_i \ge 0$). Если $A$ только nonsingular, но не PSD — корень может не существовать в нужном поле / классе (например, $-I$ не имеет real-корня).

Идея доказательства. Существование — спектрально. Единственность PSD-корня: пусть $X \succeq 0$, $X^2 = A$. Тогда $X$ коммутирует с $A$ ($XA = X^3 = AX$), значит $X$ диагонализуется в том же базисе, что $A$, и $X = U M U^*$ с $M^2 = \Lambda$, $M \succeq 0$ ⇒ $M = \Lambda^{1/2}$.

Варианты и обобщения.
- $A^t$ для $t \ge 0$: тот же spectral calculus, $A^t = U \Lambda^t U^*$.
- Loewner–Heinz (E15): $A \succeq B \succeq 0 \Rightarrow A^t \succeq B^t$ для $t \in [0, 1]$ — нетривиальное расширение monotonicity для $t = 1/2$.
- Корень в общем виде: при PD-$A$ имеется $2^n$ involutive корней через диагональные $\pm 1$.

Используется в. [IMC-2007-DAY2-4 (циркулянтная $A = B^2$, корень — через DFT-диагонализацию)], [IMC-2018-3 (поиск рациональных $K$ с $K^2 = M$)], [IMC-2024-3 ($A^2 = J$ — но не PSD сразу, через анализ rank и trace)], стандартное «возвести PSD в дробную степень».

---

### E6. Polar decomposition (полярное разложение)

Формулировка. Любая $A \in \mathbb{C}^{m \times n}$ ($m \ge n$) разлагается как
$$A = U P,$$
где $U$ — частично-унитарная (semi-unitary, $U^* U = I_n$), $P = (A^* A)^{1/2} \succeq 0$. При $\operatorname{rank}(A) = n$ матрица $U$ единственна; $P$ единственна всегда. Альтернативная (правая) форма $A = P' V$, $V$ unitary, $P' = (A A^*)^{1/2}$. Real-версия: ортогональная $U$, symmetric PSD $P$.

Условия применимости. Любое $A$. Аналог комплексного $z = e^{i\theta} |z|$ для матриц.

Идея доказательства. Через SVD $A = U_1 \Sigma V^*$ (E7): $P = V \Sigma V^* = (A^* A)^{1/2}$, $U = U_1 V^*$. Альтернативно — через $P = (A^* A)^{1/2}$, $U = A P^{-1}$ при invertible $A$, и предельный переход при rank-deficient.

Варианты и обобщения.
- Single-Value Decomposition (E7) — переформулировка polar в стандартизованной форме.
- Для real square — $U \in O(n)$, $P$ symmetric PSD.
- Polar as projection: $U$ — это решение задачи $\min_{U^* U = I} \|A - U\|_F$ — ближайшая semi-unitary к $A$.

Используется в. Когда нужно «отделить геометрию (вращение / отражение) от растяжения (PSD)»: задачи на $A = B^T B$ + ортогональные условия. Putnam-style: «доказать, что любая $n \times n$ матрица представима как произведение symmetric и orthogonal» — это и есть polar.

---

### E7. SVD (singular value decomposition / сингулярное разложение)

Формулировка. $A \in \mathbb{C}^{m \times n}$ имеет разложение
$$A = U \Sigma V^*,$$
где $U \in \mathbb{C}^{m \times m}$ unitary, $V \in \mathbb{C}^{n \times n}$ unitary, $\Sigma \in \mathbb{R}^{m \times n}$ — «диагональная» (только $\Sigma_{ii} = \sigma_i$ ненулевые) с $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_{\min(m,n)} \ge 0$. Числа $\sigma_i$ — singular values, $\sigma_i^2 = \lambda_i(A^* A) = \lambda_i(A A^*)$. Ненулевых $\sigma_i$ ровно $\operatorname{rank}(A)$.

Условия применимости. Любое $A$. Над $\mathbb{R}$ — ортогональные $U, V$. Существование — следствие spectral theorem (E1) для $A^* A$.

Идея доказательства. Применить spectral theorem к Hermitian PSD $A^* A = V \Sigma^2 V^*$. Положить $u_i = A v_i / \sigma_i$ для $\sigma_i > 0$, дополнить до ortonorm. базиса $U$. Прямая проверка $A v_i = \sigma_i u_i$.

Варианты и обобщения.
- Compact / thin SVD: $A = U_r \Sigma_r V_r^*$ с $U_r \in \mathbb{C}^{m \times r}$, $V_r \in \mathbb{C}^{n \times r}$, $\Sigma_r \in \mathbb{R}^{r \times r}$ диагональная PD, $r = \operatorname{rank}(A)$. Минимальный rank-разложение.
- Pseudoinverse (Moore–Penrose): $A^+ = V \Sigma^+ U^*$, где $\Sigma^+$ — транспонированная с обращением ненулевых $\sigma_i$. Удовлетворяет $AA^+A = A$, $A^+ A A^+ = A^+$, $(AA^+)^* = AA^+$, $(A^+ A)^* = A^+ A$.
- Eckart–Young: best rank-$k$ approximation в $\|\cdot\|_F$ и $\|\cdot\|_2$ — обрезание SVD до первых $k$ singular values. $\min_{\operatorname{rank} B \le k} \|A - B\|_2 = \sigma_{k+1}$.

Используется в. Стандарт для оценки расстояния до сингулярного семейства, для $\operatorname{rank}$-задач на возмущения, для $\|\cdot\|_2$-оценок. На IMC реже как явное название, чаще через $A^* A$ и его eigenvalues (см. E8).

---

### E8. Variational characterisation (вариационная характеризация): Courant–Fischer и min-max для $\sigma_k$

Формулировка. Для Hermitian $A \in \mathbb{C}^{n \times n}$ с $\lambda_1 \ge \dots \ge \lambda_n$ (упорядочены по убыванию):
$$\lambda_k(A) = \max_{\substack{V \subset \mathbb{C}^n \\ \dim V = k}} \min_{\substack{x \in V \\ \|x\| = 1}} x^* A x = \min_{\substack{V \subset \mathbb{C}^n \\ \dim V = n-k+1}} \max_{\substack{x \in V \\ \|x\| = 1}} x^* A x.$$
Аналогично для singular values $A \in \mathbb{C}^{m \times n}$:
$$\sigma_k(A) = \max_{\dim V = k} \min_{x \in V, \|x\|=1} \|A x\| = \min_{\dim V = n-k+1} \max_{x \in V, \|x\|=1} \|A x\|.$$
Частные случаи: $\sigma_1 = \|A\|_2 = \max_{\|x\|=1} \|Ax\|$ — operator norm; $\sigma_n = \min_{\|x\|=1} \|Ax\|$ — distance к singular at $A$ invertible.

Условия применимости. Hermitian (для $\lambda$); любая (для $\sigma$). Базовый инструмент для всех «$\min$-$\max$» оценок.

Идея доказательства. Диагонализуем $A = U \Lambda U^*$, переходим к координатам $y = U^* x$, форма становится $\sum \lambda_i |y_i|^2$. Дальше — стандартный аргумент о пересечении $k$-мерного и $(n-k+1)$-мерного подпространств в $\mathbb{C}^n$ (имеют непустое пересечение по dimension count).

Варианты и обобщения.
- Rayleigh quotient: $R(x) = x^* A x / x^* x$, $\lambda_n \le R(x) \le \lambda_1$, экстремумы достигаются на eigenvectors.
- Wielandt's min-max: $\lambda_{i_1}(A) + \dots + \lambda_{i_k}(A) = \max_{\dim V_1 < \dots < V_k = ?}\ldots$ для произвольных индексов.
- Ky Fan trace inequality: $\sum_{i=1}^k \sigma_i(A + B) \le \sum_{i=1}^k \sigma_i(A) + \sum_{i=1}^k \sigma_i(B)$.

Используется в. База для Cauchy interlacing (E9), Weyl (E10), доказательств monotonicity. На IMC — типовой приём «оценить $\lambda_1$ через подбор пробного $x$». Putnam-style: «$\|A\|_2 \ge \|A x\| / \|x\|$ для конкретного $x$» $\Rightarrow$ нижняя оценка $\sigma_1$.

---

## Записи — Standard

### E9. Cauchy interlacing (теорема о перемежении Коши)

Формулировка. Пусть $A \in \mathbb{C}^{n \times n}$ Hermitian с $\lambda_1 \ge \dots \ge \lambda_n$, $B$ — главный $(n-1) \times (n-1)$ submatrix с собственными числами $\mu_1 \ge \dots \ge \mu_{n-1}$. Тогда
$$\lambda_1 \ge \mu_1 \ge \lambda_2 \ge \mu_2 \ge \dots \ge \mu_{n-1} \ge \lambda_n.$$
Общее: для главной $(n-k) \times (n-k)$ submatrix: $\lambda_i \ge \mu_i \ge \lambda_{i+k}$ для всех $i$.

Условия применимости. Hermitian + главная submatrix (по любому подмножеству строк-столбцов с одинаковыми индексами). Для не-главных submatrix (произвольные строки / столбцы) — заменяется на singular value interlacing (см. варианты).

Идея доказательства. Через Courant–Fischer (E8): $\mu_i \ge \min_{V \cap W^\perp \ne 0} \dots \ge \lambda_{i+1}$, где $W$ — подпространство, дополнительное к строкам / столбцам $B$ в $A$. Технически — пересечение подпространств размерностей $i$ и $n-i$ в $\mathbb{C}^n$ непусто.

Варианты и обобщения.
- Poincaré separation: для $V \subset \mathbb{C}^n$ размерности $k$ и проекции $A|_V$: $\lambda_i(A) \ge \lambda_i(A|_V) \ge \lambda_{i+n-k}(A)$.
- Singular value interlacing: $\sigma_i(A) \ge \sigma_i(B) \ge \sigma_{i+1}(A)$ при удалении столбца / строки.
- Weyl monotonicity ($A \succeq B \Rightarrow \lambda_i(A) \ge \lambda_i(B)$) — следствие.

Используется в. Задачи на оценки $\lambda_{\max}, \lambda_{\min}$ через подматрицы. Например, доказательства unique-eigenvalue claims, оценки norm $\|A\|_2$ через локальные подматрицы. На IMC — фоновый инструмент в задачах про rank и spectrum.

---

### E10. Weyl's inequalities (неравенства Вейля) для eigenvalues и singular values

Формулировка. Для Hermitian $A, B \in \mathbb{C}^{n \times n}$ с собственными числами $\lambda_1 \ge \dots \ge \lambda_n$:
$$\lambda_{i+j-1}(A + B) \le \lambda_i(A) + \lambda_j(B), \quad i + j - 1 \le n,$$
$$\lambda_{i+j-n}(A + B) \ge \lambda_i(A) + \lambda_j(B), \quad i + j - n \ge 1.$$
В частности, $\lambda_i(A + B) \le \lambda_i(A) + \lambda_1(B)$ и $\lambda_i(A) - \lambda_i(B) \le \|A - B\|_2$ — perturbation bound.
Для singular values произвольных $A, B$: $\sigma_{i+j-1}(A + B) \le \sigma_i(A) + \sigma_j(B)$ и $\sigma_{i+j-1}(AB) \le \sigma_i(A) \sigma_j(B)$.

Условия применимости. Hermitian для eigen-версии; любые для singular. Доказательство через Courant–Fischer (E8) с подбором тройки подпространств.

Идея доказательства. Eigen-version: возьмём максимизирующее $i$-мерное подпространство $V_A$ для $A$, $j$-мерное $V_B$ для $B$. Их сумма имеет размерность $\ge i + j - 1$ (если пересечение нетривиально, это даёт оценку). Для $x \in V_A \cap V_B$: $x^*(A+B)x \le \lambda_i(A) + \lambda_j(B)$.

Варианты и обобщения.
- Lidskii's inequality: $\sum_i (\lambda_i(A) - \lambda_i(B)) \le \sum_i \lambda_i(A - B)$ для Hermitian.
- Hoffman–Wielandt: $\sum_i (\lambda_i(A) - \lambda_i(B))^2 \le \|A - B\|_F^2$ при normal $A, B$.
- Horn's conjecture (доказана Klyachko / Knutson–Tao): полное описание всех возможных троек $(\lambda(A), \lambda(B), \lambda(A+B))$.

Используется в. Perturbation analysis — основной инструмент. На IMC — при оценках $\|A^k\|$ через $\sigma_1(A)$, при сравнении spectrum-ов $A$ и $A + uv^*$ (rank-1 возмущения).

---

### E11. Schur complement (дополнение Шура): критерий positivity

Формулировка. Для блочной Hermitian
$$M = \begin{pmatrix} A & B \\ B^* & D \end{pmatrix}, \quad D \succ 0,$$
имеем $M \succ 0 \iff A - B D^{-1} B^* \succ 0$ (Schur complement $M / D$). Для PSD-версии: $M \succeq 0 \iff D \succeq 0$, $\operatorname{range}(B) \subseteq \operatorname{range}(D)$ и $A - B D^+ B^* \succeq 0$.

Условия применимости. Любая блочная $M$ Hermitian. Для PSD-варианта Schur complement берётся через pseudoinverse $D^+$.

Идея доказательства. Block congruence: $M = \begin{pmatrix} I & BD^{-1} \\ 0 & I \end{pmatrix} \begin{pmatrix} A - BD^{-1}B^* & 0 \\ 0 & D \end{pmatrix} \begin{pmatrix} I & 0 \\ D^{-1}B^* & I \end{pmatrix}$. Поскольку congruence сохраняет signature (Sylvester's law of inertia), $M \succ 0 \iff$ оба диагональных блока $\succ 0$.

Варианты и обобщения.
- $\det M = \det D \cdot \det(A - BD^{-1}B^*)$ (см. E2 в записках по определителям) — определительная сторона.
- Quotient property: $(M / D) / (A / D) = M / A$ — для рекурсивного шурирования.
- Для PSD: $M \succeq 0 \Rightarrow A \succeq B D^+ B^*$, что часто и используется как «sandwich»-неравенство.

Используется в. [IMC-2010-5 (PSD-проверка $3 \times 3$ через расширение и Schur complement)], LMI-задачи (Linear Matrix Inequalities), доказательства Cauchy–Schwarz-подобных bounds для PSD-форм.

---

### E12. Loewner order (порядок Loewner-а) и его базовые свойства

Формулировка. Loewner order: $A \succeq B$ означает $A - B \succeq 0$. Это частичный порядок на Hermitian-матрицах (рефлексивен, антисимметричен, транзитивен). Свойства:
1. Conjugation-invariant: $A \succeq B \Rightarrow C^* A C \succeq C^* B C$ для любой $C$.
2. Inverse-monotone (anti-tone): $0 \prec A \preceq B \Rightarrow B^{-1} \preceq A^{-1}$.
3. Square-root monotone: $0 \preceq A \preceq B \Rightarrow A^{1/2} \preceq B^{1/2}$ (частный случай Loewner–Heinz, E15).
4. Square НЕ монотонен: $A \succeq B \succeq 0 \not\Rightarrow A^2 \succeq B^2$. Стандартный контрпример: $A = \begin{pmatrix} 2 & 1 \\ 1 & 1 \end{pmatrix}$, $B = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}$.
5. $A \succeq B \succeq 0 \Rightarrow \lambda_i(A) \ge \lambda_i(B)$, $\operatorname{tr}(A) \ge \operatorname{tr}(B)$, $\det(A) \ge \det(B)$.

Условия применимости. Hermitian (real symmetric) обоих операндов. Для не-Hermitian $A$ запись $A \succeq 0$ всё ещё имеет смысл (через $A + A^* \succeq 0$ и Hermitian part), но порядок теряет антисимметричность.

Идея доказательства. (1)–(2) — прямая алгебра. (3) — частный случай Loewner–Heinz (E15). (5) — следует из Courant–Fischer (E8) и monotonicity $\det$ относительно eigenvalues.

Варианты и обобщения.
- Operator monotone functions (по Loewner-у): $f$ называется operator-monotone, если $A \succeq B \succeq 0 \Rightarrow f(A) \succeq f(B)$. Loewner's theorem характеризует такие $f$ как restriction Pick-функций (Nevanlinna представление).
- Operator convex / concave аналоги.
- $f(t) = t^\alpha$ operator-monotone $\iff \alpha \in [0, 1]$ (E15).
- $f(t) = \log t$ operator-monotone на $(0, \infty)$.

Используется в. Задачи на сравнение PSD-матриц без явного вычисления eigenvalues. Аккуратность: $\succeq$ НЕ совпадает с поэлементным $\ge$. На IMC — при контрпримерах вида «найти $A, B$ с $A \succeq B$, но $A^k \not\succeq B^k$».

---

### E13. Minkowski's determinant inequality (неравенство Минковского для определителей)

Формулировка. Для PSD-матриц $A, B \in \mathbb{C}^{n \times n}$:
$$\det(A + B)^{1/n} \ge \det(A)^{1/n} + \det(B)^{1/n}.$$
Равенство $\iff$ $A$ и $B$ пропорциональны (или одна из них $= 0$). Эквивалентная формулировка: функция $A \mapsto \det(A)^{1/n}$ — concave на конусе PSD-матриц.

Условия применимости. PSD (Hermitian с $\lambda_i \ge 0$). Для не-PSD неравенство ложно (даже знак $\det(A+B)$ может быть произвольным).

Идея доказательства. Через AM-GM на eigenvalues: при $A \succ 0$ применить unitary congruence, чтобы $A = I$, $B = D$ диагональная. Тогда LHS $= \prod (1 + d_i)^{1/n}$, RHS $= 1 + \prod d_i^{1/n}$. AM-GM на $1 + d_i = (1 - t) + t \cdot ((1 + d_i) / t)$... Корректно: положить $f(A, B) = \det(A)^{1/n} + \det(B)^{1/n}$, проверить homogeneity, свести к $\det(I + D)^{1/n} \ge 1 + \det(D)^{1/n}$, затем AM-GM.

Варианты и обобщения.
- $\log \det$ concave на PSD-конусе: $\log \det((1-t) A + tB) \ge (1-t) \log \det A + t \log \det B$ — частый log-вариант.
- Hadamard's inequality для PSD: $\det A \le \prod a_{ii}$ — следствие AM-GM или Fischer's inequality.
- Fischer: $\det \begin{pmatrix} A_{11} & A_{12} \\ A_{12}^* & A_{22} \end{pmatrix} \le \det A_{11} \det A_{22}$ для блочной PSD.
- Brunn–Minkowski для convex bodies — analytical аналог.

Используется в. [Putnam-2005-A4 (через $H H^T = nI$ — PSD конструкция и det-оценка)], типовые задачи на оценку $\det(A + B)$ снизу. Также Hadamard $\det A \le \prod a_{ii}$ — типичный rapid-trick.

---

## Записи — Exotic

### E14. Schur product theorem (теорема Шура о Hadamard-произведении)

Формулировка. Hadamard product (поэлементное) $A \circ B = (a_{ij} b_{ij})$. Если $A, B \succeq 0$ — то $A \circ B \succeq 0$ (PSD сохраняется). Если $A \succ 0$ и $B \succeq 0$ с $b_{ii} > 0$ для всех $i$ — то $A \circ B \succ 0$.

Условия применимости. Обе матрицы Hermitian PSD одинакового размера.

Идея доказательства. Записать $A = \sum_k x_k x_k^*$ (через спектральное разложение), $B = \sum_l y_l y_l^*$. Тогда $A \circ B = \sum_{k,l} (x_k \circ y_l)(x_k \circ y_l)^*$ — сумма rank-1 PSD.

Варианты и обобщения.
- Schur multiplier: оператор $M_A: B \mapsto A \circ B$ — completely positive при $A \succeq 0$.
- Bapat–Sunder inequality: $\det(A \circ B) \ge \det(A) \prod b_{ii}$ для PSD $A, B$.
- Oppenheim's inequality: $\det(A \circ B) \ge \det(B) \prod a_{ii}$ для PSD $A, B$.
- Связь с tensor product: $A \circ B$ — главная подматрица $A \otimes B$ по «диагональным» индексам.

Используется в. Задачи на матрицы вида $a_{ij} = f(i, j) g(i, j)$ — разложить как Hadamard-произведение двух PSD. [IMC-2010-5] косвенно — там степени $a^n$ через $\otimes^n$ строк, что эквивалентно $a^n_{ij} = (a_{ij})^n$ как Hadamard-степень.

---

### E15. Loewner–Heinz inequality (неравенство Лёвнера–Хайнца)

Формулировка. Если $A \succeq B \succeq 0$, то $A^t \succeq B^t$ для всех $t \in [0, 1]$. Эквивалентно: $f(t) = t^\alpha$ operator-monotone на $[0, \infty)$ при $\alpha \in [0, 1]$.

Условия применимости. PSD обе матрицы; параметр $t$ строго в $[0, 1]$. При $t > 1$ — неравенство не выполняется (см. E12.4). При $t = 1/2$ — square-root monotone, доказывается отдельно.

Идея доказательства. Через интегральное представление
$$t^\alpha = \frac{\sin(\pi \alpha)}{\pi} \int_0^\infty \frac{\lambda^{\alpha - 1} t}{\lambda + t} \, d\lambda, \quad \alpha \in (0, 1).$$
Подынтегральная функция $\lambda t / (\lambda + t) = \lambda - \lambda^2 / (\lambda + t)$ — operator-monotone (через $A \mapsto (\lambda + A)^{-1}$ anti-monotone, см. E12.2). Интегрирование сохраняет monotonicity.

Варианты и обобщения.
- Heinz inequality: $\|A^\alpha X B^{1-\alpha} + A^{1-\alpha} X B^\alpha\| \le \|AX + XB\|$ для $\alpha \in [0, 1]$.
- Furuta's inequality (1987): обобщение для $t > 1$ при дополнительных условиях.
- $\log$ operator-monotone: $A \succeq B \succ 0 \Rightarrow \log A \succeq \log B$.
- $-A^{-1}$ operator-monotone: если $A \succeq B \succ 0$ — то $-A^{-1} \succeq -B^{-1}$, т. е. $A^{-1} \preceq B^{-1}$.

Используется в. Редко на IMC, но появляется в Schweitzer / на mathematical olympiads уровня PhD entrance. Полезен в perturbation theory и в построении контрпримеров «$A^2 \not\succeq B^2$, но $\sqrt{A} \succeq \sqrt{B}$».

---

### E16. Operator geometric mean (геометрическое среднее матриц): $A \# B$ и Ando's inequality

Формулировка. Для $A, B \succ 0$ определяется
$$A \# B = A^{1/2} (A^{-1/2} B A^{-1/2})^{1/2} A^{1/2}.$$
Свойства: $A \# B = B \# A$, $(A \# B)^{-1} = A^{-1} \# B^{-1}$, monotone в обоих аргументах (Loewner). $A \# B$ — единственное PSD решение Riccati-уравнения $X A^{-1} X = B$. Ando: для PSD блочной $\begin{pmatrix} A & X \\ X^* & B \end{pmatrix} \succeq 0 \iff X = A^{1/2} K B^{1/2}$ для некоторой $K$ с $\|K\| \le 1$, и $X = A \# B$ при $K = (A^{-1/2}BA^{-1/2} + ...)^{-1/2} ...$ (или эквивалентно — максимальный $X$ Hermitian с этим свойством).

Условия применимости. PD (для определения через $A^{-1/2}$). PSD-версия — через предельный переход.

Идея доказательства. Существование корня — через E5. Симметричность $A \# B = B \# A$ — нетривиальна, проверяется через явную формулу или через Riccati-характеризацию.

Варианты и обобщения.
- AM-GM-HM для матриц: $(A^{-1} \# B^{-1})^{-1} = (A^{-1} + B^{-1})^{-1} / 2 \cdot 2$ — гармоническое среднее, которое $\preceq A \# B \preceq (A + B)/2$.
- Kubo–Ando theory: общая теория operator means, связь с operator-monotone functions через Loewner's theorem.
- $\log A + \log B \preceq 2 \log(A \# B)$ — log-AM-GM.

Используется в. Очень редко на IMC. Скорее как культурный фон для понимания, что operator geometric mean — нетривиальная конструкция. Появляется в Schweitzer-подобных задачах и в quantum information theory.

---

## Self-test

1. Пусть $A \in M_n(\mathbb{R})$ symmetric, $A^3 = A$. Опиши все возможные собственные числа $A$ и докажи, что $A^2$ — ортогональная проекция.

2. Пусть $A, B \in M_n(\mathbb{R})$ symmetric и $A B + B A \succeq 0$. Следует ли $A B \succeq 0$? Контрпример или доказательство.

3. Пусть $A \in M_n(\mathbb{C})$ — любая матрица. Покажи, что
$$\sum_{i,j} |a_{ij}|^2 = \sum_i \sigma_i(A)^2.$$

4. Пусть $A, B \succeq 0$ из $M_n(\mathbb{R})$. Докажи $\operatorname{tr}(A B) \ge 0$, и $\operatorname{tr}(A B) = 0 \iff A B = 0$.

5. Дано $A \succeq 0$ из $M_n(\mathbb{R})$ с $a_{ii} = 1$ для всех $i$. Докажи, что $|a_{ij}| \le 1$ и $\det A \le 1$.

6. Пусть $H \in M_n(\mathbb{R})$ — Hadamard matrix ($h_{ij} = \pm 1$, $H H^T = n I$). Найди $|\det H|$.

7. Пусть $A$ — $n \times n$ real symmetric с $\operatorname{tr}(A) = 0$ и $\operatorname{tr}(A^2) = n$. Докажи, что $\max(\lambda_{\max}(A), -\lambda_{\min}(A)) \ge 1$, и приведи пример равенства.

8. Пусть $A, B \succ 0$ из $M_n(\mathbb{R})$. Докажи: $\det(A + B) \ge \det A + \det B$, причём при $n \ge 2$ строго, если $A, B$ непропорциональны.

9. Пусть $u_1, \dots, u_k \in \mathbb{R}^n$ — единичные с $\langle u_i, u_j \rangle = c$ для $i \ne j$. Найди ограничения на $c$ и $k$.

10. Дано $A \in M_n(\mathbb{R})$, $\det A \neq 0$. Покажи, что $A = U P$, где $U$ ортогональная и $P$ symmetric PD, единственным образом.

---

## Решения

1. $A$ symmetric ⇒ диагонализуется, $\lambda^3 = \lambda$, $\lambda \in \{0, 1, -1\}$. $A^2$ symmetric с собственными числами $\lambda^2 \in \{0, 1\}$ ⇒ $A^2 = A^4$, $(A^2)^* = A^2$ ⇒ ортогональная проекция на $\ker(A)^\perp$.

2. Не следует. Контрпример: $A = \begin{pmatrix} 1 & 0 \\ 0 & -1 \end{pmatrix}$, $B = \begin{pmatrix} 0 & 1 \\ 1 & 0 \end{pmatrix}$. Тогда $AB + BA = 0 \succeq 0$, но $AB = \begin{pmatrix} 0 & 1 \\ -1 & 0 \end{pmatrix}$ — даже не Hermitian, поэтому $AB \succeq 0$ не имеет смысла в Loewner-смысле. Симметризованная версия (с PSD-условием на оба $A, B$ + дополнительной коммутативностью) — нужна для тривиальности.

3. $\sum_{ij} |a_{ij}|^2 = \operatorname{tr}(A^* A) = \sum_i \lambda_i(A^* A) = \sum_i \sigma_i(A)^2$. Это — Frobenius norm squared.

4. $A = X^2$, $B = Y^2$ через E5 ($X = A^{1/2}$, аналогично $Y$). Тогда $\operatorname{tr}(AB) = \operatorname{tr}(X^2 Y^2) = \operatorname{tr}(YX \cdot XY) = \operatorname{tr}((XY)^* (XY)) = \|XY\|_F^2 \ge 0$. Равенство $\iff XY = 0 \iff AB = X X Y Y = X (XY) Y = 0$.

5. Главный $2 \times 2$ минор $\begin{pmatrix} 1 & a_{ij} \\ a_{ij} & 1 \end{pmatrix} \succeq 0$ ⇒ $\det = 1 - a_{ij}^2 \ge 0$ ⇒ $|a_{ij}| \le 1$. $\det A \le 1$ — Hadamard для PSD: $\det A \le \prod a_{ii} = 1$ (E13 / E12).

6. $H H^T = nI$, $\det(H H^T) = n^n$, $|\det H|^2 = n^n$, $|\det H| = n^{n/2}$. Это — экстремум Hadamard'a, equality на ортогональных строках.

7. Положим $M = \lambda_{\max}, m = \lambda_{\min}$, $K = \max(M, -m) = \max(M, |m|)$ (одно из них $\ge 0$, другое $\le 0$ при $\operatorname{tr} = 0$, $A \ne 0$). Тогда $\lambda_i^2 \le K^2$ для всех $i$, значит $n = \sum \lambda_i^2 \le n K^2$, откуда $K \ge 1$. Равенство — на $A = \operatorname{diag}(1, -1, 0, \dots, 0)$ при $n = 2$, или на любой $A$ с собственными числами в $\{-1, 0, 1\}$ и balanced суммой (например, при чётном $n$: $n/2$ единиц и $n/2$ минус-единиц).

8. Через Minkowski (E13): $\det(A+B)^{1/n} \ge \det(A)^{1/n} + \det(B)^{1/n}$. Возведение в $n$-ю степень и AM-GM-style раскрытие $(x + y)^n \ge x^n + y^n$ при $x, y \ge 0$ даёт требуемое. Строгость при непропорциональных — из equality case Minkowski.

9. Gram matrix $G_{ij} = c$ при $i \ne j$, $G_{ii} = 1$. $G = (1 - c) I + c \mathbf{1} \mathbf{1}^T$. Eigenvalues: $1 + (k-1)c$ (на $\mathbf{1}$), $1 - c$ (кратность $k-1$). $G \succeq 0 \iff c \ge -1/(k-1)$ и $c \le 1$. Значит $c \in [-1/(k-1), 1]$.

10. $P = (A^T A)^{1/2} \succ 0$ (E5), $U = A P^{-1}$. Проверка $U^T U = P^{-1} A^T A P^{-1} = P^{-1} P^2 P^{-1} = I$. Единственность: при $A = U_1 P_1 = U_2 P_2$ имеем $U_2^{-1} U_1 = P_2 P_1^{-1}$ — ортогональная и symmetric PD одновременно, значит $= I$, ⇒ $U_1 = U_2$, $P_1 = P_2$.
