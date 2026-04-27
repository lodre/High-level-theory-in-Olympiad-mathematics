---
topic: Линейная алгебра
subtopic: "Определители: тождества, Vandermonde, блочные, Cauchy–Binet"
sources:
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Krattenthaler — Advanced Determinant Calculus"
  - "Krattenthaler — Advanced Determinant Calculus: A Complement"
  - "Polya, Szegő — Problems and Theorems in Analysis II"
  - "Engel — Problem-Solving Strategies"
  - "Yufei Zhao — Determinants: Evaluation and Manipulation (UMA Putnam Talk)"
  - "Yufei Zhao — Linear Algebra Tricks for the Putnam"
  - "Aigner, Ziegler — Proofs from THE BOOK (главы про LGV и Cauchy–Binet)"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "Stanley — Enumerative Combinatorics II (LGV, Plücker)"
  - "Horn, Johnson — Matrix Analysis"
problems_referenced:
  - IMC-1994-1
  - IMC-1996-1
  - IMC-1997-DAY2-2
  - IMC-2002-DAY2-1
  - IMC-2007-DAY2-4
  - IMC-2007-DAY2-6
  - IMC-2008-DAY2-5
  - Putnam-1992-B5
  - Putnam-1999-B5
  - Putnam-2005-A4
last_updated: 2026-04-27
---

# Определители: тождества, Vandermonde, блочные, Cauchy–Binet

## Scope
Тождества и техники вычисления / оценки определителей выше уровня базового линала. Vandermonde и его деформации (Cauchy, Frobenius, confluent), блочные тождества и Schur complement, Cauchy–Binet и его комбинаторная инкарнация (Lindström–Gessel–Viennot), Sylvester $\det(I+AB)=\det(I+BA)$, matrix determinant lemma, Hadamard как оценка сверху, Dodgson condensation. Плюс рабочий арсенал row/column-операций для типовых IMC-матриц вида $f(i,j)$ и трёхдиагонального типа.

## Записи — Core

### E1. Vandermonde determinant (определитель Вандермонда)

Формулировка. Для $x_1, \dots, x_n$ из любого поля
$$V(x_1, \dots, x_n) = \det\bigl(x_j^{i-1}\bigr)_{i,j=1}^n = \prod_{1 \le i < j \le n}(x_j - x_i).$$
Отсюда: $V \neq 0 \iff$ все $x_i$ различны. Inverse $V^{-1}$ выражается через elementary symmetric polynomials.

Условия применимости. Любое поле / коммутативное кольцо. Для прямоугольной $n \times m$ матрицы $V_{ij} = x_j^{i-1}$ ($n \le m$) Cauchy–Binet даёт $\det(VV^T) = \sum_{S} \bigl(\prod_{i<j, i,j \in S}(x_j - x_i)\bigr)^2$.

Идея доказательства. Полиномиальная: правая часть делится на $V$ как многочлен от $x_j$ (зануляется при $x_i = x_j$), степени совпадают, старший коэффициент $= 1$. Альтернатива — индукция через row operation $R_i \mapsto R_i - x_1 R_{i-1}$.

Варианты и обобщения.
- Confluent Vandermonde (E8) — повторяющиеся узлы, заменяемые производными.
- Generalised Vandermonde $\det(x_j^{a_i})$ с возрастающими $a_i$ — даёт Schur polynomials через bialternant Jacobi: $s_\lambda = \det(x_j^{\lambda_i + n - i}) / V$.
- Identity $\det(P_{i-1}(x_j)) = V(x_1, \dots, x_n)$ для любой системы monic polynomials $P_k$ степени $k$ (row reduction по leading terms). Полезно для Hermite / Legendre / Chebyshev узлов.
- Vandermonde matrix всегда невырождена ⇒ интерполяционная задача Lagrange имеет единственное решение.

Используется в. [IMC-1994-1, IMC-2007-DAY2-6 (через row reduction до диагонали $(1-x^2)^{n-1}$)], типовая редукция любого определителя $\det(P_k(x_j))$ — переход к monic базису $1, x, \dots, x^{n-1}$ через row-операции.

---

### E2. Block determinant formulas (формулы блочного определителя) и Schur complement (дополнение Шура)

Формулировка. Для блоков $A$ ($m \times m$), $B$ ($m \times n$), $C$ ($n \times m$), $D$ ($n \times n$):
$$\det\begin{pmatrix} A & B \\ C & D \end{pmatrix} = \det(A) \det(D - CA^{-1}B) \quad \text{при } A \text{ invertible}$$
$$= \det(D) \det(A - BD^{-1}C) \quad \text{при } D \text{ invertible}.$$
Schur complement $A/D := A - BD^{-1}C$. Если $A, B, C, D$ попарно коммутируют ($n = m$) и $D$ invertible — упрощается до $\det(AD - BC)$. Если только $C, D$ коммутируют — $\det(AD - BC)$ тоже верно.

Условия применимости. Один из диагональных блоков должен быть invertible (или нужно перейти к пределу через $A + \varepsilon I$, что часто работает по плотности). Для $\det(AD - BC)$ при $n = m$ ключевое — коммутация одной пары (обычно $CD = DC$).

Идея доказательства. Block-LU разложение
$$\begin{pmatrix} A & B \\ C & D \end{pmatrix} = \begin{pmatrix} I & 0 \\ CA^{-1} & I \end{pmatrix} \begin{pmatrix} A & 0 \\ 0 & D - CA^{-1}B \end{pmatrix} \begin{pmatrix} I & A^{-1}B \\ 0 & I \end{pmatrix}.$$
Случай $\det(AD - BC)$ при $CD = DC$: домножить справа на $\begin{pmatrix} D & 0 \\ -C & I \end{pmatrix}$, получить блочно-треугольную с $AD - BC$ в углу.

Варианты и обобщения.
- Fischer's inequality: для positive semi-definite $H = \begin{pmatrix}A & B \\ B^* & D\end{pmatrix}$ имеем $\det(H) \le \det(A)\det(D)$.
- Quotient property: $(M/D)/(A/D) = M/A$ — для последовательного шурирования.
- Расщепление $\det(M) > 0$ через критерий Sylvester: positive definiteness $\iff$ ведущие миноры $> 0$.

Используется в. [IMC-1997-DAY2-2 (через $M \cdot M^{-1}$ блочно)], [IMC-2008-DAY2-5 (decomposition по чётности $i+j$)], также основа для E4 (Sylvester) и E5 (matrix determinant lemma).

---

### E3. Cauchy–Binet formula (формула Коши–Бине)

Формулировка. Для $A$ размера $m \times n$, $B$ размера $n \times m$ ($m \le n$):
$$\det(AB) = \sum_{S \subset \{1, \dots, n\}, |S| = m} \det(A_{[m], S}) \det(B_{S, [m]}),$$
где $A_{[m], S}$ — подматрица $A$ из всех строк и столбцов с индексами в $S$, аналогично $B_{S, [m]}$.

Условия применимости. Произвольное коммутативное кольцо. При $m > n$ обе части $= 0$. При $m = n$ восстанавливается $\det(AB) = \det(A)\det(B)$.

Идея доказательства. Наиболее короткий путь — через exterior algebra: $\det(AB) = \Lambda^m(AB) = \Lambda^m(A) \Lambda^m(B)$ как операторы $\Lambda^m \mathbb{F}^m \to \Lambda^m \mathbb{F}^m$, разворачивая в базис $e_S$. Альтернативно — через LGV (E10) или через identity $\det(I_m - tAB) = \det(I_n - tBA)$ с раскладкой по степеням $t$.

Варианты и обобщения.
- Generalised Cauchy–Binet: для произвольных подмножеств строк / столбцов миноров $\det((AB)_{I,J}) = \sum_{|S|=k} \det(A_{I,S}) \det(B_{S,J})$.
- $\det(AB^T) \ge 0$ для real $A, B$ одного размера — частный случай (квадрат суммы) для $A = B$, и Cauchy–Schwarz для общих $A, B$.
- Plücker / Grassmann коэффициенты $\det(A_{[m], S})$ как координаты строки $\Lambda^m A$ в базисе $\{e_S\}$.

Используется в. Standard tool для Gram-определителей $\det(AA^T) = \sum_S \det(A_{[m], S})^2 \ge 0$, что даёт Cauchy–Schwarz / Hadamard. Активно используется в комбинаторных задачах (LGV, E10) и в задачах с подсчётом перестановок / spanning trees (matrix-tree theorem).

---

### E4. Sylvester's determinant identity (тождество Сильвестра): $\det(I + AB) = \det(I + BA)$

Формулировка. Для $A$ размера $m \times n$, $B$ размера $n \times m$ (любые поля)
$$\det(I_m + AB) = \det(I_n + BA).$$
Эквивалентно: $\det(\lambda I_m - AB) \cdot \lambda^n = \det(\lambda I_n - BA) \cdot \lambda^m$ — характеристические многочлены $AB$ и $BA$ совпадают с точностью до множителя $\lambda^{|m-n|}$.

Условия применимости. Прямоугольные матрицы, любое поле. Спектральная версия: ненулевые eigenvalues $AB$ и $BA$ совпадают (с учётом алгебраической кратности).

Идея доказательства. Блочная: $\det\begin{pmatrix} I_m & -A \\ B & I_n \end{pmatrix}$ вычисляется двумя способами через Schur complement (E2) — получается обе стороны.

Варианты и обобщения.
- Trace identity $\operatorname{tr}((AB)^k) = \operatorname{tr}((BA)^k)$ для всех $k$ — следует из спектральной версии (или прямо из cyclic invariance).
- Weinstein–Aronszajn identity (физика, perturbation theory) — та же формула в формулировке через rank-$k$ возмущения.
- $\det(I + AB) \ge 0$ если $AB$ similar to $A^* A$ — следует из $\det(I + B^*B) \ge 1$ для real positive case.

Используется в. Стандартный приём: «уменьшить размер матрицы». Если $AB$ имеет большой размер $m$, но $\operatorname{rank}(AB) = n \ll m$, переход к $BA$ даёт $n \times n$ задачу. Появляется регулярно на Putnam / IMC при работе с rank-low возмущениями.

---

### E5. Matrix determinant lemma (лемма об определителе при rank-$k$ возмущении)

Формулировка. Rank-1: для invertible $A$, векторов $u, v$
$$\det(A + uv^T) = \det(A) \cdot (1 + v^T A^{-1} u).$$
Rank-$k$: для $A$ ($n \times n$) invertible, $U, V$ ($n \times k$)
$$\det(A + UV^T) = \det(A) \cdot \det(I_k + V^T A^{-1} U).$$
Особый случай $A = I_n$: $\det(I_n + UV^T) = \det(I_k + V^T U)$ — частный случай Sylvester (E4).

Условия применимости. $A$ invertible (или предельный переход). Поле произвольное.

Идея доказательства. Через Schur complement (E2) для блочной матрицы $\begin{pmatrix} A & -U \\ V^T & I_k \end{pmatrix}$ — раскрытие двумя способами.

Варианты и обобщения.
- Sherman–Morrison(–Woodbury): $(A + UV^T)^{-1} = A^{-1} - A^{-1} U (I_k + V^T A^{-1} U)^{-1} V^T A^{-1}$. В паре с E5 — основной инструмент для rank-$k$ updates.
- Cauchy expansion: $\det(A + xJ) = \det(A) + x \cdot \mathbf{1}^T \operatorname{adj}(A) \mathbf{1}$, где $J$ — all-ones rank-1.
- Rank-$k$ generalisation: spectrum of $A + UV^T$ изменяется только в $\le k$ ненулевых eigenvalues по сравнению с $A$ (если коммутируют — точно).

Используется в. Задачи на матрицы вида «$c \cdot I + uv^T$», «$\alpha I + \beta J$», «единицы плюс возмущение». Putnam 2005 A4 (через $HH^T = nI$ + rank-1 трюк), типовые «найти $\det$ матрицы $n \times n$, у которой все элементы равны $a$, кроме диагонали $b$»: $\det = (b-a)^{n-1}(b + (n-1)a)$.

---

## Записи — Standard

### E6. Cauchy determinant (определитель Коши)

Формулировка. Для попарно различных $a_1, \dots, a_n$ и $b_1, \dots, b_n$ с $a_i + b_j \neq 0$:
$$\det\left(\frac{1}{a_i + b_j}\right)_{i,j=1}^n = \frac{\prod_{1 \le i < j \le n}(a_i - a_j)(b_i - b_j)}{\prod_{i,j=1}^n (a_i + b_j)}.$$

Условия применимости. Поля характеристики $0$ (или достаточно большие). При $a_i = b_i = i - 1/2$ — Hilbert determinant $\det(1/(i + j - 1)) = \prod (i!)^2 / (2i)!$ комбинаторики.

Идея доказательства. Многочлен от $a_n$ по строке $n$: знаменатель $\prod_j(a_n + b_j)$, числитель — многочлен степени $n-1$ от $a_n$ с корнями $a_1, \dots, a_{n-1}$. По Vandermonde (E1) на $a_i$ и $b_j$ восстанавливается общий множитель.

Варианты и обобщения.
- Frobenius determinant $\det(1/(1 - x_i y_j)) = \prod (x_i - x_j)(y_i - y_j) / \prod(1 - x_i y_j)$ — мультипликативный аналог.
- Borchardt $\det\bigl(1/(a_i - b_j)^2\bigr) = \det\bigl(1/(a_i - b_j)\bigr) \cdot \operatorname{perm}\bigl(1/(a_i - b_j)\bigr)$.
- Положительность $\det(1/(a_i + b_j)) > 0$ при $a_i, b_j > 0$, упорядоченных монотонно — Cauchy matrix totally positive.

Используется в. Hilbert-определитель (Putnam-classic). Доказательство положительности интегральных операторов через ядро $1/(x+y)$.

---

### E7. Circulant determinant (определитель циркулянта) и DFT-диагонализация

Формулировка. Circulant matrix $C = \operatorname{circ}(c_0, c_1, \dots, c_{n-1})$ диагонализуется матрицей DFT (Discrete Fourier Transform): eigenvalues — $p(\omega^k)$, где $\omega = e^{2\pi i / n}$, $p(x) = c_0 + c_1 x + \dots + c_{n-1} x^{n-1}$. Отсюда
$$\det(C) = \prod_{k=0}^{n-1} p(\omega^k).$$
Block-circulant — то же с заменой scalar $p$ на multivariate matrix polynomial.

Условия применимости. Любое поле, содержащее корни $n$-й степени из $1$ (для общего поля — $\det(C) = \operatorname{Res}(p(x), x^n - 1)$).

Идея доказательства. Eigenvector $(1, \omega^k, \omega^{2k}, \dots, \omega^{(n-1)k})$ для eigenvalue $p(\omega^k)$ проверяется напрямую. DFT матрица $F = (\omega^{ij}/\sqrt{n})$ диагонализует все circulant сразу.

Варианты и обобщения.
- Skew-circulant — eigenvalues на корнях $-1$.
- Циркулянт встречается как $\operatorname{adj}(C_n) = \operatorname{circ}(\dots)$ для $n$-цикла.
- Block-circulant: $\det(C) = \prod_k \det(P(\omega^k))$, где $P$ — matrix-valued polynomial.

Используется в. [IMC-2007-DAY2-4 (циклическая матрица смежности $C_n$)], [Putnam-1999-B5], типовые задачи на матрицы с записью $a_{ij} = f((i-j) \bmod n)$.

---

### E8. Confluent Vandermonde (конфлюэнтный Вандермонд)

Формулировка. При $\lambda_1, \dots, \lambda_r$ различных с кратностями $m_1, \dots, m_r$, $\sum m_k = n$, матрица $V_\Lambda$ имеет блок строк для каждого $\lambda_k$: $\bigl(\binom{j-1}{i-1}\lambda_k^{j-i}\bigr)$ — производные строки Vandermonde до порядка $m_k - 1$. Тогда
$$\det(V_\Lambda) = \prod_{1 \le i < j \le r}(\lambda_j - \lambda_i)^{m_i m_j}.$$

Условия применимости. Поля характеристики $0$ (для биномиальных коэффициентов и производных).

Идея доказательства. Предельный переход в стандартном Vandermonde при склеивании $m_k$ узлов — производные нужного порядка появляются автоматически (правило Лопиталя для $\prod(x_i - x_j)$, делённого на $0/0$).

Варианты и обобщения.
- Hermite interpolation: $V_\Lambda$ — матрица, выражающая значения функции и её производных в узлах через коэффициенты многочлена.
- Inverse confluent Vandermonde — выражение через partial fraction decomposition.
- Применение в задачах на повторяющиеся корни характеристического многочлена.

Используется в. Задачи на линейные рекурренции с кратными корнями, на дифференциальные уравнения с постоянными коэффициентами, на ranks of confluent matrices.

---

### E9. Hadamard's inequality (неравенство Адамара)

Формулировка. Для любой $n \times n$ матрицы $A$ с строками $r_1, \dots, r_n$
$$|\det(A)| \le \prod_{i=1}^n \|r_i\|_2.$$
Эквивалентно для столбцов. Для positive semi-definite $H$: $\det(H) \le \prod_i H_{ii}$.

Условия применимости. Любое скалярное произведение (real / complex). Equality $\iff$ строки попарно ортогональны (или одна из них $= 0$).

Идея доказательства. Применение Gram–Schmidt: $|\det A|^2 = \det(AA^T) = \prod \|r_i'\|^2 \le \prod \|r_i\|^2$, где $r_i'$ — orthogonalised. Альтернатива — AM–GM на eigenvalues $AA^T$ + $\det(AA^T)$ как произведение $\le$ trace$/n$ в степени $n$.

Варианты и обобщения.
- Fischer's inequality (расширение E2): $\det(H) \le \det(H_{11}) \det(H_{22})$ для PSD блочной $H$.
- Hadamard maximum problem: $|\det A| \le n^{n/2}$ при $|a_{ij}| \le 1$, equality $\iff$ Hadamard matrix (существует при $n \in \{1, 2, 4k\}$ — гипотеза).
- Volume interpretation: $|\det|$ — объём параллелепипеда, $\prod \|r_i\|$ — объём ограничивающего box.

Используется в. [Putnam-2005-A4 (через $HH^T = nI$)], граничные оценки для $\det$, оценки в задачах на $\pm 1$ матрицы.

---

### E10. Lindström–Gessel–Viennot lemma (лемма ЛГВ)

Формулировка. Acyclic digraph $D$, веса $w(e)$ на рёбрах. Для источников $A_1, \dots, A_n$ и стоков $B_1, \dots, B_n$ матрица $M$ с $M_{ij} = \sum_{P: A_i \to B_j} w(P)$, где $w(P) = \prod_{e \in P} w(e)$. Тогда
$$\det(M) = \sum_{(P_1, \dots, P_n) \text{ non-intersecting}, P_i: A_i \to B_{\sigma(i)}} \operatorname{sgn}(\sigma) \prod_i w(P_i).$$
В «совместимом» случае (где non-intersecting вынуждает $\sigma = \operatorname{id}$): $\det(M) = \sum_{(P_i) \text{ non-intersecting}} \prod w(P_i)$.

Условия применимости. Acyclic graph + источники / стоки в положении, когда любая non-intersecting система путей соответствует тождественной перестановке (типичный случай — точки на прямой / antichain).

Идея доказательства. Sign-reversing involution: для пути с пересечением — найти первое пересечение, swap хвостов, получить отображение на пары с противоположным знаком.

Варианты и обобщения.
- Доказательство Cauchy–Binet (E3) через LGV.
- Schur polynomials через LGV на полу-стандартных таблицах (Lindström–Gessel–Viennot applied to lattice paths).
- Matrix-tree theorem связан через подсчёт spanning trees как минор Лапласиана.

Используется в. Задачи на подсчёт non-crossing объектов (плоские деревья, Dyck paths, tilings). На IMC реже, но регулярно на Putnam / Schweitzer и в комбинаторных задачах с определителями.

---

### E11. Desnanot–Jacobi / Dodgson condensation (конденсация Доджсона)

Формулировка. Для $n \times n$ матрицы $M$ обозначим $M^{i,j}_{k,l}$ — минор после вычёркивания строк $i, j$ и столбцов $k, l$. Тогда
$$\det(M) \cdot \det(M^{1,n}_{1,n}) = \det(M^{1}_{1}) \det(M^{n}_{n}) - \det(M^{1}_{n}) \det(M^{n}_{1}),$$
где $M^i_j$ — минор без строки $i$ и столбца $j$ (по аналогии с двойным минором). Этот же закон — Sylvester's identity для минора $1, n$.

Условия применимости. Промежуточный «центральный» минор $\det(M^{1,n}_{1,n})$ должен быть ненулевым (или дополнить $\varepsilon$-возмущением). Поле произвольное.

Идея доказательства. Применить Schur complement (E2) к блочной форме $M$, разделив по углам $1$ и $n$. Альтернатива — через Plücker-соотношения / Dodgson's оригинальный induction.

Варианты и обобщения.
- General Sylvester's identity (E14): тот же закон для произвольной пары минор-внутри-минора.
- Recursive computation of $\det$: на каждом шаге размер уменьшается на $1$, нужны только $2 \times 2$ операции — практический метод для small structured matrices.
- Связь с Aztec diamond / alternating sign matrices.

Используется в. Хороший приём для вычисления $\det$ малых параметризованных матриц, где видно паттерн миноров. Реже в IMC, чаще в Schweitzer / комбинаторных задачах.

---

### E12. Tridiagonal determinant recurrence (трёхдиагональный определитель: трёхчленное соотношение)

Формулировка. Для трёхдиагональной матрицы $T_n$ с диагональю $a_i$, поддиагональю $b_i$, наддиагональю $c_i$ ($i = 1, \dots, n$):
$$D_n = a_n D_{n-1} - b_n c_{n-1} D_{n-2}, \quad D_0 = 1, \, D_1 = a_1.$$
Это даёт линейное рекуррентное соотношение второго порядка от $n$ — характеристическое уравнение даёт замкнутую формулу через корни $\lambda^2 = a\lambda - bc$ при постоянных коэффициентах.

Условия применимости. Любое поле. Для постоянных $a, b, c$: $D_n$ выражается через Chebyshev-like polynomials. Например, $a = 2x, b = c = 1$ даёт $D_n = U_n(x)$ — Chebyshev second kind.

Идея доказательства. Раскрытие $\det T_n$ по последней строке: один член даёт $a_n D_{n-1}$, второй (через cofactor по $(n, n-1)$) даёт $b_n c_{n-1} D_{n-2}$ со знаком.

Варианты и обобщения.
- Pentadiagonal — рекурренция четвёртого порядка.
- Block-tridiagonal — то же, но для $\det$ в блоках; нужно обращение блока.
- Cyclic tridiagonal — отдельная формула с поправкой на циклические углы.

Используется в. [IMC-1996-1 (рекурренция к нижнетреугольной с диагональю $2d$)], [IMC-2007-DAY2-4 (циркулянтная триадиагональная)], типовая редукция через row operations.

---

### E13. Row/column operation arsenal: $f(|i-j|)$, $\min(i,j)$, $\binom{i+j}{j}$ типы

Формулировка. Группа эвристик для матриц $a_{ij} = f(i, j)$ специальной формы:
1. $a_{ij} = f(i + j)$ или $f(i - j)$ (Toeplitz / Hankel): субтракция $R_i \to R_i - R_{i+1}$ часто понижает ранг возмущения.
2. $a_{ij} = f(|i - j|)$: $R_i \to R_i - R_{i+1}$ создаёт антисимметрию знаков, после второй итерации — почти двудиагональная.
3. $a_{ij} = \min(i, j)$ или $\max(i, j)$: subtraction даёт нижнетреугольную с единицами на диагонали — $\det = 1$ для $\min$ на $1, \dots, n$, $\det = (-1)^{n-1} n$ для $\max$.
4. $a_{ij} = \binom{i+j}{j}$ или Pascal-like: $R_i \to R_i - R_{i-1}$ даёт сдвинутую Pascal — определитель $= 1$ через индукцию.
5. $a_{ij} = x^{|i-j|}$: $R_i \to R_i - x R_{i-1}$ убивает внедиагональную часть, $\det = (1 - x^2)^{n-1}$.

Условия применимости. Эвристика; работает за счёт того, что разностные операторы превращают «гладкие» по индексам матрицы в low-rank структуры.

Идея доказательства. На каждом шаге $\det$ инвариантен относительно $R_i \to R_i + \alpha R_j$. После серии операций матрица приводится к треугольной — $\det = \prod \text{диаг}$.

Используется в. [IMC-2002-DAY2-1 ($(-1)^{|i-j|}$ → телескопирование → $n+1$)], [IMC-2007-DAY2-6 ($x^{|i-j|}$ → $(1-x^2)^{n-1}$)], классические задачи $\det(\min(i,j)) = 1$, $\det(|i-j|) = (-1)^{n-1}(n-1)2^{n-2}$.

---

## Записи — Exotic

### E14. Sylvester's identity for compound determinants (тождество Сильвестра для составных миноров)

Формулировка. Для $n \times n$ матрицы $M$ зафиксируем подмножество $K \subset \{1, \dots, n\}$, $|K| = k$. Определим $(n-k) \times (n-k)$ матрицу $M_K^*$ со входами
$$(M_K^*)_{i,j} = \det\bigl(M[K \cup \{i\}, K \cup \{j\}]\bigr), \quad i, j \notin K.$$
Тогда
$$\det(M_K^*) = \det(M[K, K])^{n-k-1} \cdot \det(M).$$
При $k = n - 2$ восстанавливается Desnanot–Jacobi (E11).

Условия применимости. Произвольное коммутативное кольцо. Без дополнительных условий — формула универсальная.

Идея доказательства. Cauchy–Binet или прямая блочная редукция. Альтернативная формулировка — через compound matrix $\Lambda^k M$ и его свойства.

Варианты и обобщения.
- Plücker relations — следствия для координат подпространств в $\Lambda^k$.
- Используется в задачах на матроиды и алгебраическую комбинаторику.

Используется в. Редко на IMC напрямую, но часто как «секретный соус» в задачах про определители миноров. Появляется в Schweitzer и в продвинутых комбинаторных задачах.

---

### E15. Smith normal form (нормальная форма Смита) и определительные делители

Формулировка. Для целочисленной (или над PID) $n \times n$ матрицы $M$ существует разложение $M = P \cdot D \cdot Q$, где $P, Q$ — unimodular ($\det = \pm 1$), $D$ — диагональная с $d_1 | d_2 | \dots | d_n$. При этом
$$d_1 \cdot d_2 \cdots d_k = \gcd \text{ всех } k \times k \text{ миноров } M,$$
и $\det(M) = \prod d_i$.

Условия применимости. PID (Principal Ideal Domain): $\mathbb{Z}$, $\mathbb{F}[x]$, локальные кольца. Над полем — все $d_i = 1$ для невырожденной, и форма Смита тривиальна.

Идея доказательства. Алгоритмический Gauss с заменой на gcd/lcm — последовательное обнуление.

Варианты и обобщения.
- Cokernel structure: $\mathbb{Z}^n / M \mathbb{Z}^n \cong \bigoplus \mathbb{Z}/d_i\mathbb{Z}$ — даёт structure theorem для абелевых групп.
- Применение к $\det$: для интегральной $M$ с $\det(M) = $ заданное число, Smith form контролирует структуру через делители.

Используется в. Задачи на $\det A_{ij} = \gcd(i, j)$ (Putnam-1992-B5: $\det(\gcd(i,j))_{i,j=1}^n = \prod \varphi(k)$ через теоретико-числовой Smith), задачи на $\det$ с целочисленными ограничениями, цикловые матрицы и Smith over $\mathbb{Z}[x]$.

---

## Self-test

1. Вычисли $\det\bigl(\binom{x_i}{j-1}\bigr)_{i,j=1}^n$, где $x_i$ — формальные переменные, $\binom{x}{k} = x(x-1)\cdots(x-k+1)/k!$.

2. Найди $\det A$, где $A_{ij} = i + j$ (для $1 \le i, j \le n$, $n \ge 3$).

3. Для $n \ge 2$ вычисли $\det A$, где $A_{ij} = \cos((i-1)\theta_j)$, а $\theta_j$ — попарно различные углы из $(0, \pi)$.

4. Пусть $A$ — действительная $n \times n$, $|A_{ij}| \le 1$. Докажи $|\det(A)| \le n^{n/2}$.

5. Покажи, что $\det\Bigl(\frac{1}{i + j - 1}\Bigr)_{i,j=1}^n > 0$ и найди явную формулу.

6. Пусть $u, v \in \mathbb{R}^n$, $A$ — invertible $n \times n$. Найди $\det(A + uv^T)$ через $\det(A)$ и $A^{-1}$.

7. Пусть $A$ — $m \times n$ матрица, $B$ — $n \times m$. Покажи, что характеристические многочлены $AB$ и $BA$ совпадают с точностью до множителя $\lambda^{|m-n|}$.

8. Вычисли $\det A_n$, где $A_n$ — $n \times n$ матрица с $A_{ij} = \min(i, j)$.

9. Пусть $C = \operatorname{circ}(0, 1, 0, \dots, 0, 1)$ — циклическая матрица смежности $n$-цикла. Найди $\det C$ при нечётном $n$.

10. Дано: $A$ — $n \times n$ матрица, у которой $\det \bigl(A_{[i_1, i_2], [j_1, j_2]}\bigr) = 0$ для всех пар индексов. Что можно сказать о $\operatorname{rank}(A)$?

---

## Решения

1. Через row operations $R_i \to R_i - R_{i-1}$ (или прямо: $\binom{x}{k}$ — многочлен степени $k$ по $x$ с старшим коэффициентом $1/k!$) приводим к верхнетреугольной с диагональю $1/((i-1)!)$. Базис $\{\binom{x}{k}\}$ — monic после нормировки, поэтому в Vandermonde $\det\bigl(P_{i-1}(x_j)\bigr) = V(x_1, \dots, x_n) / \prod_{k=0}^{n-1} k! = \prod_{i<j}(x_j - x_i) / \prod_{k=0}^{n-1} k!$.

2. $A_{ij} = i + j = i \cdot 1 + 1 \cdot j$, то есть $A = u \mathbf{1}^T + \mathbf{1} v^T$ — сумма двух rank-1. При $n \ge 3$ ранг $\le 2 < n$, значит $\det A = 0$. При $n = 2$: $\det \begin{pmatrix}2&3\\3&4\end{pmatrix} = -1$.

3. Через тождество $\cos(k\theta) = T_k(\cos\theta)$, где $T_k$ — Chebyshev первого рода — monic после нормировки $T_k(x) = 2^{k-1} x^k + \dots$ для $k \ge 1$, $T_0 = 1$. Значит матрица $(T_{i-1}(\cos\theta_j))$ через row-reduction до Vandermonde на $\cos\theta_j$: $\det = 2^{0+1+\dots+(n-2)} \prod_{i<j}(\cos\theta_j - \cos\theta_i) = 2^{(n-1)(n-2)/2} \cdot V(\cos\theta_1, \dots, \cos\theta_n)$.

4. Hadamard (E9): $|\det A|^2 = \det(AA^T) \le \prod \|r_i\|^2 \le \prod n = n^n$. Извлечение корня даёт $|\det A| \le n^{n/2}$.

5. Cauchy determinant (E6) с $a_i = i, b_j = j - 1$: $a_i + b_j = i + j - 1$, числитель $\prod_{i<j}(a_i - a_j)(b_i - b_j) = \prod_{i<j}(i-j)^2 = \bigl(\prod_{k=0}^{n-1} k!\bigr)^2$ (Vandermonde на $1,\dots,n$). Итог:
$$\det H_n = \frac{\bigl(\prod_{k=0}^{n-1} k!\bigr)^2}{\prod_{i,j=1}^n (i+j-1)} > 0.$$
Положительность очевидна: и числитель, и знаменатель положительны. Глубже: Cauchy matrix на положительных $a_i, b_j$ — totally positive, все миноры $> 0$.

6. Matrix determinant lemma (E5): $\det(A + uv^T) = \det(A)(1 + v^T A^{-1} u)$.

7. Sylvester (E4): $\det(\lambda I_m - AB) = \lambda^{m-n} \det(\lambda I_n - BA)$ при $m \ge n$ — следует из $\det(I + tAB) = \det(I + tBA)$ как тождество многочленов от $t$ (заменить $t = -1/\lambda$, домножить на $\lambda^m$).

8. $\min(i, j)$ матрица: $R_n \to R_n - R_{n-1}, R_{n-1} \to R_{n-1} - R_{n-2}, \dots, R_2 \to R_2 - R_1$. После этого $A_{ij}$ для $i \ge 2$ становится $1$ при $j \ge i$ и $0$ при $j < i - 1$, $0$ при $j = i - 1$ — нет, нужно аккуратнее. Прямо: $A = LL^T$, где $L$ — нижнетреугольная единичная (можно проверить $\sum_k L_{ik}L_{jk} = \min(i,j)$). Значит $\det A = (\det L)^2 = 1$.

9. $C = \operatorname{circ}(0, 1, 0, \dots, 0, 1)$ — соответствует $p(x) = x + x^{n-1}$. Через E7: $\det C = \prod_{k=0}^{n-1} (\omega^k + \omega^{(n-1)k}) = \prod_k \omega^{(n-1)k}(1 + \omega^{-(n-2)k})$. При нечётном $n$: фактор $\omega^{-(n-2)k}$ пробегает все корни $n$-й степени из $1$, $\prod (1 + \zeta) = 1 + (-1)^n = 2$ при чётном — но $n$ нечётное, $\prod_{k=0}^{n-1}(1 + \omega^k) = 1 + (-1)^{n-1} \cdot 1 = 2$. С учётом $\prod \omega^{(n-1)k} = \omega^{(n-1) \cdot n(n-1)/2} = 1$ (нечётное $n$), получаем $\det C = 2$. Значит $\det(C^2) = 4$ (как в IMC-2007-DAY2-4).

10. Если все $2 \times 2$ миноры зануляются — все строки пропорциональны (или нулевые), значит $\operatorname{rank}(A) \le 1$. Это стандартный критерий ранга через миноры: $\operatorname{rank}(A) = $ максимальный размер ненулевого минора.
