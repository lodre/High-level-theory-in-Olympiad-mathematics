---
topic: Многочлены, кольца и поля
subtopic: "Многочлены над $\\mathbb{F}_p$ и $\\mathbb{F}_q$"
sources:
  - "Keith Conrad — Finite Fields (expository note)"
  - "Keith Conrad — Roots and Irreducibles"
  - "Keith Conrad — The Artin–Schreier theorem"
  - "Noga Alon — Combinatorial Nullstellensatz (Combin. Probab. Comput. 1999)"
  - "Evan Chen — Combinatorial Nullstellensatz handout (BMC 2018)"
  - "Yufei Zhao — Integer Polynomials (MOP 2007 Black Group handout)"
  - "Lawrence Sun — Cyclotomic Polynomials in Olympiad Number Theory (AoPS)"
  - "Lidl, Niederreiter — Finite Fields (Cambridge)"
  - "Polya, Szegő — Problems and Theorems in Analysis II"
  - "Aaron Landesman — Notes on Finite Fields"
  - "Wikipedia — Chevalley–Warning theorem / Lucas's theorem / Permutation polynomial / Artin–Schreier theory"
  - "IMC Compendium / IMC official solutions 2007, 2011"
  - "Putnam Compendium"
problems_referenced:
  - IMC-1995-5
  - IMC-2003-2
  - IMC-2007-1
  - IMC-2007-5
  - IMC-2011-3
  - IMC-2011-DAY2-4
  - IMC-2022-3
  - IMC-2022-6
  - IMO-2007-6
  - Putnam-1971-B6
  - USAMO-1999-6
last_updated: 2026-04-27
---

# Многочлены над $\mathbb{F}_p$ и $\mathbb{F}_q$

## Scope
Тождества и техники, специфичные для многочленов над конечными полями: Frobenius и freshman's dream, тождество $x^q - x = \prod_{a \in \mathbb{F}_q}(x-a)$, степенные суммы $\sum_{a \in \mathbb{F}_q} a^k$, цикличность $\mathbb{F}_q^*$, различие «многочлен как формальный объект» vs «многочлен как функция $\mathbb{F}_q \to \mathbb{F}_q$», факторизация $x^{q^n} - x$ как произведение всех неприводимых делящих степеней. Полиномиальный метод: Chevalley–Warning, Combinatorial Nullstellensatz, Lucas, Hensel-lift, Artin–Schreier, EGZ через Chevalley. Acceptance — на IMC и Putnam все перечисленное допустимо без вывода.

## Записи — Core

### E1. Frobenius endomorphism (эндоморфизм Фробениуса) и freshman's dream

Формулировка. В любом коммутативном кольце характеристики $p$ (в частности в $\mathbb{F}_q[x]$, $q = p^n$) отображение $\varphi_p\colon a \mapsto a^p$ — кольцевой гомоморфизм. Следствия:
- $(x+y)^p = x^p + y^p$ (freshman's dream),
- $(f+g)^{p^k} = f^{p^k} + g^{p^k}$ для $f,g \in \mathbb{F}_q[x]$,
- $\varphi_p$ — автоморфизм $\mathbb{F}_q$ (так как поле конечно и $\varphi_p$ инъективен), порождающий циклическую группу $\operatorname{Gal}(\mathbb{F}_{p^n}/\mathbb{F}_p) = \langle \varphi_p \rangle$ порядка $n$.

Условия применимости. $\operatorname{char} = p$ — критично; в характеристике $0$ всё ломается.

Идея доказательства. $\binom{p}{k} \equiv 0 \pmod p$ для $1 \le k \le p-1$ (числитель содержит $p$, знаменатель — нет). Биномиальное разложение даёт результат.

Варианты и обобщения.
- $\sigma\colon a \mapsto a^q$ — относительный Frobenius, фиксирует $\mathbb{F}_q$ и порождает $\operatorname{Gal}(\mathbb{F}_{q^m}/\mathbb{F}_q)$.
- Если $f \in \mathbb{F}_p[x]$ и $\alpha$ — корень в $\overline{\mathbb{F}_p}$, то $\alpha^p, \alpha^{p^2}, \dots$ — тоже корни (минимальный многочлен над $\mathbb{F}_p$ инвариантен относительно $\varphi_p$). Корни разбиваются на «Frobenius orbits» длины $\deg$ минимального многочлена.

Используется в. [IMC-2011-3]: вычисление $x^{p^k} \pmod{x^p - x + 1}$ через итерации Фробениуса даёт $x^{p^k} \equiv x - k \pmod{p}$. Стандартный «атом» в задачах с многочленами над $\mathbb{F}_p$.

---

### E2. Тождество $x^q - x = \prod_{a \in \mathbb{F}_q}(x - a)$ и Wilson's theorem (теорема Вильсона) в полиномиальной форме

Формулировка. Над $\mathbb{F}_q$ выполнено
$$x^q - x = \prod_{a \in \mathbb{F}_q}(x - a), \qquad x^{q-1} - 1 = \prod_{a \in \mathbb{F}_q^\times}(x - a).$$
Подстановка $x = 0$ во вторую формулу: $-1 = (-1)^{q-1} \prod_{a \ne 0} a$, то есть $\prod_{a \in \mathbb{F}_q^\times} a = -1$ (теорема Вильсона; для $q = p$ это $(p-1)! \equiv -1 \pmod p$).

Условия применимости. Любое конечное поле $\mathbb{F}_q$. Идентификация делает $x^q - x$ универсальным «фильтром» элементов поля.

Идея доказательства. По малой теореме Ферма $a^q = a$ для всех $a \in \mathbb{F}_q$, итого $q$ различных корней у многочлена степени $q$ — все, и старший коэффициент $1$.

Варианты и обобщения.
- $\mathbb{F}_{q^n}$ — поле разложения $x^{q^n} - x$ над $\mathbb{F}_q$.
- $\gcd(f(x), x^q - x) = \prod_{a \in \mathbb{F}_q,\, f(a) = 0}(x - a)$ — выделяет корни $f$, лежащие в $\mathbb{F}_q$. База алгоритма Berlekamp.
- Если $f \in \mathbb{F}_q[x]$ удовлетворяет $f(a) = 0$ для всех $a \in \mathbb{F}_q$, то $(x^q - x) \mid f(x)$.

Используется в. [IMC-2011-3] — ключевое тождество в кольце $\mathbb{F}_p[x]/(x^p - x + 1)$: $\prod_{k=0}^{p-1}(x - k) = x^p - x \equiv -1$. Wilson's polynomial form входит в стандартный арсенал Putnam.

---

### E3. Степенные суммы $\sum_{a \in \mathbb{F}_q} a^k$

Формулировка. Для $k \ge 0$:
$$\sum_{a \in \mathbb{F}_q} a^k = \begin{cases} -1, & (q-1) \mid k,\ k > 0, \\ 0, & \text{иначе.}\end{cases}$$
Соглашение: $0^0 = 1$, поэтому при $k = 0$ сумма равна $|\mathbb{F}_q| = 0$ в $\mathbb{F}_q$.

Условия применимости. Любое конечное поле. Доказательство ровно через цикличность $\mathbb{F}_q^\times$.

Идея доказательства. $\mathbb{F}_q^\times = \langle g \rangle$, $\sum_{a \ne 0} a^k = \sum_{j=0}^{q-2} g^{jk} = \frac{g^{(q-1)k} - 1}{g^k - 1}$, если $g^k \ne 1$. Если $(q-1) \mid k$, все слагаемые $= 1$, сумма $= q - 1 = -1$ в $\mathbb{F}_q$.

Варианты и обобщения.
- Полиномиальная версия: для $f \in \mathbb{F}_q[x]$ степени $< q - 1$ сумма $\sum_{a \in \mathbb{F}_q} f(a) = 0$ (раскладываем по $a^k$).
- Это «дискретный» аналог $\int_0^{2\pi} e^{ikt} dt = 0$ при $k \ne 0$.
- Следствие, лежащее в основе Chevalley–Warning (см. E8): $\sum_{a \in \mathbb{F}_q^n} g(a) = 0$ для $g$ полинома с $\deg_{x_i} g < q - 1$ для какой-нибудь координаты.

Используется в. Стандартный приём для подсчёта решений уравнений и характерсумм; неявно — в [IMC-2003-2] (через сумму элементов и перестановку), [IMC-2022-6] (анализ симметрической суммы по перестановке).

---

### E4. Root-counting principle и polynomial vanishing (принцип «слишком много корней» в $\mathbb{F}_q[x]$)

Формулировка. Многочлен $f \in \mathbb{F}_q[x]$ степени $n$ имеет не более $n$ корней в $\mathbb{F}_q$ (и в любом расширении). Полином $f(x_1, \dots, x_n) \in \mathbb{F}_q[x_1, \dots, x_n]$ степени $\le d_i$ по $x_i$, обнуляющийся на $\prod S_i$ с $|S_i| > d_i$, тождественно $\equiv 0$.

Условия применимости. $\mathbb{F}_q$ — поле, в кольце $\mathbb{F}_q[x]$ работает обычная теорема Безу. Для функций $\mathbb{F}_q \to \mathbb{F}_q$ ограничение по степени $< q$ нужно (см. E6).

Идея доказательства. Индукция по $n$ + теорема Безу: $f(\alpha) = 0 \Rightarrow (x - \alpha) \mid f$. Многомерный случай — индукция по числу переменных.

Варианты и обобщения.
- Schwartz–Zippel: для случайного $\bar a \in S^n$ с $|S| = s$ имеем $\Pr[f(\bar a) = 0] \le \deg f / s$ для $f \not\equiv 0$.
- В $\mathbb{F}_q[x]$ полиномиальная функция степени $< q$ однозначно определяется своими значениями.
- Полезный частный случай: если $f \in \mathbb{Z}[x]$ степени $n$ удовлетворяет $f(a) \equiv 0 \pmod p$ для $> n$ различных $a$, то по mod $p$ имеем $\bar f \equiv 0$.

Используется в. [IMC-1995-5: $(A + tB)^n$ как полином от $t$ степени $\le n$ с матричными коэффициентами, $n+1$ значений $t$ дают тождественный $0$]. [IMC-2007-1: $f \in \mathbb{Z}[x]$ степени $\le 2$, $f(0), f(1), \dots, f(4) \equiv 0 \pmod 5$ — пять корней при степени $2$, значит $\bar f \equiv 0 \pmod 5$, все коэффициенты делятся на $5$]. [IMC-2007-5] аналогично.

---

### E5. Цикличность $\mathbb{F}_q^\times$ и primitive elements (первообразные элементы)

Формулировка. $\mathbb{F}_q^\times$ — циклическая группа порядка $q - 1$. Существует первообразный элемент $g$ ($\operatorname{ord}(g) = q-1$), число первообразных элементов $= \varphi(q-1)$. Любой $a \in \mathbb{F}_q^\times$ удовлетворяет $a^{q-1} = 1$, $\operatorname{ord}(a) \mid q-1$. Уравнение $x^d = 1$ имеет ровно $\gcd(d, q-1)$ решений в $\mathbb{F}_q^\times$.

Условия применимости. Любое конечное поле. Не путать со структурой $(\mathbb{Z}/n)^\times$ — там нет первообразных корней при $n = 8, 12, \dots$.

Идея доказательства. Пусть $m$ — экспонента $\mathbb{F}_q^\times$ (НОК порядков). Все $a$ удовлетворяют $x^m = 1$, степень $\le m$ — значит $|\mathbb{F}_q^\times| \le m$. Но $m \mid |G| = q - 1$, итого $m = q-1$. В абелевой группе экспонента достигается: пусть $a, b$ имеют порядки $r, s$; найдётся элемент порядка $\operatorname{lcm}(r,s)$.

Варианты и обобщения.
- Первообразных элементов «много»: $\varphi(q-1)/(q-1) \gg 1/\log\log q$ (Mertens).
- Любая конечная подгруппа $K^\times$ для произвольного поля $K$ — циклическая (тот же аргумент).
- $x^d = a$ имеет решение $\iff a^{(q-1)/\gcd(d,q-1)} = 1$, и тогда решений ровно $\gcd(d, q-1)$.

Используется в. [IMC-2007-5]: «$Q(c)=0 \Rightarrow c^N = 1$ для некоторого $N$» — из конечности порядка элемента в подходящем расширении $\mathbb{F}_{q^k}^\times$. [IMC-2011-3]: $x^p \equiv x - 1$ ⇒ через $p$ итераций возвращаемся к $x$; орбита Фробениуса в $\mathbb{F}_p[x]/(x^p - x + 1) \cong \mathbb{F}_{p^p}$ имеет длину $p$. Любая задача про порядки в $\mathbb{F}_q$.

---

### E6. Polynomial vs polynomial function: ядро отображения $\mathbb{F}_q[x] \to \operatorname{Func}(\mathbb{F}_q, \mathbb{F}_q)$

Формулировка. Отображение «многочлен → функция» $\mathbb{F}_q[x] \to \mathbb{F}_q^{\mathbb{F}_q}$ сюръективно, его ядро — главный идеал $(x^q - x)$. Следствие: каждая функция $\mathbb{F}_q \to \mathbb{F}_q$ задаётся ровно одним многочленом степени $\le q - 1$.

Условия применимости. Только конечные поля. Над $\mathbb{Q}$ или $\mathbb{R}$ разные многочлены задают разные функции.

Идея доказательства. Сюръективность — Lagrange interpolation: $f(x) = \sum_{a} c_a \prod_{b \ne a}\frac{x - b}{a - b}$. Ядро: если $f(a) = 0$ для всех $a$, то $(x^q - x) \mid f$ по E2 + E4.

Варианты и обобщения.
- Знаменитый пример: $x^p$ и $x$ — разные многочлены в $\mathbb{F}_p[x]$, но одна и та же функция (Ферма).
- Над $\mathbb{F}_q$ функция $\delta_a(x)$ (индикатор) задаётся $\delta_a(x) = 1 - (x - a)^{q-1}$.
- Permutation polynomial — формальный многочлен, задающий биекцию $\mathbb{F}_q \to \mathbb{F}_q$. Линейные $ax + b$ ($a \ne 0$), $x^k$ при $\gcd(k, q-1) = 1$, в характеристике $p$ — Frobenius $x^p$.

Используется в. [IMC-2003-2 косвенно]: подразумевает работу с суммой $\sum a_i$ как с элементом $\mathbb{F}_p$, а не как с целым числом — переход в характеристику $p$. [IMC-2022-6] и многие задачи Putnam про подсчёт решений.

---

## Записи — Standard

### E7. Универсальная факторизация: $x^{q^n} - x = \prod_{d \mid n} \prod_{\substack{f \text{ monic irr in } \mathbb{F}_q[x] \\ \deg f = d}} f(x)$

Формулировка. Над $\mathbb{F}_q$:
$$x^{q^n} - x = \prod_{d \mid n} \prod_{\substack{f \in \mathbb{F}_q[x] \\ \text{monic irr},\, \deg f = d}} f(x).$$
Корни $x^{q^n} - x$ — это $\mathbb{F}_{q^n}$ внутри $\overline{\mathbb{F}_q}$; каждый $\alpha \in \mathbb{F}_{q^n}$ имеет минимальный многочлен степени $d \mid n$, и обратно.

Условия применимости. $\mathbb{F}_q$ конечно, $n \ge 1$. Тождество без кратностей — $x^{q^n} - x$ separable.

Идея доказательства. $\alpha \in \mathbb{F}_{q^n} \iff \alpha^{q^n} = \alpha \iff \mathbb{F}_q(\alpha) \subset \mathbb{F}_{q^n} \iff [\mathbb{F}_q(\alpha) : \mathbb{F}_q] \mid n$. Минимальный многочлен $\alpha$ над $\mathbb{F}_q$ имеет степень $d = [\mathbb{F}_q(\alpha) : \mathbb{F}_q]$, $d \mid n$.

Варианты и обобщения.
- Сравнение степеней даёт формулу Гаусса: $q^n = \sum_{d \mid n} d \cdot N_q(d)$, где $N_q(d)$ — число monic неприводимых степени $d$. Mobius inversion:
  $$N_q(n) = \frac{1}{n} \sum_{d \mid n} \mu(d) q^{n/d}.$$
- Отсюда $N_q(n) > 0$ для всех $n \ge 1$ (так как доминирующий член $q^n/n$). Вывод: неприводимый многочлен любой степени над $\mathbb{F}_q$ существует, $\mathbb{F}_{q^n}$ существует.
- Алгоритм distinct-degree factorization: $f \cdot \gcd(f, x^{q^d} - x) = \prod (\text{irr factors of degree } d)$ по degree-classes.

Используется в. Putnam-style задачи на «существует многочлен без корней над $\mathbb{F}_p$ степени $n$»; используется внутри argument для [IMC-2011-3] (поле $\mathbb{F}_p[x]/(x^p - x + 1) \cong \mathbb{F}_{p^p}$, так как $x^p - x + 1$ неприводим, см. E13).

---

### E8. Chevalley–Warning theorem (теорема Шевалле–Варинга)

Формулировка. Пусть $f_1, \dots, f_r \in \mathbb{F}_q[x_1, \dots, x_n]$ и $\sum_{i=1}^r \deg f_i < n$. Тогда число $N$ общих нулей системы $\{f_i = 0\}$ в $\mathbb{F}_q^n$ удовлетворяет $N \equiv 0 \pmod p$, где $p = \operatorname{char} \mathbb{F}_q$.

Следствие (Chevalley). Если все $f_i$ однородны без свободного члена, $\sum \deg f_i < n$, то существует нетривиальное общее решение в $\mathbb{F}_q^n$ (так как $N \ge p \cdot 1 = p > 1$, а тривиальное $\bar 0$ уже учтено).

Условия применимости. $\sum \deg f_i < n$ — критично. $\deg = $ полная (total) степень.

Идея доказательства. Положим $g = \prod_i (1 - f_i^{q-1})$. Тогда $g(\bar a) = 1$ если $\bar a$ — общий нуль, иначе $0$. Значит $N \equiv \sum_{\bar a \in \mathbb{F}_q^n} g(\bar a) \pmod p$. Степень $g$ есть $(q-1) \sum \deg f_i < (q-1) n$, то есть в каждом мономе $\prod x_i^{e_i}$ сумма $\sum e_i < (q-1) n$, значит хотя бы для одного $i$ имеем $e_i < q-1$. По E3: $\sum_{x_i \in \mathbb{F}_q} x_i^{e_i} = 0$. Итого $\sum g(\bar a) = 0$ в $\mathbb{F}_q$, то есть $N \equiv 0 \pmod p$.

Варианты и обобщения.
- Ax–Katz: $N \equiv 0 \pmod{q^{\lceil (n - \sum \deg f_i)/\max \deg f_i \rceil}}$ — точная degree-of-divisibility оценка.
- Применяется к диагональным формам $\sum a_i x_i^k = 0$: при $n > k$ и $\sum a_i \ne 0$ нет решения в $\mathbb{F}_p^*$ (внимательно с условиями), но Chevalley-Warning даёт нетривиальное решение в $\mathbb{F}_p^n$.

Используется в. [Erdős–Ginzburg–Ziv: $2n - 1$ целых ⇒ найдутся $n$ с суммой $\equiv 0 \pmod n$ — классическое следствие через две квадратичные формы над $\mathbb{F}_p$ при $n = p$]. [Putnam-1971-B6 и аналоги]. На IMC прямого появления нет, но техника «найти нетривиальный нуль системы» — стандартный sledgehammer.

---

### E9. Combinatorial Nullstellensatz (комбинаторический Nullstellensatz, Alon)

Формулировка. Пусть $F$ — поле, $S_1, \dots, S_n \subset F$ конечные, $f \in F[x_1, \dots, x_n]$. Если $f$ обнуляется на $\prod S_i$, то для любого монома $\prod x_i^{t_i}$ с $t_i < |S_i|$ его коэффициент в $f$ равен $0$, при условии $\deg f \le \sum t_i$. (Версия II.) В частности: если коэффициент при $\prod x_i^{t_i}$ ненулевой и $\deg f = \sum t_i$, то существует $\bar a \in \prod S_i$ с $f(\bar a) \ne 0$.

Условия применимости. Любое поле. Особенно силён над $\mathbb{F}_p$: позволяет строить полином с предсказуемым старшим коэффициентом и заключать существование решения.

Идея доказательства. Лемма: $g_i(x_i) = \prod_{s \in S_i}(x_i - s) = x_i^{|S_i|} - h_i(x_i)$, $\deg h_i < |S_i|$. Любой $f$ редуцируется по идеалу $(g_1, \dots, g_n)$ к многочлену $\tilde f$ с $\deg_{x_i} \tilde f < |S_i|$, причём $\tilde f$ обнуляется на $\prod S_i$ ровно когда $f$ обнуляется. Из E4 (root-counting в $n$ переменных) следует $\tilde f \equiv 0$. Возврат к коэффициентам $f$.

Варианты и обобщения.
- Cauchy–Davenport ($|A + B| \ge \min(p, |A| + |B| - 1)$ в $\mathbb{F}_p$) — следствие через $f(x,y) = \prod_{c \in C}(x + y - c)$ при подходящих $C$.
- Erdős–Heilbronn (restricted sumset): $|A \hat + A| \ge \min(p, 2|A| - 3)$ — также.
- Альтернативный взгляд на Chevalley–Warning через тот же базис $g_i$.

Используется в. [IMO-2007-6: прямое применение — $3n$ плоскостей покрывают $\{0, \dots, n\}^3 \setminus \{(0,0,0)\}$, нижняя оценка через CN]. На IMC конкретного появления не задокументировано, но идея используется в комбинаторных задачах с условием «полином не зануляется».

---

### E10. Lucas's theorem (теорема Лукаса) для $\binom{n}{k} \pmod p$

Формулировка. Пусть $p$ простое, $n = \sum n_i p^i$, $k = \sum k_i p^i$ — записи в системе с основанием $p$. Тогда
$$\binom{n}{k} \equiv \prod_i \binom{n_i}{k_i} \pmod p.$$
В частности, $\binom{n}{k} \not\equiv 0 \pmod p \iff k_i \le n_i$ для всех $i$ («$k \subset n$ как битовая маска» при $p = 2$).

Условия применимости. $p$ простое; $n, k$ — неотрицательные целые. Для составного $m$ нужно использовать отдельно для каждого простого делителя + CRT.

Идея доказательства. $(1+x)^n = \prod_i (1+x)^{n_i p^i} = \prod_i ((1+x)^{p^i})^{n_i} \equiv \prod_i (1 + x^{p^i})^{n_i} \pmod p$ (freshman's dream многократно). Сравниваем коэффициенты при $x^k$ — единственный способ выбрать $k_i$ из $n_i$ в каждой группе.

Варианты и обобщения.
- Кумера: $v_p\!\binom{n}{k} = $ число переносов при сложении $k + (n - k)$ в системе с основанием $p$.
- Granville: расширения для $\binom{n}{k} \pmod{p^a}$.
- Wolstenholme: $\binom{2p}{p} \equiv 2 \pmod{p^3}$ для $p \ge 5$.

Используется в. [IMC-2022-3: central trinomial coefficient $\equiv 3 \pmod p$ через Lucas-style разложение $(1 + x + x^{-1})^{p-1}$]. Putnam: задачи «когда $\binom{n}{k}$ нечётно» — проверка $k \subset n$ в двоичной записи. Универсальный инструмент в комбинаторно-теоретико-числовых задачах.

---

### E11. Hensel's lemma (лемма Гензеля) над $\mathbb{Z}/p^k$

Формулировка. Пусть $f \in \mathbb{Z}[x]$, $a \in \mathbb{Z}$ удовлетворяет $f(a) \equiv 0 \pmod p$ и $f'(a) \not\equiv 0 \pmod p$. Тогда для каждого $k \ge 1$ существует единственный $\tilde a \pmod{p^k}$ с $\tilde a \equiv a \pmod p$ и $f(\tilde a) \equiv 0 \pmod{p^k}$. Явная итерация: $a_{k+1} = a_k - f(a_k)/f'(a_k)$ (Newton's method в $\mathbb{Z}_p$).

Условия применимости. $f'(a) \ne 0 \pmod p$ — критично (простой корень). Если $f'(a) \equiv 0$, lift существует, но не единственный или не существует — отдельный анализ.

Идея доказательства. Индукция: ищем $a_{k+1} = a_k + p^k t$, разложение $f(a_k + p^k t) = f(a_k) + p^k t f'(a_k) + O(p^{2k})$. Условие $f(a_{k+1}) \equiv 0 \pmod{p^{k+1}}$ даёт $t \equiv -f(a_k)/p^k / f'(a_k) \pmod p$.

Варианты и обобщения.
- Многомерная версия: $f\colon \mathbb{Z}_p^n \to \mathbb{Z}_p^n$, якобиан обратим mod $p$.
- Hensel в $\mathbb{Z}_p$ или в полных DVR.
- Frobenius lift: единственный $\sigma \in \operatorname{End}(\mathbb{Z}_p[\zeta])$ с $\sigma(x) \equiv x^p \pmod p$.

Используется в. [IMC-2006-2: число решений $x(x-1) \equiv 0 \pmod{10^k}$ — через CRT задача распадается на $x(x-1) \equiv 0 \pmod{2^k}$ и $\pmod{5^k}$; для каждой простой степени Hensel поднимает корни $0, 1$ единственным способом, итого $2 \times 2 = 4$ решения]. Задачи про многочлены, не имеющие корней в $\mathbb{Z}/p^k$ ни для какого $k$, vs имеющие для всех $k$, — Hensel стандартный аргумент.

---

### E12. Множитель $\gcd(f, x^q - x)$ и squarefree-разложение в $\mathbb{F}_q[x]$

Формулировка. Для $f \in \mathbb{F}_q[x]$:
- $\gcd(f, x^q - x) = \prod_{a \in \mathbb{F}_q,\, f(a) = 0}(x - a)$ — выделяет корни в $\mathbb{F}_q$.
- $\gcd(f, x^{q^d} - x) = \prod_{\text{irr factors of }f\text{ of deg dividing }d}$.
- $\gcd(f, f') = \prod$ кратных делителей; $f / \gcd(f, f')$ — squarefree-часть. Если $\gcd(f, f') = 1$, то $f$ separable.

Условия применимости. Char $p$ — нужно следить за inseparability: $f' \equiv 0 \iff f(x) = g(x^p)$, тогда squarefree decomposition требует другого подхода.

Идея доказательства. Корень $\alpha$ кратный $\iff f(\alpha) = f'(\alpha) = 0$. Над расширением: $f$ имеет все корни в $\mathbb{F}_{q^d} \iff \alpha^{q^d} = \alpha$ для всех корней $\iff (x^{q^d} - x) \cap f$ содержит все эти линейные множители.

Варианты и обобщения.
- Berlekamp's algorithm факторизации $f \in \mathbb{F}_q[x]$: основан на наблюдении, что Frobenius $\varphi\colon \mathbb{F}_q[x]/(f) \to \mathbb{F}_q[x]/(f)$ имеет собственное подпространство фиксированных точек размерности = числу неприводимых множителей.
- Cantor–Zassenhaus — рандомизированная факторизация equal-degree.

Используется в. [IMC-2007-5]: $Q(c) = 0 \Rightarrow Q(c^m) = 0$ для всех $m \Rightarrow Q(c), Q(c^2), \dots$ все $0$ ⇒ $c$ имеет конечный порядок $N$ ⇒ $Q(1) = 0$ — использует структуру корней в $\overline{\mathbb{F}_q}$ через E5+E12. Стандартный приём в задачах про invariant ideals.

---

## Записи — Exotic

### E13. Artin–Schreier polynomial: $x^p - x - a$

Формулировка. Над $\mathbb{F}_q$ ($q = p^n$) полином $f(x) = x^p - x - a$ либо имеет все $p$ корней в $\mathbb{F}_q$ (если $a$ — в образе $\wp\colon x \mapsto x^p - x$), либо неприводим. Образ $\wp$ — это $\mathbb{F}_q$-подпространство коразмерности $\le 1$ в $\mathbb{F}_q$ (ядро $\wp$ есть $\mathbb{F}_p$, образ — гиперплоскость в $\mathbb{F}_q$). Если $a \notin \operatorname{im} \wp$, расширение $\mathbb{F}_q[x]/(f) = \mathbb{F}_{q^p}$, степени $p$, циклическое (Artin–Schreier).

Условия применимости. Char $= p$. Аналог Kummer-расширения $x^n - a$ в коприм-к-$p$ случае.

Идея доказательства. Если $\alpha$ — корень, то $\alpha + 1, \alpha + 2, \dots, \alpha + (p-1)$ — тоже (так как $(x+1)^p - (x+1) = x^p - x$ в char $p$), итого $p$ различных корней — все. Группа Galois: $\sigma\colon \alpha \mapsto \alpha + 1$, циклическая порядка $p$.

Варианты и обобщения.
- $x^p - x + 1$ неприводим над $\mathbb{F}_p$ для всех $p$ (так как $\wp$ имеет образ $\mathbb{F}_p \setminus \mathbb{F}_p^?$ — точнее, образ $\wp$ на $\mathbb{F}_p$ есть $\{0\}$, поэтому $-1 \notin \operatorname{im} \wp$ при $p \ne $ ?). Аккуратно: $\wp\colon \mathbb{F}_p \to \mathbb{F}_p$ имеет ядро $\mathbb{F}_p$ всё, значит образ $= \{0\}$. Так что $x^p - x - a$ для $a \ne 0$ ВСЕГДА неприводим над $\mathbb{F}_p$.
- $\mathbb{F}_p[x]/(x^p - x + 1) \cong \mathbb{F}_{p^p}$ — основное наблюдение в [IMC-2011-3].

Используется в. [IMC-2011-3]: ровно $x^p - x + 1$ — Artin–Schreier polynomial; неприводимость над $\mathbb{F}_p$ автоматически. Иногда применяется для построения «странных» полей малого размера.

---

### E14. Erdős–Ginzburg–Ziv (теорема Эрдёша–Гинзбурга–Зива) через Chevalley–Warning

Формулировка. Любые $2n - 1$ целых содержат подмножество размера $n$ с суммой делящейся на $n$.

Условия применимости. Достаточно доказать для $n = p$ простого (мультипликативно собирается через индукцию по $n$).

Идея доказательства. Для $a_1, \dots, a_{2p-1} \in \mathbb{Z}$ рассматриваем систему в $\mathbb{F}_p[x_1, \dots, x_{2p-1}]$:
$$f_1 = \sum_{i=1}^{2p-1} a_i x_i^{p-1}, \quad f_2 = \sum_{i=1}^{2p-1} x_i^{p-1}.$$
Степени $\deg f_1 = \deg f_2 = p - 1$, итого $\sum \deg = 2(p-1) < 2p - 1 = n_{\text{var}}$. По Chevalley–Warning есть нетривиальное решение $\bar x \ne \bar 0$. Носитель $I = \{i : x_i \ne 0\}$ — нужное подмножество: по малой Ферма $x_i^{p-1} = 1$ для $i \in I$, $0$ иначе, итого $f_2(\bar x) = |I| \equiv 0 \pmod p$, значит $|I| \in \{p, 2p\}$ (т.к. $1 \le |I| \le 2p-1$, остаётся $|I| = p$). Аналогично $f_1(\bar x) = \sum_{i \in I} a_i \equiv 0 \pmod p$.

Варианты и обобщения.
- Davenport constant $D(G)$ для абелевой группы $G$.
- Olson's bound: $D(\mathbb{Z}/p^a \oplus \mathbb{Z}/p^b) = p^a + p^b - 1$.
- Reiher's theorem: $D(\mathbb{Z}/n \oplus \mathbb{Z}/n) = 2n - 1$.

Используется в. На IMC напрямую не появлялось, но концепция «Chevalley-Warning ⇒ комбинаторное утверждение» — типовая для shortlist. [USAMO-1999-6] частично связан.

---

### E15. Cauchy–Davenport и Combinatorial Nullstellensatz proof

Формулировка. Для $A, B \subset \mathbb{F}_p$ непустых: $|A + B| \ge \min(p, |A| + |B| - 1)$.

Условия применимости. $\mathbb{F}_p$ — простое поле; в $\mathbb{F}_q$ при $q$ составном утверждение ломается (взять подгруппу).

Идея доказательства (через CN). От противного: пусть $|A + B| \le |A| + |B| - 2 =: m$ и $m < p$. Возьмём $C \supseteq A + B$ с $|C| = m$ (если $|A + B| < m$, добавим элементы). Полином $f(x, y) = \prod_{c \in C}(x + y - c)$ обнуляется на $A \times B$. Степень $|A| + |B| - 2$, коэффициент при $x^{|A|-1} y^{|B|-1}$ равен $\binom{|A| + |B| - 2}{|A| - 1} \not\equiv 0 \pmod p$ (так как $|A| + |B| - 2 < p$). По CN — противоречие.

Варианты и обобщения.
- Vosper's theorem: точное описание случая равенства.
- Erdős–Ginzburg–Ziv следствие.
- Kneser's theorem для произвольной абелевой группы.

Используется в. Множество комбинаторных задач про сумсеты, в т.ч. на shortlists. На IMC прямого нет, но вместе с E9 — стандартный полиномиальный приём.

---

## Self-test

1. Пусть $p$ — простое, $f \in \mathbb{F}_p[x]$ удовлетворяет $f(a) = 0$ для всех $a \in \mathbb{F}_p$. Доказать, что $(x^p - x) \mid f(x)$.
2. Найти все целые $n \ge 1$, для которых $x^n - 1$ делится на $x^p - x + 1$ в кольце $\mathbb{F}_p[x]$.
3. Пусть $p$ — нечётное простое. Доказать, что $x^p - x + 1 \in \mathbb{F}_p[x]$ неприводим.
4. Полином $f \in \mathbb{F}_p[x]$ степени $\le p - 2$ удовлетворяет $\sum_{a \in \mathbb{F}_p} a \cdot f(a) = 0$ и $\sum_{a \in \mathbb{F}_p} f(a) = 0$. Что можно сказать про коэффициенты $f$?
5. Доказать, что для любого простого $p$ и любых $a_1, \dots, a_{2p-1} \in \mathbb{Z}$ существует подмножество $I \subset \{1, \dots, 2p-1\}$ размера $p$ с $\sum_{i \in I} a_i \equiv 0 \pmod p$.
6. Доказать, что число monic неприводимых полиномов степени $n$ над $\mathbb{F}_q$ равно $\frac{1}{n} \sum_{d \mid n} \mu(d) q^{n/d}$, и что оно строго положительно для всех $n \ge 1$, $q \ge 2$.
7. Доказать, что $\binom{2^k}{j} \equiv 0 \pmod 2$ для всех $1 \le j \le 2^k - 1$.
8. Пусть $f \in \mathbb{Z}[x]$ степени не выше $4$ и $f(a) \equiv 0 \pmod 5$ для $a = 0, 1, 2, 3, 4$. Доказать, что все коэффициенты $f$ делятся на $5$.
9. Над $\mathbb{F}_p$ ($p$ нечётное) посчитать $\prod_{a \in \mathbb{F}_p^\times} a^2$ и $\sum_{a \in \mathbb{F}_p} a^{p-1}$.
10. Пусть $A, B \subset \mathbb{F}_p$ имеют $|A| + |B| > p$. Доказать, что $A + B = \mathbb{F}_p$.

## Решения

1. По малой теореме Ферма $a^p = a$ для $a \in \mathbb{F}_p$, так что $x^p - x$ имеет $p$ различных корней — все элементы $\mathbb{F}_p$. Если $f(a) = 0$ во всех $a$, то $\prod_a (x - a) = x^p - x$ делит $f$ в $\mathbb{F}_p[x]$ (каждый $(x-a)$ делит $f$, и они попарно взаимно просты). См. [E2], [E6].

2. По E1+E13 кольцо $R = \mathbb{F}_p[x]/(x^p - x + 1) \cong \mathbb{F}_{p^p}$. Элемент $x \in R$ удовлетворяет $x^p = x - 1$, итерируя: $x^{p^k} = x - k \pmod p$. Значит $x^{p^p} = x$, т.е. $\operatorname{ord}_{R^\times}(x) \mid p^p - 1$. С другой стороны $x \notin \mathbb{F}_p$ (он не удовлетворяет $x^p = x$), поэтому $\operatorname{ord}(x) \nmid p^d - 1$ для $d < p$, значит $\operatorname{ord}(x) = p^p - 1$. Условие $(x^p - x + 1) \mid (x^n - 1)$ ⟺ $x^n = 1$ в $R$ ⟺ $(p^p - 1) \mid n$. См. [E1], [E5], [E13].

3. Образ отображения $\wp\colon \mathbb{F}_p \to \mathbb{F}_p$, $\wp(t) = t^p - t = 0$ в $\mathbb{F}_p$ (ферма). Значит $\operatorname{im} \wp = \{0\}$, и $a = -1 \ne 0$ не лежит в образе. По Artin–Schreier (E13) $x^p - x + 1$ неприводим над $\mathbb{F}_p$.

4. Пусть $f(x) = \sum_{k=0}^{p-2} c_k x^k$. По E3:
   - $\sum_a f(a) = \sum_k c_k \sum_a a^k = c_0 \cdot 0 + c_1 \cdot 0 + \dots = 0$ автоматически (так как все $k < p - 1$, $\sum_a a^k = 0$ при $k > 0$, и $\sum_a 1 = p \cdot 1 = 0$ в $\mathbb{F}_p$). То есть это тождество, не даёт информации.
   - $\sum_a a f(a) = \sum_k c_k \sum_a a^{k+1}$. Слагаемое не нулевое только если $k+1 = p-1$, т.е. $k = p-2$, и тогда оно равно $-c_{p-2}$. Условие $\sum_a a f(a) = 0$ даёт $c_{p-2} = 0$.

   Итого: над $\mathbb{F}_p$ информация — старший коэффициент $c_{p-2} = 0$, остальные не ограничены. См. [E3].

5. Применяем E14: рассмотрим в $\mathbb{F}_p^{2p-1}$ систему $f_1 = \sum a_i x_i^{p-1}$, $f_2 = \sum x_i^{p-1}$. $\deg f_1 = \deg f_2 = p - 1$, сумма $= 2p - 2 < 2p - 1$. По Chevalley-Warning (E8) число решений $\equiv 0 \pmod p$, $\bar 0$ — решение, значит есть нетривиальное $\bar x$. Носитель $I = \{i : x_i \ne 0\}$: на нём $x_i^{p-1} = 1$ (Ферма), значит $|I| \equiv 0 \pmod p$, $1 \le |I| \le 2p-1$, значит $|I| = p$, и $\sum_{i \in I} a_i \equiv 0 \pmod p$.

6. Из E7 имеем $x^{q^n} - x = \prod_{d \mid n} \prod_{\substack{f \text{ monic irr} \\ \deg f = d}} f$. Сравниваем степени: $q^n = \sum_{d \mid n} d \cdot N_q(d)$. Mobius inversion: $n N_q(n) = \sum_{d \mid n} \mu(n/d) q^d$, что эквивалентно нужной формуле. Положительность: $N_q(n) \ge \frac{1}{n}(q^n - \sum_{d < n,\, d \mid n} q^d) \ge \frac{1}{n}(q^n - n q^{n/2}) > 0$ для $q \ge 2$, $n \ge 1$.

7. Лукас (E10): $2^k$ в двоичной записи $= 100\dots0$. Для $j$ с $1 \le j \le 2^k - 1$ в его двоичной записи есть позиция $i < k$ с $j_i = 1$, в то время как $(2^k)_i = 0$. Тогда $\binom{(2^k)_i}{j_i} = \binom{0}{1} = 0$, итого $\binom{2^k}{j} \equiv 0 \pmod 2$.

8. Полином $\bar f \in \mathbb{F}_5[x]$ степени $\le 4$ обнуляется в $5$ точках $0, 1, 2, 3, 4$ — больше степени, значит $\bar f \equiv 0 \pmod 5$, т.е. все коэффициенты делятся на $5$. См. [E4]. Альтернативно: $(x^5 - x) \mid \bar f$ по E2, но $\deg \bar f \le 4 < 5$, значит $\bar f = 0$.

9. $\prod_{a \ne 0} a^2 = (\prod_a a)^2 = (-1)^2 = 1$ по E2 (Wilson в полиномиальной форме). $\sum_{a \in \mathbb{F}_p} a^{p-1}$: при $a = 0$ слагаемое $0$, при $a \ne 0$ имеем $a^{p-1} = 1$ (Ферма), всего $p - 1$ слагаемых, итого $-1$ в $\mathbb{F}_p$. Согласуется с E3 (случай $(p-1) \mid (p-1)$).

10. $A + B = \mathbb{F}_p$ ⟺ для каждого $c \in \mathbb{F}_p$ существуют $a \in A, b \in B$ с $a + b = c$, т.е. $b = c - a$, т.е. $A \cap (c - B) \ne \emptyset$. По принципу включений-исключений $|A| + |c - B| - |\mathbb{F}_p| = |A| + |B| - p > 0$, значит $A \cap (c - B) \ne \emptyset$. Альтернативно — Cauchy-Davenport (E15): $|A + B| \ge \min(p, |A| + |B| - 1) = p$.
