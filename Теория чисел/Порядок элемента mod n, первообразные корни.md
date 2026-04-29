---
topic: Теория чисел
subtopic: "Порядок элемента mod n, первообразные корни"
sources:
  - "Evan Chen — Orders Modulo a Prime (handout, 2015)"
  - "Lawrence Sun — Cyclotomic Polynomials in Olympiad Number Theory (AoPS handout)"
  - "Yufei Zhao — Trinity Training 2011: $a^n \\pm 1$"
  - "Ryan C. Daileda — Primitive Roots Modulo Prime Powers (Trinity University, lecture 16)"
  - "Math 115 (Berkeley, P. Vojta) — Primitive Roots"
  - "Math Excalibur Vol. 15 No. 1 — Primitive Roots Modulo Primes (HKUST, 2010)"
  - "Justin Stevens — Olympiad Number Theory Through Challenging Problems"
  - "Alexander Remorov — Winter Camp 2010: Exponents and Primes"
  - "Andreescu, Andrica, Feng — Putnam and Beyond (Number Theory)"
  - "Engel — Problem-Solving Strategies (ch. Number Theory)"
  - "K. Ireland, M. Rosen — A Classical Introduction to Modern Number Theory (ch. 4, 6, 8)"
  - "Wikipedia — Primitive root modulo n / Carmichael function / Cyclotomic polynomial / Multiplicative group of integers modulo n / Gauss sum"
  - "IMC Compendium"
  - "Putnam Compendium"
problems_referenced:
  - IMO-1990-3
  - IMO-1999-4
  - IMO-2003-6
  - Putnam-1972-A6
  - Putnam-1991-B4
  - Putnam-2008-A4
  - IMC-2022-3
  - IMC-2023-4
last_updated: 2026-04-29
---

# Порядок элемента mod n, первообразные корни

## Scope
Структура $(\mathbb{Z}/n)^*$ как группы: порядок элемента, primitive root (первообразный корень), Carmichael $\lambda(n)$, индекс / discrete log, циклотомические критерии и их применение к построениям. Не повторяет LTE-стек (см. `Lifting the exponent (LTE).md`, особенно E6 — order lifting и E7 — $v_p(\Phi_n(a))$); здесь — структурный и комбинаторный слой: критерии существования, smallest-prime-factor, степенные суммы $\sum a^m \bmod p$, Wilson-like, инфинитные конструкции простых $\equiv 1 \pmod n$. На IMC/Putnam применяется в задачах вида «найти все $n$ с $n \mid a^n \pm b$», построение элементов больших порядков, оценка $\sum_a a^k \bmod p$, контрпримеры в $(\mathbb{Z}/2^k)^*$.

## Записи — Core

### E1. Свойства order ($\operatorname{ord}_n a$) — алгебраический минимум

Формулировка. Пусть $\gcd(a, n) = 1$, $d := \operatorname{ord}_n(a)$ (наименьший $k \ge 1$ с $a^k \equiv 1 \pmod n$). Тогда:
1. $a^k \equiv 1 \pmod n \iff d \mid k$. В частности $d \mid \varphi(n)$ (Euler), $d \mid \lambda(n)$ (E5).
2. $\operatorname{ord}_n(a^k) = \dfrac{d}{\gcd(d, k)}$.
3. Если $\gcd(\operatorname{ord}_n a, \operatorname{ord}_n b) = 1$, то $\operatorname{ord}_n(ab) = \operatorname{ord}_n(a) \cdot \operatorname{ord}_n(b)$ (в любой абелевой группе). Без коммутативности — ложно.
4. В абелевой группе всегда существует элемент с порядком $\operatorname{lcm}(\operatorname{ord}_n a, \operatorname{ord}_n b)$ (но не обязательно $ab$).

Условия применимости. $\gcd(a, n) = 1$ — иначе порядок не определён. Для пункта 4 — коммутативность критична.

Идея доказательства. (1) Стандартное евклидово деление $k$ на $d$. (2) $a^{km} = 1 \iff d \mid km \iff (d/\gcd(d,k)) \mid m$. (3) Из $\gcd$-условия и абелевости. (4) Каноническая конструкция: разложить $\operatorname{lcm}$ на копрост множители $u \cdot v$ с $u \mid \operatorname{ord} a$, $v \mid \operatorname{ord} b$, $\gcd(u,v)=1$, и взять $a^{(\operatorname{ord} a)/u} \cdot b^{(\operatorname{ord} b)/v}$.

Используется в. Каждой задаче на orders. [Putnam-1972-A6], [IMO-1990-3] — без этого пункта (1) не сдвинуть.

---

### E2. Существование первообразного корня mod $p$ (Gauss)

Формулировка. Для простого $p$ группа $(\mathbb{Z}/p)^*$ циклична порядка $p-1$. Число первообразных корней (primitive roots) в $\{1, \dots, p-1\}$ равно $\varphi(p-1)$. Более общо: число элементов точного порядка $d$ при $d \mid p-1$ равно $\varphi(d)$.

Условия применимости. $p$ — простое. Для $p = 2$ единственный первообразный корень — $1$.

Идея доказательства. Пусть $\psi(d)$ — число элементов порядка ровно $d$. Все эти элементы — корни $x^d - 1 \in \mathbb{F}_p[x]$, у которого ровно $d$ корней. Из них $\sum_{e \mid d} \psi(e) = d$, поэтому $\psi(d) \le \varphi(d)$ (классическое тождество $\sum_{e \mid d}\varphi(e) = d$ + Möbius-инверсия). Суммируя $\sum_{d \mid p-1} \psi(d) = p-1 = \sum_{d \mid p-1} \varphi(d)$, получаем $\psi(d) = \varphi(d)$ для всех $d \mid p-1$, в частности $\psi(p-1) = \varphi(p-1) > 0$.

Варианты и обобщения.
- В любом конечном поле $\mathbb{F}_q$ группа $\mathbb{F}_q^*$ циклична — тот же аргумент.
- Конструктивно primitive root тестируется: $g$ — primitive root mod $p$ $\iff$ $g^{(p-1)/q} \not\equiv 1 \pmod p$ для каждого простого $q \mid p-1$.

Используется в. Все задачи с primitive root: [Putnam-1991-B4 (вариация на сумму первообразных корней)], индекс / discrete log (E9), формулы степенных сумм (E10).

---

### E3. Структура $(\mathbb{Z}/n)^*$ и критерий существования primitive root

Формулировка. $(\mathbb{Z}/n)^*$ цикличен тогда и только тогда, когда $n \in \{1, 2, 4, p^k, 2p^k\}$, где $p$ — нечётное простое. В остальных случаях группа — нетривиальное прямое произведение.

Конкретно: по CRT $(\mathbb{Z}/n)^* \cong \prod_i (\mathbb{Z}/p_i^{a_i})^*$, и:
- $(\mathbb{Z}/p^k)^* \cong \mathbb{Z}/p^{k-1}(p-1)$ для нечётного $p$ (циклична).
- $(\mathbb{Z}/2)^* = 1$, $(\mathbb{Z}/4)^* \cong \mathbb{Z}/2$.
- $(\mathbb{Z}/2^k)^* \cong \mathbb{Z}/2 \times \mathbb{Z}/2^{k-2}$ при $k \ge 3$, генераторы $-1$ и $5$ (порядки $2$ и $2^{k-2}$).

Условия применимости. Универсально для $n \ge 1$.

Идея доказательства. CRT редуцирует к простым степеням. Для нечётного $p^k$ — лифтинг primitive root с $p$ на $p^k$ (E6). Для $2^k$, $k \ge 3$: $5^{2^{k-3}} \equiv 1 + 2^{k-1} \pmod{2^k}$ (индукция через $v_2((1+x)^2 - 1) = v_2(x) + v_2(x+2)$), значит $\operatorname{ord}_{2^k}(5) = 2^{k-2}$; $-1 \notin \langle 5 \rangle$ т.к. все степени $5$ — $\equiv 1 \pmod 4$.

Варианты и обобщения. Структура объясняет, почему «первообразный корень mod $2^k$» не существует при $k \ge 3$ — частая ловушка в задачах. Конкретно: для нечётного $a$ и $k \ge 3$, $a^{2^{k-2}} \equiv 1 \pmod{2^k}$, т.е. $\lambda(2^k) = 2^{k-2}$.

Используется в. Любая задача со степенями mod $2^k$; контрпримеры к «обобщённому» Ферма-Эйлеру; [IMO-1999-4: $n^2 \mid (n-1)! + 1$ только для $n$ простого] — структурный анализ через $\lambda(n)$.

---

### E4. Smallest-prime-factor argument («трюк наименьшего простого делителя»)

Формулировка. Пусть $n \ge 2$, $p$ — наименьший простой делитель $n$, $a \in \mathbb{Z}$ с $\gcd(a, p) = 1$. Если $n \mid a^n - 1$, то $\operatorname{ord}_p(a) \mid \gcd(n, p-1) = 1$, т.е. $a \equiv 1 \pmod p$.

Аналогично: если $n \mid a^n + 1$ и $n$ нечётно, то $\operatorname{ord}_p(a) \mid \gcd(2n, p-1)$, причём $\operatorname{ord}_p(a) \nmid n$ (иначе $a^n \equiv 1$, а нужно $\equiv -1$). Значит $\operatorname{ord}_p(a) = 2 \cdot d$ с $d \mid n$, и $2d \mid p-1$. По минимальности $p$: $d = 1$, $\operatorname{ord}_p(a) = 2$, $p \mid a + 1$ (исключая $a \equiv 1 \pmod p$).

Условия применимости. $n \ge 2$. Аналог для $n \mid a^n + b$ работает в той же логике, главное — записать условие через $a^{2n}$ или $a^n$ и оценить $\operatorname{ord}_p(a)$.

Идея доказательства. $p \mid n \mid a^n - 1 \Rightarrow \operatorname{ord}_p(a) \mid n$. Также $\operatorname{ord}_p(a) \mid p - 1$ (Ферма). Значит $\operatorname{ord}_p(a) \mid \gcd(n, p-1)$. Все простые делители $\gcd(n, p-1)$ делят $n$ и одновременно $< p$ — но $p$ — наименьший простой делитель $n$, противоречие. Значит $\gcd = 1$, $\operatorname{ord}_p(a) = 1$.

Варианты и обобщения.
- Версия для $f(n) \mid a^{g(n)} \pm b^{h(n)}$ — та же идея.
- Иногда не сразу даёт ответ: получив $p \mid a - 1$ или $p \mid a + 1$, нужно ещё LTE-шаг для оценки $v_p$.

Используется в. [IMO-1990-3: $n^2 \mid 2^n + 1$ — стартует именно так, $p=3$], [Putnam-1972-A6], [IMO-1999-4], шаблон для всех задач «найти все $n$ с $n \mid a^n \pm b$».

---

## Записи — Standard

### E5. Carmichael's $\lambda$-function — экспонента группы

Формулировка. $\lambda(n)$ — наименьшее $m \ge 1$ с $a^m \equiv 1 \pmod n$ для всех $a$ с $\gcd(a, n) = 1$. Это экспонента (показатель) группы $(\mathbb{Z}/n)^*$. Формула:
$$
\lambda(n) = \operatorname{lcm}\bigl(\lambda(p_1^{a_1}), \dots, \lambda(p_r^{a_r})\bigr), \quad
\lambda(p^k) = \begin{cases} p^{k-1}(p-1) & p \text{ нечётное, или } p^k \in \{2, 4\}, \\ 2^{k-2} & p=2, k \ge 3. \end{cases}
$$
Свойство достижимости: существует $a$ с $\operatorname{ord}_n(a) = \lambda(n)$ (т.н. $\lambda$-primitive root).

Условия применимости. Любые $n \ge 1$. $\lambda(n) \mid \varphi(n)$, равенство $\iff (\mathbb{Z}/n)^*$ цикличен (E3).

Идея доказательства. Экспонента $\prod G_i$ — это $\operatorname{lcm}$ экспонент. Достижимость: в каждом $(\mathbb{Z}/p_i^{a_i})^*$ берём элемент порядка $\lambda(p_i^{a_i})$ (primitive root для нечётного $p_i$, либо $5$ или $-5$ для $2^k$), CRT-склеиваем — получаем элемент порядка $\operatorname{lcm}$.

Варианты и обобщения. Carmichael число — составное $n$ с $a^{n-1} \equiv 1 \pmod n$ для всех $\gcd(a,n)=1$, т.е. $\lambda(n) \mid n - 1$. Korselt's criterion: $n$ — Carmichael $\iff n$ squarefree и $(p-1) \mid (n-1)$ для каждого простого $p \mid n$.

Используется в. Корректное обобщение Ферма для составного модуля; задачи на «всеобщий показатель» mod $n$; [Putnam-2008-A4-style (псевдо-Ферма)].

---

### E6. Lifting primitive root: $p \to p^k$ (нечётное $p$)

Формулировка. Пусть $p$ — нечётное простое, $g$ — primitive root mod $p$. Тогда:
- если $g^{p-1} \not\equiv 1 \pmod{p^2}$, то $g$ — primitive root mod $p^k$ для всех $k \ge 1$;
- если $g^{p-1} \equiv 1 \pmod{p^2}$ (генерический случай — Wieferich-style, см. LTE.md E11), то $g + p$ — primitive root mod $p^k$ для всех $k$.

Кроме того, если $g$ — primitive root mod $p^2$, то $g$ — primitive root mod $p^k$ для всех $k$.

Условия применимости. $p$ нечётное. Для $p = 2$ нет primitive root при $k \ge 3$ (см. E3); используется пара $(-1, 5)$.

Идея доказательства. $\operatorname{ord}_{p^k}(g) \mid p^{k-1}(p-1) = \varphi(p^k)$. Поскольку $g$ primitive mod $p$, $(p-1) \mid \operatorname{ord}_{p^k}(g)$. Значит $\operatorname{ord}_{p^k}(g) = p^j (p-1)$ для некоторого $0 \le j \le k-1$. По LTE.md E1 с $x=g$, $y=1$: при $g^{p-1} \equiv 1 + cp \pmod{p^2}$ с $p \nmid c$ имеем $v_p(g^{(p-1)p^m} - 1) = 1 + m$, так что $\operatorname{ord}_{p^k}(g) = (p-1) p^{k-1}$. Если $p \mid c$ (т.е. $g^{p-1} \equiv 1 \pmod{p^2}$), сдвиг $g \to g + p$ обычно «чинит» $c$.

Варианты и обобщения. Для $p = 2$, $k \ge 3$: $(\mathbb{Z}/2^k)^*$ не циклична; $\lambda$-primitive root — $\pm 5$ или $\pm 3$, и при $a$ нечётном
$$
v_2(a^{2^m} - 1) = v_2(a^2 - 1) + m - 1 \quad (m \ge 1).
$$

Используется в. Конструкция элементов больших порядков mod $p^k$; обоснование E3; [IMO-2003-6] частично.

---

### E7. Cyclotomic prime divisor characterization

Формулировка. Пусть $a \in \mathbb{Z}$, $p$ — простое, $p \nmid a$. Тогда $p \mid \Phi_n(a)$ влечёт ровно одно из двух:
1. $\operatorname{ord}_p(a) = n$, и тогда $n \mid p - 1$ (т.е. $p \equiv 1 \pmod n$);
2. $p \mid n$.

Обратно: если $\operatorname{ord}_p(a) = n$, то $p \mid \Phi_n(a)$.

Условия применимости. $p \nmid a$. При $p \mid n$ оценка $v_p(\Phi_n(a))$ — детально в LTE.md E7 (обычно $\le 1$).

Идея доказательства. $a^n \equiv 1 \pmod p$, поэтому $\operatorname{ord}_p(a) \mid n$. Если $\operatorname{ord}_p(a) = d < n$, то $a^d - 1 \equiv 0 \pmod p$, и $\gcd_{\mathbb{F}_p[x]}(\Phi_n, x^d - 1) \ne 1$. В $\overline{\mathbb{F}_p}$ это означает общий корень — примитивный $n$-й корень из единицы совпадает с примитивным $d$-м, что возможно только если $\operatorname{char} = p$ и $p \mid n/d$, т.е. $p \mid n$.

Варианты и обобщения. Это структурный аналог LTE.md E7 в обратную сторону: вместо «как считать $v_p(\Phi_n(a))$» — «какие $p$ вообще могут делить $\Phi_n(a)$». Основной инструмент для построения простых $\equiv 1 \pmod n$ (E8) и доказательства Zsygmondy (LTE.md E8).

Используется в. [IMO-2003-6], [IMC-2022-3] (через $\Phi_p$ при $p$ простом), [Putnam-1991-B4] стиль.

---

### E8. Бесконечность простых $\equiv 1 \pmod n$ (элементарно)

Формулировка. Для каждого $n \ge 1$ существует бесконечно много простых $p \equiv 1 \pmod n$.

Условия применимости. Универсально. Это — частный случай теоремы Дирихле о простых в арифметической прогрессии, но имеет элементарное доказательство (без $L$-функций).

Идея доказательства. Стандартное по Эйлеру: пусть $p_1, \dots, p_t$ — известные простые $\equiv 1 \pmod n$. Положим $N = n p_1 \cdots p_t$ и рассмотрим $\Phi_n(N \cdot \ell)$ для большого $\ell \ge 1$. Это целое число $> 1$ (по росту $\Phi_n$), поэтому имеет простой делитель $q$. По E7: либо $q \equiv 1 \pmod n$, либо $q \mid n$ — но $q \mid \Phi_n(N\ell)$ и $\gcd(N, q) = 1$ исключает второй вариант (по построению $N$ кратно $n$ и всем $p_i$, а $\Phi_n(N\ell) \equiv \Phi_n(0) \pmod{N}$ — единица или $\pm 1$ в зависимости от $n$). Значит $q$ — новый простой $\equiv 1 \pmod n$.

Варианты и обобщения. То же доказательство показывает: для любого подгруппы $H \le (\mathbb{Z}/n)^*$ — нельзя получить «все простые $p$ с $p \bmod n \in H$» элементарно (для $H \ne \{1\}$ нужны $L$-функции).

Используется в. Конструктивные задачи «существует простое $p$ с свойством $X$» (часто через $p \equiv 1 \pmod n$ для нужного $n$); [IMO-2003-6: существование простого $q$ с $q \nmid n^p - p$ для всех $n$] напрямую через Zsygmondy + E8.

---

### E9. Discrete log (index) и критерий QR через primitive root

Формулировка. Пусть $g$ — primitive root mod $p$ ($p$ нечётное простое). Для $a \in (\mathbb{Z}/p)^*$ определён $\operatorname{ind}_g(a) \in \mathbb{Z}/(p-1)$ — единственное $k$ с $a \equiv g^k \pmod p$. Свойства:
$$
\operatorname{ind}_g(ab) = \operatorname{ind}_g(a) + \operatorname{ind}_g(b), \quad \operatorname{ord}_p(a) = \frac{p-1}{\gcd(p-1, \operatorname{ind}_g(a))}.
$$
$a$ — quadratic residue mod $p$ $\iff \operatorname{ind}_g(a)$ чётно $\iff a^{(p-1)/2} \equiv 1 \pmod p$ (Euler's criterion). Более общо: $a$ — $k$-я степень в $(\mathbb{Z}/p)^*$ $\iff \gcd(k, p-1) \mid \operatorname{ind}_g(a) \iff a^{(p-1)/\gcd(k, p-1)} \equiv 1 \pmod p$. Число $k$-х степеней — $(p-1)/\gcd(k, p-1)$.

Условия применимости. $p$ простое нечётное, $g$ primitive root. По CRT обобщается на $(\mathbb{Z}/p^j)^*$ и $(\mathbb{Z}/2p^j)^*$.

Идея доказательства. Изоморфизм $(\mathbb{Z}/p)^* \cong \mathbb{Z}/(p-1)$ через $g^k \mapsto k$. QR — образы чётных $k$.

Варианты и обобщения. В конечной абелевой группе $G$ число $k$-х степеней равно $|G|/|G[k]|$, где $G[k]$ — $k$-кручение.

Используется в. [Putnam-1991-B4], [IMC-2023-4: $a_i = i^k + i$ — комплектная система вычетов, через критерий $k$-й степени], стандарт для квадратичных вычетов.

---

### E10. Степенные суммы $\sum_{a=1}^{p-1} a^m \pmod p$

Формулировка. Для простого $p$ и $m \ge 0$:
$$
S_m(p) := \sum_{a=1}^{p-1} a^m \equiv \begin{cases}
-1 \pmod p, & (p-1) \mid m \text{ и } m \ge 1, \\
0 \pmod p, & (p-1) \nmid m \text{ и } m \ge 1, \\
p - 1 \equiv -1 \pmod p, & m = 0.
\end{cases}
$$

Условия применимости. $p$ простое. Для составного $n$ суммы $\sum_{a \in (\mathbb{Z}/n)^*} a^m$ выражаются через $\lambda(n)$ и характеры.

Идея доказательства. Если $(p-1) \mid m$: каждый член $\equiv 1 \pmod p$ по Ферма, сумма $\equiv p - 1 \equiv -1$. Если $(p-1) \nmid m$: возьмём primitive root $g$, тогда $S_m \equiv \sum_{k=0}^{p-2} g^{km} = \frac{g^{(p-1)m} - 1}{g^m - 1} \equiv 0$, т.к. $g^m \not\equiv 1$ (числитель ровно $0$, знаменатель ненулевой).

Варианты и обобщения. Та же логика для $\sum \chi(a) a^m$ с характером $\chi$, что даёт связь с Gauss sums.

Используется в. Очень частый «ход» в Putnam-задачах с биномиальными или степенными суммами; вычисление $\sum_a (a^p - a)/p \pmod p$ (квотиент Ферма, теорема Eisenstein-Glaisher); [Putnam-1991-B4].

---

### E11. Generalized Wilson's theorem

Формулировка. Для $n \ge 2$:
$$
\prod_{\substack{1 \le a \le n \\ \gcd(a, n) = 1}} a \equiv \begin{cases}
-1 \pmod n, & n \in \{1, 2, 4, p^k, 2 p^k\} \text{ для нечётного простого } p, \\
+1 \pmod n, & \text{иначе.}
\end{cases}
$$
Случай $n = p$ — классическая теорема Вильсона: $(p-1)! \equiv -1 \pmod p$.

Условия применимости. $n \ge 2$.

Идея доказательства. В конечной абелевой группе $G$ произведение всех элементов равно произведению элементов порядка $\le 2$ (остальные образуют пары $a, a^{-1}$). Если $G = (\mathbb{Z}/n)^*$ цикличен (E3), то ровно один элемент порядка $2$ — $-1$, и произведение $\equiv -1$. Иначе — элементов порядка $\le 2$ ровно $2^r$ с $r \ge 2$, и они образуют $\mathbb{F}_2$-векторное пространство; их произведение — нейтральный элемент (т.к. в $\mathbb{F}_2^r$ при $r \ge 2$ сумма всех векторов — $0$).

Варианты и обобщения.
- $\prod_{a=1}^{p-1} a^{a} \pmod p$, $\prod \binom{p}{k} \pmod p$ — родственные тождества.
- Lerch's формула для $\sum_{a=1}^{p-1} a^{p-1} \pmod{p^2}$ (в духе Wolstenholme).

Используется в. Базовый «закрывающий» аккорд во многих NT-задачах; [Putnam-1996-B5 style], проверка корректности конструкций.

---

## Записи — Exotic

### E12. Quadratic Gauss sum — точное значение

Формулировка. Пусть $p$ — нечётное простое, $\zeta = e^{2\pi i / p}$, $\chi(a) = \left(\frac{a}{p}\right)$ — символ Лежандра. Положим
$$
\tau := \sum_{a=1}^{p-1} \chi(a) \zeta^a.
$$
Тогда $\tau^2 = \chi(-1) p = (-1)^{(p-1)/2} p$, т.е.
$$
\tau = \begin{cases} \sqrt{p}, & p \equiv 1 \pmod 4, \\ i \sqrt{p}, & p \equiv 3 \pmod 4. \end{cases}
$$
(Знак — теорема Гаусса, нетривиальная часть; квадрат — элементарно.)

Условия применимости. $p$ нечётное простое. Аналог для составного $n$ — Gauss sum по Дирихле-характеру.

Идея доказательства. $\tau^2 = \sum_{a, b} \chi(ab) \zeta^{a+b}$. Замена $b = ac$: $\sum_c \chi(c) \sum_a \zeta^{a(1+c)} = \sum_c \chi(c) \cdot [\text{Ramanujan sum}]$. Внутренняя сумма $= p - 1$ при $c = -1$ и $= -1$ иначе, что даёт $\tau^2 = \chi(-1)(p-1) - \sum_{c \ne -1, 0} \chi(c) = \chi(-1) p$.

Варианты и обобщения.
- Через Gauss sum доказывается quadratic reciprocity: $\tau_p \cdot \tau_q$ в $\mathbb{Z}[\zeta_{pq}]$ выражается двумя способами.
- Аналог для $k$-х степеней — Jacobi sums.

Используется в. [Putnam-2008-A4-style] с суммами $\sum \zeta^{a^2}$; вычисление сумм $\sum_{a=1}^{p-1} \chi(a) e^{2\pi i a/p}$ в задачах на корни из единицы.

---

### E13. Артиновская осторожность и pseudo-primitive roots

Формулировка. Гипотеза Артина: для каждого $a \in \mathbb{Z}$, $a \ne -1$ и $a$ не полный квадрат, существует бесконечно много простых $p$, для которых $a$ — primitive root mod $p$ (плотность — постоянная Артина $\approx 0.3739558\ldots$). Доказана условно (GRH). Безусловно — есть лишь редкие частные случаи (Heath-Brown 1986: «хотя бы одно из $2, 3, 5$ — primitive root для $\infty$ простых»).

Практическое следствие. На олимпиаде нельзя ссылаться на «$a$ — primitive root mod $p$» без явного предъявления / проверки. Конструктивно работает только обратное: для данного $p$ предъявить generator через $g^{(p-1)/q} \not\equiv 1$ для каждого $q \mid p - 1$ (E2).

Условия применимости. Теоретический «контрольный знак»: останавливает попытки использовать «среднее $p$» как primitive-root-источник.

Идея доказательства. Гипотеза Артина не доказана — ничего не дать. Heath-Brown — глубокий sieve.

Используется в. Не используется как лемма — только как граница «куда не ходить». Полезно при отбрасывании ложных подходов в Putnam Problem 6.

---

## Self-test

1. Найти все простые $p \le 50$, для которых $2$ — primitive root mod $p$.

2. Доказать, что для каждого $n \ge 3$ сумма
$$\sum_{\substack{1 \le k \le n \\ \gcd(k, n) = 1}} k \equiv 0 \pmod n.$$

3. Доказать, что $n \mid \varphi(2^n - 1)$ для всех $n \ge 1$.

4. Пусть $p \ge 3$ — простое. Доказать, что
$$\sum_{k=1}^{p-1} \frac{1}{k} \equiv 0 \pmod p$$
(в смысле: числитель этой дроби в наименьшем виде делится на $p$).

5. Пусть $p$ — нечётное простое, $g$ — primitive root mod $p$. Доказать, что $-g$ — primitive root mod $p$ тогда и только тогда, когда $p \equiv 1 \pmod 4$.

6. Пусть $p$ — нечётное простое и $p \mid n^4 + 1$ для некоторого $n$. Доказать, что $p \equiv 1 \pmod 8$.

7. Существует ли натуральное $n > 1$, такое что $n \mid 2^n - 1$?

8. Пусть $p$ — нечётное простое, $a, b \in \mathbb{Z}$, $p \nmid ab$. Доказать, что число решений $x \in \mathbb{Z}/p$ уравнения $a x^2 \equiv b \pmod p$ равно $1 + \left(\dfrac{ab}{p}\right)$.

## Решения

1. Тест из E2: $2$ — primitive root mod $p \iff 2^{(p-1)/q} \not\equiv 1 \pmod p$ для каждого простого $q \mid p - 1$. Прямой перебор:

| $p$ | $p-1$ | $\operatorname{ord}_p(2)$ | primitive? |
|---|---|---|---|
| 3 | 2 | 2 | ✓ |
| 5 | 4 | 4 | ✓ |
| 7 | 6 | 3 | ✗ |
| 11 | 10 | 10 | ✓ |
| 13 | 12 | 12 | ✓ |
| 17 | 16 | 8 | ✗ |
| 19 | 18 | 18 | ✓ |
| 23 | 22 | 11 | ✗ |
| 29 | 28 | 28 | ✓ |
| 31 | 30 | 5 | ✗ |
| 37 | 36 | 36 | ✓ |
| 41 | 40 | 20 | ✗ |
| 43 | 42 | 14 | ✗ |
| 47 | 46 | 23 | ✗ |

Ответ: $p \in \{3, 5, 11, 13, 19, 29, 37\}$.

2. Если $\gcd(k, n) = 1$, то и $\gcd(n - k, n) = 1$. Группируем парами $(k, n - k)$: каждая пара даёт сумму $n$. Особый случай $k = n - k$ требует $n = 2k$ с $\gcd(k, 2k) = k = 1$, т.е. $n = 2$ — исключено условием $n \ge 3$. При $n \ge 3$ число пар $= \varphi(n)/2 \in \mathbb{Z}$ (т.к. $\varphi(n)$ чётно при $n \ge 3$), сумма $= n \cdot \varphi(n)/2 \equiv 0 \pmod n$. ✓

3. Число $2^n - 1$ нечётно, $\gcd(2, 2^n - 1) = 1$, и $2^n \equiv 1 \pmod{2^n - 1}$. Покажем $\operatorname{ord}_{2^n - 1}(2) = n$: для $1 \le k < n$, $2^k < 2^n - 1$, поэтому $2^k \not\equiv 1 \pmod{2^n - 1}$ (т.к. $2^k - 1 < 2^n - 1$ и $2^k - 1 > 0$). По E1: $n = \operatorname{ord}_{2^n - 1}(2) \mid \varphi(2^n - 1)$. ✓

4. Группируем $k \leftrightarrow p - k$:
$$\frac{1}{k} + \frac{1}{p-k} = \frac{p}{k(p-k)}.$$
Тогда $\sum_{k=1}^{p-1} \frac{1}{k} = \sum_{k=1}^{(p-1)/2} \frac{p}{k(p-k)}$ — каждое слагаемое содержит множитель $p$ в числителе, знаменатель $k(p-k)$ взаимно прост с $p$. После приведения к общему знаменателю числитель кратен $p$. (Усиление Wolstenholme: при $p \ge 5$ числитель $\equiv 0 \pmod{p^2}$.)

5. Пусть $d = \operatorname{ord}_p(-g)$. $(-g)^k = (-1)^k g^k = 1 \iff g^k = (-1)^k$.
- $k$ чётно: $g^k = 1 \iff (p-1) \mid k$. Минимальное чётное $k$ с этим — $k = p - 1$ ($p$ нечётное $\Rightarrow p-1$ чётно).
- $k$ нечётно: $g^k = -1 = g^{(p-1)/2} \iff k \equiv (p-1)/2 \pmod{p-1}$. Минимальное нечётное $k$ существует $\iff (p-1)/2$ нечётно $\iff p \equiv 3 \pmod 4$, и тогда $k = (p-1)/2$.

При $p \equiv 3 \pmod 4$: $d = (p-1)/2 < p - 1$, не primitive. При $p \equiv 1 \pmod 4$: нечётных $k < p - 1$ нет, $d = p - 1$, primitive. ✓

6. $p \mid n^4 + 1 \Rightarrow n^8 \equiv 1 \pmod p$, причём $n^4 \equiv -1 \not\equiv 1$, поэтому $\operatorname{ord}_p(n) \nmid 4$. Из $\operatorname{ord}_p(n) \mid 8$ следует $\operatorname{ord}_p(n) = 8$. По E1: $8 \mid p - 1$, т.е. $p \equiv 1 \pmod 8$. ✓

7. Ответ: нет. Пусть $n > 1$, $p$ — наименьший простой делитель $n$. По E4: $\operatorname{ord}_p(2) \mid \gcd(n, p-1) = 1$ (все простые делители $\gcd$ — $< p$ и одновременно $\mid n$, противоречие минимальности $p$). Значит $2 \equiv 1 \pmod p$, $p \mid 1$ — противоречие.

8. $a, b \in (\mathbb{Z}/p)^*$, уравнение эквивалентно $x^2 \equiv ba^{-1} \pmod p$. Число решений: $0$ если $ba^{-1}$ — non-residue, $2$ — если residue (и $\ne 0$). Через символ Лежандра: $1 + \left(\frac{ba^{-1}}{p}\right)$. Поскольку $\left(\frac{a^{-1}}{p}\right) = \left(\frac{a}{p}\right)$ (квадрат символа равен $1$), имеем $\left(\frac{ba^{-1}}{p}\right) = \left(\frac{ab}{p}\right)$. ✓
