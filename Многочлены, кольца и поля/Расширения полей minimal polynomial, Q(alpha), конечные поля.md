---
topic: Многочлены, кольца и поля
subtopic: "Расширения полей: minimal polynomial, $\\mathbb{Q}(\\alpha)$, конечные поля"
sources:
  - "Keith Conrad — Trace and Norm I/II (expository notes)"
  - "Keith Conrad — Finite fields (expository note)"
  - "Keith Conrad — The Minimal Polynomial and Some Applications"
  - "Victor Wang — MOP 2018: Algebraic Conjugates and Number Theory (handout)"
  - "Yufei Zhao — Olympiad training handouts (algebraic conjugates / cyclotomic)"
  - "Lawrence Sun — Cyclotomic Polynomials in Olympiad Number Theory (AoPS)"
  - "Ray Li — Roots of Unity (Stanford lecture notes)"
  - "Dubickas–Smyth — Two Variations of a Theorem of Kronecker"
  - "Bogoşel — Kronecker's theorem on cyclotomic polynomials (blog/proof)"
  - "Engel — Problem-Solving Strategies (главы Polynomials, Number Theory)"
  - "Polya, Szegő — Problems and Theorems in Analysis II"
  - "M. Filaseta — Math 784: Algebraic Number Theory (lecture notes)"
  - "Wikipedia — Chevalley–Warning theorem / Liouville's theorem / Primitive element theorem / Finite field"
  - "IMC Compendium / Putnam Compendium"
problems_referenced:
  - IMC-2001-4
  - IMC-2007-6
  - IMC-2008-2
  - IMC-2008-DAY2-1
  - IMC-2010-DAY2-5
  - IMC-2018-2
  - IMC-2019-5
  - Putnam-1971-A6
  - Putnam-1985-A6
  - Putnam-1995-A4
  - Putnam-2008-B6
last_updated: 2026-04-27
---

# Расширения полей: minimal polynomial, $\mathbb{Q}(\alpha)$, конечные поля

## Scope
Тонкая работа с алгебраическими элементами над $\mathbb{Q}$, $\mathbb{F}_p$ и общим полем $K$: минимальный многочлен и его роль как «универсального соотношения», Galois-сопряжённые и симметрические функции, $\mathrm{Tr}$ и $\mathrm{N}$ как коэффициенты $m_\alpha$, структура $\mathbb{F}_q$ (циклическая группа $\mathbb{F}_q^\times$, Frobenius, решётка подполей), цикломатические $\Phi_n$ и Möbius-инверсия, Kronecker для алгебраических целых на единичной окружности, Liouville-неравенство как нижняя оценка $|q\alpha - p|$, Chevalley–Warning. Eisenstein и Capelli даны в соседнем файле «Факторизация и неприводимость» — здесь не повторяются.

## Записи — Core

### E1. Minimal polynomial (минимальный многочлен) — базовая теорема

Формулировка. Пусть $K$ — поле, $L/K$ — расширение, $\alpha \in L$ алгебраичен над $K$. Существует единственный монический многочлен $m_\alpha \in K[x]$ наименьшей степени с $m_\alpha(\alpha) = 0$. Свойства:
- $m_\alpha$ неприводим над $K$;
- $m_\alpha \mid f$ в $K[x]$ для любого $f \in K[x]$ с $f(\alpha) = 0$;
- $K[\alpha] = K(\alpha)$, $\dim_K K(\alpha) = \deg m_\alpha$;
- базис $K(\alpha)/K$ — $\{1, \alpha, \dots, \alpha^{n-1}\}$, $n = \deg m_\alpha$.

Условия применимости. Любое поле $K$. Для $K = \mathbb{Q}$ можно дополнительно потребовать $m_\alpha \in \mathbb{Z}[x]$ — это эквивалентно тому, что $\alpha$ — algebraic integer (E3).

Идея доказательства. Идеал $I_\alpha = \{f \in K[x]: f(\alpha) = 0\}$ — главный (PID), его генератор и есть $m_\alpha$. Неприводимость — из $K[x]/(m_\alpha) \cong K(\alpha)$ — поле.

Используется в. Универсальный язык для всех остальных записей. Упрощает оценку $\deg \alpha$ снизу: если можно показать, что $\alpha \notin K(\beta)$ для всех $\beta$ степени $< n$, то $\deg \alpha = n$.

---

### E2. Galois conjugates и симметрические функции

Формулировка. Пусть $\alpha$ алгебраичен над $K$, $m_\alpha = \prod_{i=1}^n (x - \alpha_i)$ в алгебраическом замыкании $\bar K$ (separable case). Тогда $\alpha_1, \dots, \alpha_n$ — $K$-сопряжённые $\alpha$, и любой $K$-симметрический полином от них лежит в $K$. В частности, для любого $f \in K[x]$
$$\prod_{i=1}^n f(\alpha_i) \in K, \qquad \sum_{i=1}^n f(\alpha_i) \in K.$$

Условия применимости. Separable extension (для $\mathrm{char}\, K = 0$ — всегда). Для несепарабельных надо учитывать кратности.

Идея доказательства. Симметрические функции — полиномы от элементарных $e_k$, а $e_k(\alpha_1,\dots,\alpha_n) = \pm$ коэффициент $m_\alpha \in K$.

Варианты и обобщения.
- **Galois closure**: если $L/K$ — Galois, то $\sigma(\alpha)$ для $\sigma \in \mathrm{Gal}(L/K)$ перебирает все сопряжённые с правильными кратностями.
- **Sum-trick для иррациональностей**: чтобы доказать $\alpha + \beta \notin \mathbb{Q}$ — оценить $\deg(\alpha + \beta)$ и проверить, что соответствующая симметрическая функция не лежит в $\mathbb{Q}$.

Используется в. [IMC-2001-4: $\Phi_q$ корни $\varepsilon_j$ — все сопряжены, $\prod p(\varepsilon_j)$ — целое число; либо $r$ обнуляется на всех $\varepsilon_j$, либо ни на одном], [IMC-2008-DAY2-1: использование примитивного корня и его сопряжённых].

---

### E3. Алгебраические целые: $\mathbb{Z} \cap \overline{\mathbb{Z}} = \mathbb{Z}$

Формулировка. $\alpha \in \mathbb{C}$ — algebraic integer (алгебраическое целое), если $m_\alpha \in \mathbb{Z}[x]$ (эквивалентно: $\alpha$ — корень монического $f \in \mathbb{Z}[x]$). Множество $\overline{\mathbb{Z}}$ всех таких $\alpha$ — кольцо. Ключевой факт: $\overline{\mathbb{Z}} \cap \mathbb{Q} = \mathbb{Z}$.

Условия применимости. Нужно $\mathbb{Z}$ как UFD; обобщается на любой нормальный домен (в смысле integral closure).

Идея доказательства. Если $\alpha = a/b \in \mathbb{Q}$ в несократимом виде и $\alpha^n + c_{n-1}\alpha^{n-1} + \dots + c_0 = 0$, домножая на $b^n$: $a^n = -b(c_{n-1} a^{n-1} + b\,\cdot \dots) \Rightarrow b \mid a^n \Rightarrow b = \pm 1$. Замкнутость $\overline{\mathbb{Z}}$ относительно $+, \times$ — через тензорное произведение колец конечного типа над $\mathbb{Z}$.

Варианты и обобщения.
- **Critical lemma**: $\alpha \in \overline{\mathbb{Z}} \iff \mathbb{Z}[\alpha]$ — конечно-порождённый $\mathbb{Z}$-модуль.
- **Sum of roots of unity** — algebraic integer; если ещё и $\in \mathbb{Q}$, то $\in \mathbb{Z}$ — стандартный финиш в задачах с $\zeta_n$-вычислениями.

Используется в. [Putnam-1985-A6 — sum of roots of unity rational ⇒ integer], [IMC-2007-6 (косвенно, через $a_0 = \prod \alpha_i \in \mathbb{Z}$)]. Универсальный финишер для argumenta типа «целое число, ограниченное по модулю $< 1$ ⇒ нуль».

---

### E4. Trace и Norm в $L/K$

Формулировка. Пусть $L/K$ — конечное separable, $[L:K] = n$, $\sigma_1, \dots, \sigma_n$ — все вложения $L \hookrightarrow \bar K$, тождественные на $K$. Для $\alpha \in L$
$$\mathrm{Tr}_{L/K}(\alpha) = \sum_{i} \sigma_i(\alpha), \qquad \mathrm{N}_{L/K}(\alpha) = \prod_{i} \sigma_i(\alpha).$$
Оба значения лежат в $K$. Если $L = K(\alpha)$ и $m_\alpha = x^n + c_{n-1}x^{n-1} + \dots + c_0$, то $\mathrm{Tr}(\alpha) = -c_{n-1}$, $\mathrm{N}(\alpha) = (-1)^n c_0$. Транзитивность: $\mathrm{Tr}_{M/K} = \mathrm{Tr}_{L/K} \circ \mathrm{Tr}_{M/L}$, аналогично для $\mathrm{N}$.

Условия применимости. Separable. Для $L \ne K(\alpha)$: вычисление $\mathrm{Tr}, \mathrm{N}$ через минимальный многочлен идёт со степенью $[L:K(\alpha)]$ как кратностью.

Идея доказательства. $\mathrm{Tr}, \mathrm{N}$ — характеристический многочлен умножения $m_\alpha: L \to L$ как $K$-линейного оператора. Совпадение с симметрическими функциями — стандартное.

Варианты и обобщения.
- **Norm equation**: $\mathrm{N}_{\mathbb{Q}(i)/\mathbb{Q}}(a+bi) = a^2 + b^2$, $\mathrm{N}_{\mathbb{Q}(\zeta_n)/\mathbb{Q}}(a - \zeta_n b) = \prod (a - \zeta_n^k b)$ — основа задач «представимо ли $N$ в виде $\dots$».
- **Trace nondegenerate**: $\langle x, y \rangle = \mathrm{Tr}(xy)$ — невырождённая билинейная форма (для separable). Используется в discriminant-based аргументах.

Используется в. [IMC-2019-5: разложение $A^4 + 4A^2B^2 + 16B^4 = (A^2+2AB+4B^2)(A^2-2AB+4B^2)$ как нормa в $\mathbb{Z}[\zeta_8]$ (или $\mathbb{Z}[i]$); анализ $\det = $ норма], стандартный приём в задачах с $\mathbb{Z}[i], \mathbb{Z}[\omega]$.

---

### E5. Структура $\mathbb{F}_q$: $|\mathbb{F}_q| = p^n$, $\mathbb{F}_q^\times$ циклическая, $x^q - x = \prod_{a \in \mathbb{F}_q}(x - a)$

Формулировка. Для каждого $q = p^n$ существует ровно одно (с точностью до изоморфизма) поле $\mathbb{F}_q$ из $q$ элементов. Свойства:
- $\mathbb{F}_q$ — splitting field $x^q - x$ над $\mathbb{F}_p$, причём $\{a \in \bar{\mathbb{F}}_p : a^q = a\} = \mathbb{F}_q$;
- $\mathbb{F}_q^\times$ — циклическая порядка $q-1$;
- $\mathrm{char}\,\mathbb{F}_q = p$, $a + a + \dots + a$ ($p$ раз) $= 0$ для всех $a$.

Условия применимости. Любое конечное поле.

Идея доказательства. Существование: в алгебраическом замыкании $\bar{\mathbb{F}}_p$ корни $x^q - x$ образуют подполе (т.к. Frobenius — гомоморфизм, $(\text{root})^q = \text{root}$). Цикличность $\mathbb{F}_q^\times$: конечная подгруппа $K^\times$ для любого поля $K$ — циклическая (через структурную теорему для абелевых конечных групп: если $|G| = n$, то $G$ имеет элемент порядка $\mathrm{exp}(G)$, и $\mathrm{exp}(G) \mid n$, а в поле $x^d = 1$ имеет $\le d$ корней).

Варианты и обобщения.
- **Frobenius automorphism** $\varphi: x \mapsto x^p$ — образующая $\mathrm{Gal}(\mathbb{F}_{p^n}/\mathbb{F}_p) \cong \mathbb{Z}/n\mathbb{Z}$.
- **Орбиты Frobenius на корнях**: для $f \in \mathbb{F}_p[x]$ неприводимый степени $d \iff$ один из его корней имеет $\varphi$-орбиту длины $d$.

Используется в. [IMC-2007-5: идеал в $R[X]$ и анализ корней через $\mathbb{F}_p$-структуру], [IMC-2018-2: $|F^+|$ vs $|F^\times|$ — несовместимы при изоморфизме], стандартный фон под все задачи с $\bmod p$.

---

### E6. Action of Frobenius and irreducible factors of $x^{q^n} - x$

Формулировка. Пусть $q = p^k$. Тогда в $\mathbb{F}_q[x]$
$$x^{q^n} - x = \prod_{d \mid n} \prod_{\substack{f \in \mathbb{F}_q[x] \\ f \text{ моник.\ непривод.} \\ \deg f = d}} f(x).$$
В частности, $\mathbb{F}_{q^n}$ содержит $\mathbb{F}_{q^d} \iff d \mid n$, и количество монических неприводимых $f \in \mathbb{F}_q[x]$ степени $n$ равно $\frac{1}{n} \sum_{d \mid n} \mu(d) q^{n/d}$ (формула Гаусса–Мёбиуса).

Условия применимости. $q = p^k$ простая степень. Для произвольного поля $K$ аналог не работает.

Идея доказательства. $\alpha \in \bar{\mathbb{F}}_q$ имеет $\alpha^{q^n} = \alpha \iff \alpha \in \mathbb{F}_{q^n} \iff [\mathbb{F}_q(\alpha):\mathbb{F}_q] \mid n$. Минимальный многочлен $\alpha$ имеет степень $[\mathbb{F}_q(\alpha):\mathbb{F}_q] = d \mid n$, его корни — Frobenius-орбита $\{\alpha, \alpha^q, \dots, \alpha^{q^{d-1}}\}$.

Варианты и обобщения.
- **Subfield lattice**: $\mathbb{F}_{p^a} \cap \mathbb{F}_{p^b} = \mathbb{F}_{p^{\gcd(a,b)}}$, $\mathbb{F}_{p^a} \cdot \mathbb{F}_{p^b} = \mathbb{F}_{p^{\mathrm{lcm}(a,b)}}$.
- **$\Phi_n$ над $\mathbb{F}_p$**: $\Phi_n$ распадается в $\mathbb{F}_p[x]$ на неприводимые одной степени $d = \mathrm{ord}_n(p)$ (порядок $p$ в $(\mathbb{Z}/n\mathbb{Z})^\times$).

Используется в. [IMC-2007-5: $R(X) \in I$, генератор $Q(X)$, корни $Q$ — корни единицы через анализ $c \mapsto c^m$ — это ровно Frobenius-orbit]; шаблонный аргумент «$\bar f$ распадается mod $p$ в произведение $f_d$ степеней $d \mid n$» для перебора возможных факторизаций.

---

### E7. Cyclotomic $\Phi_n$ — степень и неприводимость над $\mathbb{Q}$

Формулировка. Для $n \ge 1$
$$\Phi_n(x) = \prod_{\substack{1 \le k \le n \\ \gcd(k,n)=1}} (x - \zeta_n^k) \in \mathbb{Z}[x], \qquad \deg \Phi_n = \varphi(n).$$
$\Phi_n$ неприводим над $\mathbb{Q}$. Тождество $x^n - 1 = \prod_{d \mid n} \Phi_d(x)$ позволяет рекурсивно вычислять $\Phi_n$.

Условия применимости. $n \ge 1$ произвольное. Над $\mathbb{F}_p$ неприводимость теряется (см. E6).

Идея доказательства неприводимости (Дедекинд). Если $\zeta = \zeta_n$ имеет минимальный многочлен $f \mid \Phi_n$, и $p \nmid n$ простое, то $\zeta^p$ — также примитивный корень. Достаточно показать, что $\zeta^p$ — корень $f$. Допустим $g(\zeta^p) = 0$ для $g \mid \Phi_n$, $g \ne f$. Тогда $f(x) \mid g(x^p)$ в $\mathbb{Z}[x]$. Reduction mod $p$: $\bar g(x^p) = \bar g(x)^p$ (Frobenius), значит $\bar f \mid \bar g^p$, и $\gcd(\bar f, \bar g) \ne 1$ — но $\bar f \bar g \mid x^n - \bar 1$, у которого нет кратных корней (т.к. $p \nmid n$) — противоречие.

Варианты и обобщения.
- $\deg \Phi_n = \varphi(n)$, $\sum_{d \mid n} \varphi(d) = n$.
- **Möbius inversion**: $\Phi_n(x) = \prod_{d \mid n} (x^d - 1)^{\mu(n/d)}$.
- $\Phi_n(1) = p$, если $n = p^k$ — степень простого; $= 1$ иначе ($n > 1$, не степень простого).

Используется в. [IMC-2001-4: $\Phi_q$ как «общий аннулятор» сопряжённых], [IMC-2010-DAY2-5: $\gcd_{p \mid N}\frac{x^N-1}{x^{N/p}-1} = \Phi_N$], [IMC-2012-5: $\Phi_{2^{n+1}}$ через подстановку $Y = X(X+a)$], [IMC-2008-DAY2-1: примитивные корни порядка делящего $6k$].

---

## Записи — Standard

### E8. Tower law (мультипликативность степени)

Формулировка. Пусть $K \subset F \subset L$ — башня конечных расширений. Тогда $[L:K] = [L:F] \cdot [F:K]$. Базис $L/K$ получается перемножением базисов $F/K$ и $L/F$.

Условия применимости. Конечность критична. Для бесконечных расширений работает «трансцендентная степень + алгебраическая степень».

Идея доказательства. Если $\{e_i\}$ — базис $F/K$, $\{f_j\}$ — базис $L/F$, то $\{e_i f_j\}$ — базис $L/K$.

Варианты и обобщения.
- **Делимость**: $[K(\alpha):K] \mid [L:K]$ для любого $\alpha \in L$ — даёт мощные ограничения на возможные степени минимальных многочленов.
- Используется для доказательства иррациональности: $\sqrt[3]{2} \notin \mathbb{Q}(\sqrt 2)$, т.к. $3 \nmid 2$.

Используется в. Базовый. Применяется в любой задаче с этажами расширений: из $\alpha \in L$, $[L:\mathbb{Q}] = n$ ⇒ $\deg \alpha \mid n$.

---

### E9. Primitive element theorem (теорема о примитивном элементе)

Формулировка. Любое конечное separable расширение $L/K$ простое: $L = K(\theta)$ для некоторого $\theta \in L$. Конструктивно: если $L = K(\alpha, \beta)$, то для бесконечного $K$ почти все $\theta = \alpha + c \beta$, $c \in K$, подходят.

Условия применимости. Separable critical (для $\mathrm{char} = 0$ и для конечных полей выполнено автоматически). Для несепарабельных — контрпример $\mathbb{F}_p(x, y) / \mathbb{F}_p(x^p, y^p)$.

Идея доказательства. Над бесконечным $K$: $\theta = \alpha + c\beta$ имеет $\deg \theta = [K(\alpha,\beta):K]$ для всех, кроме конечного числа $c$ (исключаются $c$, для которых сопряжённые $\theta$ не различны). Над конечным $K$ — $\mathbb{F}_q$ — $L^\times$ циклична, генератор $\theta$ работает.

Используется в. Любая задача, где нужно «один общий $\theta$ вместо двух алгебраичных $\alpha, \beta$». Важно для редукции к одному минимальному многочлену.

---

### E10. Sum of $k$-th powers over $\mathbb{F}_q$ (тождество Лагранжа)

Формулировка. Для $q = p^n$ и $k \ge 0$ целого
$$\sum_{x \in \mathbb{F}_q} x^k = \begin{cases} -1 \pmod p, & k > 0 \text{ и } (q-1) \mid k, \\ 0, & k = 0 \text{ (трактуем } 0^0 = 1\text{) даёт } q \equiv 0, \text{ или } k > 0,\ (q-1) \nmid k. \end{cases}$$
(Точнее: при $k > 0$ сумма $= -1$ если $(q-1) \mid k$, иначе $0$.)

Условия применимости. $\mathbb{F}_q$ конечное. Доказательство для $0^0$: пишут отдельно; конвенция $0^0 = 0$ или $1$ — выбирается под задачу.

Идея доказательства. $\mathbb{F}_q^\times$ — циклическая порядка $q-1$ с образующей $g$. $\sum_{x \in \mathbb{F}_q^\times} x^k = \sum_{j=0}^{q-2} g^{jk}$ — геометрическая сумма; обнуляется при $g^k \ne 1$, т.е. $(q-1) \nmid k$, и равна $q - 1 \equiv -1$ иначе.

Варианты и обобщения.
- **Combinatorial nullstellensatz** (Alon) использует это тождество как ядро.
- Применяется в Chevalley–Warning (E12).

Используется в. Putnam, классический инструмент. [Putnam-1971-A6 — character sum / counting]. На IMC явно реже, но за многими $\bmod p$-аргументами стоит именно это тождество.

---

### E11. Chevalley–Warning theorem

Формулировка. Пусть $f_1, \dots, f_r \in \mathbb{F}_q[x_1, \dots, x_n]$ — полиномы с $\sum_i \deg f_i < n$. Обозначим $V = \{x \in \mathbb{F}_q^n: f_1(x) = \dots = f_r(x) = 0\}$. Тогда $|V| \equiv 0 \pmod p$ (где $p = \mathrm{char}\,\mathbb{F}_q$). В частности, если $(0,\dots,0) \in V$, то существует и нетривиальное решение.

Условия применимости. Конечное поле; ограничение на сумму степеней.

Идея доказательства. Индикатор: $\mathbf{1}_{f_i = 0}(x) = 1 - f_i(x)^{q-1}$. Тогда $|V| \equiv \sum_x \prod_i (1 - f_i^{q-1}) \pmod p$. Раскрывая скобки и применяя E10 к мономам, видим, что каждый член — сумма $\prod x_j^{e_j}$ по $\mathbb{F}_q^n$ — обнуляется, если хотя бы один $e_j$ не делится на $q - 1$ или $e_j = 0$. Условие $\sum \deg f_i < n$ гарантирует, что максимальная общая степень $< n(q-1)$, т.е. в любом мономе хотя бы один $e_j < q - 1$ — обнуление.

Варианты и обобщения.
- **Ax–Katz**: уточнение по $p$-адической оценке $|V|$.
- **Combinatorial Nullstellensatz** (Alon) — конкретная неконструктивная техника на той же основе.

Используется в. [Putnam-2008-B6 (через подсчёт нулей)], классическое применение — теорема Эрдёша–Гинзбурга–Зива (любые $2n-1$ целых содержат подмножество из $n$ с суммой $\equiv 0 \pmod n$) для $n = p$.

---

### E12. Möbius inversion для цикломатических

Формулировка. Из $x^n - 1 = \prod_{d \mid n} \Phi_d(x)$ Möbius-инверсия даёт
$$\Phi_n(x) = \prod_{d \mid n} (x^{n/d} - 1)^{\mu(d)} = \prod_{d \mid n} (x^d - 1)^{\mu(n/d)}.$$
В частности, для $n = pq$, $p \ne q$ простые: $\Phi_{pq}(x) = \frac{(x^{pq} - 1)(x - 1)}{(x^p - 1)(x^q - 1)}$.

Условия применимости. $n \ge 1$.

Идея доказательства. Möbius inversion в мультипликативном виде на функции $f(n) = \Phi_n$, $g(n) = x^n - 1$: $f(n) = \prod_{d \mid n} g(d)^{\mu(n/d)}$.

Варианты и обобщения. Аналогично для любой мультипликативной свёртки полиномов / последовательностей.

Используется в. [IMC-2010-DAY2-5: $\Phi_N$ как $\gcd$ нескольких $(x^N-1)/(x^{N/p}-1)$, всё через Möbius], формальные манипуляции с подсчётом полиномов в $\mathbb{F}_p[x]$.

---

### E13. Kronecker's theorem (теорема Кронекера) о корнях единицы

Формулировка. Пусть $\alpha \in \overline{\mathbb{Z}} \setminus \{0\}$ — ненулевое алгебраическое целое, и все его сопряжённые $\alpha = \alpha_1, \dots, \alpha_n$ удовлетворяют $|\alpha_i| \le 1$. Тогда $\alpha$ — корень единицы.

Условия применимости. Только для алгебраических целых ($m_\alpha \in \mathbb{Z}[x]$, монический).

Идея доказательства. Степени $\alpha^k$ — все алгебраические целые той же степени $\le n$ с сопряжёнными $|\alpha_i^k| \le 1$. Коэффициенты $m_{\alpha^k}$ — элементарные симметрические $\le \binom{n}{j}$, целые ⇒ конечно много возможностей. Значит среди $\alpha, \alpha^2, \dots$ есть совпадающие: $\alpha^a = \alpha^b$ ⇒ $\alpha^{b-a} = 1$.

Варианты и обобщения.
- **Smyth (1971)**: если $\alpha$ — алгебраическое целое и $\alpha \ne $ корень единицы и $\alpha$ не сопряжено своему обратному, то $M(\alpha) \ge $ корень $x^3 - x - 1$ ($\approx 1.32$).
- **Lehmer's problem** (open): нижняя оценка $M(\alpha) > 1$ для $\alpha$ не корень единицы, не доказана с конкретной константой выше $\approx 1.176$ (Mahler measure).

Используется в. [IMC-2007-6: $|P(z)| \le 2$ на $|z| = 1$, $a_0 = 1, |a_n| = 1$ ⇒ роли корней — корни единицы], стандартный приём в задачах «алгебраический + ограниченный ⇒ конечная структура».

---

### E14. Multiplicative ↛ additive: $(\mathbb{F},+) \not\cong (\mathbb{F}^\times,\cdot)$

Формулировка. Для любого поля $\mathbb{F}$ группы $(\mathbb{F},+)$ и $(\mathbb{F}^\times,\cdot)$ не изоморфны.

Условия применимости. Любое поле. В характеристике $0$ — очевидно (одна делится, другая имеет $\pm 1$ без $\sqrt{-1}$ или с, в любом случае mismatched torsion). В характеристике $p > 0$: $(\mathbb{F},+)$ — $p$-периодическая, $(\mathbb{F}^\times,\cdot)$ — содержит элементы любого порядка делящего $|F^\times|$, не делящегося на $p$.

Идея доказательства.
- Конечный случай: $|F^\times| = |F| - 1 \ne |F|$ — несовпадение порядков.
- $\mathrm{char}\,F = 0$: $(F,+)$ torsion-free (содержит $\mathbb{Z}$), а $-1 \in F^\times$ имеет порядок $2$. Противоречие.
- $\mathrm{char}\,F = p > 2$: $(F,+)$ — $\mathbb{F}_p$-векторное пространство, все элементы порядка $1$ или $p$. Но $-1 \in F^\times$ имеет порядок $2 \ne p$.
- $\mathrm{char}\,F = 2$: $(F,+)$ — $\mathbb{F}_2$-векторное пространство, все элементы порядка $\le 2$. Если $\cong (F^\times,\cdot)$, то $x^2 = 1$ для всех $x \in F^\times$, но в поле уравнение $x^2 = 1$ имеет $\le 2$ корня, значит $|F^\times| \le 2$, $|F| \le 3$. Перебор $|F| \in \{2, 3\}$: $|\mathbb{F}_2| = 2$, $|\mathbb{F}_2^\times| = 1$ — не равны; $\mathrm{char} 3 \ne 2$.

Варианты и обобщения. Для общих коммутативных колец вопрос усложняется, но «структурная разница из Frobenius» — общий шаблон.

Используется в. [IMC-2018-2: ответ — изоморфизм невозможен. Аккуратно разобрать оба случая char = 0 и char = p].

---

### E15. Liouville's inequality (неравенство Лиувилля)

Формулировка. Пусть $\alpha$ — алгебраическое число степени $n \ge 2$ с минимальным многочленом $m_\alpha \in \mathbb{Z}[x]$. Существует $C(\alpha) > 0$ такая, что для всех $p, q \in \mathbb{Z}$, $q > 0$, $p/q \ne \alpha$:
$$\left| \alpha - \frac{p}{q} \right| \ge \frac{C(\alpha)}{q^n}.$$

Условия применимости. $n \ge 2$ (для $n = 1$ $\alpha \in \mathbb{Q}$ и $|q\alpha - p|$ может быть нулём).

Идея доказательства. $|m_\alpha(p/q)| \ge 1/q^n$ (числитель $\ne 0$ т.к. $\alpha$ иррационально и $m_\alpha$ — неприводим, значит не имеет рациональных корней; числитель — целое $\ne 0$, $\ge 1$). С другой стороны, $|m_\alpha(p/q)| \le |\alpha - p/q| \cdot \max_{x \in [\alpha-1, \alpha+1]} |m_\alpha'(x)|$.

Варианты и обобщения.
- **Thue–Siegel–Roth**: $|\alpha - p/q| \ge c/q^{2+\varepsilon}$ для алгебраических $\alpha$ (но неэффективно).
- Используется для доказательства трансцендентности $\sum 10^{-k!}$ — Liouville number.

Используется в. Putnam-style задачи на «$\alpha$ плохо приближается рациональным $\Rightarrow$ структурное следствие». На IMC прямого использования нет, но техника «минимальный многочлен → нижняя оценка» — ценна.

---

## Записи — Exotic

### E16. Discriminant и trace pairing nondegenerate

Формулировка. Пусть $L/K$ — finite separable, $\{e_1,\dots,e_n\}$ — $K$-базис $L$. Discriminant $\mathrm{disc}(e_1,\dots,e_n) = \det(\mathrm{Tr}_{L/K}(e_i e_j))_{i,j}$. Для $L = K(\alpha)$, базиса $\{1, \alpha, \dots, \alpha^{n-1}\}$:
$$\mathrm{disc} = \prod_{i < j} (\sigma_i \alpha - \sigma_j \alpha)^2 = (-1)^{n(n-1)/2} \mathrm{N}_{L/K}(m_\alpha'(\alpha)).$$
Дискриминант ненулевой $\iff$ $L/K$ separable.

Условия применимости. Separable. В характеристике $p$ для несепарабельных $\mathrm{disc} = 0$.

Идея доказательства. Vandermonde $(\sigma_i \alpha^j) \cdot (\sigma_i \alpha^j)^T$ даёт матрицу $\mathrm{Tr}(\alpha^{i+j})$, определитель — Vandermonde в квадрате.

Используется в. Стандартный инструмент в алгебраической теории чисел; на олимпиадах — редко напрямую. Но для оценки $[\mathbb{Z}[\alpha] : \mathcal{O}_K]^2 = \mathrm{disc}(\alpha)/\mathrm{disc}(\mathcal{O}_K)$ — мощный аргумент в задачах с algebraic integers.

---

### E17. Capelli's theorem (см. соседний файл)

Формулировка. См. файл «Факторизация и неприводимость…», запись E19. Утверждение: $f(g(x))$ неприводим над $K$ $\iff$ $g(x) - \alpha$ неприводим над $K(\alpha)$, где $\alpha$ — корень $f$.

Используется в. [IMC-2012-5]. В этой подтеме включён как cross-link — ключевой пример «работа в $K(\alpha)$ вместо $K$».

---

## Self-test

1. Пусть $\alpha = \sqrt{2} + \sqrt{3}$. Найти $m_\alpha \in \mathbb{Z}[x]$ и доказать, что $\deg \alpha = 4$, в частности $\alpha \notin \mathbb{Q}(\sqrt 2) \cup \mathbb{Q}(\sqrt 3)$.
2. Пусть $\alpha = 2\cos(2\pi/7)$. Доказать, что $\alpha$ — алгебраическое целое, найти $m_\alpha$.
3. Доказать: если $a_1, \dots, a_n$ — корни $n$-й степени из единицы, и $\sum a_i \in \mathbb{Q}$, то $\sum a_i \in \mathbb{Z}$.
4. Пусть $f \in \mathbb{Z}[x]$ — монический степени $n$, все корни которого по модулю $\le 1$. Доказать, что все корни — корни единицы или нуль.
5. $|F| = q$ конечное поле, $f \in F[x_1, x_2, x_3]$ — полиномиал с $\deg f \le 2$. Доказать, что $f$ имеет хотя бы один корень в $F^3$ (если $f(0,0,0) = 0$ — то нетривиальный).
6. Поле $\mathbb{F}$ удовлетворяет $(\mathbb{F},+) \cong (\mathbb{F}^\times,\cdot)$. Доказать, что таких полей не существует.
7. Доказать тождество: $\sum_{x \in \mathbb{F}_p} x^{p-1} \equiv -1 \pmod p$ и $\sum_{x \in \mathbb{F}_p} x^{p-2} \equiv 0 \pmod p$.
8. Пусть $\alpha \in \mathbb{C}$ алгебраичен над $\mathbb{Q}$ степени $n$, и $\alpha + \alpha^{-1} \in \mathbb{Q}$. Что можно сказать про степень $\mathbb{Q}(\alpha)/\mathbb{Q}(\alpha + \alpha^{-1})$? Привести пример с $n = 4$.
9. Пусть $K$ — поле, $a, b \in K$, $\alpha = \sqrt[3]{a} + \sqrt[3]{b}$ (фиксированные корни в $\bar K$). Найти явно полином в $K[x]$, аннулирующий $\alpha$, степени $\le 9$. Когда он минимальный?
10. $f \in \mathbb{F}_p[x]$ неприводим степени $n$. Сколько существует подполей в $\mathbb{F}_p[x]/(f)$, и какие у них размеры?

## Решения

1. $\alpha^2 = 5 + 2\sqrt 6$, $(\alpha^2 - 5)^2 = 24$, итого $\alpha$ — корень $f(x) = x^4 - 10x^2 + 1$. Покажем неприводимость через структуру: $\alpha \in \mathbb{Q}(\sqrt 2, \sqrt 3)$, причём $\alpha^2 - 5 = 2\sqrt 6 \in \mathbb{Q}(\alpha) \Rightarrow \sqrt 6 \in \mathbb{Q}(\alpha)$. Тогда $\alpha \sqrt 6 = 2\sqrt 3 + 3\sqrt 2$, из системы $\{\alpha = \sqrt 2 + \sqrt 3,\ \alpha\sqrt 6 = 3\sqrt 2 + 2\sqrt 3\}$ выражаются $\sqrt 2, \sqrt 3$ — значит $\mathbb{Q}(\alpha) = \mathbb{Q}(\sqrt 2, \sqrt 3)$, $[\mathbb{Q}(\alpha):\mathbb{Q}] = 4$. Значит $\deg \alpha = 4$ и $f = m_\alpha$ неприводим. См. [E1, E8].

2. $\alpha = \zeta_7 + \zeta_7^{-1}$, $\zeta_7$ удовлетворяет $\Phi_7$. $\alpha^3 + \alpha^2 - 2\alpha - 1 = 0$ (стандартное вычисление через $\zeta + 1/\zeta$ и Newton). $m_\alpha = x^3 + x^2 - 2x - 1$ — неприводим над $\mathbb{Q}$ (рациональных корней нет, $\deg = 3$). См. [E2, E7].

3. Сумма корней единицы — algebraic integer (E3). Если она $\in \mathbb{Q}$, то $\in \overline{\mathbb{Z}} \cap \mathbb{Q} = \mathbb{Z}$. См. [E3].

4. См. [E13]. Степени $\alpha^k$ имеют ограниченные сопряжённые, конечное число возможных $m_{\alpha^k}$ ⇒ совпадение, т.е. $\alpha^a = \alpha^b$.

5. Применить Chevalley–Warning: $\deg f \le 2 < 3 =$ число переменных, и $f(0,0,0) = 0$ ⇒ количество нулей делится на $p$ (или $\ge 1$), значит нетривиальный нуль есть. См. [E11].

6. См. [E14]. Char $0$: $-1 \in F^\times$ — порядок $2$, $(F,+)$ — torsion-free (содержит $\mathbb{Z}$). Char $p > 2$: $(F,+)$ имеет экспоненту $p$, но $-1 \in F^\times$ — порядок $2 \ne p$. Char $2$: $(F,+)$ — $\mathbb{F}_2$-vector space ⇒ если $(F^\times,\cdot) \cong (F,+)$, то $x^2 = 1$ для всех $x \in F^\times$ ⇒ $|F^\times| \le 2$, разбираем $|F| \in \{2,3\}$ — не сходится.

7. По малой теореме Ферма $x^{p-1} = 1$ для $x \in \mathbb{F}_p^\times$, $0$ для $x = 0$. Сумма $= p - 1 \equiv -1 \pmod p$. Для $x^{p-2}$: $(p-1) \nmid (p-2)$ при $p \ge 3$, значит сумма $\equiv 0$ по E10.

8. Пусть $\beta = \alpha + \alpha^{-1} \in \mathbb{Q}$. Тогда $\alpha$ удовлетворяет $x^2 - \beta x + 1 = 0$ над $\mathbb{Q}(\beta) = \mathbb{Q}$. Значит $[\mathbb{Q}(\alpha):\mathbb{Q}(\beta)] \in \{1,2\}$. При $n = 4$: $\alpha = \zeta_5$, $\beta = 2\cos(2\pi/5) = (\sqrt 5 - 1)/2$, $[\mathbb{Q}(\zeta_5):\mathbb{Q}(\beta)] = 2$, $[\mathbb{Q}(\beta):\mathbb{Q}] = 2$, итого $4 = n$. См. [E1, E8].

9. $\alpha^3 = (\sqrt[3]{a} + \sqrt[3]{b})^3 = a + b + 3\sqrt[3]{ab}\,\alpha$. Пусть $c = \sqrt[3]{ab}$, тогда $\alpha^3 - 3c\alpha - (a+b) = 0$ и $c^3 = ab$. Из первого: $c = (\alpha^3 - (a+b))/(3\alpha)$, кубируем и используем $c^3 = ab$:
$$(\alpha^3 - (a+b))^3 = 27\, ab\, \alpha^3.$$
Это даёт многочлен $g(x) = (x^3 - (a+b))^3 - 27\,ab\,x^3 \in K[x]$ степени $9$, аннулирующий $\alpha$. $g$ — минимальный, когда $\alpha$ имеет степень $9$, что эквивалентно $[K(\sqrt[3]{a}, \sqrt[3]{b}):K] = 9$ (т.е. $\sqrt[3]{a} \notin K$, $\sqrt[3]{b} \notin K(\sqrt[3]{a})$, что включает $\sqrt[3]{ab} \notin K$). См. [E1, E8].

10. Подполя $\mathbb{F}_{p^n}$ — $\mathbb{F}_{p^d}$, $d \mid n$, по одному на каждый делитель. См. [E6].
