---
topic: Линейная алгебра
subtopic: "Жорданова форма + спектральная теорема (symmetric / Hermitian / unitary / orthogonal / normal)"
sources:
  - "Horn, Johnson — Matrix Analysis"
  - "Bhatia — Matrix Analysis (GTM 169)"
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Keith Conrad — The Minimal Polynomial and Some Applications"
  - "Keith Conrad — Simultaneous Commutativity of Operators"
  - "Higham — Functions of Matrices: Theory and Computation"
  - "Tao — 254A Notes 3a: Eigenvalues and sums of Hermitian matrices"
  - "Wikipedia — Jordan normal form, Schur decomposition, Spectral theorem, Specht's theorem, Min-max theorem, Polar decomposition"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "Engel — Problem-Solving Strategies"
problems_referenced:
  - IMC-1995-1
  - IMC-1997-3
  - IMC-1999-1
  - IMC-2000-3
  - IMC-2001-5
  - IMC-2002-DAY2-5
  - IMC-2003-3
  - IMC-2004-DAY2-4
  - IMC-2006-DAY2-6
  - IMC-2013-1
  - IMC-2014-DAY2-2
  - IMC-2015-1
  - IMC-2015-9
  - IMC-2016-10
  - IMC-2017-8
  - IMC-2019-2
  - IMC-2021-5
  - IMC-2022-2
  - IMC-2023-2
  - IMC-2024-7
  - IMC-2025-8
  - Putnam-1991-A2
  - Putnam-1996-B4
last_updated: 2026-04-27
---

# Жорданова форма + спектральная теорема (symmetric / Hermitian / unitary / orthogonal / normal)

## Scope
Канонические формы операторов на конечномерном пространстве над $\mathbb{C}$ (и $\mathbb{R}$): Jordan canonical form (жорданова форма) для произвольной $A \in M_n(\mathbb{C})$, Schur triangularization (унитарная триангуляризация), spectral theorem для нормальных / эрмитовых / унитарных / симметричных / ортогональных операторов, real Schur / real Jordan для $\mathbb{R}$. Производные инструменты: minimal polynomial и критерий диагонализуемости, Cayley–Hamilton, AB / BA — общий ненулевой спектр, nilpotent через след, common eigenvector для коммутирующих, square root и polar / SVD, Courant–Fischer + Weyl + interlacing для эрмитовых, functional calculus на нормальных, Schur–Hadamard и Frobenius-норменные тождества, Specht (unitary equivalence через trace words) как «крайний» инструмент.

## Записи — Core

### E1. Jordan canonical form (жорданова нормальная форма)

Формулировка. Для любой $A \in M_n(\mathbb{C})$ существует $S \in GL_n(\mathbb{C})$ такая, что
$$S^{-1} A S = J = \bigoplus_{k} J_{m_k}(\lambda_k), \qquad J_m(\lambda) = \lambda I_m + N_m,$$
где $N_m$ — стандартный nilpotent shift ($(N_m)_{i, i+1} = 1$, остальные нули). Разложение единственно с точностью до перестановки блоков. Спектр $A$ — мультимножество $\{\lambda_k\}$ с алгебраической кратностью $\sum m_k$ для данного $\lambda$. Геометрическая кратность $\lambda$ — число блоков с этим $\lambda$.

Условия применимости. Алгебраически замкнутое поле или поле, над которым характеристический многочлен раскладывается в линейные множители. Над $\mathbb{R}$ — real Jordan form (E12).

Идея доказательства. Разложение $\mathbb{C}^n = \bigoplus \ker(A - \lambda_k I)^{n}$ (генерализованные собственные подпространства). На каждом обобщённом подпространстве $A - \lambda_k I$ нильпотентен — выбор «жордановой цепочки» $v, (A - \lambda)v, (A - \lambda)^2 v, \dots$ из ядер увеличивающейся размерности.

Варианты и обобщения.
- Jordan–Chevalley decomposition: $A = A_s + A_n$, $A_s$ диагонализуемая, $A_n$ нильпотентная, $A_s A_n = A_n A_s$, обе — многочлены от $A$. Уникально.
- Размер крупнейшего жорданова блока для $\lambda$ — кратность $\lambda$ как корня minimal polynomial.
- Число блоков размера $\ge k$ для $\lambda$: $\dim \ker(A - \lambda)^k - \dim \ker(A - \lambda)^{k-1}$.
- $\operatorname{rank}(A - \lambda I)^k$ убывает «лестницей» — даёт диаграмму Юнга жордановой структуры.

Используется в. [IMC-1995-1 (подобие нильпотент-сдвигу $J$ через $A = X J X^{-1}$, ранг $= n-1$)], [IMC-2000-3 ($AB - BA$ ранга 1 и нулевого следа $\Rightarrow$ один $2\times 2$ блок $\Rightarrow C^2 = 0$)], [IMC-2001-5 (приведение к форме с одним ненулевым диагональным элементом)], [IMC-2016-10 ($\|A^n\| \le (n / \ln 2) \|A\|^{n-1}$ через анализ блоков и биномиальной оценки $\binom{n}{k}$)], [IMC-2023-2].

---

### E2. Cayley–Hamilton (теорема Кэли–Гамильтона) + minimal polynomial (минимальный многочлен)

Формулировка. Пусть $\chi_A(t) = \det(tI - A) \in \mathbb{F}[t]$ — характеристический многочлен. Тогда $\chi_A(A) = 0$. Minimal polynomial $\mu_A(t)$ — monic многочлен наименьшей степени с $\mu_A(A) = 0$; он делит $\chi_A$ и имеет те же корни (с возможно меньшими кратностями).

Условия применимости. Любое коммутативное кольцо (для $\chi_A$) — Cayley–Hamilton остаётся верной. $\mu_A$ корректно определён над полем (или над $\mathbb{Z}$ для целочисленных $A$, через содержательный аргумент Gauss).

Идея доказательства. Самое короткое: формальный аргумент через $(tI - A) \cdot \operatorname{adj}(tI - A) = \chi_A(t) I$, разложение $\operatorname{adj}(tI - A) = \sum t^i B_i$ и сравнение коэффициентов. Концептуальное: проверка на алгебраически замкнутом поле через Jordan form (E1) — на блоке $J_m(\lambda)$ имеем $(J - \lambda I)^m = 0$, значит $\chi_J(J) = 0$.

Варианты и обобщения.
- Diagonalizable $\iff \mu_A$ — squarefree (произведение различных линейных множителей). Прямое следствие Jordan: блок размера $> 1$ требует $(t - \lambda)^2 \mid \mu_A$.
- Minimal polynomial = НОД соотношений $\sum c_i A^i = 0$ как многочленов.
- Над $\mathbb{Z}/p$: $\mu_A$ выражает порядок $A$ в $GL_n(\mathbb{F}_p)$ для невырожденной $A$.

Используется в. [IMC-1999-1 ($A^3 = A + I \Rightarrow \mu_A \mid x^3 - x - 1$, корни описывают спектр, $\det A > 0$)], [IMC-2003-3 ($3x^3 - x^2 - x - 1$ имеет различные корни $\Rightarrow A$ диагонализуема $\Rightarrow A^k$ имеет идемпотентный предел)], [IMC-2017-8 (рекурсия $A_{n+1}$ блочно $\Rightarrow$ спектр через свёртку)], [IMC-2023-2 (через комбинации $A^2 = B^2 = C^2$, $B^3 = ABC + 2I \Rightarrow B^6 = I$ через алгебраические манипуляции)].

---

### E3. Spectral theorem (спектральная теорема) для normal matrices

Формулировка. Пусть $A \in M_n(\mathbb{C})$. Тогда эквивалентны:
1. $A$ нормальна: $A A^* = A^* A$.
2. $A$ унитарно диагонализуема: $\exists U \in U(n)$ с $U^* A U = \operatorname{diag}(\lambda_1, \dots, \lambda_n)$.
3. У $\mathbb{C}^n$ есть orthonormal basis из собственных векторов $A$.

Подслучаи (фиксируют локализацию спектра):
- $A = A^*$ (Hermitian, эрмитова) $\iff$ нормальна и спектр $\subset \mathbb{R}$.
- $A^* A = I$ (unitary, унитарная) $\iff$ нормальна и спектр $\subset S^1 = \{|z| = 1\}$.
- $A$ real symmetric ($A = A^T$, real) $\iff$ ортогонально диагонализуема в $\mathbb{R}^n$ ($\exists Q \in O(n)$ с $Q^T A Q$ диагональной), real spectrum.
- $A$ real orthogonal ($A^T A = I$) $\iff$ ортогонально подобна блочно-диагональной матрице с блоками $\pm 1$ и $2\times 2$-вращениями $R_\theta$.

Условия применимости. Только финитная размерность; над $\mathbb{C}$ для версий 1–3, для real версий — над $\mathbb{R}$. Принципиально: спектральная теорема не работает для произвольных коммутирующих $A$ и $A^T$ над $\mathbb{R}$ без перехода к real Schur form.

Идея доказательства. Через Schur (E4): нормальная $\Rightarrow$ Schur upper-triangular $T = U^* A U$ нормальна, но из $T T^* = T^* T$ для треугольной следует $T$ диагональна (сравнение $(1,1)$-элементов матриц $T T^*$ и $T^* T$ даёт зануление первой строки $T$ кроме $(1,1)$, индукция).

Варианты и обобщения.
- Functional calculus: для нормальной $A = U \Lambda U^*$ и $f: \sigma(A) \to \mathbb{C}$ определяется $f(A) := U f(\Lambda) U^*$, где $f(\Lambda) = \operatorname{diag}(f(\lambda_i))$. Совпадает с многочленным $f(A)$ при многочленном $f$.
- Polar decomposition (E10): следует из спектральной теоремы для PSD $\sqrt{A^* A}$.
- Sum $\|A\|_F^2 = \operatorname{tr}(A^* A) = \sum |\lambda_i|^2$ для нормальной — иначе $\sum |\lambda_i|^2 \le \|A\|_F^2$ (Schur–Hadamard, E14).
- Для real symmetric: $\lambda_1 \ge \dots \ge \lambda_n$ — порядок имеет смысл (real spectrum), формула Rayleigh (E11).

Используется в. [IMC-2013-1 (positive definite симметричные с $\lambda_{\min} > 1 \Rightarrow AB$ имеет $\lambda_{\min} > 1$ через $AB \sim A^{1/2} B A^{1/2}$)], [IMC-2014-DAY2-2 (Schur–Hadamard на нормальной)], [IMC-2015-9 ($t$-normal: $A A^T = A^T A$ — структура максимального подпространства)], [IMC-2021-5 ($2021 B - B^2 = A^m$ с симметричной $B$ ограничивает spectral radius $A$)], [IMC-2025-8 (rotation-symmetric $A$ — собственные значения чисто real или imaginary)].

---

### E4. Schur triangularization (унитарная триангуляризация)

Формулировка. Для любой $A \in M_n(\mathbb{C})$ существует унитарная $U$ и upper-triangular $T$ с
$$U^* A U = T, \quad T_{ii} = \lambda_i \text{ (eigenvalues, в любом наперёд заданном порядке)}.$$
Над $\mathbb{R}$ — real Schur form: $Q \in O(n)$, $T$ block-upper-triangular с блоками $1\times 1$ (real eigenvalues) и $2\times 2$ (комплексно-сопряжённые пары) на диагонали.

Условия применимости. Над $\mathbb{C}$ — без условий. Над $\mathbb{R}$ — block-real Schur, без диагонализуемости.

Идея доказательства. Индукция: возьми собственный вектор $v_1$, продолжи до ортонормированного базиса. В этом базисе $A$ имеет первый столбец $(\lambda_1, 0, \dots, 0)^T$, остальное — $(n-1) \times (n-1)$ блок, к которому применяется индуктивное предположение.

Варианты и обобщения.
- Simultaneous Schur triangularization для коммутирующих $A_1, \dots, A_k$ — общий ortonormal basis даёт одновременно верхнетреугольный вид (E8).
- Spectrum + nilpotent decomposition: $T = D + N$, $D$ диагональная, $N$ строго upper-triangular nilpotent. Это и есть Jordan–Chevalley в унитарном базисе для нормальной $A$ (тогда $N = 0$).
- Если $A^* A - A A^* \succeq 0$ (hyponormal), то $T$ автоматически имеет малую внедиагональ — хорошие оценки.

Используется в. Универсальный «передний приём» для оценок спектра через trace / Frobenius. [IMC-2014-DAY2-2 (через Schur — $\sum |\lambda_i|^2 \le \sum |a_{ij}|^2$, Schur–Hadamard)], [IMC-2016-10 (анализ $A = U(D+N)U^*$, оценка $\|(D+N)^n\|$ через биномиальное разложение и треугольную структуру)]. Часто пара $A$ + Schur form $\rightarrow$ задача о треугольной матрице.

---

### E5. Eigenvalues of $AB$ and $BA$ совпадают (с точностью до нулей)

Формулировка. Для $A \in M_{m \times n}$, $B \in M_{n \times m}$: ненулевой спектр $AB$ и $BA$ совпадает с алгебраическими кратностями. Точнее
$$t^n \chi_{AB}(t) = t^m \chi_{BA}(t).$$
При $m = n$: $\chi_{AB} = \chi_{BA}$.

Условия применимости. Произвольное поле. Жорданова структура $AB$ и $BA$ совпадает на ненулевых $\lambda$ (Flanders, см. ELA «Jordan forms of $AB$ and $BA$»). На $\lambda = 0$ блоки могут отличаться — но размеры блоков образуют пары $(k, k)$ или $(k, k+1)$.

Идея доказательства. Через E4 (Sylvester) из заметки про определители: $\det(I + tAB) = \det(I + tBA)$. Альтернативно: если $ABv = \lambda v, \lambda \neq 0$, то $BA(Bv) = \lambda(Bv)$ и $Bv \neq 0$ (иначе $\lambda v = ABv = A \cdot 0 = 0$). Аналогичный аргумент для обобщённых eigenspaces даёт совпадение жордановой структуры на $\lambda \neq 0$.

Варианты и обобщения.
- $\operatorname{tr}((AB)^k) = \operatorname{tr}((BA)^k)$ для всех $k \ge 1$ — следует напрямую из cyclic invariance, без перехода к Jordan / Sylvester.
- Если $A$ или $B$ обратима — $AB \sim BA$ (подобие), то есть Jordan совпадает полностью.
- Связь с rank-low возмущениями: если $\operatorname{rank}(B) = r$, то $AB$ имеет $\le r$ ненулевых eigenvalues.

Используется в. [IMC-2000-3 ($C = AB - BA$ ранга 1, $\operatorname{tr}(C) = 0$ $\Rightarrow$ все собственные значения $0$, через E1 $C^2 = 0$ — здесь не сам $AB / BA$, а инструмент для коммутатора)]. Регулярно: «Уменьшить размер $AB$ до $BA$, если $\operatorname{rank}$ маленький».

---

## Записи — Standard

### E6. Diagonalizability via squarefree minimal polynomial (диагонализуемость через свободный от квадратов minimal polynomial)

Формулировка. $A \in M_n(\mathbb{C})$ диагонализуема (над $\mathbb{C}$) $\iff \mu_A$ — произведение различных линейных множителей. В частности: если $p(A) = 0$ для какого-то $p$ с simple roots — $A$ диагонализуема.

Условия применимости. Алгебраически замкнутое поле (или поле, над которым $\mu_A$ распадается). Над $\mathbb{R}$: диагонализуема в $\mathbb{R}^n$ $\iff \mu_A$ имеет различные корни и все они real.

Идея доказательства. Из Jordan form: блок $J_m(\lambda)$ с $m \ge 2$ требует $(t - \lambda)^2 \mid \mu_A$. Прямой аргумент без Jordan — через идеал $\{p \in \mathbb{C}[t]: p(A) = 0\}$ и теорему о структуре модулей над PID.

Варианты и обобщения.
- $A^2 = A$ (idempotent) $\iff A$ диагонализуема со спектром $\subset \{0, 1\}$.
- $A^k = I$ для какого-то $k$ $\iff A$ диагонализуема со спектром в корнях $k$-й степени из $1$ (поэтому $A \in GL_n(\mathbb{C})$ конечного порядка $\Rightarrow$ диагонализуема).
- Involution $A^2 = I$ $\iff$ диагонализуема со спектром $\subset \{\pm 1\}$ $\Rightarrow$ $\mathbb{C}^n = \ker(A - I) \oplus \ker(A + I)$.

Используется в. [IMC-2003-3 (через $3x^3 - x^2 - x - 1$ с simple roots)], типовые задачи «$p(A) = 0$ с simple roots $\Rightarrow$ всё что угодно через диагонализацию». Putnam-1996-B4 (нильпотентность через минимальный многочлен).

---

### E7. Nilpotency criterion (критерий нильпотентности через след)

Формулировка. $A \in M_n(\mathbb{C})$ нильпотентна $\iff \operatorname{tr}(A^k) = 0$ для всех $k = 1, 2, \dots, n$ ($\iff$ для всех $k \ge 1$). Эквивалентно: все eigenvalues $A$ равны $0$.

Условия применимости. Поля характеристики $0$ (или $> n$). В характеристике $p$ — лишь односторонняя импликация, см. контрпример $A = I_p$ над $\mathbb{F}_p$: $\operatorname{tr}(A^k) = p \equiv 0$, но $A$ не нильпотентна.

Идея доказательства. $\operatorname{tr}(A^k) = \sum \lambda_i^k$ — power sums. Через Newton identities выразить elementary symmetric polynomials $e_j$ через $p_k = \operatorname{tr}(A^k)$: $p_1 = \dots = p_n = 0 \Rightarrow e_1 = \dots = e_n = 0 \Rightarrow \chi_A(t) = t^n$, откуда $A^n = 0$ по Cayley–Hamilton (E2).

Варианты и обобщения.
- $A$ нильпотентна $\iff \chi_A(t) = t^n \iff$ единственное собственное значение $0$ (с кратностью $n$).
- Над $\mathbb{R}$: $A$ нильпотентна $\iff A^n = 0$ ($n = $ размер).
- $\operatorname{rank}(A) = r$ и $A$ нильпотентна $\Rightarrow A^{r+1} = 0$ (грубее $A^n = 0$).

Используется в. [IMC-2000-3 ($AB - BA$ ранга 1, $\operatorname{tr} = 0 \Rightarrow$ нильпотент; единственный нетривиальный жорданов блок размера $\le 2$, ибо $\operatorname{rank} = 1$, поэтому $C^2 = 0$)], типовые задачи на $A^k = 0$ или $\operatorname{rank}$-аргументы. Putnam-classic.

---

### E8. Common eigenvector for commuting matrices + simultaneous triangularization

Формулировка. Если $A, B \in M_n(\mathbb{C})$ коммутируют ($AB = BA$), то у них есть общий собственный вектор. Более сильно (Frobenius / Schur): любое семейство попарно коммутирующих матриц одновременно унитарно триангуляризуемо. Если все они диагонализуемы — одновременно диагонализуемы (общий ortonormal basis при условии нормальности).

Условия применимости. Алгебраически замкнутое поле для существования собственного вектора. Конечномерность критична.

Идея доказательства. Возьми $\lambda$ — собственное значение $A$, $V = \ker(A - \lambda I)$. Тогда $B(V) \subseteq V$ (из $AB = BA$), значит $B|_V$ имеет собственный вектор в $V$ — общий для $A, B$. Индукция по размерности. Для семейства — то же индукцией.

Варианты и обобщения.
- Lie–Kolchin: solvable Lie algebra матриц одновременно триангуляризуема (расширение).
- Engel theorem: семейство, состоящее из нильпотентных, и закрытое относительно скобки $[X, Y] = XY - YX$, одновременно строго upper-triangular.
- Для нормальных и коммутирующих: одновременная унитарная диагонализация (общий ortonormal basis).
- Контрпример к «обратное верно»: $A, B$ диагонализуемы и одновременно — но без $AB = BA$ может не быть (требуется именно одновременная). Если $A, B$ диагонализуемы и $AB = BA$ — одновременная диагонализуемость.

Используется в. [IMC-2002-DAY2-5 (выбор фазы $w$ для $S = wA + \bar w I$ — использует, что $A$ имеет конечный спектр; коммутируемость с $I$ — тривиально)], [IMC-2017-8 (block-recursion с участием $I$)], [IMC-2024-7 ($A + B = I$ — коммутируют, общий базис собственных)]. Putnam-1991-A2 (commuting matrices с $A^2 + B^2 = AB$).

---

### E9. Square root + similarity $AB \sim A^{1/2} B A^{1/2}$ (для PSD $A$)

Формулировка. Пусть $A \succeq 0$ (positive semi-definite, эрмитова с $\lambda_i \ge 0$). Тогда:
1. Существует единственная $A^{1/2} \succeq 0$ с $(A^{1/2})^2 = A$.
2. Для любой $B \in M_n$: $AB$ подобна $A^{1/2} B A^{1/2}$ (если $A \succ 0$, иначе через предельный переход / на $\operatorname{im}(A)$).
3. В частности, если $B = B^*$ — то $A^{1/2} B A^{1/2}$ эрмитова, значит спектр $AB$ — real. Если ещё и $B \succeq 0$ — спектр $AB$ — real $\ge 0$.

Условия применимости. $A \succeq 0$ обязательно. Корень $A^{1/2}$ — функциональное исчисление от спектральной декомпозиции $A = U \Lambda U^*$, $A^{1/2} := U \Lambda^{1/2} U^*$.

Идея доказательства. (1) — спектральная теорема (E3) + functional calculus. (2) — $A B = A^{1/2} (A^{1/2} B) = A^{1/2} (A^{1/2} B A^{1/2}) A^{-1/2}$ при невырожденной $A$. По плотности — для PSD.

Варианты и обобщения.
- $\lambda_{\min}(AB) \ge \lambda_{\min}(A) \lambda_{\min}(B)$ для $A, B \succeq 0$ (эквивалентно $A^{1/2} B A^{1/2} \succeq \lambda_{\min}(A) B$).
- Loewner order: $A \preceq B \Rightarrow C^* A C \preceq C^* B C$ — congruence сохраняет порядок.
- Geometric mean $A \# B := A^{1/2} (A^{-1/2} B A^{-1/2})^{1/2} A^{1/2}$ — единственная $X \succeq 0$ с $X A^{-1} X = B$ (Anderson–Trapp).

Используется в. [IMC-2013-1 (симметричные $A, B$ с $\lambda_{\min} > 1$: $AB \sim A^{1/2} B A^{1/2} \succeq \lambda_{\min}(A) B \succ B \succ I$)]. Часто в задачах на сравнение спектров произведений PSD.

---

### E10. Polar decomposition (полярное разложение) + SVD (singular value decomposition)

Формулировка. Любая $A \in M_n(\mathbb{C})$ раскладывается:
$$A = U P, \quad U \text{ unitary}, \quad P = (A^* A)^{1/2} \succeq 0 \quad \text{(right polar)},$$
или $A = P' U$, $P' = (A A^*)^{1/2}$. При невырожденной $A$ — $U, P$ единственны.

SVD: $A = W \Sigma V^*$, $W, V$ — unitary, $\Sigma = \operatorname{diag}(\sigma_1, \dots, \sigma_n)$, $\sigma_1 \ge \dots \ge \sigma_n \ge 0$ — singular values $A$ ($\sigma_i = \sqrt{\lambda_i(A^* A)}$).

Условия применимости. Универсальное; обобщается на прямоугольные $A \in M_{m \times n}$.

Идея доказательства. SVD: спектральная теорема (E3) на $A^* A \succeq 0$, $A^* A = V \Sigma^2 V^*$. Положить $W = AV \Sigma^{-1}$ на ненулевых сингулярных, дополнить до унитарной. Polar: $A = W \Sigma V^* = (W V^*)(V \Sigma V^*) = U P$.

Варианты и обобщения.
- $A$ нормальна $\iff$ в polar $UP = PU$ (т.е. $U, P$ коммутируют). Иначе говоря — спектральная теорема (E3) — это «диагонализующее» SVD когда $|\lambda_i| = \sigma_i$.
- Min-max для сингулярных: $\sigma_k = \min_{\dim L = n - k + 1} \max_{x \in L, \|x\| = 1} \|Ax\|$.
- Best rank-$k$ approximation в Frobenius / spectral норме: $A_k = \sum_{i \le k} \sigma_i w_i v_i^*$ (Eckart–Young).

Используется в. [IMC-2025-8 (структурные ограничения через сингулярные)], общий инструмент для оценок $\|A^n\|$, ranks, low-rank approximations. На IMC напрямую SVD редок, но через polar и сингулярные — регулярно.

---

### E11. Rayleigh quotient + Courant–Fischer min-max (формула Куранта–Фишера)

Формулировка. Для эрмитовой $A$ с $\lambda_1 \ge \dots \ge \lambda_n$:
$$\lambda_1 = \max_{\|x\| = 1} x^* A x, \quad \lambda_n = \min_{\|x\| = 1} x^* A x.$$
Courant–Fischer:
$$\lambda_k = \max_{\dim V = k} \min_{x \in V, \|x\| = 1} x^* A x = \min_{\dim V = n - k + 1} \max_{x \in V, \|x\| = 1} x^* A x.$$

Условия применимости. $A = A^*$ обязательно. Для нормальной — формула не работает «как есть» (спектр комплексный); для эрмитовой части $(A + A^*)/2$ — да.

Идея доказательства. В диагональном базисе $A = \operatorname{diag}(\lambda_1, \dots, \lambda_n)$: $x^* A x = \sum \lambda_i |x_i|^2$, выпуклая комбинация $\lambda_i$. На подпространстве $\dim = k$ всегда есть точка с $x_1 = \dots = x_{k-1} = 0$ (counting), на ней значение $\le \lambda_k$. Sup достигается на span $e_1, \dots, e_k$.

Варианты и обобщения.
- Weyl inequality: $\lambda_k(A + B) \le \lambda_i(A) + \lambda_j(B)$ для $i + j - n \le k$ (и аналогично снизу). Следует из min-max сложением подпространств.
- Cauchy interlacing: для главной $(n-1)$-минора $\tilde A$ эрмитовой $A$: $\lambda_k(A) \ge \lambda_k(\tilde A) \ge \lambda_{k+1}(A)$. Обобщение на $k$-минор: $\lambda_k(A) \ge \lambda_k(\tilde A) \ge \lambda_{k+m}(A)$.
- Hoffman–Wielandt: $\sum_i |\lambda_{\pi(i)}(A) - \lambda_i(B)|^2 \le \|A - B\|_F^2$ для нормальных $A, B$ при оптимальной перестановке.
- Lidskii: $\sum_{i \in S} \lambda_i(A + B) \le \sum_{i \in S} \lambda_i(A) + \sum_{i \le |S|} \lambda_i(B)$.

Используется в. [IMC-2021-5 (оценка $|\det A| \le 1$ через спектральный радиус $B$ и $A^m$ ограниченный)], [IMC-2013-1 ($\lambda_{\min}(AB) \ge \lambda_{\min}(A) \lambda_{\min}(B)$ — комбинация Rayleigh с E9)], классические оценки eigenvalues для structured matrices.

---

### E12. Real Jordan form / real Schur form (вещественные канонические формы)

Формулировка. Над $\mathbb{R}$ для $A \in M_n(\mathbb{R})$:
- Real Jordan: блочно-диагональная с блоками двух типов — стандартные $J_m(\lambda)$ для real $\lambda$ и «комплексно-сопряжённые» блоки $J_m^{\mathbb{R}}(a + bi)$ размера $2m \times 2m$, состоящие из $2 \times 2$-блоков $\begin{pmatrix} a & -b \\ b & a \end{pmatrix}$ на диагонали и $I_2$ на наддиагонали.
- Real Schur: $Q^T A Q = T$, $Q \in O(n)$, $T$ block-upper-triangular с блоками $1 \times 1$ (real eigenvalues) и $2 \times 2$ (комплексно-сопряжённые пары $a \pm bi$, реализованные как $\begin{pmatrix} a & -b \\ b & a \end{pmatrix}$).
- Real orthogonal: $Q \in O(n)$ ортогонально подобна $\bigoplus \pm 1 \oplus \bigoplus R_{\theta_k}$, где $R_\theta$ — стандартное вращение.

Условия применимости. Поле $\mathbb{R}$. Существование real Schur — без ограничений; real Jordan — без ограничений.

Идея доказательства. Перейти к $\mathbb{C}$, получить Jordan, заметить, что комплексно-сопряжённые блоки $J_m(\lambda), J_m(\bar\lambda)$ объединяются в один real-блок через реальную часть базиса.

Варианты и обобщения.
- Real symmetric $\Rightarrow$ ортогонально диагонализуема (real spectrum).
- Real skew-symmetric ($A^T = -A$): спектр $\subset i\mathbb{R}$, ортогонально-блочно-диагональна с $0$-блоками и $2 \times 2$-блоками $\begin{pmatrix} 0 & -b \\ b & 0 \end{pmatrix}$.
- Real normal ($A A^T = A^T A$): ортогонально-блочно-диагональна с $1 \times 1$-блоками (real eigenvalues) и $2 \times 2$-блоками $\begin{pmatrix} a & -b \\ b & a \end{pmatrix}$.

Используется в. [IMC-2006-DAY2-6 (3 случая для $A_3$ — real / complex eigenvalues / повторяющееся, через real Schur / Jordan)], [IMC-2025-8 (rotation-invariance — real Schur с $2 \times 2$-блоками вращения)]. Каждый раз когда задача формулируется в $\mathbb{R}$ и нужна классификация.

---

### E13. Functional calculus + matrix exponential для нормальных

Формулировка. Для нормальной $A = U \Lambda U^*$ и $f: \sigma(A) \to \mathbb{C}$ определяется $f(A) := U f(\Lambda) U^*$. Свойства:
- $\operatorname{tr}(f(A)) = \sum f(\lambda_i)$, $\det f(A) = \prod f(\lambda_i)$, $\sigma(f(A)) = f(\sigma(A))$.
- $f$ голоморфна в окрестности $\sigma(A) \Rightarrow f(A)$ можно определить через Cauchy integral $\frac{1}{2\pi i} \oint f(z)(zI - A)^{-1} dz$ — работает и для не-нормальных (Riesz–Dunford).
- $e^A := \sum_{k \ge 0} A^k / k!$, $\det(e^A) = e^{\operatorname{tr}(A)}$, $\sigma(e^A) = e^{\sigma(A)}$.

Условия применимости. Для unitarily invariant определения — нормальная $A$. Для общего $A \in M_n(\mathbb{C})$ — через Riesz–Dunford или Jordan form (E1): $f(J_m(\lambda)) = \sum_{k=0}^{m-1} \frac{f^{(k)}(\lambda)}{k!} N_m^k$, требуется $f$ дифференцируема нужное число раз в $\lambda$.

Идея доказательства. Спектральная теорема для нормальных (E3) + определение через диагональ. Для Jordan — формальная подстановка с Taylor, проверка что $f(g(A)) = (f \circ g)(A)$ и $(fg)(A) = f(A) g(A)$.

Варианты и обобщения.
- $\det(e^A) = e^{\operatorname{tr}(A)}$ — следует из Jordan, или из $\det e^{tA} \cdot e^{-t \operatorname{tr}(A)} \equiv 1$ (производная в $0$ равна $0$, плюс непрерывность).
- $e^A e^B = e^{A+B}$ только при $AB = BA$. Иначе — Baker–Campbell–Hausdorff.
- $\|A^n\|$-оценки через Jordan: $\|A^n\| = O(n^{m-1} \rho(A)^n)$, где $m$ — размер крупнейшего блока, $\rho(A)$ — spectral radius.

Используется в. [IMC-2016-10 ($\|A^n\| \le (n / \ln 2) \|A\|^{n-1}$ — оценки степеней через Jordan + биномиальные коэффициенты)]. Putnam с $e^A$ и $\det e^A = e^{\operatorname{tr} A}$.

---

### E14. Schur–Hadamard inequality + равенство для нормальных

Формулировка. Для $A \in M_n(\mathbb{C})$ с собственными значениями $\lambda_1, \dots, \lambda_n$ (с алгебраическими кратностями):
$$\sum_{i=1}^n |\lambda_i|^2 \le \sum_{i,j=1}^n |a_{ij}|^2 = \|A\|_F^2,$$
с равенством $\iff A$ нормальна. Из сравнения trace: $|\operatorname{tr}(A)|^2 \le n \cdot \operatorname{tr}(A^* A)$ (Cauchy–Schwarz, отдельно).

Подслучай для real $A$ с real spectrum (например, эрмитовой):
$$\sum_i a_{ii}^2 \le \sum_i \lambda_i^2 \le \sum_{i,j} a_{ij}^2.$$
Левая часть — Schur's inequality для diagonal элементов эрмитовой.

Условия применимости. Любая $A \in M_n(\mathbb{C})$. Equality conditions: правое равенство $\iff$ нормальная; левое (для эрмитовой) — $\iff A$ диагональна.

Идея доказательства. Schur form (E4): $A = U(D + N)U^*$, $D$ диагональная с $\lambda_i$, $N$ строго upper-triangular. $\|A\|_F^2 = \|D + N\|_F^2 = \sum |\lambda_i|^2 + \|N\|_F^2 \ge \sum |\lambda_i|^2$, равенство $\iff N = 0$, $\iff A$ диагонализуема в этом ортонормированном базисе $\iff$ нормальна.

Варианты и обобщения.
- $\sum |\lambda_i|^p \le$ соответствующая Schatten-$p$-норма для $p \ge 2$ (тривиально — для нормальной равенство). Для $p < 2$ обратно.
- Hoffman–Wielandt (см. E11) — Frobenius-расстояние спектров нормальных.
- Schatten norms: $\|A\|_{S_p} = \bigl(\sum \sigma_i^p\bigr)^{1/p}$, для $p = 2$ — Frobenius, для $p = \infty$ — operator norm.

Используется в. [IMC-2014-DAY2-2 ($\sum_{i<j} a_{ii} a_{jj} \ge \sum_{i<j} \lambda_i \lambda_j$ через $\|A\|_F^2 + 2 \sum_{i<j} \lambda_i \lambda_j \ge \sum a_{ii}^2 + 2 \sum a_{ii} a_{jj}$, развёртка квадрата суммы)], классические оценки eigenvalues vs entries.

---

## Записи — Exotic

### E15. Specht's theorem (теорема Шпехта): unitary equivalence через trace words

Формулировка. $A, B \in M_n(\mathbb{C})$ unitary equivalent ($\exists U \in U(n): B = U^* A U$) $\iff \operatorname{tr}(W(A, A^*)) = \operatorname{tr}(W(B, B^*))$ для всех некоммутативных мономов («слов») $W$ от двух переменных.

Для проверки достаточно конечного списка слов длины $\le f(n)$ ($f(n) = O(n)$ — Pearcy). Для $n = 2$ хватит трёх условий: $\operatorname{tr}(A) = \operatorname{tr}(B)$, $\operatorname{tr}(A^2) = \operatorname{tr}(B^2)$, $\operatorname{tr}(A A^*) = \operatorname{tr}(B B^*)$.

Условия применимости. Поле $\mathbb{C}$, конечная размерность.

Идея доказательства. Один направление тривиальна (cyclic invariance). Обратное — через теорему Burnside о неприводимых представлениях $C^* (A, A^*)$ алгебры (или Pearcy). Идея: trace-функционалы порождают все unitary-инварианты.

Варианты и обобщения.
- Для нормальных $A, B$ достаточно $\sigma(A) = \sigma(B)$ (с кратностями) — не нужны trace words.
- Расширение на $m$-tuple нормальных матриц (Sibirskii).
- Связь с moment problem: trace words $= $ моменты невещественного «распределения» собственных пар.

Используется в. Редко на IMC. На Putnam — иногда как «секретный соус» в задачах о классификации матриц с точностью до унитарной эквивалентности. Полезно для shortcut-ов: «доказать, что $A, B$ унитарно эквивалентны, проверив несколько trace identities».

---

### E16. $t$-normal matrices и $A A^T = A^T A$

Формулировка. Real $A \in M_n(\mathbb{R})$ называется $t$-normal (transpose-normal), если $A A^T = A^T A$. Эквивалентно — $A$ как complex matrix нормальна, и при том сохраняет $\mathbb{R}^n$ (тривиально, поскольку real). Над $\mathbb{R}$: $t$-normal $\iff$ ортогонально-блочно-диагонализуема как в E12 (real normal).

Любая real symmetric ($A = A^T$) — $t$-normal. Любая real skew-symmetric ($A = -A^T$) — $t$-normal. Любая real orthogonal — $t$-normal. Сумма коммутирующих $t$-normal — $t$-normal.

Условия применимости. Над $\mathbb{R}$. Не всякое подпространство $V \subset M_n(\mathbb{R})$ из $t$-normal — векторное подпространство; обычно требуется именно линейная структура.

Варианты и обобщения.
- Maximum dimension subspace из $t$-normal: $n(n+1)/2$ (симметричные) или $n(n+1)/2 + \lfloor n/2 \rfloor$ при добавлении skew-symmetric, коммутирующих с симметричными — открытый вопрос для конкретных конструкций.
- Связь с algebra $\mathbb{R}[A]$, порождённой $A$ — для $t$-normal эта алгебра нормальна как complex.

Используется в. [IMC-2015-9 (максимальная размерность подпространства $t$-normal матриц — конструкция через прямую сумму симметричных и коммутирующих skew-symmetric)]. Редкое, но «жёсткая» задача.

---

### E17. Cube-root-of-unity trick + perturbation для общего спектра (IMC-style)

Формулировка. Часто полезный трюк — рассмотреть $S = \alpha A + \beta B + \gamma C + \dots$ с тщательно выбранными $\alpha, \beta, \gamma \in \mathbb{C}$ (часто корни $1$), чтобы:
- $S$ обратима / вырождена при выборе фазы (E2002-DAY2-5: $S = wA + \bar w I$, $S$ вырождена $\iff w/\bar w \in \sigma(A)$ — конечно много значений).
- $S \bar S$ или $S^* S$ имела целевой спектр / детерминант (E1997-3: $S = A + \omega B$, $\omega = e^{2\pi i / 3}$, $\det(S \bar S)$ — вещественен и связан с $\det(BA - AB)$).

Условия применимости. Нужно работать над $\mathbb{C}$. Часто используется в комбинации с $\det(z I - A) \neq 0$ для всех $z$ кроме конечного числа.

Идея доказательства. Алгебраический трюк: записать целевую величину как многочлен от $\alpha, \beta, \dots$, исследовать его как функцию параметра. Часто значения параметра, при которых утверждение нарушается, лежат в собственном алгебраическом подмножестве $\mathbb{C}^k$ — а нам нужно показать существование «хорошего» $\alpha$.

Варианты и обобщения.
- Density argument: множество невырожденных матриц плотно ⇒ задачи для произвольных $A$ часто сводятся к задачам для невырожденных $A$.
- Полиномиальные тождества от матриц: если $P(A) = 0$ выполняется в плотном множестве $A$ — выполняется всегда (поскольку каждая координата $P(A)$ — многочлен от entries $A$).
- Continuity argument: $\det, \operatorname{tr}, \sigma$ непрерывны как функции от entries, что позволяет переносить тождества с диагонализуемых на все.

Используется в. [IMC-1997-3 (cube root of unity для $3 \mid n$)], [IMC-2002-DAY2-5 (выбор $w$ на единичной окружности)], [IMC-2019-2 (DFT на 4 элементах из дат)]. Регулярный приём в задачах с алгебраическими ограничениями.

---

## Self-test

1. Пусть $A \in M_n(\mathbb{C})$ удовлетворяет $A^k = I$ для какого-то $k \ge 1$. Докажи, что $A$ диагонализуема, и что $A$ имеет вещественный спектр $\iff A^2 = I$.

2. Пусть $A, B \in M_n(\mathbb{R})$, $AB - BA$ имеет ранг $1$. Покажи, что $\operatorname{tr}(AB - BA) = 0$ и что $(AB - BA)^2 = 0$.

3. Пусть $A \in M_n(\mathbb{C})$ нильпотентна и $\operatorname{rank}(A) = n - 1$. Найди жорданову форму $A$ и докажи, что любые две такие $A$ подобны.

4. Дана real symmetric $A$ с $A^2 + A = 2I$. Найди возможные собственные значения $A$ и докажи, что $A$ диагонализуема ортогонально.

5. Пусть $A \in M_n(\mathbb{C})$ — нормальная и $A^2 = A^*$. Опиши все возможные собственные значения $A$.

6. Пусть $A, B \in M_n(\mathbb{C})$, $AB = BA$. Докажи, что любой собственный многочлен $f$ от $A$ удовлетворяет $f(A) B = B f(A)$, и что у $A$ и $B$ есть общий собственный вектор.

7. Пусть $A \in M_n(\mathbb{C})$ удовлетворяет $\operatorname{tr}(A^k) = 0$ для $k = 1, \dots, n$. Докажи, что $A^n = 0$.

8. Пусть $A, B \in M_n(\mathbb{R})$ — симметричные, $A \succeq 0$ (positive semi-definite), $B \succeq 0$. Докажи, что все собственные значения $AB$ — вещественные неотрицательные.

9. Пусть $A \in M_n(\mathbb{C})$, $\|A\|_F^2 = \sum |\lambda_i|^2$ (где $\lambda_i$ — собственные значения с кратностями). Покажи, что $A$ нормальна.

10. Пусть $A \in M_n(\mathbb{R})$ — ортогональная и $\det A = 1$. Если $n$ нечётно, докажи, что $A$ имеет неподвижную точку (т.е. $1 \in \sigma(A)$).

---

## Решения

1. $A^k = I \Rightarrow \mu_A \mid x^k - 1$, который имеет различные корни (корни $k$-й степени из $1$). По E6 $A$ диагонализуема. Спектр $\subset \{\zeta : \zeta^k = 1\}$. Real spectrum $\iff \sigma(A) \subset \{\pm 1\} \iff \mu_A \mid x^2 - 1 \iff A^2 = I$.

2. $\operatorname{tr}(AB - BA) = 0$ — cyclic invariance. По E5 / E7: $AB - BA$ имеет $\operatorname{rank} 1$, $\operatorname{tr} 0$, значит спектр $= \{0, 0, \dots, 0\}$, нильпотентна. Жорданова форма (E1): $\operatorname{rank} = 1$ для нильпотентной размера $n \ge 2$ означает один блок $J_2(0)$ и нулевые $1\times 1$ — поэтому $(AB - BA)^2 = 0$.

3. $A$ нильпотентна $\Rightarrow$ единственное собственное значение $0$. $\operatorname{rank}(A) = n - 1 \Rightarrow \dim \ker A = 1 \Rightarrow$ один жорданов блок (геометрическая кратность = число блоков), значит размер блока $= n$. Жорданова форма $J_n(0)$ — стандартный nilpotent shift $N_n$; единственная с точностью до подобия.

4. $A^2 + A - 2I = 0 \Rightarrow \mu_A \mid x^2 + x - 2 = (x - 1)(x + 2)$. Корни $1, -2$ — различные real, по E6 + E3 (real symmetric ортогонально диагонализуема, спектр real) собственные значения $\subset \{1, -2\}$. Ортогональная диагонализуемость — из спектральной теоремы для real symmetric.

5. $A$ нормальна $\Rightarrow$ существует ortonormal basis из собственных. На собственном векторе: $A v = \lambda v \Rightarrow A^2 v = \lambda^2 v$ и $A^* v = \bar \lambda v$. Условие $A^2 = A^* \Rightarrow \lambda^2 = \bar\lambda$. В полярной форме $\lambda = r e^{i\theta}$: $r^2 e^{2i\theta} = r e^{-i\theta}$, откуда $r = 0$ или $r = 1$ и $3\theta \equiv 0 \pmod{2\pi}$. Значит $\lambda \in \{0, 1, e^{2\pi i / 3}, e^{4\pi i / 3}\}$.

6. $f(A) B = \sum c_k A^k B = \sum c_k B A^k = B f(A)$ (индукция $A^k B = B A^k$ из $AB = BA$). Общий собственный вектор: возьми $\lambda \in \sigma(A)$, $V = \ker(A - \lambda I) \neq 0$. Тогда $B(V) \subseteq V$ из $(A - \lambda I) B v = B(A - \lambda I) v = 0$. На $V$ (ненулевом конечномерном комплексном) $B|_V$ имеет собственный вектор — он же общий для $A, B$.

7. По E7: power sums $p_1, \dots, p_n = 0$ через Newton identities дают $e_1 = \dots = e_n = 0$, поэтому $\chi_A(t) = t^n$. Cayley–Hamilton (E2): $A^n = 0$.

8. По E9: $A \succeq 0 \Rightarrow A^{1/2} \succeq 0$ существует. $AB \sim A^{1/2} B A^{1/2}$ (через подобие $A^{1/2} \cdot \cdot A^{-1/2}$ при невырожденной $A$, иначе на $\operatorname{im} A$ + предельный переход / сужение). $A^{1/2} B A^{1/2}$ симметрична (так как $B$ симметрична и $(A^{1/2})^T = A^{1/2}$) и PSD (для $x \neq 0$: $x^T A^{1/2} B A^{1/2} x = (A^{1/2} x)^T B (A^{1/2} x) \ge 0$). Спектр PSD матрицы $\subset \mathbb{R}_{\ge 0}$, спектр $AB$ — тот же.

9. По E14 (доказательство через Schur): $A = U(D + N)U^*$, $\|A\|_F^2 = \|D\|_F^2 + \|N\|_F^2 = \sum |\lambda_i|^2 + \|N\|_F^2$. Условие даёт $\|N\|_F = 0 \Rightarrow N = 0 \Rightarrow A$ диагонализуема в ortonormal basis $\iff$ нормальна (E3).

10. По E12 (real orthogonal): $A$ ортогонально-блочно-диагональна, блоки $\pm 1$ и $R_{\theta}$. $\det A = (-1)^{(\text{число } -1 \text{ блоков})} \cdot \prod \det R_{\theta} = (-1)^{k}$ ($\det R_\theta = 1$). $\det A = 1 \Rightarrow k$ чётное. Размерность: $k + 2 \cdot (\text{число } R_\theta) + (\text{число } +1 \text{ блоков}) = n$. При нечётном $n$ и чётном $k$ — число $+1$ блоков нечётно $\ge 1$, значит $1 \in \sigma(A)$.
