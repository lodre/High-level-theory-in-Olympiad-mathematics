---
topic: Теория чисел
subtopic: "Квадратичные вычеты, символы Legendre / Jacobi"
sources:
  - "K. Ireland, M. Rosen — A Classical Introduction to Modern Number Theory (гл. 5, 6, 8, 11)"
  - "H. Davenport — Multiplicative Number Theory (гл. о character sums и Pólya–Vinogradov)"
  - "K. Conrad — Hensel's Lemma; Quadratic Reciprocity Proofs; Gauss Sums (UConn lecture notes)"
  - "M. R. Murty — Evaluation of the Quadratic Gauss Sum (Queen's University)"
  - "L. Goldmakher — Legendre, Jacobi, and Kronecker Symbols (Williams College)"
  - "R. Evans — Jacobsthal sums (UCSD)"
  - "Engel — Problem-Solving Strategies (гл. Number Theory)"
  - "Andreescu, Andrica, Feng — Putnam and Beyond"
  - "Niven, Zuckerman, Montgomery — An Introduction to the Theory of Numbers"
  - "Wikipedia — Legendre symbol / Jacobi symbol / Quadratic reciprocity / Quadratic Gauss sum / Pólya–Vinogradov inequality / Hasse's theorem on elliptic curves"
  - "AoPS — Quadratic residues; IMOmath — Some sums of Legendre's symbols"
  - "Dummit lecture notes (Northeastern) — Quadratic residues, Legendre and Jacobi symbols"
  - "IMC Compendium / Putnam Compendium"
problems_referenced:
  - IMC-2005-DAY2-6
  - IMC-2007-DAY2-2
  - IMC-2013-DAY2-2
  - IMC-2013-DAY2-4
  - IMC-2020-6
  - IMC-2023-4
  - IMC-2024-10
  - Putnam-1991-B5
  - Putnam-2010-B4
  - IMO-Shortlist-2008-N5
last_updated: 2026-04-29
---

# Квадратичные вычеты, символы Legendre / Jacobi

## Scope
Семейство тождеств вокруг $\left(\frac{a}{p}\right)$ и $\left(\frac{a}{n}\right)$: критерии (Euler, Gauss), закон взаимности, поведение на $p^k$ через Hensel, точные суммы $\sum \left(\frac{f(x)}{p}\right)$ для линейных и квадратичных $f$, квадратичные Gauss-суммы и их знак, оценки Pólya–Vinogradov для коротких сумм, связь с уравнениями Pell и нормами в $\mathbb{Z}[\sqrt{d}]$. На IMC/Putnam применяется в задачах вида «доказать, что у $f(x)\equiv 0 \pmod{p^k}$ нет решений», «оценить число $x$ с $f(x)$-вычетом», «связь $p \equiv \cdot \pmod{m}$ с разрешимостью», а также как мост к биквадратичным/кубическим вычетам.

## Записи — Core

### E1. Euler's criterion (критерий Эйлера)

Формулировка. Пусть $p$ — нечётное простое, $p \nmid a$. Тогда
$$
a^{(p-1)/2} \equiv \left(\frac{a}{p}\right) \pmod{p},
$$
где $\left(\frac{a}{p}\right) \in \{+1, -1\}$ — символ Legendre.

Условия применимости. $p$ нечётное, $p \nmid a$. Для $p = 2$ символ не определяется в классическом виде, и $a$ — всегда «вычет» $\bmod 2$.

Идея доказательства. $\mathbb{F}_p^\times$ — циклическая группа порядка $p-1$, оператор «возведение в $(p-1)/2$» отображает её на $\{\pm 1\}$ с ядром = квадраты.

Варианты и обобщения.
- $\left(\frac{-1}{p}\right) = (-1)^{(p-1)/2}$ — первое дополнение.
- Для $p^k$: $a^{\varphi(p^k)/2} \equiv \pm 1 \pmod{p^k}$, и $a$ — квадрат $\bmod p^k$ $\iff$ $a^{\varphi(p^k)/2} \equiv 1 \pmod{p^k}$ (см. E5).

Используется в. Базис всего блока. [IMC-2020-6] (наличие/отсутствие корня cubic через дискриминант), [IMC-2023-4] (характеристика квадратичных вычетов через $a \mapsto a^k$).

---

### E2. Gauss's lemma (лемма Гаусса)

Формулировка. Пусть $p$ — нечётное простое, $p \nmid a$. Рассмотрим остатки $a, 2a, 3a, \dots, \frac{p-1}{2}a \pmod p$, приведённые в $(-p/2, p/2)$. Пусть $\mu$ — число отрицательных среди них. Тогда
$$
\left(\frac{a}{p}\right) = (-1)^{\mu}.
$$

Условия применимости. Любое нечётное $p$, $p \nmid a$. Для $a$ небольшого — наиболее эффективный счётный метод.

Идея доказательства. Произведение всех $|ka \bmod^* p|$ для $k = 1, \dots, (p-1)/2$ совпадает с $((p-1)/2)!$ (т.к. абсолютные значения остатков пробегают $1, \dots, (p-1)/2$ без повторов). Знак — $(-1)^\mu$, а с другой стороны произведение $= a^{(p-1)/2} \cdot ((p-1)/2)!$. Сократили — получили E1.

Варианты и обобщения.
- Eisenstein form: $\left(\frac{a}{p}\right) = (-1)^{\sum_{k=1}^{(p-1)/2} \lfloor ka/p \rfloor}$ при нечётном $a$.
- Используется как «дешёвый» способ доказать второе дополнение: $\left(\frac{2}{p}\right) = (-1)^{(p^2-1)/8}$.

Используется в. Доказательство закона взаимности (E3); ручной счёт символов; [IMC-2013-DAY2-2] (там анализ $\sum (-1)^{\lfloor k/p \rfloor + \lfloor k/q \rfloor}$ — в тех же координатах, что и Eisenstein-доказательство QR).

---

### E3. Quadratic reciprocity law (закон квадратичной взаимности) и два дополнения

Формулировка. Для различных нечётных простых $p, q$:
$$
\left(\frac{p}{q}\right)\left(\frac{q}{p}\right) = (-1)^{\frac{p-1}{2} \cdot \frac{q-1}{2}}.
$$
Эквивалентно: символы совпадают, кроме случая $p \equiv q \equiv 3 \pmod 4$ — тогда отличаются знаком.

Дополнения:
$$
\left(\frac{-1}{p}\right) = (-1)^{(p-1)/2} = \begin{cases} +1, & p \equiv 1 \pmod 4, \\ -1, & p \equiv 3 \pmod 4, \end{cases}
$$
$$
\left(\frac{2}{p}\right) = (-1)^{(p^2-1)/8} = \begin{cases} +1, & p \equiv \pm 1 \pmod 8, \\ -1, & p \equiv \pm 3 \pmod 8. \end{cases}
$$

Условия применимости. $p, q$ — нечётные простые, $p \ne q$. Для $\left(\frac{2}{p}\right)$ используется отдельно.

Идея доказательства. Любое из $200{+}$ известных доказательств; стандартное — через Eisenstein/Gauss-lemma подсчёт точек решётки в прямоугольнике $[1, (p-1)/2] \times [1, (q-1)/2]$ ниже прямой $y = qx/p$. Альтернативно — через квадратичные суммы Gauss (E7) в кольце $\mathbb{Z}[\zeta_p]$.

Варианты и обобщения.
- Закон взаимности для $\left(\frac{a}{p}\right)$ при произвольном $a$ — через мультипликативность и QR.
- Биквадратичный (4-й степени) и кубический закон взаимности — для $\mathbb{Z}[i]$ и $\mathbb{Z}[\zeta_3]$ соответственно (E12).

Используется в. Любая задача, где нужно проверить $a$-QR-ность по $p$ для большого/символьного $p$. [IMC-2005-DAY2-6] (Pell с $\sqrt{7}$ — разрешимость через $\left(\frac{7}{p}\right)$), [IMC-2007-DAY2-2] (4-е степени mod 29 = квадраты от квадратов), [IMC-2013-DAY2-4] (CRT-конструкция избегает кратных $p^2$ — нужно знать, какие классы кубических вычетов).

---

### E4. Jacobi symbol (символ Якоби) и обобщённый закон взаимности

Формулировка. Для нечётного $n = p_1^{a_1} \cdots p_r^{a_r} > 0$ и любого $a \in \mathbb{Z}$:
$$
\left(\frac{a}{n}\right) := \prod_{i=1}^r \left(\frac{a}{p_i}\right)^{a_i}.
$$
Свойства: мультипликативность по обеим аргументам, $\left(\frac{a}{n}\right) \in \{-1, 0, +1\}$, $= 0 \iff \gcd(a, n) > 1$. Закон взаимности для нечётных взаимно простых $m, n > 0$:
$$
\left(\frac{m}{n}\right)\left(\frac{n}{m}\right) = (-1)^{\frac{m-1}{2} \cdot \frac{n-1}{2}}, \qquad \left(\frac{-1}{n}\right) = (-1)^{(n-1)/2}, \qquad \left(\frac{2}{n}\right) = (-1)^{(n^2-1)/8}.
$$

Условия применимости. $n$ нечётное положительное; $a \in \mathbb{Z}$. Важно: $\left(\frac{a}{n}\right) = 1$ НЕ значит, что $a$ — квадрат $\bmod n$; обратное верно — если $a$ квадрат $\bmod n$, то символ $= 1$. Контрпример: $\left(\frac{2}{15}\right) = \left(\frac{2}{3}\right)\left(\frac{2}{5}\right) = (-1)(-1) = 1$, но $2$ — не квадрат $\bmod 15$.

Идея доказательства. Свести к QR и дополнениям через мультипликативность, аккуратно отслеживая чётности $(p_i - 1)/2$.

Варианты и обобщения.
- Kronecker symbol $\left(\frac{a}{n}\right)$ — расширение на чётные $n$ и $n < 0$.
- Алгоритм быстрого вычисления $\left(\frac{a}{n}\right)$ за $O(\log^2 n)$ — аналог Euclid для GCD, без факторизации $n$. Это и есть основной выигрыш Jacobi: можно «упрощать» символ, не зная разложения знаменателя.

Используется в. [IMC-2013-DAY2-4] (CRT с большим количеством простых — Jacobi-стиль вычисления), Putnam-style оценки разрешимости диофантовых уравнений.

---

### E5. Структура $(\mathbb{Z}/p^k)^\times$ и Hensel-лифт квадратов

Формулировка. Пусть $p$ — нечётное простое, $k \ge 1$, $\gcd(a, p) = 1$. Тогда:
$$
a \text{ — квадрат в } (\mathbb{Z}/p^k)^\times \iff a \text{ — квадрат в } (\mathbb{Z}/p)^\times \iff \left(\frac{a}{p}\right) = +1.
$$
Группа $(\mathbb{Z}/p^k)^\times$ циклическая порядка $p^{k-1}(p-1)$, индекс подгруппы квадратов = $2$.

Для $p = 2$: $(\mathbb{Z}/2)^\times = \{1\}$, $(\mathbb{Z}/4)^\times \cong \mathbb{Z}/2$, $(\mathbb{Z}/2^k)^\times \cong \mathbb{Z}/2 \times \mathbb{Z}/2^{k-2}$ при $k \ge 3$. Соответственно: $a$ нечётное — квадрат $\bmod 2^k$ ($k \ge 3$) $\iff a \equiv 1 \pmod 8$. В частности индекс квадратов = $4$ при $k \ge 3$.

Условия применимости. $\gcd(a, p) = 1$ обязательно (иначе нужно отдельно отслеживать $v_p(a)$ — лифтится только если $v_p(a)$ чётно).

Идея доказательства. Hensel: $f(x) = x^2 - a$, $f'(x) = 2x$. При нечётном $p$ и $r$ — корне $\bmod p$, имеем $f'(r) = 2r \not\equiv 0 \pmod p$, поэтому $r$ единственно лифтится до корня $\bmod p^k$. При $p = 2$ требуется $f'(r) \not\equiv 0 \pmod 4$, что не выполнено, — отсюда более сильное условие $a \equiv 1 \pmod 8$.

Варианты и обобщения.
- Аналогично для $n$-х степеней: при $p \nmid n$ количество $n$-х степеней в $(\mathbb{Z}/p^k)^\times$ = $\varphi(p^k)/\gcd(n, \varphi(p^k))$.
- Полное условие разрешимости $a \equiv y^2 \pmod n$ для составного $n$ — CRT + указанные критерии для $p^k$.

Используется в. [IMC-2007-DAY2-2] (поднятие $\bmod 29$ к $\bmod 29^4$ через 4-степенной аналог Hensel: $f(x) = x^4 - a$, $f'(x) = 4x^3$ обратимо $\bmod 29$), стандарт для задач «существует ли $n$ с $n^2 \equiv a \pmod{p^k}$».

---

## Записи — Standard

### E6. Сумма Legendre-символов от линейного и квадратичного многочлена

Формулировка. Пусть $p$ — нечётное простое.

Линейный случай: при $p \nmid a$,
$$
\sum_{x=0}^{p-1} \left(\frac{ax + b}{p}\right) = 0.
$$

Квадратичный случай: для $f(x) = ax^2 + bx + c$ с $p \nmid a$ и дискриминантом $D = b^2 - 4ac$,
$$
\sum_{x=0}^{p-1} \left(\frac{ax^2 + bx + c}{p}\right) = \begin{cases}
-\left(\frac{a}{p}\right), & p \nmid D, \\
(p-1) \left(\frac{a}{p}\right), & p \mid D.
\end{cases}
$$

Условия применимости. $p$ нечётное, $p \nmid a$. При $p \mid a$ выражение сводится к линейному случаю.

Идея доказательства. Линейный случай — биекция $x \mapsto ax + b$ перебирает $\mathbb{F}_p$, а сумма $\sum_y \left(\frac{y}{p}\right) = 0$. Квадратичный — выделяем полный квадрат: $4a f(x) = (2ax+b)^2 - D$, замена $y = 2ax+b$:
$$
\left(\frac{4a}{p}\right) \sum_x \left(\frac{f(x)}{p}\right) = \sum_y \left(\frac{y^2 - D}{p}\right).
$$
При $p \nmid D$ применяем $\left(\frac{y^2 - D}{p}\right) = \left(\frac{y^2(1 - D y^{-2})}{p}\right) = \left(\frac{1 - Dy^{-2}}{p}\right)$ для $y \ne 0$ — биекция $y \mapsto Dy^{-2}$ показывает, что сумма $= -1 - \left(\frac{-D}{p}\right) \cdot 0 = -1$ после аккуратной обработки. Учитывая $\left(\frac{4a}{p}\right) = \left(\frac{a}{p}\right)$, получаем $-\left(\frac{a}{p}\right)$. При $p \mid D$ сумма вырождается в $(p-1) \left(\frac{a}{p}\right)$ — все ненулевые $f(x)$ дают одинаковый знак.

Варианты и обобщения.
- Cubic case (значительно сложнее): $\left|\sum_x \left(\frac{x^3 + ax + b}{p}\right)\right| \le 2\sqrt{p}$ — Hasse–Weil bound (E11).
- Jacobsthal-сумма $K(a) = \sum_x \left(\frac{x(x^2 + a)}{p}\right)$ для $p \equiv 1 \pmod 4$ даёт декомпозицию $p = (K(a)/2)^2 + (K(b)/2)^2$ при $a$-QR, $b$-NR.

Используется в. [IMC-2023-4] (характеристика, когда $\{i^k + i\}$ — полная система вычетов: связь с $\sum \left(\frac{i^k + i - c}{p}\right)$), [Putnam-2010-B4] (доказать существование $x$ с $\left(\frac{x^2 + 1}{p}\right) = 1$ через подсчёт суммы), [IMO-Shortlist-2008-N5].

---

### E7. Quadratic Gauss sum (квадратичная сумма Гаусса) и её знак

Формулировка. Для нечётного простого $p$ и $\zeta = e^{2\pi i / p}$,
$$
g(p) := \sum_{a=0}^{p-1} \zeta^{a^2} = \sum_{a=1}^{p-1} \left(\frac{a}{p}\right) \zeta^a + \text{(тривиальные)}.
$$
Точнее, если ввести «нормализованную» $\tau(\chi) = \sum_{a=1}^{p-1} \left(\frac{a}{p}\right) \zeta^a$, то $g(p) = \tau(\chi)$ (для квадратичного характера), и
$$
g(p) = \begin{cases} \sqrt{p}, & p \equiv 1 \pmod 4, \\ i \sqrt{p}, & p \equiv 3 \pmod 4. \end{cases}
$$
В частности $|g(p)|^2 = p$, $g(p)^2 = \left(\frac{-1}{p}\right) p$.

Условия применимости. $p$ нечётное простое. Для составного модуля $n$ — формула отличается, и знак становится тоньше (см. Hasse–Davenport relations).

Идея доказательства. $|g|^2 = p$ — стандартный подсчёт через $\sum \zeta^{a^2 - b^2}$ и замену переменных. $g^2 = \left(\frac{-1}{p}\right) p$ — через $\tau(\chi)\overline{\tau(\chi)} = \chi(-1) \tau(\chi)^2 \cdot \dots$. Знак знаменит сложностью: Гаусс боролся четыре года, известно ≥ 6 разных доказательств (через θ-функции, residue calculus, контурное интегрирование, finite Fourier). Самое короткое — через определитель матрицы DFT.

Варианты и обобщения.
- Kronecker–Hensel-Davenport: $g(\chi_1 \chi_2) = \chi_2(\text{disc}) \cdot g(\chi_1) g(\chi_2)$ при подходящих условиях.
- Доказательство QR через $g$: $g(p)^2 = \pm p$ в $\mathbb{Z}[\zeta_q]$, и подъём в $\bmod q$ даёт связь $\left(\frac{p}{q}\right)\left(\frac{q}{p}\right)$.

Используется в. Доказательство QR (E3); оценки $\left|\sum \left(\frac{x}{p}\right) f(x)\right| \le \sqrt{p} \cdot \|f\|_2$ для $f$ — как multiplicative-character-сумма; неявно во всех Pólya–Vinogradov-аргументах (E8).

---

### E8. Pólya–Vinogradov inequality (неравенство Полиа–Виноградова)

Формулировка. Пусть $\chi$ — нетривиальный Dirichlet-характер $\bmod q$ (например, $\chi(a) = \left(\frac{a}{p}\right)$ для $q = p$). Для любых целых $M$, $N \ge 1$:
$$
\left| \sum_{n = M+1}^{M+N} \chi(n) \right| \le \sqrt{q} \log q \quad (\text{с константой не более } 2 \text{ в большинстве версий}).
$$
В частности, для $\chi = $ Legendre $\bmod p$:
$$
\left| \sum_{n = M+1}^{M+N} \left(\frac{n}{p}\right) \right| < \sqrt{p} \log p.
$$

Условия применимости. $\chi$ нетривиальный (для тривиального $\chi$ сумма $\approx N$). Оценка нетривиальна при $N \gg \sqrt{p} \log p$, бессмысленна при $N \le \sqrt{p}$.

Идея доказательства. Дискретное преобразование Фурье: $\chi(n) = \frac{1}{g(\chi)} \sum_a \overline{\chi(a)} e^{2\pi i an/q}$ через сумму Гаусса (E7), $|g(\chi)| = \sqrt{q}$. Подставляем, меняем порядок суммирования, оцениваем геометрическую сумму $\sum_n e^{2\pi i a n/q}$ через $\min(N, 1/\|a/q\|)$, считаем $\sum_a 1/\|a/q\|$ — даёт $\log q$.

Варианты и обобщения.
- Burgess inequality (E13): для $N \ge p^{1/4 + \varepsilon}$ — оценка $\sqrt{N} p^{1/8 + o(1)}$, лучше PV в коротком диапазоне.
- Следствие: наименьший QR-non-residue $\bmod p$ есть $O(\sqrt{p} \log p)$ (через Pólya–Vinogradov: если на $[1, K]$ все вычеты, сумма $\approx K \ne 0$).

Используется в. Asymptotic-аргументы для распределения $\left(\frac{n}{p}\right)$; доказательства существования non-residue в малом интервале; задачи Putnam-style на «найти $n \le \sqrt{p}\log p$ с $f(n)$-вычетом».

---

### E9. Распределение QR через тождества с символами и применение к Pell

Формулировка. Полезные точные тождества (для нечётного $p$):
$$
\sum_{a=1}^{p-1} \left(\frac{a(a+1)}{p}\right) = -1, \qquad \sum_{a=1}^{p-1} \left(\frac{a^2+1}{p}\right) = -1 - \left(\frac{-1}{p}\right) \cdot 0 = -1 \text{ при } p \nmid 1.
$$
(Точнее, $\sum_a \left(\frac{a^2 + b}{p}\right) = -1$ при $p \nmid b$, $= p-1$ при $p \mid b$ — частный случай E6.)

Связь с Pell: уравнение $x^2 - dy^2 = N$ (для не-квадрата $d$) имеет решение в $\mathbb{Z}$ только если $\left(\frac{d}{p}\right) = 1$ для всех $p \mid N$ (при $\gcd(N, 2d) = 1$), и для $\left(\frac{N}{p}\right) = 1$ для всех $p \mid d$ нечётных. Это локальное условие необходимое; для $d > 0$ положительности и достаточно (через теорию binary quadratic forms над $\mathbb{Z}$, при $h(d) = 1$).

Условия применимости. Pell-связь требует фундаментального решения и теории norm-form. Тождества — для любых $p$ нечётных.

Идея доказательства. Тождества — биекция $a \mapsto a^{-1}$, замена $a \mapsto a + 1$, разложение $a(a+1) = a^2(1 + 1/a)$. Pell — норма $N: \mathbb{Z}[\sqrt{d}] \to \mathbb{Z}$ мультипликативна, а $\left(\frac{d}{p}\right) = 1 \iff p$ распадается в $\mathbb{Z}[\sqrt{d}]$ (для $p \nmid 2d$).

Варианты и обобщения.
- Фундаментальное решение $x^2 - dy^2 = 1$ существует для всех бесквадратных $d > 0$ (теорема Лагранжа), и любое $\gcd(N, d) = 1$, $\left(\frac{d}{p}\right) = 1$ для всех $p \mid N$ — даёт ∞ много решений $x^2 - dy^2 = N$ при наличии хоть одного.
- $-1$ как норма: $x^2 - dy^2 = -1$ разрешимо $\iff$ continued fraction $\sqrt{d}$ имеет нечётный период.

Используется в. [IMC-2005-DAY2-6] (Pell $s^2 - 7 \Delta^2 t^2 = 4$ ⟹ ∞ решений через $(8 \pm 3\sqrt{7})^n$), [IMC-2024-10] (анализ через $(\mathbb{Z}/p)^\times$ — норма-форма по сути).

---

## Записи — Exotic

### E10. Wilson-type для $((p-1)/2)!$

Формулировка. Пусть $p$ — нечётное простое. Тогда
$$
\left(\frac{(p-1)}{2}\right)!^2 \equiv (-1)^{(p+1)/2} \pmod p,
$$
эквивалентно: $((p-1)/2)!^2 \equiv -\left(\frac{-1}{p}\right) \pmod p$. В частности при $p \equiv 1 \pmod 4$: $((p-1)/2)!^2 \equiv -1 \pmod p$ — то есть $((p-1)/2)!$ есть «явный» $\sqrt{-1} \bmod p$.

Условия применимости. $p$ нечётное простое.

Идея доказательства. Wilson: $(p-1)! \equiv -1 \pmod p$. Парная замена $k \leftrightarrow p - k$: $(p-1)! = \prod_{k=1}^{(p-1)/2} k(p-k) \equiv \prod k \cdot (-k) = (-1)^{(p-1)/2} ((p-1)/2)!^2$. Отсюда формула.

Варианты и обобщения.
- $((p-1)/2)! \equiv \pm 1 \pmod p$ для $p \equiv 3 \pmod 4$ (знак — не элементарный, выражается через class number $h(-p)$ через формулу Чоулы–Дэвенпорта).
- Аналог: $\binom{p-1}{(p-1)/2} \equiv (-1)^{(p-1)/2} 4^{(p-1)/2} \pmod p$.

Используется в. Конструкция $\sqrt{-1} \bmod p$ для $p \equiv 1 \pmod 4$ — основа алгоритма представления $p = a^2 + b^2$ (Cornacchia). [Putnam-1991-B5 style]: «найти явное $n$ с $n^2 \equiv -1 \pmod p$» для конкретного $p \equiv 1 \pmod 4$.

---

### E11. Hasse bound для $\sum \left(\frac{f(x)}{p}\right)$, $f$ кубический

Формулировка. Пусть $f(x) \in \mathbb{F}_p[x]$ — кубический многочлен без кратных корней (в $\overline{\mathbb{F}_p}$). Тогда
$$
\left| \sum_{x=0}^{p-1} \left(\frac{f(x)}{p}\right) \right| \le 2\sqrt{p}.
$$
Эквивалентно: число точек $E(\mathbb{F}_p)$ кривой $y^2 = f(x)$ (плюс точка на бесконечности) удовлетворяет $|\#E(\mathbb{F}_p) - (p+1)| \le 2\sqrt{p}$ (Hasse, 1933).

Условия применимости. $f$ — кубика без кратных корней (т.е. $E$ — несингулярная elliptic curve), $p \ne 2, 3$ (стандартная редукция). Для $f$ с кратными корнями кривая вырождается в рациональную/кубическую с node/cusp, и оценки слабее или тривиальны.

Идея доказательства. $\#E(\mathbb{F}_p) = 1 + \sum_x (1 + \left(\frac{f(x)}{p}\right)) = p + 1 + \sum_x \left(\frac{f(x)}{p}\right)$. Hasse: $\#E(\mathbb{F}_p) = p + 1 - a_p$ с $|a_p| \le 2\sqrt{p}$ через эндоморфизм Frobenius на Tate-модуле. Олимпиадно — обычно «факт-чёрный ящик» с конкретной редукцией.

Варианты и обобщения.
- Для $f$ степени $d \ge 4$ без кратных корней: $|\sum \left(\frac{f(x)}{p}\right)| \le (d-1)\sqrt{p}$ (Weil, 1948).
- Для рациональной функции: аналогичная оценка с поправкой на полюса.

Используется в. [IMC-2020-6] (count corn solutions кубики $a^3 - 3a + 1 \equiv 0$ — через Hasse + фактор-структуру); олимпиадные задачи «доказать, что $\exists x$ с $f(x)$-вычетом» для $p$ большого; теоретический предел того, что элементарные методы дают для cubic-сумм.

---

### E12. Биквадратичный (4-й степени) и кубический закон взаимности

Формулировка. Биквадратичный (4-й степени) символ. Пусть $\pi \in \mathbb{Z}[i]$ — простой Gauss-целый, $N(\pi) = p$ (рациональное простое $\equiv 1 \pmod 4$). Для $\alpha \in \mathbb{Z}[i]$, $\gcd(\alpha, \pi) = 1$:
$$
\left(\frac{\alpha}{\pi}\right)_4 \in \{1, i, -1, -i\}, \quad \alpha^{(N(\pi)-1)/4} \equiv \left(\frac{\alpha}{\pi}\right)_4 \pmod{\pi}.
$$
Закон взаимности (для primary $\pi, \theta$): $\left(\frac{\theta}{\pi}\right)_4 \left(\frac{\pi}{\theta}\right)_4^{-1} = (-1)^{((N\pi-1)/4)((N\theta-1)/4)}$.

Кубический символ — аналогично в $\mathbb{Z}[\zeta_3]$. Связь с рациональной арифметикой: $a$ — биквадрат $\bmod p$ (где $p \equiv 1 \pmod 4$, $p = \pi \bar{\pi}$) $\iff$ $\left(\frac{a}{\pi}\right)_4 \left(\frac{a}{\bar\pi}\right)_4 = 1$.

Подсчёт: число $r$-х степенных вычетов в $\mathbb{F}_p^\times$ (при $r \mid p - 1$) равно $(p-1)/r$.

Условия применимости. Нужно работать в подходящем кольце целых $\mathbb{Z}[i]$, $\mathbb{Z}[\zeta_3]$. Олимпиадное применение — обычно ограничено явным подсчётом 4-х/3-х степеней $\bmod p$.

Идея доказательства. Аналог критерия Эйлера в $(\mathbb{Z}[i]/\pi)^\times$ — циклической группе порядка $N(\pi) - 1$, делящегося на $4$. Закон взаимности — Eisenstein-style через resultants или Gauss-суммы в $\mathbb{Z}[i]$.

Варианты и обобщения. Eisenstein reciprocity для $r$-х степеней в $\mathbb{Z}[\zeta_r]$.

Используется в. [IMC-2007-DAY2-2] (8 четвёртых степеней $\bmod 29$ — это $|F_p^\times| / 4 = 28/4 = 7$ ненулевых классов плюс $0$, итого $8$); задачи на «сколько $n$-х степеней есть $\bmod p$» для $p \equiv 1 \pmod n$.

---

## Self-test

1. Найти все простые $p$, для которых $-3$ — квадратичный вычет $\bmod p$.

2. Доказать, что $\sum_{a=1}^{p-1} \left(\frac{a^3 - a}{p}\right)$ удовлетворяет $\left|\sum\right| \le 2\sqrt{p}$.

3. Найти $\left(\frac{15}{29}\right)$ через закон взаимности и проверить через критерий Эйлера.

4. Доказать, что $7$ — четвёртая степень $\bmod 29$.

5. Пусть $p \equiv 1 \pmod 4$. Найти явный квадратный корень из $-1$ $\bmod p$ через факториал.

6. Сколько решений у $x^2 \equiv 5 \pmod{49}$? у $x^2 \equiv 5 \pmod{16}$?

7. Доказать, что $\sum_{a=1}^{p-1} \left(\frac{a + a^{-1}}{p}\right) = -1 - \left(\frac{2}{p}\right) \cdot \text{(поправка)}$ — найти точный вид.

8. Пусть $p$ — нечётное простое. Доказать: число $a \in \{1, \dots, p-1\}$, для которых одновременно $a$ и $a + 1$ — квадратичные вычеты $\bmod p$, равно $\frac{p - 4 - \left(\frac{-1}{p}\right)}{4}$.

## Решения

1. По QR и первому дополнению: $\left(\frac{-3}{p}\right) = \left(\frac{-1}{p}\right)\left(\frac{3}{p}\right)$. Для $p > 3$ нечётного: $\left(\frac{3}{p}\right) = \left(\frac{p}{3}\right) \cdot (-1)^{(p-1)/2}$ (т.к. $(3-1)/2 = 1$). Тогда $\left(\frac{-3}{p}\right) = \left(\frac{-1}{p}\right) \cdot \left(\frac{p}{3}\right) \cdot (-1)^{(p-1)/2} = (-1)^{(p-1)/2} \cdot \left(\frac{p}{3}\right) \cdot (-1)^{(p-1)/2} = \left(\frac{p}{3}\right)$. Итого $-3$ — QR $\bmod p$ $\iff$ $\left(\frac{p}{3}\right) = 1$ $\iff$ $p \equiv 1 \pmod 3$. Плюс тривиально $p = 3$ (там $-3 \equiv 0$).

2. $f(x) = x^3 - x = x(x-1)(x+1)$ — кубика с тремя различными корнями $\bmod p$ при $p > 3$, без кратных. Применяем E11 (Hasse): $|\sum_x \left(\frac{f(x)}{p}\right)| \le 2\sqrt{p}$. (Sanity: $f(x) = x(x^2 - 1)$, при $p \equiv 3 \pmod 4$ кривая $y^2 = x^3 - x$ имеет $a_p = 0$ — supersingular reduction, сумма $= 0$.)

3. $\left(\frac{15}{29}\right) = \left(\frac{3}{29}\right)\left(\frac{5}{29}\right)$. По QR: $\left(\frac{3}{29}\right) = \left(\frac{29}{3}\right)(-1)^{1 \cdot 14} = \left(\frac{2}{3}\right) = -1$. $\left(\frac{5}{29}\right) = \left(\frac{29}{5}\right)(-1)^{2 \cdot 14} = \left(\frac{4}{5}\right) = 1$. Итого $\left(\frac{15}{29}\right) = -1$. Проверка Эйлером: $15^{14} \bmod 29$. $15^2 = 225 = 7 \cdot 29 + 22 \equiv 22 \equiv -7$. $15^4 \equiv 49 \equiv 20 \equiv -9$. $15^8 \equiv 81 \equiv 81 - 2\cdot 29 = 23 \equiv -6$. $15^{14} = 15^8 \cdot 15^4 \cdot 15^2 \equiv (-6)(-9)(-7) = -378 \equiv -378 + 13 \cdot 29 = -378 + 377 = -1 \pmod{29}$. ✓

4. $7$ — четвёртая степень $\bmod 29$ $\iff$ $7$ — квадрат, и $\sqrt{7}$ — квадрат. Сначала $\left(\frac{7}{29}\right)$: $\left(\frac{7}{29}\right) = \left(\frac{29}{7}\right)(-1)^{3 \cdot 14} = \left(\frac{1}{7}\right) = 1$. Найдём $r$ с $r^2 \equiv 7 \pmod{29}$. $6^2 = 36 \equiv 7$ ✓. Теперь $\left(\frac{6}{29}\right) = \left(\frac{2}{29}\right)\left(\frac{3}{29}\right)$. $29 \equiv 5 \pmod 8 \Rightarrow \left(\frac{2}{29}\right) = -1$. $\left(\frac{3}{29}\right) = -1$ (см. (3)). $\left(\frac{6}{29}\right) = 1$. Значит $6$ — квадрат, $\sqrt{6}^2 = 6$ — это $\sqrt[4]{7}$ только если $\sqrt{7}$ выбран как $6$ или $-6 \equiv 23$. $\left(\frac{23}{29}\right) = \left(\frac{-6}{29}\right) = \left(\frac{-1}{29}\right)\left(\frac{6}{29}\right) = 1 \cdot 1 = 1$ — тоже квадрат. Итого хотя бы один из $\pm \sqrt{7}$ — квадрат, значит $7$ — биквадрат. (Альтернатива через E12: $|F_{29}^\times|/4 = 7$ ненулевых биквадратов, факт сверки с задачей IMC-2007-DAY2-2 — биквадраты $\bmod 29$ это $\{1, 7, 16, 20, 23, 24, 25\}$, $7$ среди них ✓.)

5. $((p-1)/2)! \pmod p$ — по E10 квадрат равен $(-1)^{(p+1)/2}$. При $p \equiv 1 \pmod 4$: $(p+1)/2$ нечётно, $((p-1)/2)!^2 \equiv -1 \pmod p$. Значит $\sqrt{-1} \equiv \pm ((p-1)/2)! \pmod p$.

6. Mod 49: $5$ — квадрат $\bmod 7$? $\left(\frac{5}{7}\right) = \left(\frac{7}{5}\right)(-1)^{2 \cdot 3} = \left(\frac{2}{5}\right) = -1$. Не квадрат. По E5 не квадрат и $\bmod 49$. Решений: $0$.

   Mod 16: $5 \equiv 5 \pmod 8$. По E5 ($p = 2$, $k = 4 \ge 3$): $a$ — квадрат $\bmod 2^k$ $\iff a \equiv 1 \pmod 8$. $5 \not\equiv 1 \pmod 8$. Решений: $0$.

7. По E6: $\sum_{a=1}^{p-1} \left(\frac{a + a^{-1}}{p}\right) = \sum_{a=1}^{p-1} \left(\frac{a^2 + 1}{p}\right) \cdot \left(\frac{a^{-1}}{p}\right)^{-1}$? Чище: $\left(\frac{a + a^{-1}}{p}\right) = \left(\frac{(a^2+1)/a}{p}\right) = \left(\frac{a^2 + 1}{p}\right) \left(\frac{a}{p}\right)$ (т.к. $\left(\frac{1/a}{p}\right) = \left(\frac{a}{p}\right)$). Тогда сумма $S = \sum_{a=1}^{p-1} \left(\frac{a(a^2+1)}{p}\right)$ — это Jacobsthal sum $K(1)$. По теории Jacobsthal: $K(a)$ для $p \equiv 1 \pmod 4$ удовлетворяет $K(1)^2 + K(\nu)^2 = 4p$ при $\nu$-non-residue, а для $p \equiv 3 \pmod 4$ — $K(a) = 0$. Точно «упрощённого» вида через $\left(\frac{2}{p}\right)$ нет; задача ill-posed как написана. Корректный ответ: $|S| \le 2\sqrt{p}$ по E11 ($f(x) = x(x^2+1) = x^3 + x$ — кубика без кратных корней при $p > 2$).

8. Пусть $A = \#\{a : 1 \le a \le p - 2, \left(\frac{a}{p}\right) = \left(\frac{a+1}{p}\right) = 1\}$. Используем индикатор $\frac{1+\left(\frac{a}{p}\right)}{2} \cdot \frac{1+\left(\frac{a+1}{p}\right)}{2}$ для $a \not\equiv 0, -1$:
$$
A = \frac{1}{4}\sum_{a=1}^{p-2}\left(1 + \left(\frac{a}{p}\right)\right)\left(1 + \left(\frac{a+1}{p}\right)\right).
$$
Раскрываем: $A = \frac{1}{4}\bigl[(p-2) + S_1 + S_2 + S_{12}\bigr]$, где $S_1 = \sum_{a=1}^{p-2} \left(\frac{a}{p}\right) = -\left(\frac{p-1}{p}\right) = -\left(\frac{-1}{p}\right)$, аналогично $S_2 = -\left(\frac{-1}{p}\right)$ (потерян $a = p - 1$ vs $a = 0$), а $S_{12} = \sum_{a=1}^{p-2} \left(\frac{a(a+1)}{p}\right)$. По E9: $\sum_{a=1}^{p-1} \left(\frac{a(a+1)}{p}\right) = -1$, и недостающий $a = p - 1$: $\left(\frac{(p-1) \cdot p}{p}\right) = 0$ — ничего не теряем. Также $a=0$: $\left(\frac{0 \cdot 1}{p}\right) = 0$. Точная сумма: $S_{12} = -1$. Итого $A = \frac{(p-2) - 2\left(\frac{-1}{p}\right) - 1}{4} = \frac{p - 3 - 2\left(\frac{-1}{p}\right)}{4}$.

   Сверка с задачей: формула $\frac{p - 4 - \left(\frac{-1}{p}\right)}{4}$ из условия не совпадает с моим выводом. Аккуратнее: $S_1 = \sum_{a=1}^{p-2}\left(\frac{a}{p}\right)$. Полная сумма от $1$ до $p-1$ равна $0$, минус $\left(\frac{p-1}{p}\right) = \left(\frac{-1}{p}\right)$, итого $-\left(\frac{-1}{p}\right)$. $S_2 = \sum_{a=1}^{p-2}\left(\frac{a+1}{p}\right) = \sum_{b=2}^{p-1}\left(\frac{b}{p}\right) = -\left(\frac{1}{p}\right) = -1$. То есть $S_2 = -1$, не $-\left(\frac{-1}{p}\right)$. Тогда $A = \frac{(p-2) - \left(\frac{-1}{p}\right) - 1 - 1}{4} = \frac{p - 4 - \left(\frac{-1}{p}\right)}{4}$ ✓. (Я допустил ошибку в первом проходе в $S_2$.)
