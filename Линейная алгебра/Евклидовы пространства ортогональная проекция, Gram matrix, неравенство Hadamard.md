---
topic: Линейная алгебра
subtopic: "Евклидовы пространства: ортогональная проекция, Gram matrix, неравенство Hadamard"
sources:
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Horn, Johnson — Matrix Analysis"
  - "Bhatia — Matrix Analysis (GTM 169)"
  - "Bhatia — Positive Definite Matrices (Princeton)"
  - "Engel — Problem-Solving Strategies"
  - "Polya, Szegő — Problems and Theorems in Analysis II"
  - "Aigner, Ziegler — Proofs from THE BOOK"
  - "Bárány, Grinberg — On the Power of Linear Dependencies (Steinitz lemma)"
  - "Lemmens, Seidel — Equiangular Lines (1973)"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "AoPS — Cauchy–Schwarz, Gram matrix wiki"
  - "Yufei Zhao — Linear Algebra Tricks for the Putnam"
last_updated: 2026-04-27
problems_referenced:
  - IMC-1994-DAY2-5
  - IMC-2005-DAY2-3
  - IMC-2006-DAY2-4
  - IMC-2010-5
  - IMC-2013-DAY2-3
  - IMC-2014-DAY2-2
  - IMC-2021-8
  - Putnam-2003-A2
  - Putnam-2005-B6
  - Putnam-2008-A6
---

# Евклидовы пространства: ортогональная проекция, Gram matrix, неравенство Hadamard

## Scope
Конечномерные вещественные / комплексные пространства со скалярным произведением. Продвинутый рабочий аппарат: Gram matrix как универсальный мост «векторы $\leftrightarrow$ PSD матрицы», ортогональная проекция как минимизатор и идемпотентный оператор, Hadamard и Fischer как блочные оценки определителя. Дополнительно — конечно-мерные версии Bessel / Parseval, тензорная степень Gram'а как «power-up», Steinitz lemma, probabilistic method для unit-векторов и абсолютные оценки на конфигурации (mutually obtuse, equiangular). Базовый материал курса (определения, Gram–Schmidt) подразумевается.

## Записи — Core

### E1. Gram matrix (матрица Грама)

Формулировка. Для $v_1, \dots, v_m$ в евклидовом / эрмитовом пространстве матрица $G_{ij} = \langle v_i, v_j\rangle$ обладает свойствами:

1. $G$ — Hermitian PSD (положительно полуопределённая); $G$ positive definite $\iff v_1, \dots, v_m$ линейно независимы.
2. $\operatorname{rank} G = \dim \operatorname{span}(v_1, \dots, v_m)$.
3. $\det G \ge 0$, причём $\det G = \operatorname{Vol}^2(P)$ — квадрат $m$-мерного объёма параллелепипеда на $v_i$.
4. Если $A = [v_1 \,|\, \cdots \,|\, v_m]$ ($n \times m$), то $G = A^*A$.
5. Любая PSD матрица $G$ есть Gram некоторых векторов (через Cholesky $G = R^*R$); восстановление однозначно с точностью до унитарного преобразования.

Условия применимости. Любое поле скаляров с эрмитовым скалярным произведением (RR или CC). Никаких предположений о размерности span не нужно — Gram корректно определён всегда.

Идея доказательства. $x^*Gx = \|Ax\|^2 \ge 0$ даёт PSD; $\ker A = \ker G$ (если $Gx = 0$, то $\|Ax\|^2 = 0$) даёт rank-формулу; $\det G = \det(A^*A) =$ Cauchy–Binet $= \sum_S |\det A_S|^2 = \operatorname{Vol}^2$.

Варианты и обобщения.
- Schoenberg: $d_{ij} = \|v_i - v_j\|^2$ — squared distance matrix; $v_i$ восстанавливаются из $d_{ij}$ (с точностью до изометрии) через $\langle v_i, v_j \rangle = (d_{0i} + d_{0j} - d_{ij})/2$ при выбранной точке-«центре» $v_0$.
- Hadamard (entrywise) product сохраняет PSD (Schur product theorem): $G \circ H \succeq 0$, частный случай — $G^{\circ k}$ есть Gram тензорных степеней (E11).
- Принцип «PSD-сертификат»: чтобы доказать $\sum a_i a_j c_{ij} \ge 0$, ищется реализация $c_{ij} = \langle v_i, v_j\rangle$.

Используется в. [IMC-2006-DAY2-4 (рациональный Gram $\Rightarrow$ рациональное решение системы)], [IMC-2010-5 (через тензорную степень и PSD)], [IMC-2021-8 (counting unit vectors через PSD-аргумент)], типовой инструмент Putnam.

---

### E2. Hadamard's inequality (неравенство Адамара)

Формулировка. Для $A \in \mathbb{C}^{n\times n}$ со столбцами $a_1, \dots, a_n$:
$$|\det A| \le \prod_{i=1}^n \|a_i\|_2.$$
Эквивалентная PSD-форма: для любой PSD матрицы $H$
$$\det H \le \prod_{i=1}^n H_{ii}.$$
Равенство $\iff$ столбцы $a_i$ попарно ортогональны (или один из них нулевой) / $H$ диагональна.

Условия применимости. Произвольные комплексные / вещественные матрицы. Норма — стандартная $\ell_2$.

Идея доказательства. Через QR: $A = QR$, $Q$ unitary, $R$ верхне-треугольная с $|R_{ii}| \le \|a_i\|$ (как длина проекции после вычета компонент в $\operatorname{span}(a_1, \dots, a_{i-1})$). Тогда $|\det A| = \prod |R_{ii}| \le \prod \|a_i\|$. PSD-форма — итерация Fischer's inequality (E6).

Варианты и обобщения.
- Hadamard's maximal determinant problem: при $|a_{ij}| \le 1$ имеем $|\det A| \le n^{n/2}$, равенство $\iff$ $A$ — Hadamard matrix; существование при $n = 1, 2$ или $n \equiv 0 \pmod 4$ (открытая гипотеза $n \equiv 0 \pmod 4 \Rightarrow$ Hadamard exists).
- Schur–Hadamard inequality: для нормальной $A$ и собственных $\lambda_i$ имеем $\sum |a_{ii}|^2 \le \sum |\lambda_i|^2$ — диагональ зажата трасс-подобной величиной (используется в IMC-2014-DAY2-2).
- Sharpening: $\det H \le \min_i \det H^{(i)} \cdot H_{ii}$, где $H^{(i)}$ — главный $(n-1)$-минор.

Используется в. Стандартная оценка сверху на $|\det|$ через нормы строк / столбцов; работает в задачах вида «оценить $|\det A|$ при ограничении $|a_{ij}| \le M$» и для оценок объёмов.

---

### E3. Orthogonal projection (ортогональная проекция) и best approximation

Формулировка. Для подпространства $V \subseteq \mathbb{R}^n$ существует и единствен оператор $P_V$ — ортогональная проекция на $V$ — такой что:

1. $P_V^2 = P_V$, $P_V^T = P_V$ (idempotent, self-adjoint).
2. $\operatorname{im} P_V = V$, $\ker P_V = V^\perp$, $\mathbb{R}^n = V \oplus V^\perp$.
3. Best-approximation: $\|x - P_V x\| = \min_{y \in V} \|x - y\|$, минимум достигается единственно.
4. Если $A$ — матрица из базиса $V$ в столбцах, $P_V = A(A^TA)^{-1}A^T$.
5. Pythagoras: $\|x\|^2 = \|P_V x\|^2 + \|x - P_V x\|^2$.

Условия применимости. Любое конечномерное пространство со скалярным произведением; в гильбертовом случае (бесконечномерный) требуется замкнутость $V$. В $\mathbb{C}^n$ заменяем $A^T$ на $A^*$.

Идея доказательства. Существование — через Gram–Schmidt или прямую формулу с $A(A^TA)^{-1}A^T$ ($A^TA$ обратима из-за лин. независимости столбцов). Единственность — выпуклостью $\|x - y\|^2$ на $V$. Best-approximation: $\|x - y\|^2 = \|x - P_V x\|^2 + \|P_V x - y\|^2 \ge \|x - P_V x\|^2$.

Варианты и обобщения.
- Kakutani: linear projector $P$ ($P^2 = P$) ортогонален $\iff \|P\|_{op} \le 1$ $\iff \|Px\| \le \|x\|$ для всех $x$.
- Hilbert projection theorem: $V$ — выпуклое замкнутое (не обязательно подпространство) $\Rightarrow$ есть единственная ближайшая точка.
- Метод наименьших квадратов: решение $\min \|Ax - b\|$ — это $x = (A^TA)^{-1}A^Tb$, остаток $\perp \operatorname{im}(A)$.

Используется в. [IMC-1994-DAY2-5 (минимизация нормы суммы — Steinitz, см. E10)], как scaffold во всех задачах с условием «минимальная норма / расстояние / приближение».

---

### E4. Cauchy–Schwarz через PSD Gram (неравенство Коши–Буняковского–Шварца)

Формулировка. Для любых $u, v$ в эрмитовом пространстве
$$|\langle u, v\rangle|^2 \le \|u\|^2 \cdot \|v\|^2,$$
равенство $\iff u, v$ линейно зависимы. Эквивалентно: $2\times 2$ Gram $\begin{pmatrix} \|u\|^2 & \langle u,v\rangle \\ \langle v,u\rangle & \|v\|^2\end{pmatrix}$ — PSD, его $\det \ge 0$.

Условия применимости. Любая полу-форма $\langle \cdot, \cdot\rangle$, удовлетворяющая аксиомам скалярного произведения (можно даже PSD; равенство случай покрывает вырождение).

Идея доказательства. Gram любых двух векторов — PSD (E1) $\Rightarrow \det \ge 0$. Альтернативно: $\langle u - tv, u - tv\rangle \ge 0$ как квадратный многочлен от $t$, дискриминант $\le 0$.

Варианты и обобщения.
- Trace / Frobenius CS: $|\operatorname{tr}(A^*B)|^2 \le \operatorname{tr}(A^*A)\,\operatorname{tr}(B^*B)$ — частный случай для inner product $\langle A,B\rangle_F = \operatorname{tr}(A^*B)$.
- Engel / Titu / Sedrakyan: $\sum a_i^2/b_i \ge (\sum a_i)^2/\sum b_i$ при $b_i > 0$ — переписать как CS для $(a_i/\sqrt{b_i}, \sqrt{b_i})$.
- Operator CS: для PSD $X$ имеем $|\langle u, v\rangle_X|^2 \le \langle u,u\rangle_X \langle v,v\rangle_X$, где $\langle u,v\rangle_X = u^*Xv$.
- Многомерная форма: $|\det G(u_1, \dots, u_k)|^2 \le \prod \det G(u_i)^{...}$ — формализуется как E5 + Fischer.

Используется в. Инструмент-атом, прямая работа в любой задаче на оценку скалярного произведения; PSD-форма стандартная при анализе сумм $\sum c_{ij} x_i x_j$.

---

### E5. Volume via Gram determinant (объём через определитель Грама)

Формулировка. Для $v_1, \dots, v_k \in \mathbb{R}^n$ ($k \le n$) объём $k$-мерного параллелепипеда
$$\operatorname{Vol}_k(v_1, \dots, v_k) = \sqrt{\det G(v_1, \dots, v_k)},$$
где $G_{ij} = \langle v_i, v_j\rangle$. В частности при $k = n$: $|\det A|^2 = \det(A^TA) = \det G$.

Условия применимости. Любое евклидово / эрмитово конечномерное пространство. Выражение симметрично относительно изометрий: при действии ортогонального оператора $G$ не меняется.

Идея доказательства. Выбираем ortho-базис $e_1, \dots, e_k$ для $W = \operatorname{span}(v_i)$, в нём $v_i$ — $k$-вектор-столбцы матрицы $A' \in \mathbb{R}^{k\times k}$, $A^T A = (A')^T A'$, $\operatorname{Vol} = |\det A'|$. Альтернативно — Cauchy–Binet для прямоугольной $A$.

Варианты и обобщения.
- Высота параллелепипеда: $h_k = \operatorname{Vol}(v_1, \dots, v_k) / \operatorname{Vol}(v_1, \dots, v_{k-1})$ — длина перпендикуляра от $v_k$ к $\operatorname{span}(v_1, \dots, v_{k-1})$, что эквивалентно $\|(I - P)\,v_k\|$ для $P$ — проекция на span.
- Hadamard как следствие: $\det G \le \prod G_{ii} = \prod \|v_i\|^2$, т. е. $\operatorname{Vol} \le \prod \|v_i\|$ с равенством на ortho-наборе.
- Distance to subspace: $\operatorname{dist}(v, W) = \sqrt{\det G(v, w_1, \dots, w_k)/\det G(w_1, \dots, w_k)}$.

Используется в. Стандартная редукция «volume / distance $\to$ determinant»; также рабочий приём в задачах, где $\det A^T A$ возникает через Cauchy–Binet.

---

## Записи — Standard

### E6. Fischer's inequality (неравенство Фишера) и Hadamard как следствие

Формулировка. Для PSD блочной матрицы
$$H = \begin{pmatrix} A & B \\ B^* & D \end{pmatrix}, \quad A \in \mathbb{C}^{p\times p},\ D \in \mathbb{C}^{q\times q},$$
выполнено $\det H \le \det A \cdot \det D$. Равенство $\iff B = 0$ (при PD).

Условия применимости. $H$ должна быть PSD. Для произвольных Hermitian (без знака) неравенство ложно.

Идея доказательства. Schur complement: $\det H = \det A \cdot \det(D - B^*A^{-1}B)$ (при invertible $A$); $D - B^*A^{-1}B \preceq D$ (PSD-порядок), оба PSD $\Rightarrow \det(D - B^*A^{-1}B) \le \det D$ (определитель монотонен по PSD-порядку). При вырожденном $A$ — переход к пределу $A + \varepsilon I$.

Варианты и обобщения.
- Итерация по диагональным $1\times 1$ блокам $\Rightarrow$ Hadamard для PSD: $\det H \le \prod H_{ii}$.
- Koteljanskii: для PSD $H$ и любых индексов $\alpha, \beta$ — $\det H[\alpha\cup\beta]\,\det H[\alpha\cap\beta] \le \det H[\alpha]\,\det H[\beta]$.
- Minkowski's determinant inequality: $\det(A + B)^{1/n} \ge \det(A)^{1/n} + \det(B)^{1/n}$ для PSD $A, B$.

Используется в. Оценки определителей блочных матриц (типовые задачи с структурированной матрицей вида $f(i,j)$ на «двух кусках»), доказательство Hadamard, IMC-задачи на «верхнюю границу через диагональ».

---

### E7. Frobenius / trace inner product на $M_n$

Формулировка. На $M_n(\mathbb{R})$ скалярное произведение $\langle A, B\rangle = \operatorname{tr}(A^TB) = \sum_{ij} a_{ij}b_{ij}$. Соответствующая норма — Frobenius $\|A\|_F = \sqrt{\sum a_{ij}^2}$. Свойства:

1. $\operatorname{Sym}_n \perp \operatorname{Skew}_n$, $M_n = \operatorname{Sym}_n \oplus \operatorname{Skew}_n$, размерности $n(n+1)/2$ и $n(n-1)/2$.
2. Для нормальной $A$: $\|A\|_F^2 = \sum |\lambda_i|^2$ (через спектральное разложение).
3. $\operatorname{tr}(AB) = \operatorname{tr}(BA)$ — но $\operatorname{tr}(A^TB)$ симметричен в $A, B$ (для вещественных).
4. Если $A$ — orthogonal projection на подпространство $V \subseteq \mathbb{R}^n$, то $\|A\|_F^2 = \operatorname{tr}(A^TA) = \operatorname{tr}(A) = \dim V$.

Условия применимости. Все аксиомы inner product выполнены тождественно. Над $\mathbb{C}$ заменяется на $\langle A, B\rangle = \operatorname{tr}(A^*B)$.

Идея доказательства. Билинейность и положительность $\langle A, A\rangle = \sum a_{ij}^2 \ge 0$ — прямо. Ортогональность Sym vs Skew: $\operatorname{tr}(SK) = \operatorname{tr}((SK)^T) = \operatorname{tr}(-KS) = -\operatorname{tr}(SK)$ при $S = S^T$, $K = -K^T$.

Варианты и обобщения.
- Schatten-$p$ норма: $\|A\|_p = (\sum \sigma_i^p)^{1/p}$, $p=2$ — Frobenius, $p=\infty$ — operator norm.
- Hilbert–Schmidt в бесконечномерном случае.
- $\langle A, B\rangle = \operatorname{tr}(W A^TB)$ при PD $W$ — взвешенный inner product.

Используется в. [IMC-2005-DAY2-3 (max dim подпространства $V \subseteq M_n$ с $\operatorname{tr}(XY)=0$ для всех $X, Y \in V$ — ответ $n(n-1)/2$ через ортогональное дополнение Sym)], [IMC-2014-DAY2-2 (через Schur–Hadamard $\sum a_{ii}^2 \le \|A\|_F^2 = \sum \lambda_i^2$ для нормальной)].

---

### E8. Trace = rank для проектора

Формулировка. Если $P^2 = P$ (idempotent) над любым полем характеристики $0$, то $\operatorname{tr}(P) = \operatorname{rank}(P)$. Для ортогональной проекции дополнительно $P = P^T$, $\|P\|_F^2 = \operatorname{tr}(P) = \dim \operatorname{im}(P)$.

Условия применимости. Любое поле char $= 0$ (или $> n$). Обобщение «$\operatorname{tr} P^k = \operatorname{rank} P$» тоже верно для idempotent.

Идея доказательства. Спектр $P$ лежит в $\{0, 1\}$ (так как $P^2 - P = 0$); $P$ диагонализуема, число единиц в Jordan-форме = размерность $\operatorname{im}(P)$ = $\operatorname{rank}(P)$, сумма собственных значений = $\operatorname{tr}(P)$.

Варианты и обобщения.
- $P_1, \dots, P_k$ — ортогональные проекции с $\sum P_i = I \iff$ все $P_i P_j = 0$ при $i \ne j$ (то есть $\operatorname{im} P_i \perp \operatorname{im} P_j$); следствие: $\sum \operatorname{rank} P_i = \sum \operatorname{tr} P_i = \operatorname{tr}(I) = n$.
- Если $A^2 = A$ (не обязательно симметрична), то $A$ — некий (косой) проектор: $\operatorname{im}(A) \oplus \ker(A) = V$, $A$ ортогональный $\iff A = A^T$.

Используется в. Подсчёт размерностей через след; типовой приём при работе с симметричными / Hermitian матрицами и подсчётом «сколько собственных значений каждого типа».

---

### E9. Bessel's inequality (неравенство Бесселя) и Parseval

Формулировка. Пусть $e_1, \dots, e_k$ — orthonormal система в евклидовом пространстве. Для любого $x$:
$$\sum_{i=1}^k |\langle x, e_i\rangle|^2 \le \|x\|^2,$$
с равенством $\iff x \in \operatorname{span}(e_1, \dots, e_k)$. Если $\{e_i\}$ — orthonormal базис всего пространства, получаем Parseval $\sum |\langle x, e_i\rangle|^2 = \|x\|^2$.

Условия применимости. Конечно или счётно много orthonormal векторов; в Гильбертовом — применимо к любой orthonormal sequence.

Идея доказательства. $P x = \sum \langle x, e_i\rangle e_i$ — ортогональная проекция на $\operatorname{span}(e_i)$; Pythagoras $\|x\|^2 = \|Px\|^2 + \|x - Px\|^2 \ge \|Px\|^2 = \sum |\langle x, e_i\rangle|^2$.

Варианты и обобщения.
- Frame inequality (Riesz): для системы $\{f_i\}$, не обязательно ortho, $A\|x\|^2 \le \sum |\langle x, f_i\rangle|^2 \le B\|x\|^2$ — обобщённый Bessel при $B < \infty$.
- Welch bound: для $m > n$ unit векторов в $\mathbb{R}^n$ $\sum_{i\ne j} |\langle v_i, v_j\rangle|^2 \ge m(m-n)/(n)$ — даёт нижние оценки на максимальный угол.

Используется в. Оценки сверху на сумму квадратов проекций; как мост между геометрией и оценками собственных значений.

---

### E10. Steinitz lemma (лемма Штейница о перестановке)

Формулировка. Пусть $v_1, \dots, v_n \in \mathbb{R}^d$, $\|v_i\| \le 1$, $\sum v_i = 0$. Тогда существует перестановка $\sigma$ такая, что для всех $k$
$$\bigl\|v_{\sigma(1)} + v_{\sigma(2)} + \dots + v_{\sigma(k)}\bigr\| \le d.$$
Константа $d$ оптимальна по порядку (точная константа Стейница до сих пор открыта; известно $\le 2d$ и $\ge \sqrt{(d+3)/4}$).

Условия применимости. Только конечномерное евклидово (или общая конечномерная нормированная — с константой, зависящей от нормы).

Идея доказательства. Жадный алгоритм: на шаге $k$ есть $S_{k-1}$ — текущая частичная сумма. Выбирай $v_i$ из оставшихся минимизирующий $\|S_{k-1} + v_i\|$. Ключевая лемма (Bárány): среди оставшихся векторов всегда есть $v_i$ с $\langle S_{k-1}, v_i\rangle \le 0$ (так как $\sum_{i \in A} v_i = -S_{k-1}$ и средний $\langle S_{k-1}, v_i\rangle = -\|S_{k-1}\|^2/|A| \le 0$). Тогда $\|S_{k-1} + v_i\|^2 \le \|S_{k-1}\|^2 + 1$, индукция даёт оценку.

Варианты и обобщения.
- Levy–Steinitz theorem: множество всех сумм $\sum a_{\sigma(i)}$ перестановок условно сходящегося ряда в $\mathbb{R}^d$ — аффинное подпространство.
- Matrix / colorful versions: Bárány 2023 — обобщения для интегрального программирования.

Используется в. [IMC-1994-DAY2-5 (прямой триггер Steinitz, формулировка задачи — частный случай для $d$-мерных векторов нормы $\le 1$ с нулевой суммой)]; стандартный приём в комбинаторных задачах с упорядочением векторов.

---

### E11. Tensor-power Gram trick (тензорная степень для усиления)

Формулировка. Пусть $u_1, \dots, u_m$ — единичные векторы в $\mathbb{R}^n$ с Gram-матрицей $G$ ($G_{ij} = \langle u_i, u_j\rangle$). Тогда для каждого $k \ge 1$ векторы $u_i^{\otimes k}$ — единичные в $(\mathbb{R}^n)^{\otimes k}$, а их Gram равен $G^{\circ k}$ (entrywise $k$-я степень). Следовательно $G^{\circ k} \succeq 0$ для всех $k$.

Условия применимости. Любые векторы (необязательно единичные). Полезно когда хочется «дотащить» спектральное / определительное условие до асимптотики $k\to\infty$.

Идея доказательства. $\langle u^{\otimes k}, v^{\otimes k}\rangle = \langle u, v\rangle^k$ — прямое раскрытие тензорного произведения. Подставив в формулу Gram'а, получаем покомпонентную $k$-ю степень.

Варианты и обобщения.
- Schur product theorem: PSD матрицы замкнуты относительно Hadamard product, поэтому из PSD $G$ автоматически $G^{\circ k}$ PSD.
- Аналог для Hermitian unit векторов в $\mathbb{C}^n$ — то же самое.

Используется в. [IMC-2010-5 (доказывает $1 + 2(abc)^k - a^{2k} - b^{2k} - c^{2k} \ge 0$ для $a, b, c \in [-1, 1]$ через PSD $3\times 3$ Gram'а тензорных степеней)].

---

### E12. QR-разложение и Gram–Schmidt

Формулировка. Для матрицы $A \in \mathbb{R}^{n\times m}$ ($n \ge m$) с лин. независимыми столбцами существует разложение $A = QR$, где $Q \in \mathbb{R}^{n\times m}$ имеет ortho-нормированные столбцы, $R \in \mathbb{R}^{m\times m}$ — верхне-треугольная с положительными диагональными элементами. Разложение единственно.

Условия применимости. Лин. независимость столбцов; иначе $R$ имеет нули на диагонали (модифицированный Gram–Schmidt всё равно работает с разрешением лин. зависимостей).

Идея доказательства. Gram–Schmidt: $q_i = (a_i - \sum_{j<i} \langle a_i, q_j\rangle q_j)/r_{ii}$, где $r_{ii}$ — нормировка. Запись в матричном виде: $a_i = \sum_{j\le i} r_{ji} q_j$, что есть $A = QR$.

Варианты и обобщения.
- Numerical stability: модифицированный GS избегает потери ортогональности, вместо классического в численных задачах.
- Householder reflections: $Q$ собирается как произведение симметричных reflection-ов $H_v = I - 2vv^T/\|v\|^2$, более устойчиво численно. $\det H_v = -1$.
- $A^TA = R^TR$ — Cholesky-разложение Gram'а; даёт алгоритм $O(m^3)$ на вычисление $\det A^TA$.

Используется в. Доказательство Hadamard'а через $|\det A| = \prod r_{ii}$. Стандартный мост «ortho-set $\leftrightarrow$ upper-triangular factorization».

---

### E13. Gram matrix как обратимая система над полем (rationality argument)

Формулировка. Пусть $\langle v_i, v_j\rangle \in \mathbb{Q}$ для всех $i, j$, и векторы $v_1, \dots, v_n$ линейно независимы. Тогда матрица $G = (\langle v_i, v_j\rangle)$ обратима, $G^{-1}$ имеет рациональные элементы; следовательно любая система вида $G\lambda = w$ с рациональным $w$ имеет рациональное решение $\lambda \in \mathbb{Q}^n$.

Условия применимости. Поле, замкнутое относительно операций (Q, R, любое подполе). Лин. независимость нужна именно для обратимости.

Идея доказательства. $G$ — symmetric PSD, при лин. независимости PD $\Rightarrow$ обратима. $G^{-1} = \operatorname{adj}(G)/\det G$ — все элементы — отношения многочленов от элементов $G$, значит остаются в Q.

Варианты и обобщения.
- Расширение распадается на «идентификация скалярного произведения»: $\langle v_i, v_j\rangle = (\|v_i\|^2 + \|v_j\|^2 - \|v_i - v_j\|^2)/2$ — если правые части в Q, то Gram в Q.
- Аналог в $\mathbb{F}_p$: при char $\ne 2$ всё работает; при char $= 2$ нужно отдельно (Hermitian форма иначе устроена).

Используется в. [IMC-2006-DAY2-4 (если $\|v_i\|^2$ и $\|v_i - v_j\|^2$ рациональны и $\sum \lambda_i v_i = w$ — рациональный, тогда $\lambda \in \mathbb{Q}^n$)].

---

## Записи — Exotic

### E14. Probabilistic ±1 unit vector (вероятностный метод для ortho-векторов)

Формулировка. Пусть $v_1, \dots, v_d$ — единичные векторы в $\mathbb{R}^d$. Тогда существует единичный вектор $u$ такой что
$$|\langle u, v_i\rangle| \le \frac{1}{\sqrt d} \quad \text{для всех } i.$$
Граница достигается, например, на $v_i = e_i$ и $u = (\pm 1, \dots, \pm 1)/\sqrt d$.

Условия применимости. Только конечномерное вещественное пространство. Для $\mathbb{C}^d$ работает с заменой на эрмитов скаляр.

Идея доказательства. Возьми $u = \sum \varepsilon_i e_i / \sqrt d$ с независимыми $\varepsilon_i \in \{-1, +1\}$ равновероятно. Тогда $\mathbb{E}[\langle u, v_i\rangle^2] = \sum_j v_{ij}^2 / d = \|v_i\|^2/d = 1/d$. Существует $\varepsilon$ с $\max_i \langle u, v_i\rangle^2 \le 1/d$ (не сразу — нужно усреднить по worst-case через минимакс или предельный переход; стандартный probabilistic: при строгом $<$ получаем по мат. ожиданию хотя бы один $u$, дальше предельный случай — компактностью).

Варианты и обобщения.
- KKL-style derandomization: можно построить $u$ детерминированно за полиномиальное время (linear-algebra construction).
- Multi-vector: для $d$ обобщается до $\sum |\langle u, v_i\rangle|^2 \le m/d$ (тривиально из Bessel).

Используется в. [IMC-2013-DAY2-3 (8) (точная формулировка: для $v_1, \dots, v_d$ единичных найти $u$ с $|\langle u, v_i\rangle| \le 1/\sqrt d$)].

---

### E15. Mutually obtuse / acute vectors — абсолютные оценки

Формулировка.

1. (Mutually obtuse) В $\mathbb{R}^n$ количество векторов с попарно строго отрицательными скалярными произведениями $\langle v_i, v_j\rangle < 0$ не превосходит $n+1$. Граница достигается на векторах simplex (центр $\to$ вершины правильного симплекса).
2. (Mutually acute) Количество векторов с $\langle v_i, v_j\rangle > 0$ для всех пар не ограничено сверху (можно взять много векторов в одном open half-space).
3. (Equiangular lines, Gerzon's bound) Количество прямых через $0$ в $\mathbb{R}^n$, попарно образующих равный угол $\alpha \in (0, \pi/2)$, не превосходит $n(n+1)/2$ (для $\mathbb{C}^n$ — $n^2$).

Условия применимости. (1) — тонкое, опирается на размерность. (3) — оценка через PSD-аргумент в пространстве симметричных матриц.

Идея доказательства. (1) Если $v_1, \dots, v_{n+2}$ попарно obtuse, выберем максимальный лин. независимый поднабор $S$, $|S| = k \le n$. Оставшиеся $n + 2 - k \ge 2$ выражаются как $v = \sum c_i v_i$ ($v_i \in S$), не все $c_i \ge 0$ (иначе $\langle v, v_j\rangle$ для $v_j \in S$ имеет неоднозначный знак — противоречие); противоречие через знак $\langle v, v\rangle$. Стандартное доказательство — индукция по $n$ через проекцию.

(3) Каждой прямой $\ell_i$ сопоставь rank-1 проектор $P_i = v_iv_i^T$ ($v_i$ — ед. вектор $\in \ell_i$). Условие $|\langle v_i, v_j\rangle| = \alpha$ даёт $\operatorname{tr}(P_i P_j) = \alpha^2$ — все $P_i$ имеют одинаковую попарную «корреляцию» в Frobenius inner product. PSD матрица из $\langle P_i, P_j\rangle_F$ должна быть PSD ранга $\le \dim(\operatorname{Sym}_n) = n(n+1)/2$, что даёт оценку.

Варианты и обобщения.
- Lemmens–Seidel: при фиксированном $\alpha = 1/(2k-1)$ для больших $n$ — точная асимптотика $\sim 2(n-1)$ (улучшение за счёт specific $\alpha$).
- Spherical codes, kissing number: смежные проблемы; $\tau_n$ — kissing number в $\mathbb{R}^n$, известно для $n = 1, 2, 3, 4, 8, 24$.

Используется в. (1) — типовой Putnam-стиль; (3) — задачи на максимум числа конфигураций с условием.

---

## Self-test

1. (Инверсия Gram'а) Пусть $v_1, \dots, v_n \in \mathbb{R}^n$ линейно независимы, $G$ — их матрица Грама. Доказать, что коэффициенты разложения $w = \sum \lambda_i v_i$ выражаются как $\lambda = G^{-1}c$, где $c_i = \langle w, v_i\rangle$.

2. (Hadamard-style) Пусть $A \in \mathbb{R}^{n\times n}$ имеет $|a_{ij}| \le 1$. Доказать $|\det A| \le n^{n/2}$ и охарактеризовать случай равенства.

3. (Trace bilinear form) Описать максимальное по размерности подпространство $V \subseteq M_n(\mathbb{R})$ такое что $\operatorname{tr}(XY) = 0$ для всех $X, Y \in V$. Чему равна максимальная размерность?

4. (Sum-of-squares projection) Пусть $u_1, \dots, u_m$ — единичные векторы в $\mathbb{R}^n$. Доказать, что для любого $x$ выполнено $\sum |\langle x, u_i\rangle|^2 \le \|x\|^2 \cdot \|U\|_{op}^2$, где $U$ — матрица со столбцами $u_i$ и $\|\cdot\|_{op}$ — operator norm.

5. (Obtuse) Доказать, что в $\mathbb{R}^n$ нельзя выбрать $n + 2$ ненулевых векторов с попарно строго отрицательными скалярными произведениями.

6. (Tensor power) Для $a, b, c \in [-1, 1]$ доказать $1 + 2(abc)^k \ge a^{2k} + b^{2k} + c^{2k}$ для всех целых $k \ge 1$.

7. (Random unit vector) Дано $d$ единичных векторов $v_1, \dots, v_d \in \mathbb{R}^d$. Найти единичный $u$ с $|\langle u, v_i\rangle| \le 1/\sqrt d$ для каждого $i$.

8. (Gram rationality) Пусть $v_1, \dots, v_n \in \mathbb{R}^n$ линейно независимы, все $\|v_i\|^2 \in \mathbb{Q}$ и $\|v_i - v_j\|^2 \in \mathbb{Q}$. Доказать, что для любого $w$ с $\|w\|^2, \|w - v_i\|^2 \in \mathbb{Q}$ единственное $\lambda$ с $w = \sum \lambda_i v_i$ имеет рациональные координаты.

9. (Steinitz, ослабленная) Пусть $v_1, \dots, v_n \in \mathbb{R}^d$, $\|v_i\| \le 1$. Доказать существование перестановки $\sigma$ с $\|v_{\sigma(1)} + \dots + v_{\sigma(k)}\| \le \sqrt n$ для всех $k \le n$. (Замечание: оригинальный Steinitz даёт $\le d$ при условии $\sum v_i = 0$, что сильнее, но требует более тонкого жадного шага.)

10. (Idempotent) Пусть $A, B \in M_n(\mathbb{R})$ — ортогональные проекции, $A + B$ тоже ортогональная проекция. Доказать $AB = 0$.

## Решения

1. $\langle w, v_j\rangle = \sum \lambda_i \langle v_i, v_j\rangle = (G\lambda)_j$, откуда $\lambda = G^{-1}c$. Обратимость $G$ — из лин. независимости (E1).

2. Hadamard: $|\det A| \le \prod \|a_i\| \le \prod \sqrt n = n^{n/2}$. Равенство $\iff$ строки попарно ортогональны и нормы $\sqrt n$, т.е. $A$ — Hadamard matrix; существование при $n = 1, 2$ или $n \equiv 0 \pmod 4$ (необходимое условие).

3. Билинейная форма $B(X, Y) = \operatorname{tr}(XY)$ симметрична, на $\operatorname{Sym}$ совпадает с Frobenius (PD), на $\operatorname{Skew}$ — с минус-Frobenius (ND); сигнатура $(n(n+1)/2, n(n-1)/2)$. Подставляя $X = Y \in V$: $\operatorname{tr}(X^2) = 0$ для всех $X \in V$ — $V$ изотропно. Утверждение: $V \cap \operatorname{Sym} = 0$ (если $S \in V \cap \operatorname{Sym}$, $\operatorname{tr}(S^2) = \|S\|_F^2 = 0 \Rightarrow S = 0$). Тогда $\dim V + \dim \operatorname{Sym} \le n^2$, откуда $\dim V \le n^2 - n(n+1)/2 = n(n-1)/2$. Достижимо на строго верхне-треугольных матрицах: $X, Y$ строго верхне-треугольные $\Rightarrow XY$ строго верхне-треугольная $\Rightarrow \operatorname{tr}(XY) = 0$. Ответ: $\boxed{n(n-1)/2}$.

4. $\sum |\langle x, u_i\rangle|^2 = \|U^Tx\|^2 \le \|U^T\|_{op}^2 \|x\|^2 = \|U\|_{op}^2 \|x\|^2$ (operator norm самосопряжённого = max singular value, и $\|U\|_{op} = \|U^T\|_{op}$). Equality при $x$ — собственный вектор $UU^T$ с максимальным собственным значением.

5. Индукция по $n$. База $n = 1$: на прямой не более $2$ ненулевых векторов c $\langle v_i, v_j\rangle < 0$ (т.е. разных знаков), $2 < 3 = n+2$. Шаг: пусть $v_1, \dots, v_{n+2}$ попарно obtuse в $\mathbb{R}^n$. Спроектируй $v_1, \dots, v_{n+1}$ на $v_{n+2}^\perp$: $u_i = v_i - \frac{\langle v_i, v_{n+2}\rangle}{\|v_{n+2}\|^2} v_{n+2}$. Тогда
$$\langle u_i, u_j\rangle = \langle v_i, v_j\rangle - \frac{\langle v_i, v_{n+2}\rangle \langle v_j, v_{n+2}\rangle}{\|v_{n+2}\|^2}.$$
Первое слагаемое $< 0$; второе — частное двух отрицательных и положительного, т.е. $> 0$, поэтому вычитается $> 0$ из $< 0$, итог $< 0$. Получили $n + 1$ векторов в $v_{n+2}^\perp \cong \mathbb{R}^{n-1}$ попарно obtuse — противоречие индукционному предположению (для $n - 1$ их максимум $n + 1$, что как раз $n + 1$, граница достигается; нужно $\ge n + 2$ для противоречия). Тонкость: при $n - 1 = 0$ или нулевых $u_i$ — отдельный аккуратный аргумент через позитивную лин. комбинацию (см. Aigner–Ziegler).

6. Возьми единичные $x, y, z \in \mathbb{R}^3$ с $\langle x, y\rangle = a$, $\langle y, z\rangle = c$, $\langle z, x\rangle = b$ (существуют при $a, b, c \in [-1, 1]$ удовлетворяющих условию PSD: $1 + 2abc \ge a^2 + b^2 + c^2$ — сама задача начинается с этого случая, иначе тривиально). Их Gram $G = \begin{pmatrix} 1 & a & b \\ a & 1 & c \\ b & c & 1\end{pmatrix}$ PSD. По E11 $G^{\circ k}$ тоже PSD, а $\det G^{\circ k} = 1 + 2(abc)^k - a^{2k} - b^{2k} - c^{2k} \ge 0$.

7. Положи $u = \frac{1}{\sqrt d}\sum \varepsilon_i e_i$ с $\varepsilon_i \in \{-1, +1\}$. Тогда $\mathbb{E}_\varepsilon\bigl[(\langle u, v_i\rangle)^2\bigr] = \mathbb{E}\bigl[\frac{1}{d}\sum_{j,k}\varepsilon_j\varepsilon_k v_{ij}v_{ik}\bigr] = \frac{1}{d}\sum_j v_{ij}^2 = \frac{1}{d}$. По probabilistic method хотя бы одно $\varepsilon$ даёт $\max_i (\langle u, v_i\rangle)^2 \le 1/d$ (если все $> 1/d$ строго, то среднее $> 1/d$ — противоречие). Граничный случай (все $= 1/d$) — отдельно или предельным переходом по компактности сферы.

8. По формуле поляризации $\langle v_i, v_j\rangle = (\|v_i\|^2 + \|v_j\|^2 - \|v_i - v_j\|^2)/2 \in \mathbb{Q}$. Аналогично $\langle w, v_j\rangle \in \mathbb{Q}$. Система $G\lambda = c$ с $G \in \mathbb{Q}^{n\times n}$, $c \in \mathbb{Q}^n$ — обратима (PD из лин. независимости). $\lambda = G^{-1}c \in \mathbb{Q}^n$ (E13).

9. Greedy: на шаге $k$ среди оставшихся $\{v_i : i \notin \sigma(\{1,\dots,k-1\})\}$ выбираем тот $v$, что минимизирует $\|S_{k-1} + v\|$. Утверждение: можно выбрать $v$ с $\langle S_{k-1}, v\rangle \le 0$. Замечание: тут условие $\sum v_i = 0$ не требуется (лишь смягчает). Без него альтернатива — рассматривать пары $\pm v$; в общем случае достаточно: либо $\langle S_{k-1}, v\rangle \le 0$ для какого-то $v$, либо все $\langle S_{k-1}, v\rangle > 0$, тогда брать $-v$ (но нет таких) — нужна точная формулировка задачи. Для версии «$\sum v_i = 0$» имеем $\sum_{v \in \text{rest}} v = -S_{k-1}$, среднее $\langle S_{k-1}, \cdot\rangle$ среди оставшихся $\le 0$. Тогда $\|S_k\|^2 \le \|S_{k-1}\|^2 + 1$, по индукции $\|S_k\|^2 \le k \le n$. Усиление до $\le d$ — точнее греди + триаж по конусу (Bárány).

10. $(A + B)^2 = A + B \Rightarrow A^2 + AB + BA + B^2 = A + B \Rightarrow AB + BA = 0$, т.е. $AB = -BA$. След: $\operatorname{tr}(AB) = -\operatorname{tr}(BA) = -\operatorname{tr}(AB)$, значит $\operatorname{tr}(AB) = 0$. Так как $A, B$ — orthogonal projections, обе PSD, тогда $\operatorname{tr}(AB) = \operatorname{tr}(B^{1/2}AB^{1/2})$, где правая часть — след PSD матрицы $B^{1/2}AB^{1/2}$. След PSD равен нулю $\iff$ сама матрица нулевая, т.е. $B^{1/2}AB^{1/2} = 0 \Rightarrow (A^{1/2}B^{1/2})^* (A^{1/2}B^{1/2}) = 0 \Rightarrow A^{1/2}B^{1/2} = 0 \Rightarrow AB = A^{1/2}(A^{1/2}B^{1/2})B^{1/2} = 0$.
