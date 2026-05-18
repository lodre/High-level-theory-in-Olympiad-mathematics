---
topic: Линейная алгебра
subtopic: "Tensor / Kronecker product (базово)"
sources:
  - "Horn, Johnson — Topics in Matrix Analysis (гл. 4)"
  - "Horn, Johnson — Matrix Analysis (гл. 7, произведение Адамара)"
  - "Bhatia — Matrix Analysis (GTM 169)"
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Schäcke — On the Kronecker Product (UWaterloo, 2013)"
  - "Bhatia, Rosenthal — How and Why to Solve the Operator Equation AX − XB = Y"
  - "Marcus — Finite Dimensional Multilinear Algebra"
  - "Greub — Multilinear Algebra"
  - "Yufei Zhao — Algebraic Combinatorics (MOP 2007 Black Group)"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "Wikipedia — Kronecker product, Sylvester equation, Schur product theorem, Compound matrix"
problems_referenced:
  - IMC-2004-DAY2-1
  - IMC-2007-DAY2-5
last_updated: 2026-05-18
---

# Tensor / Kronecker product (базово)

## Scope
Произведение Кронекера матриц как координатная запись тензорного произведения операторов. Базовая алгебра: билинейность, ассоциативность, правило смешанного произведения. Поведение спектра, ранга, следа, определителя, норм. Векторизация и матричные уравнения — $AXB = C$, уравнение Сильвестра $AX - XB = C$, уравнение Ляпунова. Кронекерова сумма и теорема Сильвестра–Розенблюма (Sylvester–Rosenblum). Внешние степени, составная матрица и связь с Cauchy–Binet. Теорема Шура о произведении Адамара. Тензорные степени как способ строить экстремальные конструкции (коммутирующие нильпотенты с ненулевым произведением).

## Определения

Везде ниже $F$ — поле, для спектральных утверждений $F = \mathbb{C}$.

**Произведение Кронекера** (Kronecker product) матриц $A \in M_{m \times n}(F)$ и $B \in M_{p \times q}(F)$:
$$A \otimes B = \begin{pmatrix} a_{11} B & \cdots & a_{1n} B \\ \vdots & & \vdots \\ a_{m1} B & \cdots & a_{mn} B \end{pmatrix} \in M_{mp \times nq}(F).$$

**Тензорное произведение пространств** (tensor product) $V \otimes W$ — пространство размерности $\dim V \cdot \dim W$ с базисом $\{e_i \otimes f_j\}$. Если $A\colon V\to V'$ и $B\colon W\to W'$, то $A\otimes B\colon V\otimes W\to V'\otimes W'$ имеет матрицу из определения выше.

**Векторизация** (vec): $\operatorname{vec}\colon M_{m\times n}(F)\to F^{mn}$ ставит столбцы матрицы один под другим.

**Кронекерова сумма**: $A\oplus B := A\otimes I_m + I_n \otimes B$ для $A\in M_n$, $B\in M_m$.

**Произведение Адамара** (Hadamard product): поэлементное $(A\circ B)_{ij} = a_{ij} b_{ij}$ для матриц одинакового размера.

**Внешняя степень** (exterior power) $\Lambda^k V$ — антисимметричная часть $V^{\otimes k}$, размерность $\binom{n}{k}$.

**Составная матрица** (compound matrix) $C_k(A) = \Lambda^k A$ — матрица оператора $\Lambda^k A$ на $\Lambda^k V$; элемент на позиции $(I, J)$, где $|I| = |J| = k$, равен минору $\det A[I, J]$.

## Записи — Основные

### E1. Базовая алгебра произведения Кронекера

**Формулировка.** Операция $A \otimes B$ билинейна по каждому аргументу. Она ассоциативна: $(A\otimes B)\otimes C = A\otimes (B\otimes C)$. Для согласованных $A, B$ выполнены $(A\otimes B)^T = A^T \otimes B^T$ и $(A\otimes B)^* = A^*\otimes B^*$. Операция не коммутативна, однако $A\otimes B$ перестановочно подобна $B\otimes A$ (E12).

**Условия применимости.** Любое поле. Для $T$ и $^*$ — те же, что для обычных $T$ и $^*$.

**Идея.** $A \otimes B$ — матрица оператора $A \otimes B$ на $V \otimes W$ в лексикографическом базисе $e_i\otimes f_j$.

---

### E2. Правило смешанного произведения (mixed product property)

**Формулировка.** Если размеры согласованы (определены произведения $AC$ и $BD$), то
$$(A \otimes B)(C \otimes D) = (AC) \otimes (BD).$$
Следствия:

- $A\otimes B = (A\otimes I_p)(I_n\otimes B) = (I_m\otimes B)(A\otimes I_q)$.
- $(A\otimes B)^k = A^k \otimes B^k$ для квадратных $A, B$.
- Если $A$ и $B$ обратимы, то $(A\otimes B)^{-1} = A^{-1}\otimes B^{-1}$.

**Условия применимости.** Совпадение внутренних размеров: $A \in M_{m\times n}$, $C \in M_{n\times r}$, $B \in M_{p\times q}$, $D \in M_{q\times s}$.

**Идея.** Блочный $(i, j)$-блок левой части равен $\sum_k a_{ik} c_{kj}\, BD = (AC)_{ij}\, BD$.

---

### E3. Спектр произведения Кронекера

**Формулировка.** Пусть $A \in M_n(\mathbb{C})$ имеет собственные значения $\lambda_1, \dots, \lambda_n$ (с алгебраической кратностью), $B \in M_m(\mathbb{C})$ — собственные значения $\mu_1, \dots, \mu_m$. Тогда $A\otimes B$ имеет ровно $nm$ собственных значений вида $\lambda_i \mu_j$. Если $Av = \lambda v$ и $Bw = \mu w$, то $(A\otimes B)(v\otimes w) = \lambda\mu\,(v\otimes w)$.

**Условия применимости.** Поле, в котором характеристические многочлены $A$ и $B$ разлагаются полностью (например $\mathbb{C}$).
Контрпример нужности замыкания: $A = B = \begin{pmatrix}0 & -1\\ 1 & 0\end{pmatrix} \in M_2(\mathbb{R})$ — собственных значений над $\mathbb{R}$ нет; формула «по парам» теряет смысл без перехода в $\mathbb{C}$.

**Идея.** Унитарная триангуляризация Шура: $A = U_A T_A U_A^*$, $B = U_B T_B U_B^*$. По E2:
$$A\otimes B = (U_A\otimes U_B)\,(T_A\otimes T_B)\,(U_A\otimes U_B)^*.$$
Матрица $T_A \otimes T_B$ верхнетреугольная с диагональю $\lambda_i \mu_j$; матрица $U_A \otimes U_B$ унитарна (E10).

---

### E4. След, определитель и ранг произведения Кронекера

**Формулировка.** Для $A \in M_n(F)$, $B \in M_m(F)$:
$$\operatorname{tr}(A\otimes B) = \operatorname{tr}(A)\,\operatorname{tr}(B), \qquad \det(A\otimes B) = (\det A)^m (\det B)^n.$$
Для произвольных прямоугольных $A, B$:
$$\operatorname{rank}(A\otimes B) = \operatorname{rank}(A)\cdot\operatorname{rank}(B).$$
В частности $A\otimes B$ обратима тогда и только тогда, когда обратимы $A$ и $B$.

**Условия применимости.** Любое поле. Для определителя необходимы квадратные $A$ и $B$.

**Идея.** След — сумма $\lambda_i \mu_j = \bigl(\sum \lambda_i\bigr)\bigl(\sum \mu_j\bigr)$, или прямой блочный подсчёт. Определитель — произведение $\lambda_i\mu_j$ по всем парам. Ранг — через сингулярное разложение или ранг-один разложение каждого сомножителя.

---

### E5. Векторизация и тождество $\operatorname{vec}(AXB) = (B^T\otimes A)\operatorname{vec}(X)$

**Формулировка.** Для $A \in M_{p\times m}$, $B \in M_{n\times q}$, $X \in M_{m\times n}$:
$$\operatorname{vec}(AXB) = (B^T \otimes A)\,\operatorname{vec}(X).$$
Частные случаи:

- $\operatorname{vec}(AX) = (I_n \otimes A)\,\operatorname{vec}(X)$;
- $\operatorname{vec}(XB) = (B^T \otimes I_m)\,\operatorname{vec}(X)$.

**Условия применимости.** Согласованные размеры. Любое поле.

**Идея.** $j$-й столбец $AXB$ равен $A X b_j = \sum_k b_{kj}\,A x_k$, где $x_k$ — столбцы $X$. Сбор в один вектор даёт блочное умножение на $B^T \otimes A$.

---

### E6. Кронекерова сумма и теорема Сильвестра–Розенблюма

**Формулировка.** $A\oplus B = A\otimes I_m + I_n \otimes B$ имеет собственные значения $\lambda_i(A) + \mu_j(B)$ (E3, применённое к коммутирующим $A\otimes I$ и $I\otimes B$).

**Теорема Сильвестра–Розенблюма** (Sylvester–Rosenblum). Уравнение $AX - XB = C$ имеет единственное решение $X$ для каждого $C$ тогда и только тогда, когда $\operatorname{spec}(A)\cap\operatorname{spec}(B) = \emptyset$.

**Условия применимости.** Спектры берутся в общем алгебраическом замыкании. Условие пересечения спектров обязательно.
Контрпример: $A = B = I_n$. Тогда $AX - XB = 0$ для любой $X$, и единственного решения уравнения $AX - XB = C$ нет ни при каком $C \neq 0$.

**Идея.** Через E5 оператор $X \mapsto AX - XB$ имеет в координатах $\operatorname{vec}$ матрицу $I \otimes A - B^T \otimes I$. Его собственные значения — $\lambda_i(A) - \mu_j(B)$. Невырожденность эквивалентна непересечению спектров.

---

## Записи — Стандартные

### E7. Тензорное произведение пространств: универсальное свойство

**Формулировка.** $V\otimes W$ — пара $(V\otimes W, \tau)$, где $\tau\colon V \times W \to V\otimes W$ билинейно. Для любой билинейной формы $\beta\colon V\times W \to U$ существует единственное линейное $\tilde\beta\colon V\otimes W \to U$ с $\beta = \tilde\beta \circ \tau$. Размерность мультипликативна: $\dim(V\otimes W) = \dim V \cdot \dim W$.

Канонические изоморфизмы:

- $V^* \otimes W \cong \operatorname{Hom}(V, W)$ через $(\varphi\otimes w)(v) = \varphi(v)\, w$.
- $V^* \otimes V \cong \operatorname{End}(V)$; под этим изоморфизмом след $\operatorname{tr}\colon V^*\otimes V \to F$ — естественное спаривание $\varphi\otimes v \mapsto \varphi(v)$.

**Условия применимости.** Любое поле.

**Идея.** Конструкция через факторизацию свободного модуля $F^{V\times W}$ по соотношениям билинейности. Универсальное свойство определяет $V\otimes W$ единственным образом с точностью до изоморфизма.

---

### E8. Составная матрица и формула Cauchy–Binet

**Формулировка.** Для $A \in M_{m\times n}(F)$ и $1 \le k \le \min(m, n)$ составная матрица $C_k(A)$ имеет размер $\binom{m}{k} \times \binom{n}{k}$; её элементы — миноры $\det A[I, J]$.

Свойства:

- Мультипликативность: $C_k(AB) = C_k(A)\, C_k(B)$. Это формула Cauchy–Binet в матричной форме.
- Для $A \in M_n$ с собственными значениями $\lambda_1, \dots, \lambda_n$ матрица $C_k(A)$ имеет собственные значения $\lambda_{i_1}\cdots\lambda_{i_k}$, $i_1 < \cdots < i_k$.
- $\operatorname{tr} C_k(A) = e_k(\lambda_1, \dots, \lambda_n)$ — $k$-й элементарный симметрический многочлен. Это коэффициенты характеристического многочлена.
- $\det C_k(A) = (\det A)^{\binom{n-1}{k-1}}$ (тождество Sylvester–Franke).

**Условия применимости.** Алгебраические утверждения работают над любым полем. Для собственных значений нужна замкнутость.

**Идея.** Действие $A^{\otimes k}$ сохраняет антисимметрию тензоров. Ограничение на $\Lambda^k V$ — оператор $\Lambda^k A$, в стандартном базисе $\{e_{i_1}\wedge\dots\wedge e_{i_k}\}$ его матрица и есть $C_k(A)$.

---

### E9. Теорема Шура о произведении Адамара

**Формулировка.** Если $A, B \in M_n(\mathbb{C})$ положительно полуопределены, то $A\circ B$ положительно полуопределена. Если дополнительно $A \succ 0$ и диагональ $B$ строго положительна, то $A\circ B \succ 0$.

**Условия применимости.** Эрмитовость и положительная полуопределённость обоих сомножителей.
Контрпример нужности положительности: $A = B = \begin{pmatrix} 1 & 2 \\ 2 & 1 \end{pmatrix}$. Обе симметричны, не PSD (собственные значения $-1, 3$). Тогда $A\circ B = \begin{pmatrix} 1 & 4 \\ 4 & 1 \end{pmatrix}$ имеет собственные значения $-3, 5$ — не PSD.

**Идея.** $A\circ B$ — главная подматрица $A\otimes B$ на индексах $((i,i), (j,j))_{i,j}$. Из $A = R^*R$ и $B = S^*S$ следует $A\otimes B = (R\otimes S)^*(R\otimes S) \succeq 0$. Главная подматрица положительно полуопределённой матрицы положительно полуопределена.

**Варианты и обобщения.** Неравенство Оппенхейма: $\det(A\circ B) \ge \det(A)\prod_i b_{ii}$ для $A, B \succeq 0$.

---

### E10. Сингулярные числа и нормы $A\otimes B$

**Формулировка.** Если $A = U_A \Sigma_A V_A^*$ и $B = U_B \Sigma_B V_B^*$ — сингулярные разложения, то
$$A\otimes B = (U_A\otimes U_B)\,(\Sigma_A\otimes \Sigma_B)\,(V_A\otimes V_B)^*$$
— сингулярное разложение $A\otimes B$. Сингулярные числа: $\sigma_i(A)\,\sigma_j(B)$.

Следствия:

- $\|A\otimes B\|_F = \|A\|_F\,\|B\|_F$.
- $\|A\otimes B\|_{\text{op}} = \|A\|_{\text{op}}\,\|B\|_{\text{op}}$.
- $\rho(A\otimes B) = \rho(A)\,\rho(B)$.

**Условия применимости.** $\mathbb{C}$ или $\mathbb{R}$ с вещественным сингулярным разложением.

**Идея.** Произведение унитарных под $\otimes$ унитарно (по E2). Произведение диагональных под $\otimes$ диагонально. Подставляем — получаем сингулярное разложение.

---

## Записи — Редкие

### E11. Тензорная степень как конструкция коммутирующих нильпотентов

**Формулировка.** На $V = (\mathbb{C}^2)^{\otimes k}$ положим $A_i = I^{\otimes (i-1)} \otimes N \otimes I^{\otimes (k - i)}$, где $N = \begin{pmatrix}0 & 1\\ 0 & 0\end{pmatrix}$. Матрицы $A_i$ коммутируют, $A_i^2 = 0$, и $A_1 \cdots A_k = N^{\otimes k} \neq 0$. Это даёт достижимое значение $\dim V = 2^k$ для задачи «минимальная размерность пространства, на котором живут $k$ коммутирующих $A_i$ с $A_i^2 = 0$ и ненулевым произведением».

**Идея.** Коммутативность и нильпотентность следуют из E2 (множители на разных позициях коммутируют, повторение $N$ на одной позиции даёт $N^2 = 0$).

### E12. Матрица перестановки векторизации $K_{m,n}$

**Формулировка.** $K_{m,n}$ — единственная матрица перестановки размера $mn \times mn$ с $K_{m,n}\,\operatorname{vec}(X) = \operatorname{vec}(X^T)$. Для $A \in M_n$, $B \in M_m$ верно $K_{n,m}\,(A\otimes B)\,K_{m,n} = B\otimes A$. Следствие: $A\otimes B$ и $B\otimes A$ имеют одинаковый спектр, ранг, жорданову форму и все унитарно-инвариантные нормы.

**Идея.** Перестановка пар индексов $(i, j) \leftrightarrow (j, i)$ переводит лексикографический базис $V\otimes W$ в $W\otimes V$.

---

## Self-test

1. Дано $A \in M_3(\mathbb{C})$, $B \in M_4(\mathbb{C})$ с $\det A = 2$, $\det B = -3$, $\operatorname{tr} A = 5$, $\operatorname{tr} B = 7$. Найти $\det(A\otimes B)$ и $\operatorname{tr}(A\otimes B)$.

2. Пусть $A, B \in M_n(\mathbb{C})$ не имеют общих собственных значений. Доказать, что для каждой $C \in M_n(\mathbb{C})$ существует единственная $X$ с $AX - XB = C$. В частности, $AX = XB$ влечёт $X = 0$.

3. Построить $k$ попарно коммутирующих матриц $A_1, \dots, A_k \in M_{2^k}(\mathbb{C})$ таких, что $A_i^2 = 0$ для всех $i$, но $A_1 A_2 \cdots A_k \neq 0$.

4. Пусть $A \in M_n(\mathbb{C})$ ранга $r$. Найти $\operatorname{rank}(A\otimes A)$. Привести пример матриц $A, B \in M_2(\mathbb{C})$ ранга $1$ с $\operatorname{rank}(A\otimes B + B\otimes A) = 1$.

5. Пусть $A, B \in M_n(\mathbb{C})$ — эрмитовы положительно полуопределённые. Доказать, что матрица $C$ с $C_{ij} = a_{ij} b_{ij}$ — также положительно полуопределена.

6. Найти спектр матрицы $A\otimes I_m + I_n \otimes B$ для $A \in M_n(\mathbb{C})$, $B \in M_m(\mathbb{C})$. Выразить её определитель через характеристические многочлены $A$ и $B$.

7. Пусть $A \in M_n(\mathbb{C})$ имеет попарно различные собственные значения. Доказать, что отображение $X \mapsto AX - XA$ на $M_n(\mathbb{C})$ диагонализуемо. Найти его собственные значения.

## Решения

1. $\det(A\otimes B) = (\det A)^4 (\det B)^3 = 2^4 \cdot (-3)^3 = -432$. $\operatorname{tr}(A\otimes B) = \operatorname{tr}(A)\,\operatorname{tr}(B) = 35$.

2. Оператор $\mathcal{L}\colon X \mapsto AX - XB$ на $M_n$ в координатах $\operatorname{vec}$ имеет матрицу $I_n \otimes A - B^T \otimes I_n$. Его собственные значения — $\lambda_i(A) - \lambda_j(B)$. Непересечение спектров эквивалентно тому, что ни одно из этих чисел не равно нулю, то есть $\mathcal{L}$ обратим. Отсюда — единственность решения для любого $C$ и $X = 0$ для $C = 0$.

3. Конструкция из E11. На $V = (\mathbb{C}^2)^{\otimes k}$ возьмём $N = \begin{pmatrix}0 & 1 \\ 0 & 0\end{pmatrix}$ и $A_i = I^{\otimes (i-1)} \otimes N \otimes I^{\otimes (k - i)}$. По E2 разные $A_i$ коммутируют. $A_i^2$ содержит множитель $N^2 = 0$, поэтому $A_i^2 = 0$. Произведение $A_1 \cdots A_k = N^{\otimes k}$ переводит $e_0^{\otimes k}$ в $e_1^{\otimes k} \neq 0$.

4. $\operatorname{rank}(A\otimes A) = r^2$ из E4. Пример: $A = B = \begin{pmatrix}1 & 0 \\ 0 & 0\end{pmatrix}$. Тогда $A\otimes B = B\otimes A$, и $A\otimes B + B\otimes A = 2(A\otimes A)$ имеет ранг $1$. Общая причина: при пропорциональных $A$ и $B$ матрицы $A\otimes B$ и $B\otimes A$ линейно зависимы.

5. Теорема Шура (E9). Запишем $A = R^* R$, $B = S^* S$. Тогда $A\otimes B = (R\otimes S)^*(R\otimes S) \succeq 0$. Матрица $C = A\circ B$ — главная подматрица $A\otimes B$ на индексах $((i, i), (j, j))_{i,j}$. Главная подматрица положительно полуопределённой матрицы положительно полуопределена.

6. Спектр Кронекеровой суммы — $\{\lambda_i(A) + \mu_j(B)\}$ (E6). Определитель равен произведению всех собственных значений:
$$\det(A\otimes I + I\otimes B) = \prod_{i, j}(\lambda_i + \mu_j) = \prod_i \chi_B(-\lambda_i) \cdot (-1)^{nm}.$$
Это с точностью до знака результант многочленов $\chi_A(x)$ и $\chi_B(-x)$.

7. Оператор $\operatorname{ad}_A\colon X \mapsto AX - XA$ имеет в координатах $\operatorname{vec}$ матрицу $I\otimes A - A^T\otimes I$. Его собственные значения — $\lambda_i - \lambda_j$. Перейдём к базису из собственных векторов $A$: тогда $A = \operatorname{diag}(\lambda_1, \dots, \lambda_n)$, и матричные единицы $E_{ij}$ — собственные векторы $\operatorname{ad}_A$ с собственными значениями $\lambda_i - \lambda_j$. Различимость $\lambda_i$ обеспечивает $n^2$ ненулевых собственных пар плюс $n$ нулевых (на диагональных $E_{ii}$). Ядро — диагональные матрицы.

---

## Использования

| Запись | Задачи и инструменты |
| --- | --- |
| E1, E2, E11 | IMC-2007-DAY2-5 (коммутирующие нильпотенты с ненулевым произведением, тензорная конструкция) |
| E1, E4 | IMC-2004-DAY2-1 (блочная структура $2\times 2$ как $\otimes$ с $M_2$, подсчёты следа и ранга) |
| E2 | Базовая «алгебра тензоров»: ни одно вычисление в этой подтеме не обходится без правила смешанного произведения |
| E3 | Спектральные подсчёты — $\det(I + A\otimes B)$, $\rho(A\otimes B)$, $\operatorname{tr}((A\otimes B)^k)$ |
| E5, E6 | Сведение матричных уравнений к скалярным линейным системам; стандартный приём «$AX = XB$ + непересечение спектров $\Rightarrow X = 0$» для блочной диагонализации |
| E8 | Тождества и оценки определителей через миноры; неравенства Адамара, Фишера, Оппенхейма |
| E9 | Доказательства неравенств с положительно полуопределёнными матрицами и определителей Грама |
| E10 | Оценки норм матричных полиномов, контроль спектрального радиуса и операторной нормы |
| E12 | Симметризация утверждений вида «свойство $X(A\otimes B)$ симметрично по $A$ и $B$» |
