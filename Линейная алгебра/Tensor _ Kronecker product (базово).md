---
topic: Линейная алгебра
subtopic: "Tensor / Kronecker product (базово)"
sources:
  - "Horn, Johnson — Topics in Matrix Analysis (Ch. 4: Matrix Equations and the Kronecker Product)"
  - "Horn, Johnson — Matrix Analysis (Ch. 7: Hadamard product, Schur product theorem)"
  - "Bhatia — Matrix Analysis (GTM 169)"
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Schäcke — On the Kronecker Product (UWaterloo, 2013)"
  - "Bhatia, Rosenthal — How and Why to Solve the Operator Equation AX − XB = Y (Bull. London Math. Soc.)"
  - "Marcus — Finite Dimensional Multilinear Algebra (Vol. I, II)"
  - "Greub — Multilinear Algebra"
  - "Yufei Zhao — Algebraic Combinatorics (MOP 2007 Black Group)"
  - "IMC Compendium"
  - "Putnam Compendium"
  - "Wikipedia — Kronecker product, Sylvester equation, Schur product theorem, Compound matrix, Vec-permutation matrix"
problems_referenced:
  - IMC-2004-DAY2-1
  - IMC-2007-DAY2-5
last_updated: 2026-04-27
---

# Tensor / Kronecker product (базово)

## Scope
Кронекерово / тензорное произведение матриц $A \otimes B$ как координатный образ тензорного произведения линейных операторов на $V \otimes W$. Базовая алгебра: билинейность, ассоциативность, mixed product property, поведение спектра, ранга, следа, определителя, нормы. Vec operator и сведение матричных уравнений ($AXB = C$, Sylvester $AX - XB = C$, Lyapunov) к скалярным линейным системам с матрицей $B^T \otimes A$ или $I \otimes A \pm B^T \otimes I$. Kronecker sum $A \oplus B = A \otimes I + I \otimes B$ и теорема Сильвестра–Розенблюма (Sylvester–Rosenblum). Внешние и симметрические степени, compound matrix $C_k(A) = \Lambda^k A$ и связь с Cauchy–Binet. Schur product theorem (Hadamard $A \circ B$ как principal submatrix $A \otimes B$). Тензорные степени $V^{\otimes k}$ как механизм построения экстремальных конструкций (commuting nilpotents с ненулевым произведением).

## Записи — Core

### E1. Kronecker product (произведение Кронекера): определение и формальная алгебра

Формулировка. Для $A = (a_{ij}) \in M_{m \times n}(F)$, $B \in M_{p \times q}(F)$ матрица $A \otimes B \in M_{mp \times nq}(F)$ задаётся блочно
$$A \otimes B = \begin{pmatrix} a_{11} B & \cdots & a_{1n} B \\ \vdots & & \vdots \\ a_{m1} B & \cdots & a_{mn} B \end{pmatrix}.$$
Операция билинейна по обоим аргументам и ассоциативна $(A\otimes B)\otimes C = A \otimes (B\otimes C)$. Транспонирование и сопряжение: $(A\otimes B)^T = A^T \otimes B^T$, $(A\otimes B)^* = A^*\otimes B^*$. Не коммутативно, но $A\otimes B$ перестановочно-подобно $B\otimes A$ (см. E12).

Условия применимости. Любое поле для определения; для разговора о спектре нужна $F$ алгебраически замкнутая или работа в $\overline{F}$.

Идея. $A \otimes B$ — это матрица оператора $A \otimes B \colon V \otimes W \to V'\otimes W'$ относительно lex-базиса $e_i\otimes f_j$ (E7).

Используется в. [IMC-2007-DAY2-5 (тензорная конструкция)], [IMC-2004-DAY2-1 (блочная 2×2 как $\otimes$ с $2\times 2$)].

---

### E2. Mixed product property (правило смешанного произведения)

Формулировка. Если размеры согласованы (то есть существуют произведения $AC$ и $BD$), то
$$(A \otimes B)(C \otimes D) = (AC) \otimes (BD).$$
Следствия:
- $A\otimes B = (A\otimes I_p)(I_n\otimes B) = (I_m\otimes B)(A\otimes I_q)$ — фундаментальная факторизация на «строчный» и «столбцовый» множители.
- $(A\otimes B)^k = A^k \otimes B^k$ для $A,B$ квадратных.
- $A,B$ обратимы $\Rightarrow (A\otimes B)^{-1} = A^{-1}\otimes B^{-1}$.
- Для полиномов: $f(A)\otimes g(B) = $ полином от $A\otimes I$ и $I\otimes B$ — основа functional calculus на $A \otimes I, I \otimes B$, которые коммутируют.

Условия применимости. Совпадение внутренних размеров $A,C$ и $B,D$. Над любым полем.

Идея. Прямой подсчёт по блокам: $(i,j)$-блок $(A\otimes B)(C\otimes D)$ равен $\sum_k a_{ik}c_{kj} BD = (AC)_{ij} \cdot BD$.

Используется в. Это «рабочая лошадь» — без mixed product property не работает ни E3, ни E4, ни E5.

---

### E3. Spectrum of Kronecker product (спектр кронекерова произведения)

Формулировка. Пусть $A \in M_n(\mathbb{C})$ имеет собственные значения $\lambda_1,\dots,\lambda_n$ (с алгебраической кратностью), $B\in M_m(\mathbb{C})$ — $\mu_1,\dots,\mu_m$. Тогда $A\otimes B$ имеет ровно $nm$ собственных значений
$$\lambda_i \mu_j, \qquad 1\le i\le n,\ 1\le j\le m.$$
Если $Av = \lambda v$, $Bw = \mu w$, то $(A\otimes B)(v\otimes w) = \lambda\mu\, (v\otimes w)$.

Условия применимости. $\mathbb{C}$ или поле, где оба характеристических многочлена раскладываются (иначе можно перейти к замыканию — формула для собственных значений сохранится, для собственных векторов нужно $v,w$ из расширения).

Идея. Schur triangularization: $A = U_A T_A U_A^*$, $B = U_B T_B U_B^*$. По mixed product
$$A\otimes B = (U_A\otimes U_B)(T_A\otimes T_B)(U_A\otimes U_B)^*,$$
и $T_A\otimes T_B$ верхнетреугольная с диагональю $\lambda_i\mu_j$. $U_A\otimes U_B$ унитарна (E10).

Варианты и обобщения.
- $A\oplus B := A\otimes I_m + I_n \otimes B$ — Kronecker sum, спектр $\{\lambda_i + \mu_j\}$ (см. E6).
- Для произвольной полиномиальной функции $p(X,Y)$ на коммутирующих: $p(A\otimes I, I\otimes B)$ имеет спектр $\{p(\lambda_i,\mu_j)\}$.
- Жорданова структура $A\otimes B$ выражается через Jordan blocks $A$ и $B$ — формулы громоздкие, особенно при $\lambda_i\mu_j = 0$.

Используется в. Спектральные подсчёты на $A\otimes B$ — стандартный приём; вычисление $\det(I + A\otimes B)$, $\operatorname{tr}((A\otimes B)^k)$, $\rho(A\otimes B) = \rho(A)\rho(B)$.

---

### E4. det / tr / rank матрицы $A\otimes B$

Формулировка. Для $A\in M_n(F)$, $B\in M_m(F)$:
$$\operatorname{tr}(A\otimes B) = \operatorname{tr}(A)\operatorname{tr}(B), \quad \det(A\otimes B) = \det(A)^m \det(B)^n, \quad \operatorname{rank}(A\otimes B) = \operatorname{rank}(A)\cdot\operatorname{rank}(B).$$
В частности $A\otimes B$ обратима тогда и только тогда, когда обратимы $A$ и $B$.

Условия применимости. Любое поле. Для прямоугольных $A\in M_{m\times n}, B\in M_{p\times q}$ работает только rank-формула.

Идея.
- $\operatorname{tr}$: сумма $\lambda_i\mu_j = (\sum \lambda_i)(\sum\mu_j)$, или прямой блочный подсчёт $\operatorname{tr}(A\otimes B) = \sum_i a_{ii}\operatorname{tr}(B)$.
- $\det$: $\prod_{i,j}\lambda_i\mu_j = (\prod \lambda_i)^m(\prod \mu_j)^n$.
- $\operatorname{rank}$: SVD-разложения $A=\sum \sigma_i u_i v_i^*$, $B = \sum \tau_j x_j y_j^*$ дают $A\otimes B = \sum \sigma_i\tau_j (u_i\otimes x_j)(v_i\otimes y_j)^*$ — ранг $rs$.

Варианты и обобщения.
- $\operatorname{tr}((A\otimes B)^k) = \operatorname{tr}(A^k)\operatorname{tr}(B^k)$.
- $\det(I_{nm} + A\otimes B) = \prod_{i,j}(1+\lambda_i\mu_j)$.
- $\det(I_n\otimes A + B^T \otimes I_m) = \prod_{i,j}(\lambda_i(A) + \mu_j(B))$ — ключ для Sylvester (E6).
- $\operatorname{rank}(A\otimes B + C\otimes D)$ в общем случае не выражается через rank сомножителей; есть верхняя оценка $\operatorname{rank}(A)\operatorname{rank}(B) + \operatorname{rank}(C)\operatorname{rank}(D)$.

Используется в. [IMC-2004-DAY2-1] (rank/блочные подсчёты), общие задачи на $\det$ блочных конструкций.

---

### E5. Vec operator (векторизация) и тождество $\operatorname{vec}(AXB) = (B^T\otimes A)\operatorname{vec}(X)$

Формулировка. $\operatorname{vec}\colon M_{m\times n}(F) \to F^{mn}$ ставит столбцы матрицы один под другим. Для $A\in M_{p\times m}, B\in M_{n\times q}, X\in M_{m\times n}$:
$$\operatorname{vec}(AXB) = (B^T\otimes A)\operatorname{vec}(X).$$
Частные случаи: $\operatorname{vec}(AX) = (I\otimes A)\operatorname{vec}(X)$, $\operatorname{vec}(XB) = (B^T\otimes I)\operatorname{vec}(X)$.

Условия применимости. Любое поле. Размеры согласованы.

Идея. Прямая проверка по столбцам: $j$-й столбец $AXB$ есть $A X b_j = A\sum_k b_{kj} x_k = \sum_k b_{kj}(A x_k)$, где $x_k$ — столбцы $X$; собрать в $\operatorname{vec}$ — даст блочное умножение на $B^T\otimes A$.

Варианты и обобщения.
- Уравнение $AXB = C$ — линейная система с матрицей $B^T\otimes A$ размера $pq \times mn$.
- Sylvester $AX - XB = C$ → $(I_n\otimes A - B^T\otimes I_m)\operatorname{vec}(X) = \operatorname{vec}(C)$ (E6).
- Lyapunov $AX + XA^* = -Q$ → $(I\otimes A + \overline{A}\otimes I)\operatorname{vec}(X) = -\operatorname{vec}(Q)$.
- Frobenius inner product: $\langle X, Y\rangle_F = \operatorname{vec}(X)^*\operatorname{vec}(Y)$ — линейный функционал $\operatorname{tr}(A^*X) = \operatorname{vec}(A)^*\operatorname{vec}(X)$.

Используется в. Все задачи, где «матричное уравнение» удобнее переписать как линейную систему — особенно когда нужно подсчитать $\dim\{X: AX = XB\}$ или показать единственность решения через невырожденность $I\otimes A - B^T\otimes I$.

---

### E6. Kronecker sum и Sylvester–Rosenblum theorem (теорема Сильвестра–Розенблюма)

Формулировка. $A\oplus B := A\otimes I_m + I_n \otimes B$ для $A\in M_n, B\in M_m$. Спектр: $\{\lambda_i(A) + \mu_j(B)\}$.

Sylvester–Rosenblum theorem. Уравнение $AX - XB = C$ имеет единственное решение $X\in M_{n\times m}(\mathbb{C})$ для каждого $C$ тогда и только тогда, когда $\operatorname{spec}(A)\cap \operatorname{spec}(B) = \emptyset$.

Условия применимости. $\mathbb{C}$ (или поле, где спектры считаются в общем замыкании). Для $AX + XB = C$ — условие $\operatorname{spec}(A)\cap\operatorname{spec}(-B) = \emptyset$.

Идея. Через E5: оператор $X\mapsto AX - XB$ это $I\otimes A - B^T\otimes I$, его собственные значения — $\lambda_i - \mu_j$. Невырожден $\iff$ ни один не нуль $\iff \operatorname{spec}(A)\cap\operatorname{spec}(B)=\emptyset$. Альтернатива: контурный интеграл $X = \frac{1}{2\pi i}\oint (zI-A)^{-1}C(zI-B)^{-1}dz$ по контуру, разделяющему спектры (Rosenblum, 1956).

Варианты и обобщения.
- Если $AX = XB$ и $\operatorname{spec}(A)\cap\operatorname{spec}(B)=\emptyset$, то $X=0$ — стандартная лемма для блочной диагонализации.
- Lyapunov: $AX + XA^* = Q$ имеет единственное решение для всех $Q$ $\iff$ $\lambda_i + \overline{\lambda_j} \neq 0$ для всех $i,j$. Если $A$ Hurwitz и $Q\succeq 0$, то $X\succeq 0$.
- $X = AXB + C$ (Stein equation) — единственное решение $\iff \lambda_i(A)\mu_j(B) \neq 1$ для всех $i,j$.
- Полное обобщение: для аналитической функции $f$, не имеющей сингулярностей в спектрах — формула $X = \frac{1}{2\pi i}\oint f(z)(zI-A)^{-1} dz \cdot \cdots$ (functional calculus).

Используется в. Стандартный приём: «$AX = XB$ + спектры не пересекаются $\Rightarrow X=0$» закрывает массу задач на одновременную блочную структуру / commuting subalgebras.

---

## Записи — Standard

### E7. Tensor product of vector spaces (тензорное произведение пространств) и универсальное свойство

Формулировка. Тензорное произведение $V\otimes W$ — пара $(V\otimes W, \tau)$ с билинейным $\tau\colon V\times W \to V\otimes W$, такая что для любого билинейного $\beta\colon V\times W \to U$ существует единственное линейное $\tilde\beta\colon V\otimes W \to U$ с $\beta = \tilde\beta\circ \tau$. Базис $\{e_i\otimes f_j\}_{i,j}$, $\dim(V\otimes W) = \dim V \cdot \dim W$.

Канонические изоморфизмы:
- $V^*\otimes W \cong \operatorname{Hom}(V,W)$ через $(\varphi\otimes w)(v) = \varphi(v) w$ (rank-one операторы).
- $V^*\otimes V \cong \operatorname{End}(V)$, под этим $\operatorname{tr}\colon V^*\otimes V \to F$ — естественное спаривание $\varphi\otimes v \mapsto \varphi(v)$.
- $\operatorname{Hom}(V_1\otimes V_2, U) \cong \operatorname{Bil}(V_1,V_2; U)$.
- $A\otimes B$ (E1) — матрица оператора $A\otimes B\colon V\otimes W \to V'\otimes W'$ в lex-базисе.

Условия применимости. Любое поле, конечная или бесконечная размерность (для бесконечной — алгебраическое тензорное произведение).

Идея. Конструкция через факторизацию свободного модуля $F^{V\times W}/R$, где $R$ — отношения билинейности. Универсальное свойство — определяющее, всё остальное вытекает.

Варианты и обобщения.
- Symmetric power $\operatorname{Sym}^k V$ и exterior power $\Lambda^k V$ — факторы / прямые слагаемые $V^{\otimes k}$ по $S_k$-действию, $\dim \operatorname{Sym}^k V = \binom{n+k-1}{k}$, $\dim \Lambda^k V = \binom{n}{k}$.
- $V_1\otimes\cdots\otimes V_k$ ассоциативно, размерность мультипликативна.

Используется в. Каждый раз, когда от матрицы $A\otimes B$ делается шаг к оператору на абстрактном пространстве (особенно в комбинаторных конструкциях).

---

### E8. Compound matrix $C_k(A) = \Lambda^k A$ и Cauchy–Binet

Формулировка. Для $A\in M_{m\times n}(F)$, $1\le k\le \min(m,n)$, compound matrix $C_k(A)$ — матрица $\binom{m}{k}\times\binom{n}{k}$, строки и столбцы которой индексированы $k$-элементными подмножествами в lex-порядке, элемент на $(I,J)$-позиции — минор $\det A[I,J]$. Это матрица оператора $\Lambda^k A\colon \Lambda^k F^n \to \Lambda^k F^m$ в стандартном базисе.

Свойства:
- $C_k(AB) = C_k(A) C_k(B)$ (мультипликативность) — это и есть Cauchy–Binet в матричной форме.
- $C_k(I) = I$, $C_k(A^T) = C_k(A)^T$, $C_k(A^{-1}) = C_k(A)^{-1}$.
- Для $A\in M_n$ с собственными значениями $\lambda_1,\dots,\lambda_n$: $C_k(A)$ имеет собственные значения $\lambda_{i_1}\cdots\lambda_{i_k}$, $i_1<\cdots<i_k$. В частности $\det C_k(A) = (\det A)^{\binom{n-1}{k-1}}$, $\operatorname{tr} C_k(A) = e_k(\lambda_1,\dots,\lambda_n)$ — $k$-й элементарный симметрический многочлен (т.е. коэффициент характеристического многочлена).
- $C_n(A) = \det A$ (1×1).

Условия применимости. Любое поле для алгебраических утверждений; для собственных значений — $\mathbb{C}$ или замыкание.

Идея. $\Lambda^k V$ — это $V^{\otimes k}/(\text{симметричные тензоры})$, или подпространство антисимметричных тензоров. Действие $A^{\otimes k}$ сохраняет антисимметрию, ограничение и есть $\Lambda^k A$. В базисе $\{e_{i_1}\wedge\cdots\wedge e_{i_k}\}$ матрица — компаунд.

Варианты и обобщения.
- Cauchy–Binet: $\det(AB) = \sum_{|S|=n} \det(A[\cdot,S])\det(B[S,\cdot])$ для $A\in M_{n\times m}, B\in M_{m\times n}$ ($m\ge n$) — частный случай $C_n(AB) = C_n(A)C_n(B)$.
- Тождества Newton, $e_k$ vs $p_k$, через $\det(I + tA) = \sum_k t^k e_k(\lambda)$ и $\sum_k t^k \operatorname{tr} C_k(A)$.
- Sylvester–Franke: $\det C_k(A) = (\det A)^{\binom{n-1}{k-1}}$.

Используется в. Cauchy–Binet — часто в IMC-задачах на определители; через compound matrices доказываются неравенства типа Hadamard, Fischer, Oppenheim.

---

### E9. Schur product theorem (теорема Шура о произведении): $A\circ B \succeq 0$ для PSD

Формулировка. Hadamard product $(A\circ B)_{ij} = a_{ij} b_{ij}$. Если $A,B\in M_n(\mathbb{C})$ PSD, то $A\circ B$ PSD. Если $A\succ 0$ и $B\succeq 0$ с ненулевой диагональю, то $A\circ B\succ 0$.

Условия применимости. $A,B$ эрмитовы PSD над $\mathbb{C}$.

Идея. $A\circ B$ — главная подматрица $A\otimes B$ на индексах $(i,i),(j,j)$. $A,B\succeq 0 \Rightarrow A\otimes B\succeq 0$ (mixed product даёт $A\otimes B = (A^{1/2}\otimes B^{1/2})^*(A^{1/2}\otimes B^{1/2})$). Главная подматрица PSD — PSD.

Варианты и обобщения.
- Oppenheim's inequality: $\det(A\circ B) \ge \det(B)\prod_i a_{ii}$ для $A,B\succeq 0$.
- Если $A\succeq 0$ ранга $r$: $\operatorname{rank}(A\circ B)\le r\cdot\operatorname{rank}(B)$.
- Schur–Hadamard: для $A,B$ нормальных $\|A\circ B\|_{op}\le \|A\|_{op}\|B\|_{op}$ — частный случай для $\otimes$.

Используется в. Доказательства неравенств с PSD матрицами, оценки определителей Грама.

---

### E10. SVD and norms of $A\otimes B$ (сингулярные числа и нормы)

Формулировка. Если $A = U_A \Sigma_A V_A^*$, $B = U_B \Sigma_B V_B^*$ — SVD, то
$$A\otimes B = (U_A\otimes U_B)(\Sigma_A\otimes \Sigma_B)(V_A\otimes V_B)^*$$
— SVD матрицы $A\otimes B$. Сингулярные числа: $\sigma_i(A)\sigma_j(B)$. Унитарность $U\otimes V$ при $U,V$ унитарных следует из mixed product.

Следствия:
- $\|A\otimes B\|_F = \|A\|_F\|B\|_F$, $\|A\otimes B\|_{op} = \|A\|_{op}\|B\|_{op}$.
- Для любой unitarily invariant norm $\|\cdot\|$: $\|A\otimes B\| = \|A\|_{op}\|B\|$ или симметричный вариант (Horn–Johnson Topics, Th. 4.3.10) — мультипликативность работает не для всех $\|\cdot\|$ напрямую, но для Schatten-$p$ верно $\|A\otimes B\|_p = \|A\|_p\|B\|_p$.
- Spectral radius: $\rho(A\otimes B) = \rho(A)\rho(B)$ (следствие E3).

Условия применимости. $\mathbb{C}$ (или $\mathbb{R}$ с реальным SVD).

Идея. Mixed product property + унитарность тензора унитарных + диагональность тензора диагональных.

Используется в. Оценки норм матричных полиномов, контроль $\rho$ и operator norm в задачах на сходимость / устойчивость.

---

## Записи — Exotic

### E11. Tensor power как механизм построения экстремальных commuting nilpotents (IMC-2007 D2-5)

Формулировка. На $V = (\mathbb{C}^2)^{\otimes k}$ размерности $2^k$ зададим
$$A_i = I^{\otimes(i-1)} \otimes N \otimes I^{\otimes(k-i)}, \qquad N = \begin{pmatrix} 0 & 1 \\ 0 & 0 \end{pmatrix}.$$
Тогда $A_i$ попарно коммутируют (mixed product даёт $A_i A_j = I^{\otimes\cdots} \otimes N\otimes I^{\otimes\cdots}\otimes N\otimes I^{\otimes\cdots}$ симметрично), $A_i^2 = 0$, и $A_1 A_2\cdots A_k = N^{\otimes k} \neq 0$ (отображает $e_0^{\otimes k} \mapsto e_1^{\otimes k}$). Это даёт $n_k = 2^k$ — достижимое значение в задаче «найти минимальное $n$, на котором существуют $k$ коммутирующих $A_i\in M_n(\mathbb{C})$ с $A_i^2=0$ и $A_1\cdots A_k\neq 0$».

Условия применимости. Решающая лемма-конструкция — переход к $V^{\otimes k}$. Базисное пространство $\mathbb{C}^2$ можно заменить на любое с нилпотентным $N$, $N^2=0$, $N\neq 0$, и фиксированным $v$ с $Nv\ne 0$.

Идея. Удобно мыслить: базис $V$ — векторы $|S\rangle$, $S\subseteq\{1,\dots,k\}$; $A_i|S\rangle = |S\cup\{i\}\rangle$ если $i\notin S$, иначе $0$. Это и есть $N\otimes\cdots$ в координатах. Booleнова решётка подмножеств — ровно $V^{\otimes k}$.

Варианты и обобщения.
- Доказательство нижней оценки $n\ge 2^k$ (что $2^k$ оптимально): рассмотреть $v$ с $A_1\cdots A_k v\ne 0$; $\{A_S v : S\subseteq\{1,\dots,k\}\}$ линейно независимы (рассматривая старшую степень), значит $\dim V \ge 2^k$.
- Аналогичная конструкция работает для других семейств: $A_i^{m_i}=0$ — заменить $\mathbb{C}^2$ на $\mathbb{C}^{m_i}$.

Используется в. [IMC-2007-DAY2-5].

---

### E12. Vec-permutation matrix (коммутационная матрица) $K_{m,n}$

Формулировка. $K_{m,n}\in M_{mn}(\mathbb{R})$ — единственная permutation matrix с $K_{m,n}\operatorname{vec}(X) = \operatorname{vec}(X^T)$ для $X\in M_{m\times n}$. Свойства: $K_{m,n}^T = K_{n,m} = K_{m,n}^{-1}$. Для $A\in M_{m\times n}, B\in M_{p\times q}$:
$$K_{p,m} (A\otimes B) K_{n,q} = B\otimes A.$$
В частности при квадратных $A\in M_n, B\in M_m$: $A\otimes B$ и $B\otimes A$ перестановочно подобны $\Rightarrow$ имеют одинаковый спектр, ранг, жорданову форму, нормы.

Условия применимости. Любое поле.

Идея. $K_{m,n}$ переставляет «строчно-столбцовый» и «столбцово-строчный» порядок индексов на $\{1,\dots,m\}\times\{1,\dots,n\}$.

Варианты и обобщения.
- $K_{m,n} = \sum_{i,j} E_{ij}\otimes E_{ji}$ (где $E_{ij}\in M_{m\times n}$, $E_{ji}\in M_{n\times m}$ — стандартные базисные).
- Используется при сведении $\operatorname{vec}(AXB)$ к различным эквивалентным формам и в задачах, где «порядок» тензорного произведения существенен (квантовые вычисления, signal processing).

Используется в. Аккуратные доказательства симметричных свойств $A\otimes B$ vs $B\otimes A$; иногда — в комбинаторных тождествах через индексные перестановки.

---

## Self-test

1. $A\in M_3(\mathbb{C}), B\in M_4(\mathbb{C})$, $\det A = 2$, $\det B = -3$, $\operatorname{tr} A = 5$, $\operatorname{tr} B = 7$. Найти $\det(A\otimes B)$ и $\operatorname{tr}(A\otimes B)$.

2. $A\in M_n(\mathbb{C})$ с собственными значениями $\lambda_1,\dots,\lambda_n$. Найти $\det(I_{n^2} + A\otimes A^{-1})$ для невырожденной $A$.

3. Пусть $A,B\in M_n(\mathbb{C})$ не имеют общих собственных значений. Доказать: для любой $C\in M_n(\mathbb{C})$ существует единственная $X$ с $AX - XB = C$. Доказать также, что $X = 0$ — единственное решение однородного $AX = XB$.

4. Постройте $k$ попарно коммутирующих матриц $A_1,\dots,A_k\in M_{2^k}(\mathbb{C})$ таких, что $A_i^2 = 0$ для всех $i$, но $A_1 A_2\cdots A_k \neq 0$.

5. $A\in M_n(\mathbb{C})$ ранга $r$. Найти $\operatorname{rank}(A\otimes A)$. Привести пример матриц $A,B \in M_2(\mathbb{C})$ ранга 1, для которых $\operatorname{rank}(A\otimes B + B\otimes A) = 1$ (т.е. строго меньше $2\operatorname{rank}(A)\operatorname{rank}(B)$).

6. $A,B\in M_n(\mathbb{C})$ — эрмитовы PSD с положительными диагональными элементами. Доказать, что матрица $C_{ij} = a_{ij}b_{ij}$ — также PSD, и привести пример, когда $C$ строго positive definite, хотя $B$ только PSD.

7. Найти спектр $A\otimes I_m + I_n\otimes B$ для $A\in M_n, B\in M_m$. Используя это, выразить $\det(A\otimes I + I\otimes B)$ через характеристические многочлены $A$ и $B$.

8. $A\in M_n(\mathbb{C})$ с попарно различными собственными значениями. Доказать, что отображение $X\mapsto AX - XA$ на $M_n(\mathbb{C})$ диагонализуемо, и найти его собственные значения и собственные подпространства.

---

## Решения

1. $\det(A\otimes B) = (\det A)^4 (\det B)^3 = 2^4\cdot(-3)^3 = 16\cdot(-27) = -432$. $\operatorname{tr}(A\otimes B) = \operatorname{tr}(A)\operatorname{tr}(B) = 35$.

2. Спектр $A\otimes A^{-1}$ — мультимножество $\{\lambda_i/\lambda_j\}_{i,j}$ (E3). Тогда
$$\det(I + A\otimes A^{-1}) = \prod_{i,j}(1+\lambda_i/\lambda_j) = \frac{\prod_{i,j}(\lambda_i+\lambda_j)}{\prod_{i,j}\lambda_j} = \frac{\prod_{i,j}(\lambda_i+\lambda_j)}{(\det A)^n}.$$
При $n=2$: числитель $= (2\lambda_1)(2\lambda_2)(\lambda_1+\lambda_2)^2 = 4\det A\cdot(\operatorname{tr} A)^2$, ответ $4(\operatorname{tr} A)^2/\det A$.

3. Оператор $\mathcal{L}\colon X\mapsto AX - XB$ на $M_n$ имеет в координатах $\operatorname{vec}$ матрицу $I_n\otimes A - B^T\otimes I_n$ (E5, E6). Его собственные значения — $\lambda_i(A) - \lambda_j(B)$. Условие отсутствия общих собственных значений $\Leftrightarrow$ ни одно не нуль $\Leftrightarrow \mathcal{L}$ обратим $\Leftrightarrow$ единственное решение для каждого $C$, в частности $X=0$ для $C=0$.

4. Конструкция E11. $V = (\mathbb{C}^2)^{\otimes k}$, $N = \begin{pmatrix}0&1\\0&0\end{pmatrix}$, $A_i = I^{\otimes(i-1)}\otimes N \otimes I^{\otimes(k-i)}$. Mixed product даёт $A_i A_j = I^{\otimes\cdots}\otimes N\otimes I^{\otimes\cdots}\otimes N\otimes I^{\otimes\cdots} = A_j A_i$. $A_i^2$ содержит фактор $N^2 = 0$, значит $A_i^2 = 0$. $A_1\cdots A_k = N^{\otimes k}$ переводит $e_0^{\otimes k}$ в $e_1^{\otimes k}\neq 0$.

5. $\operatorname{rank}(A\otimes A) = r^2$ (E4). Пример: $A = B = \begin{pmatrix}1&0\\0&0\end{pmatrix}$ rank-one. Тогда $A\otimes B = B\otimes A$, и $A\otimes B + B\otimes A = 2(A\otimes A)$ ранга $\operatorname{rank}(A\otimes A) = 1 < 2 = 2\operatorname{rank}(A)\operatorname{rank}(B)$. Общая причина: при $A,B$ пропорциональных $A\otimes B$ и $B\otimes A$ линейно зависимы.

6. Schur product theorem (E9). $C = A\circ B$ — главная подматрица $A\otimes B$ на индексах $(i,i;j,j)$. $A\otimes B = (A^{1/2}\otimes B^{1/2})^*(A^{1/2}\otimes B^{1/2})\succeq 0$, главная подматрица PSD — PSD. Строгая положительность: если $A\succ 0$ и $\operatorname{diag}(B) > 0$, $B\succeq 0$ ранга $\ge 1$ — Schur showed $A\circ B\succ 0$ при $A\succ 0$, $B\succeq 0$, $\operatorname{diag} B > 0$ (фактически достаточно, чтобы $B$ не имела нулевых столбцов).

7. Спектр Kronecker sum: $\lambda_i(A) + \mu_j(B)$ (E6). $\det(A\otimes I + I\otimes B) = \prod_{i,j}(\lambda_i+\mu_j) = \prod_i \chi_B(-\lambda_i) \cdot (-1)^{nm} = \operatorname{Res}(\chi_A(x), \chi_B(-x))$ (с точностью до знака) — результант характеристических многочленов. Эквивалентно $\prod_j \chi_A(-\mu_j)\cdot(-1)^{nm}$.

8. $\operatorname{ad}_A\colon X\mapsto AX - XA$ имеет в $\operatorname{vec}$-координатах матрицу $I\otimes A - A^T\otimes I$. Спектр — $\{\lambda_i - \lambda_j\}_{i,j}$. При $A = \operatorname{diag}(\lambda_1,\dots,\lambda_n)$ собственные векторы — $E_{ij}$ (стандартные матричные единицы) с $\operatorname{ad}_A(E_{ij}) = (\lambda_i - \lambda_j)E_{ij}$. Различимость $\lambda_i$ обеспечивает диагонализуемость и явно даёт собственное разложение. Ядро $\operatorname{ad}_A$ — диагональные матрицы (для $i = j$), размерности $n$.
