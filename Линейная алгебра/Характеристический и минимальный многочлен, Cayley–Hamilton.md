---
topic: Линейная алгебра
subtopic: Характеристический и минимальный многочлен, Cayley–Hamilton
sources:
  - "Prasolov — Problems and Theorems in Linear Algebra"
  - "Horn, Johnson — Matrix Analysis"
  - "Lancaster, Tismenetsky — The Theory of Matrices"
  - "Gantmacher — Theory of Matrices"
  - "Engel — Problem-Solving Strategies"
  - "Putnam Compendium / Kedlaya archive"
  - "IMC Compendium (imc-math.org.uk)"
  - "Keith Conrad — The minimal polynomial and some applications"
  - "Wikipedia: Cayley–Hamilton, Frobenius covariant, Faddeev–LeVerrier, Nakayama's lemma"
  - "Сборник.csv (локальный)"
problems_referenced:
  - IMC-2000-DAY2-6
  - IMC-2003-3
  - IMC-2009-DAY2-3
  - Putnam-1996-B4
  - Putnam-2007-B6
  - Putnam-1979-B6
last_updated: 2026-04-27
---

# Характеристический и минимальный многочлен, Cayley–Hamilton

## Scope
Структурные тождества для $\chi_A(t) = \det(tI - A)$ и минимального многочлена $\mu_A$, и техники, выводимые из соотношения $\chi_A(A) = 0$. Сюда же — переход «ограничения на спектр $\Leftrightarrow$ ограничения на $\mu_A$», тождества вида $\chi_{AB} = \chi_{BA}$, выражения степеней и обратных через младшие степени, derivation-трюки и спектральные проекторы.

## Записи - Core

### E1. Cayley–Hamilton (теорема Кэли–Гамильтона)

Формулировка. Для $A \in M_n(R)$, $R$ — коммутативное кольцо, $\chi_A(A) = 0$, где $\chi_A(t) = \det(tI - A) = t^n - c_1 t^{n-1} + c_2 t^{n-2} - \dots + (-1)^n c_n$ и $c_k = e_k(\lambda_1,\dots,\lambda_n)$ — элементарные симметрические от собственных значений (то есть $c_1 = \operatorname{tr} A$, $c_n = \det A$).

Условия применимости. Любое коммутативное кольцо коэффициентов; в частности любое поле. Для матриц над некоммутативным кольцом утверждение, как правило, неверно.

Идея доказательства. Через формулу adjugate: $(tI-A)\,\operatorname{adj}(tI - A) = \chi_A(t) I$. Левая часть — многочлен по $t$ с матричными коэффициентами; подстановка $t \mapsto A$ корректна, поскольку коэффициенты коммутируют с $A$. Альтернативно — density: тождество $\chi_A(A)=0$ полиномиально по элементам $A$; на плотном открытом множестве диагонализуемых матриц над $\mathbb C$ оно очевидно.

Варианты и обобщения. Generalized Cayley–Hamilton (см. E14) для эндоморфизмов конечно-порождённых модулей.

Используется в. [IMC-2000-DAY2-6, IMC-2009-DAY2-3, Putnam-1996-B4, Putnam-2007-B6, Putnam-1979-B6].

---

### E2. Минимальный многочлен (minimal polynomial) и связь со спектром

Формулировка. $\mu_A \in F[t]$ — унитарный многочлен наименьшей степени с $\mu_A(A) = 0$. Свойства: (i) $\mu_A \mid p$ для любого аннулирующего $p$; (ii) $\mu_A \mid \chi_A$; (iii) $\mu_A$ и $\chi_A$ имеют одинаковое множество корней (но не кратностей); (iv) над алгебраически замкнутым $F$: если $\chi_A = \prod (t-\lambda_i)^{a_i}$ и $b_i$ — размер наибольшего Жордановой блока на $\lambda_i$, то $\mu_A = \prod (t-\lambda_i)^{b_i}$.

Условия применимости. Любое поле. Для (iv) — алгебраически замкнутое или $\mu_A$ расщепляется.

Идея доказательства. (i)–(ii) — деление с остатком в $F[t]$. (iii) — корни $\chi_A$ суть собственные значения, и каждое собственное значение аннулирует $\mu_A$ на соответствующем eigenvector. (iv) — прямое вычисление на Jordan blocks: для блока $J_k(\lambda)$ имеем $\mu = (t-\lambda)^k$.

Варианты и обобщения. Над $F[t]$ как $F[t]$-module: invariant factors $f_1 \mid f_2 \mid \dots \mid f_r$, $\mu_A = f_r$, $\chi_A = \prod f_i$ (Frobenius rational canonical form, см. E7).

Используется в. [IMC-2003-3].

---

### E3. Критерий диагонализуемости через минимальный многочлен

Формулировка. $A \in M_n(F)$ диагонализуема над $F$ $\iff$ $\mu_A$ расщепляется над $F$ и не имеет кратных корней (squarefree).

Условия применимости. Любое поле. Достаточное условие «есть $n$ различных собственных значений в $F$» — частный случай.

Идея доказательства. $\Leftarrow$: $\mu_A = \prod (t-\lambda_i)$ с разными $\lambda_i$; по китайской теореме об остатках $F[t]/(\mu_A) \cong \prod F[t]/(t-\lambda_i) = F^k$, и $V$ распадается в прямую сумму $\ker(A-\lambda_i I)$. $\Rightarrow$: если $A = P D P^{-1}$ с $D = \operatorname{diag}(\lambda_i)$, то $\prod_{\lambda \in \sigma(A)} (t-\lambda)$ аннулирует $A$.

Варианты и обобщения. $A$ полупроста (semisimple) $\iff$ $\mu_A$ squarefree (без расщепления). Идемпотент $\iff$ $\mu_A \mid t^2 - t$. Инволюция $\iff$ $\mu_A \mid t^2 - 1$ (в $\operatorname{char} \neq 2$).

Используется в. [IMC-2003-3].

---

### E4. $AB$ и $BA$ имеют одинаковый характеристический многочлен

Формулировка. (a) Если $A, B \in M_n(F)$, то $\chi_{AB} = \chi_{BA}$. (b) Прямоугольный вариант (Sylvester): для $A \in M_{m\times n}$, $B \in M_{n \times m}$,
$$t^n \chi_{AB}(t) = t^m \chi_{BA}(t),$$
эквивалентно $\det(I_m + AB) = \det(I_n + BA)$ (Sylvester's determinant identity / Weinstein–Aronszajn).

Условия применимости. Любое поле; для (b) — $A$, $B$ согласованных размеров.

Идея доказательства. Для (a): на открытом плотном множестве $\det A \neq 0$ имеем $BA = A^{-1}(AB)A$, значит $\chi_{AB} = \chi_{BA}$; полином по $A$ — продолжаем по непрерывности (density argument). Для (b): блочная формула определителя для $\begin{pmatrix} I_m & -A \\ B & tI_n \end{pmatrix}$ двумя способами Шура.

Варианты и обобщения. Минимальные многочлены $\mu_{AB}$ и $\mu_{BA}$ отличаются не более чем на множитель $t$ (см. E15). Ненулевые собственные значения $AB$ и $BA$ (с алгебраическими кратностями) совпадают.

Используется в. [IMC-2000-DAY2-6, Putnam-2007-B6].

---

### E5. Спектральное отображение и тождества Newton (Newton's identities) для следов степеней

Формулировка. Для любого многочлена $p \in F[t]$ и $A \in M_n(F)$ собственные значения $p(A)$ суть $p(\lambda_i)$ с теми же кратностями (spectral mapping); в частности $\operatorname{tr}(A^k) = \sum_i \lambda_i^k =: p_k$. Соотношения Newton'а связывают power sums $p_k$ с $e_k = (-1)^k \cdot [t^{n-k}] \chi_A$:
$$p_k - e_1 p_{k-1} + e_2 p_{k-2} - \dots + (-1)^{k-1} e_{k-1} p_1 + (-1)^k k\, e_k = 0, \quad 1 \le k \le n.$$

Условия применимости. $\operatorname{char} F = 0$ или $\operatorname{char} F > n$ (иначе деление на $k$ в формулах Newton'а проблематично). Spectral mapping — любое поле, рассматривая собственные значения в алгебраическом замыкании.

Идея доказательства. Newton — алгебраическое тождество в кольце симметрических многочленов; см. Macdonald. Spectral mapping — упростить до Jordan: $p(J_k(\lambda))$ — верхнетреугольна с $p(\lambda)$ на диагонали.

Варианты и обобщения. Faddeev–LeVerrier (E12) — алгоритмическая упаковка. Над $\operatorname{char} 0$: знание $p_1, \dots, p_n$ восстанавливает $\chi_A$.

Используется в. [Putnam-1996-B4, IMC-2000-DAY2-6 (через trace)].

---

### E6. Trace-критерий нильпотентности

Формулировка. Над полем $\operatorname{char} 0$ (например $\mathbb Q, \mathbb R, \mathbb C$): $A \in M_n(F)$ нильпотентна $\iff$ $\operatorname{tr}(A^k) = 0$ для всех $k = 1, 2, \dots, n$ (равносильно — для всех $k \ge 1$).

Условия применимости. Только $\operatorname{char} F = 0$. Контрпример в $\operatorname{char} p$: $A = I_p$ над $\mathbb F_p$, $\operatorname{tr}(A^k) = p \equiv 0$, но $A$ не нильпотент.

Идея доказательства. По Newton (E5) равенства $p_1 = \dots = p_n = 0$ дают $e_1 = \dots = e_n = 0$, значит $\chi_A(t) = t^n$ и $A$ нильпотент по Cayley–Hamilton. Достаточно $k = 1, \dots, n$, дальнейшие $p_k$ автоматически нули.

Варианты и обобщения. Эквивалентные формулировки: $\sigma(A) = \{0\}$; $\det(I + xA) = 1$ как многочлен по $x$; $\det(\exp(xA)) = e^{x \operatorname{tr} A}$ и т.д.

Используется в. Putnam-1979-B6 ($A_1, \dots, A_k$ коммутируют, $A_i^2 = 0$ ⇒ ограничения на trace), типичный олимпиадный прием.

---

## Записи - Standard

### E7. Companion matrix, non-derogatory matrix, центразиатор

Формулировка. Companion matrix $C(p)$ многочлена $p(t) = t^n + a_{n-1} t^{n-1} + \dots + a_0$ имеет $\chi_{C(p)} = \mu_{C(p)} = p$. Матрица $A$ называется non-derogatory (циклической, неприводимой), если $\mu_A = \chi_A$. Эквивалентные характеризации:
1. $\exists v$ такой, что $\{v, Av, \dots, A^{n-1} v\}$ — базис ($v$ — cyclic vector).
2. Каждое собственное значение имеет геометрическую кратность $1$.
3. $A$ подобна companion'у $C(\chi_A)$.
4. $\dim Z(A) = n$, где $Z(A) = \{X : XA = AX\}$, и $Z(A) = F[A]$.

Условия применимости. Любое поле. (4) — теорема Frobenius'a о размерности centralizer'а; в общем случае $\dim Z(A) \ge n$, равенство $\iff A$ non-derogatory.

Идея доказательства. (1)$\Rightarrow$(3) — матрица $A$ в базисе $v, Av, \dots$ есть $C(\chi_A)$. $(2) \iff (1)$ — через жорданову форму. Frobenius формула: $\dim Z(A) = \sum_{i,j} \min(b_i, b_j)$ по размерам Jordan blocks; минимум $= n$ когда все $b_i$ различны и сосредоточены в одном блоке на каждое значение.

Варианты и обобщения. Frobenius rational canonical form: $A$ подобна $\bigoplus_i C(f_i)$ с $f_1 \mid f_2 \mid \dots \mid f_r = \mu_A$; $\prod f_i = \chi_A$. Для генерических $A$ $\mu_A = \chi_A$.

Используется в. Многократно — задачи на коммутаторы, classification under similarity.

---

### E8. Cayley–Hamilton как редукция степеней

Формулировка. $\operatorname{span}_F\{I, A, A^2, \dots\} = \operatorname{span}_F\{I, A, \dots, A^{n-1}\}$ имеет размерность $\deg \mu_A \le n$. В частности:
$$A^{-1} = \frac{(-1)^{n-1}}{\det A} \big( A^{n-1} - c_1 A^{n-2} + \dots + (-1)^{n-1} c_{n-1} I \big)$$
если $\det A \neq 0$. И $\operatorname{adj}(A) = (-1)^{n-1}\big(A^{n-1} - c_1 A^{n-2} + \dots + (-1)^{n-1} c_{n-1} I\big)$.

Условия применимости. Любое коммутативное кольцо; для формулы $A^{-1}$ — $\det A$ обратим.

Идея доказательства. По Cayley–Hamilton $A^n = c_1 A^{n-1} - c_2 A^{n-2} + \dots - (-1)^n c_n I$. Индукция — все $A^k$, $k \ge n$, выражаются через младшие. Для adjugate — переписать $\chi_A(A) = 0$ как $A \cdot Q(A) = c_n I$ с $Q$ степени $n-1$.

Варианты и обобщения. В коммутативной алгебре — выражение $A^{-1}$ как многочлена от $A$ полезно для аргумента «обратная остается в подалгебре». Faddeev–LeVerrier (E12) — рекурсия для $c_k$.

Используется в. [IMC-2000-DAY2-6, IMC-2009-DAY2-3] — основной приём, превращающий CH в инструмент.

---

### E9. Frobenius covariants и формула Сильвестра (Sylvester's formula)

Формулировка. Если $\mu_A = \prod_{i=1}^k (t - \lambda_i)$ (различные $\lambda_i$, в частности — $A$ диагонализуема), то проекторы
$$F_i := \prod_{j \neq i} \frac{A - \lambda_j I}{\lambda_i - \lambda_j}$$
удовлетворяют $F_i F_j = \delta_{ij} F_i$, $\sum F_i = I$, $A = \sum \lambda_i F_i$, и для любой функции $f$, корректной на $\sigma(A)$,
$$f(A) = \sum_{i=1}^k f(\lambda_i)\, F_i.$$
Это и есть Lagrange interpolation в матричной форме.

Условия применимости. $\mu_A$ имеет различные корни в $F$. Если корни кратные — нужна более общая Hermite interpolation (производные $f$ в $\lambda_i$ до порядка кратности минус один).

Идея доказательства. $F_i$ обнуляет $A - \lambda_j I$ для $j \neq i$, поэтому действует тождественно на $\ker(A - \lambda_i I)$ и нулём на остальных собственных подпространствах. $f(A) = \sum f(\lambda_i) F_i$ — проверяется на собственных подпространствах.

Варианты и обобщения. Hermite formula для случая кратных корней. Численно — Schur–Parlett.

Используется в. Любое вычисление $A^k$, $e^A$, $\sqrt{A}$ при diagonalizability.

---

### E10. Inner derivation $\Delta_A(X) = AX - XA$ + Cayley–Hamilton

Формулировка. Оператор $\Delta = \Delta_A : M_n \to M_n$, $\Delta X = AX - XA$, является derivation: $\Delta(XY) = (\Delta X) Y + X (\Delta Y)$. Собственные значения $\Delta$ суть $\lambda_i - \lambda_j$ для $\lambda_i, \lambda_j \in \sigma(A)$. Если $\Delta^2 B = 0$, то по индукции $\Delta^k(B^k) = k! (\Delta B)^k$; применение Cayley–Hamilton к $B$ (выражение $B^n$ через младшие степени) и линейности $\Delta^n$ даёт $\Delta^n(B^n) = 0$, откуда $(\Delta B)^n = 0$, то есть $AB - BA$ нильпотент.

Условия применимости. $A, B \in M_n(\mathbb C)$, условие $A^2 B + B A^2 = 2ABA$ ($= \Delta^2 B = 0$). Аналог работает над $\mathbb R$ и над $\overline F$, $\operatorname{char} F = 0$ (нужны $k!$).

Идея доказательства. Леibниц для $\Delta$ + индукция по $k$. Затем $B^n = \sum_{j<n} \alpha_j B^j$ по CH ⇒ $\Delta^n B^n = \sum \alpha_j \Delta^n B^j = 0$, так как $\Delta^n B^j = 0$ при $j < n$ (поскольку $\Delta^2 B = 0$ ⇒ $\Delta^k B^j$ убивается при $k > j$).

Используется в. [IMC-2009-DAY2-3]. Более широко — proof of Kleinecke–Shirokov: $[A, B]$ нильпотентен, если $[A, [A, B]] = 0$.

---

### E11. Density / continuity argument для матричных тождеств

Формулировка. Множество диагонализуемых матриц над $\mathbb C$ плотно в $M_n(\mathbb C)$ (открыто в Зариском смысле). Любое полиномиальное по элементам $A$ тождество достаточно проверить на диагонализуемых.

Условия применимости. Поле $\mathbb C$ или любое алгебраически замкнутое; работает и над $\mathbb R$ если тождество комплекс-аналитично. Нужна полиномиальность (или непрерывность) утверждения.

Идея доказательства. Матрицы с попарно различными собственными значениями = $\{A : \operatorname{disc}(\chi_A) \neq 0\}$ — дополнение к гиперповерхности, поэтому открыто плотно. На таких $A$ — диагонализуема и многие тождества тривиальны.

Варианты и обобщения. Стандартное доказательство Cayley–Hamilton; $\chi_{AB} = \chi_{BA}$; $\det e^A = e^{\operatorname{tr} A}$; равенство $\chi_{A \otimes B}(t)$ через $\sigma(A) \cdot \sigma(B)$ и т.д.

Используется в. Универсальный метод; в частности [IMC-2000-DAY2-6, Putnam-2007-B6].

---

## Записи - Exotic

### E12. Faddeev–LeVerrier (алгоритм Леверье–Фаддеева)

Формулировка. Рекурсия на коэффициенты $\chi_A$ через следы степеней. Полагаем $M_0 = 0$, $M_k = A M_{k-1} + c_{n-k+1} I$ для $k = 1, \dots, n$, где $c_{n-k} = -\frac{1}{k} \operatorname{tr}(A M_k)$, начиная с $c_n = 1$ (старший коэффициент $\chi_A(t) = t^n - c_{n-1} t^{n-1} - \dots$ в одной из нормировок). Эквивалентно — Newton'овские тождества переписаны как процедура.

Условия применимости. $\operatorname{char} F = 0$ или $> n$.

Идея доказательства. Прямое следствие Newton (E5) в матричной упаковке: $M_k$ — частичные суммы $\operatorname{adj}$-разложения.

Варианты и обобщения. Даёт побочно $\operatorname{adj}(A)$ и $A^{-1}$ за $O(n^4)$. Олимпиадное применение редко, но как инструмент «вычислить $\chi_A$ через $\operatorname{tr} A^k$» периодически возникает.

---

### E13. Putzer formula для $e^{tA}$

Формулировка. Пусть $\lambda_1, \dots, \lambda_n$ — собственные значения $A$ (с кратностями). Положим $P_0 = I$, $P_k = (A - \lambda_k I) P_{k-1}$ для $k = 1, \dots, n-1$. Тогда $P_n = \chi_A(A) = 0$ (Cayley–Hamilton) и
$$e^{tA} = \sum_{k=0}^{n-1} r_{k+1}(t)\, P_k,$$
где $r_1' = \lambda_1 r_1$, $r_1(0) = 1$; $r_k' = \lambda_k r_k + r_{k-1}$, $r_k(0) = 0$ для $k \ge 2$.

Условия применимости. $A \in M_n(\mathbb C)$, любые собственные значения (включая повторяющиеся, в любом порядке).

Идея доказательства. Подстановка проверяет $\frac{d}{dt} \sum r_{k+1} P_k = A \sum r_{k+1} P_k$ за счёт $A P_k = P_{k+1} + \lambda_{k+1} P_k$ и $P_n = 0$ (CH).

---

### E14. Generalized Cayley–Hamilton + determinant trick (трюк с определителем)

Формулировка. Пусть $M$ — конечно-порождённый модуль над коммутативным кольцом $R$, $I \subseteq R$ — идеал, $\varphi : M \to M$ — $R$-линейный с $\varphi(M) \subseteq IM$. Тогда существуют $a_1, \dots, a_n \in R$, $a_k \in I^k$, такие что
$$\varphi^n + a_1 \varphi^{n-1} + \dots + a_n \cdot \mathrm{id} = 0 \quad \text{в } \operatorname{End}_R(M).$$
В частности, $\varphi$ удовлетворяет монику $n$-й степени над $R$. Следствие — лемма Накаямы: если $IM = M$ и $I$ содержится в Jacobson radical'е $R$, то $M = 0$.

Условия применимости. $R$ — коммутативное; $M$ — конечно порождённый.

Идея доказательства. Записать образующие $m_1, \dots, m_n$ и $\varphi(m_i) = \sum a_{ij} m_j$ с $a_{ij} \in I$. Для матрицы $\Phi = (\delta_{ij} \varphi - a_{ij}) \in \operatorname{End}(M)^{n \times n}$ выполнено $\Phi (m_1, \dots, m_n)^T = 0$. Умножая слева на $\operatorname{adj} \Phi$, получаем $\det \Phi \cdot m_i = 0$ для всех $i$, то есть $\det \Phi \in \operatorname{Ann}(M)$ обнуляет $\mathrm{id}_M$. Раскрытие $\det$ даёт нужный многочлен.

Варианты и обобщения. Источник конструктивных доказательств целостности (integral element $\iff$ удовлетворяет монику над подкольцом). На олимпиаде встречается редко, но даёт мгновенные доказательства типа «образующие $\mathbb Z[\sqrt 2]$ как $\mathbb Z$-модуля → $\sqrt 2$ — корень моники».

---

### E15. Минимальные многочлены $AB$ и $BA$

Формулировка. Для $A, B \in M_n(F)$: $\mu_{AB}$ и $\mu_{BA}$ либо равны, либо отличаются множителем $t$, то есть $\mu_{AB}(t) \cdot t^{\varepsilon_1} = \mu_{BA}(t) \cdot t^{\varepsilon_2}$ для некоторых $\varepsilon_i \in \{0, 1\}$. Точнее: $t \mu_{AB}(t)$ и $t \mu_{BA}(t)$ имеют один и тот же набор корней, с теми же кратностями.

Условия применимости. Любое поле. Аналог для прямоугольных размеров — с поправкой на $t^{|m-n|}$ как в E4.

Идея доказательства. Для $\lambda \neq 0$: $(AB - \lambda I) X = 0 \Leftrightarrow (BA - \lambda I) (BX) = 0$, и $BX \neq 0$ (умножая исходное равенство на $A$ слева). Размерности обобщённых eigenspace'ов на $\lambda \neq 0$ совпадают. Для $\lambda = 0$ — могут различаться на $1$ (пример $A = (1,0)$, $B = (1,0)^T$: $AB = 1$, $BA = \begin{pmatrix} 1 & 0 \\ 0 & 0 \end{pmatrix}$).

Варианты и обобщения. Полный результат — теорема Flanders'a о возможных Jordan структурах $AB$ vs $BA$.

---

## Self-test

1. Пусть $A \in M_n(\mathbb C)$ и $\operatorname{tr}(A^k) = 0$ для $k = 1, 2, \dots, n$. Докажи, что $\det(I + A) = 1$.

2. $A, B \in M_n(\mathbb C)$. Докажи: $I - AB$ обратим $\iff I - BA$ обратим, и в этом случае $(I - BA)^{-1} = I + B(I - AB)^{-1} A$.

3. $A \in M_n(\mathbb R)$, $A^3 = A + I$. Докажи, что $\det A > 0$.

4. $A \in M_n(\mathbb C)$, $A^2 = A$. Найди $\dim \{X \in M_n : XA = AX\}$ через $r = \operatorname{rk} A$.

5. $A, B \in M_n(\mathbb C)$, $AB - BA = A$. Докажи, что $A$ нильпотентна.

6. $A \in M_n(\mathbb C)$, $A^k = I$ при некотором $k \ge 1$. Докажи, что $A$ диагонализуема.

7. $A \in M_n(\mathbb C)$ удовлетворяет $\operatorname{tr}(A^j) = 0$ для $j = 1, \dots, n$. Докажи, что для любого многочлена $p$ со $p(0) = 0$ выполнено $\operatorname{tr}(p(A)) = 0$.

8. $A \in M_n(\mathbb C)$, и пусть $f \in \mathbb C[t]$ имеет $f(\lambda) \neq 0$ для всех $\lambda \in \sigma(A)$. Докажи, что $f(A)$ обратима, и выпиши $f(A)^{-1}$ как многочлен от $A$ степени $\le n - 1$.

## Решения

1. По Newton (E5) условия $p_1 = \dots = p_n = 0$ дают $e_1 = \dots = e_n = 0$, то есть $\chi_A(t) = t^n$. Тогда все $\lambda_i = 0$, $\det(I + A) = \prod (1 + \lambda_i) = 1$.

2. Если $C := (I - AB)^{-1}$ существует, проверим прямой подстановкой: $(I - BA)(I + BCA) = I - BA + BCA - BABCA = I - BA + B(I - AB)CA = I - BA + BA = I$. Симметрично — обратное направление. (Hua identity, частный случай E4.)

3. Над $\mathbb C$ корни $t^3 - t - 1 = 0$ — один вещественный $\alpha \approx 1.3247$ и пара комплексно-сопряжённых $\beta, \bar\beta$ с $\beta \bar\beta = 1/\alpha > 0$. Спектр $A$ лежит в $\{\alpha, \beta, \bar\beta\}$, причём пара $\beta, \bar\beta$ входит с одинаковой кратностью (вещественный $A$). $\det A = \alpha^a (\beta\bar\beta)^b = \alpha^{a - b} > 0$.

4. $A$ — идемпотент, $\mu_A \mid t^2 - t$, диагонализуема: $A \sim \begin{pmatrix} I_r & 0 \\ 0 & 0 \end{pmatrix}$. Centralizer — блочно-диагональные $\begin{pmatrix} X & 0 \\ 0 & Y \end{pmatrix}$ с $X \in M_r$, $Y \in M_{n-r}$, размерность $r^2 + (n-r)^2$.

5. $\Delta_B(A) := BA - AB = -A$, то есть $A$ — собственный вектор $\Delta_B$ с собственным значением $-1$. По Leibniz'у $\Delta_B(A^k) = \sum_{i=0}^{k-1} A^i (\Delta_B A) A^{k-1-i} = -k A^k$, то есть $A, A^2, A^3, \dots$ — собственные векторы $\Delta_B$ на $-1, -2, -3, \dots$. У линейного оператора в $M_n(\mathbb C)$ (размерность $n^2$) лишь конечно много собственных значений, поэтому при некотором $k$ обязано быть $A^k = 0$. Альтернатива через trace: из $A = AB - BA$ имеем $\operatorname{tr} A = 0$; для $k \ge 1$ — $\operatorname{tr}(A^k) = \operatorname{tr}(A^{k-1}(AB - BA)) = \operatorname{tr}(A^k B) - \operatorname{tr}(A^{k-1} BA) = 0$ по cyclic property ($\operatorname{tr}(A^{k-1} B A) = \operatorname{tr}(A^k B)$). Значит $\operatorname{tr}(A^k) = 0 \, \forall k$, и по E6 $A$ нильпотентна.

6. $A^k = I \Rightarrow$ $A$ аннулируется $t^k - 1$. Над $\mathbb C$ многочлен $t^k - 1$ имеет различные корни (корни из единицы), значит $\mu_A \mid t^k - 1$ — squarefree. По E3 $A$ диагонализуема.

7. Newton + индукция: знание $p_1, \dots, p_n$ восстанавливает $e_1, \dots, e_n$, значит и весь $\chi_A$. Из $p_1 = \dots = p_n = 0$ ⇒ $\chi_A(t) = t^n$, значит $\sigma(A) = \{0\}$. Для любого $p$ с $p(0) = 0$ имеем $\sigma(p(A)) = \{p(0)\} = \{0\}$ по E5, значит $\operatorname{tr}(p(A)) = 0$.

8. По E5 $\sigma(f(A)) = \{f(\lambda) : \lambda \in \sigma(A)\}$, все ненулевые ⇒ $\det f(A) \neq 0$. Формула: возьми $g, h \in \mathbb C[t]$ с $g \cdot f + h \cdot \mu_A = 1$ (Bézout, поскольку $\gcd(f, \mu_A) = 1$); тогда $g(A) f(A) = I - h(A) \mu_A(A) = I$, так что $f(A)^{-1} = g(A) \bmod \mu_A$. Степень $g \bmod \mu_A$ — менее $\deg \mu_A \le n$.
