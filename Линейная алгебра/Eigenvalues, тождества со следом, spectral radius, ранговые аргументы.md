---
topic: Линейная алгебра
subtopic: "Eigenvalues, тождества со следом (trace), spectral radius, ранговые аргументы"
sources:
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Horn, Johnson — Matrix Analysis"
  - "Horn, Johnson — Topics in Matrix Analysis"
  - "Bhatia — Matrix Analysis (GTM 169)"
  - "Engel — Problem-Solving Strategies"
  - "Yufei Zhao — Linear Algebra Tricks for the Putnam"
  - "Newman — A Problem Seminar"
  - "Polya, Szegő — Problems and Theorems in Analysis II"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "Robin Visser — IMC 2023 Training, Linear Algebra"
  - "Joel Tropp — An Elementary Proof of the Spectral Radius Formula"
  - "W. Kahan — Only Commutators Have Trace Zero (Math H110 notes)"
  - "Joel Shapiro — Burnside's Theorem on Matrix Algebras"
problems_referenced:
  - IMC-1994-1
  - IMC-1994-4
  - IMC-1997-DAY2-4
  - IMC-1998-1
  - IMC-1998-DAY2-1
  - IMC-2001-DAY2-4
  - IMC-2005-1
  - IMC-2007-2
  - IMC-2009-DAY2-3
  - IMC-2009-DAY2-5
  - IMC-2011-2
  - IMC-2012-2
  - IMC-2017-1
  - IMC-2020-2
  - IMC-2025-3
  - Putnam-1991-A6
  - Putnam-2005-A4
last_updated: 2026-04-27
---

# Eigenvalues, тождества со следом (trace), spectral radius, ранговые аргументы

## Scope
Спектральные и ранговые техники для $n\times n$ матриц над $\mathbb{R}$, $\mathbb{C}$ и произвольным полем. Trace как линейный функционал и как сумма eigenvalues, цикличность и инварианты следа от слов в матрицах. Связь spectrum / characteristic polynomial / minimal polynomial / annihilating polynomial; Cayley–Hamilton и spectral mapping. Spectrum продукта $AB$ vs $BA$. Newton identities и критерий nilpotent через $\operatorname{tr}(A^k)$. Spectral radius и Gelfand. Rank через миноры, через ker/im, rank-1 декомпозиции, Sylvester / Frobenius rank inequalities. Идемпотенты и идентичность $\operatorname{rank} = \operatorname{tr}$. Polynomial annihilator → ограничения на спектр. Schur triangularization + одновременная триангуляризация. Hermitian / симметричные: Rayleigh, Courant–Fischer, Cauchy interlacing. Экзотика — Shoda, Burnside, Jordan-структура.

## Записи — Core

### E1. Trace properties (свойства следа): cyclic invariance, $\operatorname{tr} = \sum \lambda_i$, инвариантность

Формулировка. Для $A,B,C$ согласованных размеров:
$$\operatorname{tr}(AB) = \operatorname{tr}(BA), \qquad \operatorname{tr}(ABC) = \operatorname{tr}(BCA) = \operatorname{tr}(CAB).$$
Trace — единственный (с точностью до константы) линейный функционал на $M_n(F)$ с $f(AB) = f(BA)$. Для $A\in M_n(\mathbb{C})$: $\operatorname{tr}(A) = \sum_{i=1}^n \lambda_i(A)$, $\operatorname{tr}(A^k) = \sum \lambda_i^k$ (с учётом алгебраической кратности). Trace инвариантен при сопряжении $A \mapsto S^{-1}AS$.

Условия применимости. Любое поле для алгебраической части. Для $\sum \lambda_i^k$ — поле, в котором характеристический многочлен раскладывается (или работаем в алгебраическом замыкании).

Идея доказательства. Cyclic invariance — прямой подсчёт: $\operatorname{tr}(AB) = \sum_i (AB)_{ii} = \sum_{i,j} A_{ij}B_{ji} = \operatorname{tr}(BA)$. Уникальность: пространство $\{f: f(AB) = f(BA)\}$ — это annihilator коммутаторов, а commutators порождают $\{X: \operatorname{tr}(X) = 0\}$ (Shoda, см. E13).

Варианты и обобщения.
- $\operatorname{tr}(AB) = 0$ для всех $B$ $\iff A = 0$ — невырожденность билинейной формы $(A,B) \mapsto \operatorname{tr}(AB)$.
- Для PSD матриц $A,B$: $\operatorname{tr}(AB) \ge 0$ и $\operatorname{tr}(AB) = 0 \iff AB = 0$.
- Frobenius inner product $\langle A, B \rangle_F = \operatorname{tr}(A^*B)$.

Используется в. [IMC-1997-DAY2-4 (характеризация trace через $f(AB)=f(BA)$)], [IMC-2009-DAY2-3 (вычисление $\operatorname{tr}(AX^k B - X^k BA) = 0$)], [IMC-2020-2 ($\operatorname{tr}(AB-BA) = 0$ + развёртка $\operatorname{tr}(ABAB)$)]. Базовая «арифметика следа» используется почти в каждой задаче этого блока.

---

### E2. Spectrum продукта: $AB$ и $BA$ совпадают на ненулевой части

Формулировка. Для $A$ размера $m \times n$, $B$ размера $n \times m$ ($m \le n$):
$$\det(\lambda I_n - BA) = \lambda^{n-m}\det(\lambda I_m - AB).$$
Эквивалентно: $\operatorname{spec}(AB) \setminus \{0\} = \operatorname{spec}(BA) \setminus \{0\}$ как мультимножества (с алгебраической кратностью). Для квадратных $A,B$ ($m=n$): $\det(\lambda I - AB) = \det(\lambda I - BA)$, то есть характеристические многочлены $AB$ и $BA$ совпадают полностью.

Условия применимости. Любое поле. При $m = n$ кратности нуля тоже совпадают. При $m \ne n$ — кратности нуля отличаются на $|m - n|$.

Идея доказательства. (a) При $A$ invertible: $BA = A^{-1}(AB)A$, значит подобны. Общий случай — плотность invertible матриц + непрерывность характеристического многочлена. (b) Блочная: $\det(\lambda I - AB)\lambda^n = \det\begin{pmatrix}\lambda I_m & A \\ B & I_n\end{pmatrix}\cdot \lambda = \det(\lambda I - BA)\lambda^m$ через два разложения по Schur complement.

Варианты и обобщения.
- $\operatorname{tr}((AB)^k) = \operatorname{tr}((BA)^k)$ для всех $k \ge 1$ — следствие либо cyclic invariance, либо spectral версии.
- Sylvester $\det(I + AB) = \det(I + BA)$ — частный случай при $\lambda = -1$.
- Жорданова структура $AB$ и $BA$ совпадает в части ненулевых eigenvalues; для нулевого eigenvalue блоки могут отличаться (Flanders' theorem: размеры жордановых блоков для $\lambda = 0$ отличаются не более чем на 1).

Используется в. [IMC-1994-4 (spectrum оператора $L_F$)], стандартный приём «уменьшить размер»: rank-low возмущение $A + UV^T$ с $U, V \in M_{n,k}$ — спектр сдвигается только в $k$ ненулевых eigenvalues. См. также Определители E4.

---

### E3. Cayley–Hamilton (теорема Кэли–Гамильтона) + Spectral mapping

Формулировка. Пусть $\chi_A(\lambda) = \det(\lambda I - A) = \lambda^n - c_1 \lambda^{n-1} + \dots + (-1)^n c_n$. Тогда $\chi_A(A) = 0$. Минимальный многочлен $\mu_A(x)$ делит $\chi_A(x)$, имеет те же корни (с возможно меньшими кратностями).

Spectral mapping: для $p \in F[x]$ имеем $\operatorname{spec}(p(A)) = \{p(\lambda): \lambda \in \operatorname{spec}(A)\}$ (с учётом алгебраической кратности). Для invertible $A$: $\operatorname{spec}(A^{-1}) = \{1/\lambda: \lambda \in \operatorname{spec}(A)\}$, значит $A^{-1}$ — многочлен от $A$ степени $\le n-1$ (через Cayley–Hamilton).

Условия применимости. Любое коммутативное кольцо для Cayley–Hamilton. Spectral mapping — любое поле, eigenvalues берутся в алгебраическом замыкании.

Идея доказательства. Cayley–Hamilton: $\det(\lambda I - A)\cdot I = (\lambda I - A)\cdot \operatorname{adj}(\lambda I - A)$ как тождество многочленов от $\lambda$ с матричными коэффициентами; подставить $\lambda = A$ через formal substitution (нужна аккуратность с некоммутативностью). Spectral mapping — Schur triangularization (E9): $A = U T U^*$ с $T$ upper triangular, $p(A) = U p(T) U^*$, $p(T)$ тоже upper triangular с диагональю $p(\lambda_i)$.

Варианты и обобщения.
- $\operatorname{tr}(A^k)$ для $k = 1, \dots, n$ через Newton identities (E4) полностью определяют $\chi_A$ в характеристике $0$.
- $A^n = c_1 A^{n-1} - c_2 A^{n-2} + \dots$: высокие степени выражаются через $I, A, \dots, A^{n-1}$.
- $\det(A) = (-1)^n \chi_A(0)$, и $\chi_A(0) = \det(-A) = (-1)^n\prod \lambda_i$.

Используется в. [IMC-2011-2 (из $A^2 + A^T = I$ выводим $A^4 - 2A^2 + A = 0$ ⇒ ограничение спектра)], [IMC-2017-1 ($A^2 = A^T \Rightarrow A^4 = A$, $\lambda^4 = \lambda$)], типовая редукция при «$A$ удовлетворяет полиномиальному соотношению».

---

### E4. Newton's identities + критерий nilpotent через $\operatorname{tr}(A^k) = 0$

Формулировка. Пусть $p_k = \sum \lambda_i^k = \operatorname{tr}(A^k)$, $e_k = $ $k$-й elementary symmetric polynomial от $\lambda_i$ ($e_k = $ коэффициент при $\lambda^{n-k}$ в $\chi_A$ с точностью до знака). Newton identities:
$$p_k - e_1 p_{k-1} + e_2 p_{k-2} - \dots + (-1)^{k-1} k e_k = 0, \quad k = 1, \dots, n.$$
В характеристике $0$: $p_1, \dots, p_n$ однозначно определяют $e_1, \dots, e_n$, значит и $\chi_A$.

Критерий nilpotent. Над полем характеристики $0$: $A$ nilpotent $\iff \operatorname{tr}(A^k) = 0$ для всех $k = 1, \dots, n$ $\iff \operatorname{tr}(A^k) = 0$ для всех $k \ge 1$.

Условия применимости. Newton identities — любое коммутативное кольцо. Критерий nilpotent — характеристика $0$ (или $> n$); в положительной характеристике контрпримеры (matrix permutation от $p$-цикла в $\mathbb{F}_p$).

Идея доказательства. Newton — раскладка $\sum \log(1 - \lambda_i x) = -\sum_k p_k x^k / k$ и сравнение с $\log\det(I - xA)$. Nilpotent: если все $p_k = 0$, то по Newton все $e_k = 0$ ⇒ $\chi_A(\lambda) = \lambda^n$ ⇒ Cayley–Hamilton даёт $A^n = 0$.

Варианты и обобщения.
- Эквивалентно: $A$ nilpotent $\iff$ все eigenvalues $= 0$ $\iff \chi_A(\lambda) = \lambda^n$.
- $\operatorname{tr}(A^k)$ полностью определяют algebraic similarity invariants $A$ при characteristic $0$ через characteristic polynomial; не определяют Jordan structure.
- Specht's theorem: $A$ unitarily similar to $B$ $\iff \operatorname{tr}(w(A,A^*)) = \operatorname{tr}(w(B,B^*))$ для всех слов $w$. Чисто следовая характеризация unitary similarity.

Используется в. [IMC-2009-DAY2-3 (показать $X = AB - BA$ nilpotent через $\operatorname{tr}(X^k) = 0$)], классические задачи «$\operatorname{tr}(A^k) = $ const $\Rightarrow A$ — конкретный тип». Putnam-1991-A6 (структура матрицы через trace tables).

---

### E5. Rank: основные характеризации, миноры, rank-1 декомпозиции

Формулировка. Для $A \in M_{m,n}(F)$ эквивалентны:
1. $\operatorname{rank}(A) = r$.
2. Максимальный размер ненулевого минора $A$ равен $r$ (то есть $\exists$ невырожденный $r \times r$ минор, и все $(r+1) \times (r+1)$ миноры $= 0$).
3. $A = \sum_{k=1}^r u_k v_k^T$ — разложение в сумму $r$ матриц ранга $1$, и $r$ — минимально возможное.
4. $\dim \operatorname{im}(A) = r$ $\iff \dim \ker(A) = n - r$.
5. $A = LR$, где $L \in M_{m,r}$, $R \in M_{r,n}$, обе ранга $r$ (full-rank factorization).

В частности, $\operatorname{rank}(A) \le 1 \iff A = uv^T$ для некоторых $u, v$ $\iff$ все $2 \times 2$ миноры зануляются.

Условия применимости. Любое поле.

Идея доказательства. Эквивалентность через Gauss elimination. Минор-критерий: $r$-й столбец характеристического разложения по строкам / столбцам; если все $(r+1)$-миноры нулевые, любая комбинация $r+1$ строк / столбцов линейно зависима.

Варианты и обобщения.
- $\operatorname{rank}(A + B) \le \operatorname{rank}(A) + \operatorname{rank}(B)$ (subadditivity).
- $|\operatorname{rank}(A) - \operatorname{rank}(B)| \le \operatorname{rank}(A - B)$.
- Rank stable под малым возмущением сверху: если $\operatorname{rank}(A) = r$, то для $\|E\|$ малой $\operatorname{rank}(A + E) \ge r$ (полу-непрерывность снизу).
- $\operatorname{tr}(uv^T) = v^T u$, $(uv^T)^2 = (v^T u) uv^T$, eigenvalues: $v^T u$ и $0$ ($n-1$ раз).

Используется в. [IMC-1994-1 (≥2 ненулевых на столбец $A^{-1}$)], [IMC-2005-1 ($A_{ij} = i + j$ — сумма двух rank-1)], [IMC-2007-2 (минимальный ранг через 2×2 миноры)], [IMC-2012-2 (минимальный ранг = 3 через 3×3 миноры)], [IMC-2025-3 (rank-1 ±1 матрицы и условие коммутации)].

---

### E6. Sylvester rank inequality + Frobenius rank inequality

Формулировка. Для матриц $A \in M_{m,n}$, $B \in M_{n,p}$:
$$\operatorname{rank}(A) + \operatorname{rank}(B) - n \le \operatorname{rank}(AB) \le \min(\operatorname{rank}(A), \operatorname{rank}(B)).$$
Левая — Sylvester rank inequality (неравенство Сильвестра).

Frobenius rank inequality. Для $A \in M_{m,n}$, $B \in M_{n,p}$, $C \in M_{p,q}$:
$$\operatorname{rank}(AB) + \operatorname{rank}(BC) \le \operatorname{rank}(B) + \operatorname{rank}(ABC).$$
При $B = I_n$ возвращается Sylvester.

Условия применимости. Любое поле, любые согласованные размеры.

Идея доказательства. Sylvester: $\operatorname{rank}(AB) = \dim A(\operatorname{im} B) = \dim \operatorname{im} B - \dim(\operatorname{im} B \cap \ker A) \ge \operatorname{rank} B - \dim \ker A = \operatorname{rank} B - (n - \operatorname{rank} A)$. Frobenius: применить Sylvester к ограничению $A$ на $\operatorname{im}(BC) \subseteq \operatorname{im}(B)$ + dim count.

Варианты и обобщения.
- $\operatorname{rank}(A^k) - \operatorname{rank}(A^{k+1})$ не возрастает по $k$ (последовательность $\operatorname{rank}(A^k)$ выпукла); это даёт верхнюю оценку числа жордановых блоков.
- Stable rank: $\operatorname{rank}(A^k) = \operatorname{rank}(A^{k+1}) \Rightarrow$ постоянна для всех $j \ge k$. Минимальное такое $k$ — индекс $A$ (длина самого длинного жорданова блока для $\lambda = 0$).
- Идемпотент / проектор: $\operatorname{rank}(P) + \operatorname{rank}(I - P) = n$ при $P^2 = P$.

Используется в. [IMC-1998-1 (dim $E$ через блочные ранги $3+6+10$)], [IMC-2009-DAY2-5 (iterated rank reduction и оценка размера covering)], типовые задачи «$AB = 0$, оценить $\operatorname{rank}(A) + \operatorname{rank}(B) \le n$».

---

## Записи — Standard

### E7. Idempotent (идемпотент / проектор): $A^2 = A$ ⇒ $\operatorname{rank}(A) = \operatorname{tr}(A)$ + диагонализуемость

Формулировка. Если $A^2 = A$, то:
1. $A$ диагонализуема, $\operatorname{spec}(A) \subseteq \{0, 1\}$, $F^n = \ker A \oplus \operatorname{im} A$.
2. $\operatorname{rank}(A) = \operatorname{tr}(A)$ — оба равны числу единичных eigenvalues.
3. $I - A$ — тоже идемпотент с $\operatorname{rank}(I - A) = n - \operatorname{rank}(A)$.

Обобщение для $A^2 = cA$ ($c \ne 0$): $A/c$ идемпотент, $\operatorname{rank}(A) = \operatorname{tr}(A)/c$.

Условия применимости. Поле характеристики $\ne 2$ для красоты (на $\mathbb{F}_2$ всё работает, но trace может стать нулём по модулю 2). Для $A^k = A$ ($k \ge 2$): спектр $\subseteq$ корней $\lambda^k = \lambda$, диагонализуемость над алгебраическим замыканием.

Идея доказательства. Минимальный многочлен делит $x^2 - x = x(x-1)$, без кратных корней ⇒ диагонализуемость. Trace = sum eigenvalues = (число $1$-eigenvalues) = $\dim \operatorname{im}(A) = \operatorname{rank}(A)$.

Варианты и обобщения.
- Сумма проекторов $P_1 + \dots + P_k = I$ — разложение $F^n$ в прямую сумму $\bigoplus \operatorname{im}(P_i)$, $P_i P_j = \delta_{ij} P_i$ автоматически если $P_i$ ortho.
- Для $A^3 = A$: $\operatorname{spec} \subseteq \{0, \pm 1\}$, $A$ диагонализуема, и $\operatorname{rank}(A) = \operatorname{rank}(A^2)$.
- $A^k = I$ для какого-то $k \ge 1$: $A$ диагонализуема над $\mathbb{C}$ (если $\operatorname{char}(F) \nmid k$).

Используется в. [IMC-2017-1 ($A^2 = A^T$)], [IMC-2011-2 ($A^2 + A^T = I$)], классические Putnam-style «найти $\operatorname{rank}(A)$, если $A$ удовлетворяет $p(A) = 0$ с известным $p$».

---

### E8. Polynomial annihilator → ограничения на спектр и структуру

Формулировка. Если $p(A) = 0$ для $p \in F[x]$, то $\mu_A(x) \mid p(x)$, в частности $\operatorname{spec}(A) \subseteq \{$корни $p\}$. $A$ диагонализуема $\iff \mu_A$ имеет только простые корни (в алгебраическом замыкании).

Trace constraint. Если $\operatorname{spec}(A) \subseteq \{r_1, \dots, r_s\}$ с алгебраическими кратностями $m_1, \dots, m_s$, то $\sum m_i = n$ и
$$\operatorname{tr}(A^k) = \sum_{i=1}^s m_i r_i^k \quad \text{для всех } k \ge 0.$$
Эта система линейных уравнений на $m_i$ часто переопределена и даёт противоречие в задачах типа «не существует такой матрицы».

Условия применимости. Любое поле. Для diagonalizability — нужна простота корней (в характеристике $p$ кратные корни — настоящая преграда).

Идея доказательства. $p(A) = 0 \Rightarrow \mu_A | p$. Spec идёт по корням $\mu_A$. Trace constraint — сумма по жордановым блокам с учётом кратностей.

Варианты и обобщения.
- $A^2 = -I$ над $\mathbb{R}$ ⇒ $n$ чётно, $\operatorname{spec}(A) = \{\pm i\}$ с равными кратностями, $\operatorname{tr}(A) = 0$.
- $A^2 = I$, $A \ne \pm I$ ⇒ $A$ — non-trivial reflection, $\operatorname{rank}(A - I) + \operatorname{rank}(A + I) = n$, $\operatorname{tr}(A) = \operatorname{rank}(A+I) - \operatorname{rank}(A-I)$ через E7.
- Bounded eigenvalues: $\|A^k\|$ bounded по $k$ $\iff |\lambda| \le 1$ для всех $\lambda$ и $|\lambda| = 1$ — простой корень $\mu_A$.

Используется в. [IMC-2011-2 ($A^4 - 2A^2 + A = 0$ + trace)], [IMC-2017-1 ($\lambda^4 = \lambda$)]. Стандарт для задач «дано полиномиальное уравнение, найти возможные $A$ или $\operatorname{tr}(A)$».

---

### E9. Schur triangularization (теорема Шура) + одновременная триангуляризация

Формулировка. Schur: для любой $A \in M_n(\mathbb{C})$ существует unitary $U$ такая, что $U^*AU = T$ — upper triangular с диагональю из eigenvalues $A$. Над $\mathbb{R}$ — quasi-triangular с $1\times 1$ и $2\times 2$ блоками (real Schur).

Simultaneous triangularization. Семейство $\mathcal{F} \subset M_n(\mathbb{C})$ одновременно триангуляризуется (одной unitary $U$) $\iff$ $\mathcal{F}$ имеет общий собственный вектор и условие наследуется на factor space. Достаточные условия:
- $\mathcal{F}$ коммутирующее (все пары $[A,B] = 0$).
- McCoy's theorem: $\mathcal{F}$ одновременно триангуляризуема $\iff$ $p(A,B)\cdot[A,B]$ nilpotent для всех $A,B \in \mathcal{F}$ и всех некоммутативных полиномов $p$.

Условия применимости. Schur — алгебраически замкнутое поле (для треугольной формы с eigenvalues на диагонали). Реальная версия — $\mathbb{R}$ через $2\times 2$ блоки.

Идея доказательства. Schur: индукция по $n$. Возьмём eigenvector $v_1$, продолжим до ortho базиса; $A$ в этом базисе блочно-треугольная, рекурсия на $(n-1)\times(n-1)$ блок. Simultaneous (комм. случай): общий eigenvector коммутирующих операторов через инвариантность eigenspace.

Варианты и обобщения.
- Spectral theorem (E13): для нормальных $A$ ($AA^* = A^*A$) Schur даёт diagonal $T$, то есть unitary diagonalization.
- Для коммутирующих normal — одновременная unitary diagonalization.
- Lie–Kolchin: разрешимая группа матриц — одновременно триангуляризуема (над алгебраически замкнутым полем).

Используется в. Стандартный приём «привести к треугольному виду» для подсчёта $\operatorname{tr}(p(A))$, $\det(p(A))$, и для доказательства spectral mapping (E3). На IMC реже как явный шаг, но как backbone — везде.

---

### E10. Spectral radius (спектральный радиус) и Gelfand formula

Формулировка. $\rho(A) = \max\{|\lambda|: \lambda \in \operatorname{spec}(A)\}$. Gelfand formula: для любой матричной нормы $\|\cdot\|$
$$\rho(A) = \lim_{k \to \infty} \|A^k\|^{1/k} = \inf_{k \ge 1} \|A^k\|^{1/k}.$$
Эквивалентно: $A^k \to 0$ ($k \to \infty$) $\iff \rho(A) < 1$.

Условия применимости. $A \in M_n(\mathbb{C})$. На $\mathbb{R}$ работает с тем же определением (eigenvalues берутся в $\mathbb{C}$).

Идея доказательства. $\le$: для submultiplicative нормы $\|A^k\| \ge \rho(A)^k$ (eigenvector). $\ge$: Schur triangularization (E9) $A = UTU^*$, оценить $\|T^k\|$ через eigenvalues + nilpotent часть, последняя растёт полиномиально. Альтернатива (Tropp): $A/(\rho + \varepsilon)$ имеет $\rho < 1$, по resolvent series $(I - z A)^{-1}$ сходится для $|z| < 1/\rho$, отсюда $\|A^k\| \le C(\rho + \varepsilon)^k$.

Варианты и обобщения.
- $\rho(AB) = \rho(BA)$ — следствие E2 (характеристические многочлены совпадают).
- $\rho(A + B) \le \rho(A) + \rho(B)$ ложно в общем; верно для коммутирующих $A,B$.
- Для PSD $A$: $\rho(A) = \|A\|_2$ (operator norm). Для нормальных $A$: $\rho(A) = \|A\|_2$.
- Joint spectral radius для семейств — обобщение.

Используется в. Задачи «$A^n \to 0$» / «$\sum A^k$ сходится» / оценки степеней матриц. На Putnam регулярно ($A^n \to A^\infty$ и т.п.). Связан с Markov chains через $\rho \le 1$ и Perron–Frobenius.

---

### E11. Real matrices: комплексные eigenvalues идут парами + signs $\det$ и $\operatorname{tr}$

Формулировка. $A \in M_n(\mathbb{R})$. Если $\lambda \in \mathbb{C} \setminus \mathbb{R}$ — eigenvalue с алгебраической кратностью $m$, то $\bar\lambda$ тоже eigenvalue с той же кратностью $m$. Следствие: число невещественных eigenvalues с учётом кратности — чётное.

Если $n$ нечётно ⇒ $A$ имеет хотя бы одно вещественное eigenvalue. $\det(A) = \prod \lambda_i \in \mathbb{R}$, $\operatorname{tr}(A) \in \mathbb{R}$ автоматически. $\det(A) > 0 \iff$ число отрицательных вещественных eigenvalues + $0$ среди невещественных — чётное.

Условия применимости. $A \in M_n(\mathbb{R})$.

Идея доказательства. $\chi_A \in \mathbb{R}[x]$, его комплексные корни идут сопряжёнными парами.

Варианты и обобщения.
- Для $A \in M_n(\mathbb{R})$ skew-symmetric ($A^T = -A$): eigenvalues чисто мнимые $\pm i\mu_k$, $\det = \prod \mu_k^2 \ge 0$ (Pfaffian квадрат).
- Symmetric $A^T = A$ — все eigenvalues real (E13).
- Signature $(p, q, r)$ — число положительных, отрицательных, нулевых eigenvalues; инвариантно под congruence (Sylvester's law of inertia).

Используется в. [IMC-2017-1 (real $A$ с $\lambda^4 = \lambda$ ⇒ только real eigenvalues $0, 1$ + comp. parties)], [IMC-2011-2 (несовместимость trace constraint с парностью невещественных eigenvalues)]. Часто выручает в «не существует такой $A$»-задачах.

---

### E12. Hermitian / симметричные матрицы: real spectrum, Rayleigh, Courant–Fischer, Cauchy interlacing

Формулировка. $A = A^*$ ($A \in M_n(\mathbb{C})$, hermitian, или $A \in M_n(\mathbb{R})$ symmetric). Тогда:
1. Все eigenvalues вещественны, $A$ unitarily diagonalizable.
2. Rayleigh quotient: $\lambda_1 \le \frac{x^* A x}{x^* x} \le \lambda_n$ для $x \ne 0$ (eigenvalues по возрастанию). Достигаются на eigenvectors.
3. Courant–Fischer min-max:
$$\lambda_k = \min_{\dim V = n-k+1} \max_{x \in V \setminus 0} \frac{x^*Ax}{x^*x} = \max_{\dim V = k} \min_{x \in V \setminus 0} \frac{x^*Ax}{x^*x}.$$
4. Cauchy interlacing: для главного минора $B$ размера $(n-1)\times(n-1)$ с eigenvalues $\mu_1 \le \dots \le \mu_{n-1}$:
$$\lambda_1 \le \mu_1 \le \lambda_2 \le \mu_2 \le \dots \le \mu_{n-1} \le \lambda_n.$$

Условия применимости. Hermitian / symmetric. Для $4$ — главный минор $B = A_{S,S}$ для $S \subset [n]$, $|S| = n - 1$.

Идея доказательства. (1) $\lambda \langle v, v \rangle = \langle Av, v \rangle = \langle v, Av\rangle = \bar\lambda \langle v, v\rangle$ ⇒ $\lambda \in \mathbb{R}$. Schur + норм-ть. (2,3) Compactness $\{x: \|x\| = 1\}$ + Lagrange multipliers. (4) Min-max применить к ограничению $A$ на $\mathbb{C}^{n-1} \subset \mathbb{C}^n$.

Варианты и обобщения.
- Weyl's inequalities: $\lambda_k(A) + \lambda_1(B) \le \lambda_k(A + B) \le \lambda_k(A) + \lambda_n(B)$ для hermitian $A, B$.
- Schur–Horn: диагональ hermitian $A$ majorized eigenvalues $A$.
- PSD criterion: $A \succeq 0 \iff \lambda_i \ge 0 \forall i \iff x^*Ax \ge 0 \forall x \iff $ все главные миноры $\ge 0$ (Sylvester).
- Cauchy interlacing для $k$-уровневой подматрицы — interlace степени $k$.

Используется в. Задачи на оценки eigenvalues, экстремальные значения квадратичных форм, оценки $\det / \operatorname{tr}$ через eigenvalues. На IMC реже как явный шаг, чаще как фон в задачах с симметричными матрицами.

---

### E13. Shoda's theorem: $\operatorname{tr}(A) = 0 \iff A = BC - CB$

Формулировка. Над полем $F$ характеристики $0$ (или произвольной, по Albert–Muckenhoupt): $A \in M_n(F)$ представима как коммутатор $A = BC - CB$ $\iff \operatorname{tr}(A) = 0$.

Условия применимости. Поле (любой характеристики). Для произвольного коммутативного кольца — неверно (контрпример Rosset–Rosset для $n = 2$ над специальным кольцом).

Идея доказательства. ($\Rightarrow$) тривиально. ($\Leftarrow$) Двух-шаговая: (a) свести $A$ к матрице с нулевой диагональю через сопряжение и сдвиг $A \mapsto A - \operatorname{tr}(A)/n \cdot I$ (но тут $\operatorname{tr} = 0$, так что ОК); (b) явно построить $B, C$. Стандартная конструкция: $B = \operatorname{diag}(1, 2, \dots, n)$, $C$ из условия $(BC - CB)_{ij} = (i - j)C_{ij}$ — система решается при нулевой диагонали $A$.

Варианты и обобщения.
- Sum of two commutators: $A = [B_1, C_1] + [B_2, C_2]$ для любого $A \in M_n$ (без условия trace).
- Rank one commutators: $A = vw^T - wv^T$ (skew rank-2 update) бывает rank-1 только в вырожденных случаях.
- В более общих алгебрах — связан с гомологиями Hochschild $HH_0$.

Используется в. Концептуальная роль: «trace — единственное препятствие для commutator-разложения». На IMC напрямую редко, но в задачах с коммутаторами часто полезен. Putnam-style: «представить $A$ с trace $0$ в нужной форме».

---

## Записи — Exotic

### E14. Burnside's theorem (теорема Бёрнсайда) о неприводимых матричных алгебрах

Формулировка. Пусть $\mathcal{A} \subseteq M_n(\mathbb{C})$ — подалгебра (с $I$). $\mathcal{A}$ действует неприводимо на $\mathbb{C}^n$ (нет нетривиального инвариантного подпространства) $\iff \mathcal{A} = M_n(\mathbb{C})$.

Эквивалентная форма: если набор матриц $\mathcal{F} \subseteq M_n(\mathbb{C})$ не имеет общего инвариантного подпространства, то линейная оболочка всех произведений элементов $\mathcal{F}$ равна $M_n(\mathbb{C})$.

Условия применимости. Алгебраически замкнутое поле (на $\mathbb{R}$ — нужны обобщения через division algebras: $M_n(\mathbb{R})$, $M_n(\mathbb{H})$ или $M_{n/2}(\mathbb{C})$ с $\mathbb{R}$-структурой).

Идея доказательства (Lomonosov-style). Если $\mathcal{A} \ne M_n$, то $\dim \mathcal{A} < n^2$, но действие на $\operatorname{End}(\mathbb{C}^n)$ не транзитивно — найдётся ненулевой $X$ с $\operatorname{tr}(X \mathcal{A}) = 0$. Тогда $\ker X$ или $\operatorname{im} X^*$ — нетривиальное инвариантное подпространство. Современный простой проф (Lomonosov, Halmos) — через rank-one операторы.

Варианты и обобщения.
- Schur's lemma: операторы, коммутирующие со всем $\mathcal{A}$ (centralizer) — скаляры, если $\mathcal{A}$ неприводима.
- Wedderburn–Artin: полупростые алгебры — суммы матричных алгебр.
- Двойной централизатор для finite groups (representation theory).

Используется в. Задачи на структуру коммутирующих семейств матриц, на классификацию подпространств матриц с заданными свойствами. На Schweitzer / IMO Shortlist-уровне иногда полезен.

---

### E15. Jordan canonical form (жорданова форма): структура nilpotent части и cyclic vectors

Формулировка. $A \in M_n(\mathbb{C})$ similar к блочно-диагональной $J = \bigoplus J_{m_i}(\lambda_i)$, где $J_m(\lambda)$ — жорданов блок размера $m$ с $\lambda$ на диагонали и $1$ на наддиагонали. Размеры блоков для каждого eigenvalue $\lambda$ определены однозначно.

Структура для $\lambda$. Число жордановых блоков для $\lambda$ = $\dim \ker(A - \lambda I)$ (геометрическая кратность). Размеры — через
$$d_k(\lambda) = \operatorname{rank}((A - \lambda I)^{k-1}) - 2\operatorname{rank}((A - \lambda I)^k) + \operatorname{rank}((A - \lambda I)^{k+1})$$
— число блоков размера ровно $k$. Длина наибольшего блока = индекс $\lambda$ (минимальное $k$ с $\ker(A-\lambda I)^k = \ker(A-\lambda I)^{k+1}$).

Cyclic matrix. $A$ cyclic (есть вектор $v$ с $\{v, Av, \dots, A^{n-1}v\}$ — базис) $\iff \mu_A = \chi_A$ $\iff$ для каждого eigenvalue ровно один жорданов блок $\iff$ centralizer $A$ имеет размерность $n$ (минимальная).

Условия применимости. Алгебраически замкнутое поле. Над $\mathbb{R}$ — real Jordan form с $2\times 2$ блоками для пар $\lambda, \bar\lambda$.

Идея доказательства. Декомпозиция $\mathbb{C}^n = \bigoplus \ker(A - \lambda_i I)^{n}$ — generalized eigenspaces. На каждом — $A - \lambda I$ nilpotent, делается choice cyclic basis (chains).

Варианты и обобщения.
- Rank sequences $\operatorname{rank}((A - \lambda)^k)$ полностью кодируют Jordan structure — это и есть E5 + E6 in extremis.
- Frobenius rational canonical form — без перехода к алгебраическому замыканию.
- Smith normal form для $\lambda I - A$ над $F[\lambda]$ — alternative encoding.

Используется в. Тонкие задачи о структуре операторов: «найти $\dim \{B: AB = BA\}$» (centralizer dim = $\sum (2k-1) m_k$ для блоков размера $m_1 \ge m_2 \ge \dots$). [IMC-1994-4 (counting eigenvalues оператора $L_F(X) = FX - XF$ через Jordan)], [IMC-1998-1 (блочная dim count)].

---

## Self-test

1. $A \in M_n(\mathbb{C})$, $\operatorname{tr}(A^k) = n$ для всех $k = 1, \dots, n$. Найди $\chi_A(\lambda)$.

2. $A, B \in M_n(\mathbb{C})$, $AB - BA = A$. Покажи, что $A$ nilpotent.

3. $A \in M_n(\mathbb{R})$, $A^3 = A + I$. Покажи, что $\det(A) > 0$.

4. $A \in M_n(\mathbb{R})$, $A$ невырожденная, все $a_{ij} \ge 0$, и $A^{-1}$ имеет все элементы $\ge 0$. Что можно сказать о структуре $A$?

5. $A \in M_n(\mathbb{C})$ удовлетворяет $A^k = I$ для какого-то $k \ge 1$. Покажи, что $|\operatorname{tr}(A)| \le n$ и равенство только при $A = \zeta I$ для корня $\zeta^k = 1$.

6. $A, B \in M_n(\mathbb{C})$ коммутируют. Покажи, что есть общий eigenvector. Покажи, что $\operatorname{spec}(A + B) \subseteq \operatorname{spec}(A) + \operatorname{spec}(B)$ как мультимножество (с учётом подходящего сопоставления).

7. $A \in M_n(\mathbb{C})$, $\operatorname{rank}(A - I) = 1$. Вырази $\det(A)$ через $\operatorname{tr}(A)$.

8. $A, B \in M_n(\mathbb{C})$, $AB = 0$. Докажи, что $\operatorname{rank}(A) + \operatorname{rank}(B) \le n$.

9. $A \in M_n(\mathbb{C})$, $A \ne 0$, $A^2 = 0$. Покажи, что $A$ similar к матрице вида $\begin{pmatrix}0 & I_r \\ 0 & 0\end{pmatrix}$, где $r = \operatorname{rank}(A)$, и $2r \le n$.

10. $A \in M_n(\mathbb{R})$ skew-symmetric ($A^T = -A$). Покажи, что $\operatorname{rank}(A)$ чётный, а $\det(A) \ge 0$.

## Решения

1. Newton identities (E4) от $p_k = \operatorname{tr}(A^k)$ к $e_k$: $p_1 = n$, $p_2 = n$, $p_3 = n$, ... Известно, что у конфигурации $\lambda_1 = \dots = \lambda_n = 1$ имеем $p_k = n$ для всех $k$. Решение Newton recurrence уникально, значит $e_k = \binom{n}{k}$, то есть $\chi_A(\lambda) = (\lambda - 1)^n$. Замечание: это не значит $A = I$ — например, $A = I + N$ с $N$ nilpotent даёт тот же характеристический многочлен.

2. $X = A$, имеем $AB - BA = A$, значит $\operatorname{ad}_B(A) = -A$ (с точностью до знака). По индукции $\operatorname{ad}_B(A^m) = -m A^m$ ⇒ $A^m B - B A^m = m A^m$. Trace: $0 = \operatorname{tr}(A^m B - B A^m) = m \operatorname{tr}(A^m)$. Значит $\operatorname{tr}(A^m) = 0$ для всех $m \ge 1$. По E4 $A$ nilpotent. (Шаблон IMC-2009-DAY2-3.)

3. $A^3 - A - I = 0$, корни $p(x) = x^3 - x - 1$: один real $\alpha \approx 1.3247$ и пара комплексно сопряжённых $\beta, \bar\beta$ с $|\beta|^2 = 1/\alpha$ (произведение корней $= 1$, по теореме Виета $\alpha \cdot |\beta|^2 = 1$). $\det(A) = \prod \lambda_i = \alpha^a (\beta \bar\beta)^b = \alpha^{a - b}$, где $a + 2b = n$, $a, b \ge 0$ — алгебраические кратности. Поскольку $\alpha > 0$, $\det(A) > 0$.

4. $A$ — мономиальная (perm-matrix умножена на положительную диагональ). Аргумент E5 / IMC-1994-1: строка $i$ матрицы $A$ ортогональна столбцу $j$ ($j \ne i$) матрицы $A^{-1}$. Если в строке $i$ есть $\ge 2$ положительных элемента, то для ортогональности с другим столбцом $A^{-1}$ нужны и положительные, и отрицательные (или хотя бы один отрицательный) элементы — противоречит $A^{-1} \ge 0$. Значит в каждой строке $A$ ровно один ненулевой элемент, и $A$ мономиальная.

5. $A^k = I$ ⇒ $\mu_A | x^k - 1$, корни простые ⇒ $A$ диагонализуема (E8), $\operatorname{spec}(A) \subseteq \{\zeta: \zeta^k = 1\}$. $\operatorname{tr}(A) = \sum \zeta_i$, $|\operatorname{tr}(A)| \le \sum |\zeta_i| = n$. Равенство по треугольному неравенству ⇒ все $\zeta_i$ — параллельные комплексные числа, имея одинаковый модуль $1$ ⇒ равны. Значит $A$ — скаляр $\zeta I$.

6. Общий eigenvector: $E_\lambda(A) = \ker(A - \lambda I)$ инвариантно для $B$ (т.к. $B$ коммутирует с $A - \lambda I$); ограничение $B$ на $E_\lambda(A)$ имеет свой eigenvector — он общий для $A$ и $B$. Индукцией по $n$ (faktor space) — одновременная триангуляризация (E9). На общем диагональном basis Schur eigenvalues $A + B$ — суммы $\lambda_i + \mu_i$ диагональных элементов.

7. $A - I = uv^T$ rank-1, $A = I + uv^T$. Matrix determinant lemma: $\det(A) = 1 + v^T u$. $\operatorname{tr}(A) = n + v^T u$ ⇒ $v^T u = \operatorname{tr}(A) - n$. Итог: $\det(A) = \operatorname{tr}(A) - (n - 1)$.

8. $AB = 0$ ⇒ $\operatorname{im}(B) \subseteq \ker(A)$. $\operatorname{rank}(B) = \dim \operatorname{im}(B) \le \dim \ker(A) = n - \operatorname{rank}(A)$. Эквивалентно — Sylvester rank inequality (E6): $\operatorname{rank}(A) + \operatorname{rank}(B) - n \le \operatorname{rank}(AB) = 0$.

9. $A^2 = 0$ ⇒ $\operatorname{im}(A) \subseteq \ker(A)$ ⇒ $\operatorname{rank}(A) \le n - \operatorname{rank}(A)$, то есть $2r \le n$. Базис: возьмём $u_1, \dots, u_r$ — базис $\operatorname{im}(A)$, продолжим до базиса $\ker(A)$ векторами $w_1, \dots, w_{n - 2r}$, и выберем $v_1, \dots, v_r$ с $A v_i = u_i$. В базисе $(u_1, \dots, u_r, w_1, \dots, w_{n-2r}, v_1, \dots, v_r)$ матрица $A$ имеет блоки $0, 0, I_r$ — после переупорядочивания нужная форма. Это в точности один Jordan block размера $\le 2$ для каждого «слоя» (E15).

10. $A^T = -A$ ⇒ eigenvalues $\lambda$ удовлетворяют $\lambda \in \overline{-\operatorname{spec}(A)}$ + взятие транспонирования сохраняет spectrum ⇒ $\operatorname{spec}(A) = -\operatorname{spec}(A)$, ненулевые eigenvalues идут парами $\lambda, -\lambda$. Над $\mathbb{C}$ дополнительно: real $A$ ⇒ $\operatorname{spec}(A) = \overline{\operatorname{spec}(A)}$. Комбинируя — ненулевые eigenvalues идут четвёрками $\pm i\mu_k$ (чисто мнимые) или приходят как пары $\pm i\mu_k$ для real skew-symmetric. Значит $\operatorname{rank}(A)$ — число ненулевых eigenvalues — чётно. $\det(A) = \prod (i\mu_k)(-i\mu_k) = \prod \mu_k^2 \ge 0$ (Pfaffian-квадрат тождество).

Sources:
- [IMC 2025 Day 2 Solutions](https://www.imc-math.org.uk/imc2025/imc2025-day2-solutions.pdf)
- [IMC 2009 Day 2 Solutions](https://www.imc-math.org.uk/imc2009/imc2009-day2-solutions.pdf)
- [IMC 2005 Day 2 Solutions](https://www.imc-math.org.uk/imc2005/day2_solutions.pdf)
- [Joel Tropp — Spectral Radius Formula](https://users.cms.caltech.edu/~jtropp/notes/Tro01-Spectral-Radius.pdf)
- [W. Kahan — Only Commutators Have Trace Zero](https://people.eecs.berkeley.edu/~wkahan/MathH110/trace0.pdf)
- [Suwama — On Trace Zero Matrices and Commutators](https://arxiv.org/pdf/2111.04884)
- [Joel Shapiro — Burnside's Theorem on Matrix Algebras](https://www.joelshapiro.org/Pubvit/Downloads/BurnsideThm/burnside.pdf)
- [Howard — The Characteristic Polynomial of a Product](https://people.math.sc.edu/howard/Classes/700/charAB.pdf)
- [Wikipedia — Cayley–Hamilton theorem](https://en.wikipedia.org/wiki/Cayley%E2%80%93Hamilton_theorem)
- [Wikipedia — Spectral radius](https://en.wikipedia.org/wiki/Spectral_radius)
