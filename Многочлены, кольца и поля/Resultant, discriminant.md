---
topic: Многочлены, кольца и поля
subtopic: "Resultant, discriminant"
sources:
  - "Prasolov — Polynomials (Springer 2010), §1.3 The resultant and the discriminant"
  - "Svante Janson — Resultant and Discriminant of Polynomials (lecture notes)"
  - "Henry Woody — Polynomial Resultants (UPS senior thesis, 2016)"
  - "Pierre-Loïc Méliot — The resultant of two polynomials (Paris-Saclay notes)"
  - "Tom M. Apostol — Resultants of Cyclotomic Polynomials, Proc. AMS 24 (1970)"
  - "R. G. Swan — Factorization of polynomials over finite fields, Pacific J. Math. 12 (1962)"
  - "Cox, Little, O'Shea — Ideals, Varieties, and Algorithms (гл. 3, elimination)"
  - "Andreescu, Andrica — Putnam and Beyond (раздел Polynomials)"
  - "Engel — Problem-Solving Strategies (гл. Polynomials)"
  - "Wikipedia — Resultant / Discriminant / Cyclotomic polynomial / Mason–Stothers theorem"
  - "IMC Compendium"
  - "Putnam Compendium"
problems_referenced:
  - IMC-2017-5
  - IMC-2018-9
last_updated: 2026-04-27
---

# Resultant, discriminant

## Scope
Resultant двух многочленов как критерий общего корня и его представления (Sylvester matrix, $\prod(\alpha_i-\beta_j)$, Bezout-форма как элемент идеала $(f,g)$); discriminant как $\operatorname{Res}(f,f')$ и его поведение при сдвиге, произведении, специализации; явные формулы для трёхчленов $x^n+ax+b$, $\Phi_n$, $\operatorname{Res}(\Phi_m,\Phi_n)$ (Apostol); сигнатура $\Delta\in\mathbb{R}$ и количество вещественных корней; Stickelberger–Swan для $\mathbb{F}_p[x]$. Эти инструменты дают олимпиадные решения там, где «корни сложные, симметрии нет», но через коэффициенты получается чистый ответ. Наиболее частая роль на IMC — резюмировать аргумент «общий корень $\Rightarrow$ полиномиальное соотношение между параметрами».

## Записи — Core

### E1. Resultant (результант) через Sylvester matrix

Формулировка. Пусть $f(x)=a_n x^n+\dots+a_0$, $g(x)=b_m x^m+\dots+b_0$ над коммутативным кольцом $R$, $a_n,b_m\ne 0$. Sylvester matrix $\mathrm{Syl}(f,g)\in R^{(n+m)\times(n+m)}$:
$$
\mathrm{Syl}(f,g)=\begin{pmatrix}
a_n & a_{n-1} & \cdots & a_0 & & \\
& a_n & a_{n-1} & \cdots & a_0 & \\
& & \ddots & & & \ddots \\
b_m & b_{m-1} & \cdots & b_0 & & \\
& b_m & b_{m-1} & \cdots & b_0 & \\
& & \ddots & & & \ddots
\end{pmatrix}
$$
($m$ строк коэффициентов $f$, $n$ строк коэффициентов $g$). Тогда $\operatorname{Res}(f,g):=\det\mathrm{Syl}(f,g)\in R$. Над любым integral domain
$$\operatorname{Res}(f,g)=0 \iff f,g \text{ имеют общий делитель степени }\ge 1\text{ в }\overline{K}[x].$$

Условия применимости. $a_n,b_m\ne 0$ обязательно; иначе нужно специальное соглашение или работа в $\overline{K}$. Над $\mathbb{Z}$ результант — целое число.

Идея доказательства. Существование общего делителя $\iff$ существование $u,v$ с $uf+vg=0$, $\deg u<m$, $\deg v<n$ — это в точности нетривиальное ядро транспонированной $\mathrm{Syl}$.

Используется в. Базис всех нижних записей. [IMC-2017-5: общие корни $f$ и $z^n-1$ — задача формулируется как $\operatorname{Res}(f,z^n-1)=0$, но решается тоньше через структуру коэффициентов].

---

### E2. Resultant через корни (product-of-differences формула)

Формулировка. Если $f(x)=a_n\prod_{i=1}^n (x-\alpha_i)$, $g(x)=b_m\prod_{j=1}^m (x-\beta_j)$ над $\overline{K}$, то
$$
\operatorname{Res}(f,g)=a_n^m b_m^n \prod_{i,j}(\alpha_i-\beta_j)=a_n^m \prod_i g(\alpha_i)=(-1)^{nm} b_m^n \prod_j f(\beta_j).
$$
Следствия:
- мультипликативность $\operatorname{Res}(fg,h)=\operatorname{Res}(f,h)\operatorname{Res}(g,h)$;
- симметрия $\operatorname{Res}(g,f)=(-1)^{nm}\operatorname{Res}(f,g)$;
- инвариантность относительно сдвига: $\operatorname{Res}(f(x+c),g(x+c))=\operatorname{Res}(f,g)$;
- $\operatorname{Res}(f,x-a)=f(a)$ — на этом строится оценка $f(\alpha)$ через коэффициенты.

Условия применимости. Любое поле; формула «через коэффициенты» работает в любом кольце через лифт $R\hookrightarrow R[a_n^{-1},b_m^{-1}]$ или через коэффициентную природу $\det\mathrm{Syl}$.

Идея доказательства. Обе стороны — multilinear, antisymmetric, той же степени по коэффициентам $f$ и $g$ — это однозначно фиксирует формулу с точностью до константы; она проверяется на $f=x-\alpha$.

Варианты и обобщения. $\operatorname{Res}(f,g_1 g_2)=\operatorname{Res}(f,g_1)\operatorname{Res}(f,g_2)$ — главный workhorse. $\operatorname{Res}$ для reverse: если $\hat f(x)=x^n f(1/x)$, $\hat g(x)=x^m g(1/x)$, то $\operatorname{Res}(\hat f,\hat g)=(-1)^{nm}\operatorname{Res}(f,g)$ (с поправкой на старшие коэффициенты, см. Janson).

Используется в. Стандартный приём для построения многочлена с «комбинированными» корнями $\alpha_i+\beta_j$ (через $\operatorname{Res}_y(f(y),g(x-y))$) или $\alpha_i\beta_j$ (через $\operatorname{Res}_y(y^m f(x/y),g(y))$); регулярная Putnam-конструкция. Все формулы из E10–E13 — частные случаи product-of-differences.

---

### E3. Discriminant (дискриминант) и связь $\operatorname{Res}(f,f')$

Формулировка. Для $f=a_n\prod(x-\alpha_i)$ степени $n$:
$$
\Delta(f)=a_n^{2n-2}\prod_{i<j}(\alpha_i-\alpha_j)^2=\frac{(-1)^{n(n-1)/2}}{a_n}\operatorname{Res}(f,f').
$$
Свойства:
- $\Delta(f)=0 \iff f$ имеет кратный корень;
- инвариантность относительно сдвига: $\Delta(f(x+c))=\Delta(f)$;
- скейлинг $\Delta(c f)=c^{2n-2}\Delta(f)$;
- произведение: $\Delta(fg)=\Delta(f)\Delta(g)\operatorname{Res}(f,g)^2$.

Условия применимости. Любое поле, $\operatorname{char}=0$ или $\operatorname{char}\nmid n a_n$ (иначе $\deg f'<n-1$ и нужна осторожность; см. E14).

Идея доказательства. $f'(\alpha_i)=a_n\prod_{j\ne i}(\alpha_i-\alpha_j)$, подставив в product-of-differences, получаем $\operatorname{Res}(f,f')=a_n^{n-1}\prod f'(\alpha_i)=a_n^{2n-1}\prod_{i\ne j}(\alpha_i-\alpha_j)=(-1)^{n(n-1)/2}a_n\Delta(f)$.

Варианты и обобщения. Discriminant $\in \mathbb{Z}$ для $f\in\mathbb{Z}[x]$ — это сильное целочисленное ограничение, которое часто и используется на олимпиадах.

Используется в. Базовая запись — служит мостиком между «корни» и «коэффициенты». Многочисленные Putnam-задачи на кубический трёхчлен $x^3+px+q$ (типа «при каких $p,q$ ровно один real root») решаются через $\Delta=-4p^3-27q^2$.

---

### E4. Bezout-представление результанта (resultant как элемент идеала $(f,g)$)

Формулировка. Существуют $u(x),v(x)\in R[x]$ с $\deg u<m=\deg g$, $\deg v<n=\deg f$, такие что
$$
\operatorname{Res}(f,g)=u(x) f(x)+v(x) g(x).
$$
Следствие: $\operatorname{Res}(f,g)\in (f,g)\cap R$. Если $f,g\in\mathbb{Z}[x]$ и $f(\xi)=g(\xi)=0$ для алгебраического $\xi$, то $\operatorname{Res}(f,g)=0$, но если $\xi\in\mathbb{Z}$ только модуло $p$ — то $p\mid\operatorname{Res}(f,g)$.

Условия применимости. Любое коммутативное кольцо. Особенно полезно над $\mathbb{Z}$: даёт «многочленный эквивалент» обычного $\gcd$.

Идея доказательства. Cofactor-разложение $\det\mathrm{Syl}(f,g)$: умножение $\mathrm{Syl}$ на вектор $(x^{n+m-1},\dots,x,1)^T$ слева даёт многочлены $x^{m-1}f, x^{m-2}f, \dots, f, x^{n-1}g, \dots, g$, поэтому $\det\mathrm{Syl}$ — линейная комбинация $f,g$ с многочленными коэффициентами.

Варианты и обобщения. Аналог leftover: если $h\mid f$, $h\mid g$, то $h\mid\operatorname{Res}(f,g)$ — но т.к. $\operatorname{Res}\in R$, это даёт $h$ — константу или $0$. Этот трюк, в частности, заменяет Гёделевский «общий корень $\Rightarrow$ резюмированное полиномиальное тождество» в задачах с integer constraints.

Используется в. Задачи вида «$f,g\in\mathbb{Z}[x]$ имеют общим алгебраический корень $\xi$ — что можно сказать о коэффициентах» решаются через $\operatorname{Res}(f,m_\xi)$, где $m_\xi$ — минимальный многочлен. [IMC-2018-9: $P\mid Q^2+1$, $Q\mid P^2+1$ — через $\operatorname{Res}_x(P,Q^2+1)\cdot\operatorname{Res}_x(Q,P^2+1)$ и оценку степеней].

---

## Записи — Standard

### E5. Discriminant трёхчлена $x^n+ax+b$

Формулировка. Для $f(x)=x^n+ax+b$, $n\ge 2$, в $\operatorname{char}=0$:
$$
\Delta(f)=(-1)^{n(n-1)/2}\bigl((1-n)^{n-1} a^n + n^n b^{n-1}\bigr).
$$
Проверки: $n=2$: $\Delta=a^2-4b$; $n=3$, $f=x^3+ax+b$: $\Delta=-(4a^3+27b^2)$.

Условия применимости. Любое поле char $\nmid n$. При $\operatorname{char}=p\mid n$ формула остаётся как identity в $\mathbb{Z}[a,b]$, но содержательно $\Delta\equiv 0$.

Идея доказательства. $\operatorname{Res}(x^n+ax+b, nx^{n-1}+a)$ через product-of-differences: корни $f'$ — это $(-a/n)^{1/(n-1)}\cdot\zeta$ по корням $(n-1)$-й степени из единицы, после симметризации остаётся $a^n$ и $b^{n-1}$.

Варианты и обобщения. Для $f=x^n+a x^k+b$ есть аналогичная компактная формула (см. Swan 1962); классически даёт критерий неприводимости $x^n-x-1$ (Selmer): дискриминант не квадрат для всех $n\ge 2$ (ничего не доказывает напрямую, но индуцирует.)

Используется в. [Putnam-1971-A6: дискриминант $x^3+ax+b$], стандартный кирпич для трёхчленов в Putnam shortlists. Контрольный тест неприводимости через Stickelberger–Swan (E13).

---

### E6. Sign of $\Delta\in\mathbb{R}$ и количество вещественных корней

Формулировка. Пусть $f\in\mathbb{R}[x]$, $\deg f=n$, без кратных корней. Если $s$ — число пар комплексно-сопряжённых корней (так что вещественных корней $r=n-2s$), то
$$
\operatorname{sign}(\Delta(f))=(-1)^s.
$$
В частности: $\Delta>0 \iff s$ чётно $\iff$ число невещественных корней делится на $4$. Для $n=2$: $\Delta>0\iff$ два вещественных корня. Для $n=3$: $\Delta>0\iff$ три вещественных корня; $\Delta<0\iff$ один.

Условия применимости. $f\in\mathbb{R}[x]$, $\Delta\ne 0$. Аналог в $p$-adic / $\mathbb{F}_p$ — Stickelberger–Swan (E13).

Идея доказательства. Каждая пара $(\alpha,\bar\alpha)$ даёт $(\alpha-\bar\alpha)^2=-4(\operatorname{Im}\alpha)^2<0$; пары real–real и real–complex/complex–real дают парные множители комплексно-сопряжённых, т.е. квадрат модуля — положительное.

Используется в. Стандартный приём для real-root counting там, где Sturm sequence громоздок; кубики и quartics в Putnam регулярны (типа «при каких $a$ многочлен $x^4+ax^2+1$ имеет 4 real roots»).

---

### E7. Multiplicativity и поведение под замены переменных

Формулировка. Помимо $\operatorname{Res}(fg,h)=\operatorname{Res}(f,h)\operatorname{Res}(g,h)$, полезно:
- $\operatorname{Res}(f(x),g(x))=\operatorname{Res}(f(x+c),g(x+c))$ — translation;
- $\operatorname{Res}(f(\lambda x),g(\lambda x))=\lambda^{nm}\operatorname{Res}(f,g)$ если $f,g$ моничные (общий случай — с поправкой на старшие коэффициенты);
- если $h(x)=p(q(x))$ с $\deg q=k$, то $\operatorname{Res}(f,h)=\operatorname{Res}(f,p\circ q)=\prod_\alpha p(q(\alpha))=\operatorname{Res}_y(f(\text{?}),...)$ — composition formula: $\operatorname{Res}_x(f(x),p(q(x)))=a_n^{\deg p}\prod_\alpha p(q(\alpha))$, что часто переписывается через $\operatorname{Res}(p, f \circ q^{-1})$ символически.

Условия применимости. Все формулы — над любым полем; над кольцом нужны обратимости старших коэффициентов в нужных местах.

Идея доказательства. Все три — прямой подсчёт через product-of-differences.

Варианты и обобщения. Формула для $\operatorname{Res}(f(x),g(y)-x)$ как многочлена от $y$ — стандартный путь для построения многочлена с корнями $\alpha_i+\beta_j$ (через $\operatorname{Res}_x(f(x),g(y-x))$), $\alpha_i\beta_j$ (через $\operatorname{Res}_x(f(x), x^m g(y/x))$), $\alpha_i^k$ (через $\operatorname{Res}_x(f(x), y-x^k)$). Это конструктивный аналог Vieta для составных корней.

Используется в. Построить многочлен с заданными «комбинированными» корнями — типичный прелим к задачам про Galois-симметрию (Putnam-archive несколько раз).

---

### E8. Resultant $\operatorname{Res}(x^n-a^n,x^m-b^m)$ и $x^n-1$, $x^m-1$

Формулировка.
$$
\operatorname{Res}(x^n-1,x^m-1)=\begin{cases}0,& d=\gcd(m,n)>1,\\ 0,& d=1, m,n>1 \text{ — нет, see ниже}\end{cases}
$$
Точнее: $x^n-1$ и $x^m-1$ имеют общим делителем $x^d-1$, $d=\gcd(m,n)$, поэтому $\operatorname{Res}=0\iff d>1\iff (m,n)\ne(1,k)$. Для $a,b\in\mathbb{C}^\times$:
$$
\operatorname{Res}(x^n-a^n,x^m-b^m)=\prod_{i,j}(a\zeta_n^i - b\zeta_m^j),\quad \zeta_k=e^{2\pi i/k}.
$$

Условия применимости. Стандартный шаблон для trig-сумм и multiplicative identities.

Идея доказательства. Корни $x^n-a^n$ — $\{a\zeta_n^i\}$, корни $x^m-b^m$ — $\{b\zeta_m^j\}$; product-of-differences даёт ответ.

Варианты и обобщения. Для $\gcd(m,n)=1$ известны компактные представления через циклотомические тождества. Дал тождества типа $\prod_{k=1}^{n-1}(1-\zeta_n^k)=n$ — частный случай $\operatorname{Res}(x^n-1, x-1)/(x-1)|_{x=1}=n$.

Используется в. Задачи на циклотомические тождества и trig-произведения; типичный олимпиадный шаблон.

---

### E9. Discriminant of $\Phi_n$ (циклотомика)

Формулировка. Для cyclotomic polynomial $\Phi_n$:
$$
\operatorname{disc}(\Phi_n)=\frac{(-1)^{\varphi(n)/2}\, n^{\varphi(n)}}{\prod_{p\mid n} p^{\varphi(n)/(p-1)}}.
$$
В частности: для простого $p$, $\operatorname{disc}(\Phi_p)=(-1)^{(p-1)/2}p^{p-2}$. Для $p^k$ — формула $(-1)^{\varphi(p^k)/2}p^{p^{k-1}((p-1)k-1)}$.

Условия применимости. $n\ge 3$. Знак — $(-1)^{\varphi(n)/2}$.

Идея доказательства. $\operatorname{disc}(\Phi_n)\cdot\prod_{d<n,\,d\mid n}\operatorname{disc}(\Phi_d)\cdot\prod_{d_1\ne d_2}\operatorname{Res}(\Phi_{d_1},\Phi_{d_2})=\operatorname{disc}(x^n-1)=(-1)^{(n-1)n/2}n^n$ (с поправкой на $x=1$); индукцией по делителям + Apostol (E11).

Варианты и обобщения. Discriminant of $\mathbb{Q}(\zeta_n)$ совпадает (с точностью до $\pm$) с $\operatorname{disc}(\Phi_n)/(\text{conductor stuff})$; даёт integer ring $\mathbb{Z}[\zeta_n]$ для $n=p^k$.

Используется в. Аргументы про $p$-адические оценки циклотомических значений; Lawrence Sun handout по олимпиадной teorii чисел использует $v_p(\Phi_n(a))$.

---

### E10. Elimination через $\operatorname{Res}_y$: проекция системы на одну переменную

Формулировка. Пусть $P(x,y),Q(x,y)\in K[x,y]$ — многочлены; $R(x):=\operatorname{Res}_y(P,Q)\in K[x]$. Тогда $R(\alpha)=0\iff$ существует $\beta\in\overline{K}$ с $P(\alpha,\beta)=Q(\alpha,\beta)=0$ ИЛИ старшие коэффициенты $P,Q$ по $y$ оба обнуляются при $x=\alpha$.

Условия применимости. Нужно либо предполагать, что хотя бы один старший по $y$ коэффициент не зануляется, либо отдельно обработать degenerate locus.

Идея доказательства. Прямое следствие E1 для $P,Q\in (K[x])[y]$.

Варианты и обобщения. Для систем из $k+1$ уравнений в $k$ переменных — sparse/multivariate resultant (Macaulay), но это уже за рамками IMC. На олимпиаде elimination через $\operatorname{Res}$ применим в задачах вида «найти все рациональные точки кривой $C_1\cap C_2$».

Используется в. [IMC-2018-9: $\operatorname{Res}_x(P(x), Q(x)^2+1)\in\mathbb{Z}$ — целочисленное ограничение, дающее ограниченный набор пар $(P,Q)$].

---

## Записи — Exotic

### E11. Apostol's resultant formula для $\Phi_m,\Phi_n$

Формулировка. Для $1\le m<n$:
$$
\operatorname{Res}(\Phi_m,\Phi_n)=\begin{cases}
p^{\varphi(m)},& n/m=p^k, p\text{ — простое},k\ge 1,\\
1,& \text{иначе (т.е. }n/m\text{ имеет }\ge 2\text{ простых делителей или дроб.)}.
\end{cases}
$$

Условия применимости. $m\ne n$. Симметрию $\operatorname{Res}(\Phi_n,\Phi_m)=\pm\operatorname{Res}(\Phi_m,\Phi_n)$ используем при необходимости.

Идея доказательства. $\operatorname{Res}(\Phi_m,\Phi_n)=\prod_{\zeta:\,\Phi_n(\zeta)=0}\Phi_m(\zeta)$; для primitive $n$-го корня $\zeta$ значение $\Phi_m(\zeta)$ — известный $p$-power по теории циклотомических полей (Apostol 1970, Лемма 1).

Используется в. Доказательства, что $\Phi_n(a)$ имеют специфические простые делители (Lawrence Sun handout), Bang's theorem (Zsygmondy для $a^n-b^n$). Чисто на IMC встречается косвенно — через Zsygmondy.

---

### E12. Discriminant произведения $\Delta(fg)$ и подъём через $\operatorname{Res}$

Формулировка.
$$
\Delta(fg)=\Delta(f)\,\Delta(g)\,\operatorname{Res}(f,g)^2.
$$
В частности, если $f,g$ имеют общий корень, $\Delta(fg)=0$ автоматически (через $\operatorname{Res}=0$).

Условия применимости. Любое поле char $\nmid$ степени.

Идея доказательства. $\Delta=\prod_{i<j}(\gamma_i-\gamma_j)^2$ для всех корней $\gamma$ объединения; разделить пары на «оба из $f$», «оба из $g$», «одна из $f$ одна из $g$» — последняя группа даёт $\operatorname{Res}(f,g)^2/\text{lc}^2$.

Варианты и обобщения. Аналог для $\Delta(f^k)=0$ при $k\ge 2$, потому что есть кратные корни.

Используется в. Конструктивные доказательства неприводимости через сравнение дискриминантов: если разложение $f=gh$ имеет $\Delta(f)$ не делящееся на $\Delta(g)\Delta(h)$ корректно — противоречие.

---

### E13. Stickelberger–Swan: дискриминант и чётность числа неприводимых множителей в $\mathbb{F}_p[x]$

Формулировка. Пусть $f\in\mathbb{F}_p[x]$ — squarefree моничный, $\deg f=n$, и $r$ — число его неприводимых множителей над $\mathbb{F}_p$.
- При $p$ нечётном: $r\equiv n\pmod 2 \iff \Delta(f)\in(\mathbb{F}_p^\times)^2$.
- При $p=2$: пусть $F\in\mathbb{Z}[x]$ — лифт $f$, $\Delta(F)\in\mathbb{Z}$. Тогда $\Delta(F)\equiv 1\pmod 8 \iff r\equiv n\pmod 2$, иначе $\Delta(F)\equiv 5\pmod 8$.

Условия применимости. Squarefree (иначе $\Delta=0$); характеристика поля сравнима с условиями.

Идея доказательства. Для нечётного $p$: action of $\operatorname{Frob}_p$ на корнях имеет signature $(-1)^{n-r}$, что совпадает с символом Лежандра $\left(\frac{\Delta}{p}\right)$ через Vandermonde. Случай $p=2$ требует $2$-адического подъёма (Swan 1962).

Варианты и обобщения. Swan даёт явную формулу для дискриминанта трёхчленов $x^n+x^k+1\in\mathbb{F}_2[x]$ — приложения в кодах и криптографии.

Используется в. Тест неприводимости трёхчленов и пентаномов над $\mathbb{F}_2$. На IMC встречается редко — но идея «проверить $\Delta$ на квадратичность» общеолимпиадная.

---

## Self-test

1. Найди все целые $(p,q)$ с $|q|\le 2$, при которых $x^3+px+q$ имеет ровно один вещественный корень.

2. Пусть $f(x)=x^3+ax+b$ и $g(x)=x^3+cx+d$ имеют общий комплексный корень, причём $(a,b)\ne(c,d)$. Покажи, что общий корень $\alpha$ рационален и удовлетворяет $\alpha=(d-b)/(a-c)$ (при $a\ne c$).

3. Пусть $f\in\mathbb{Z}[x]$ моничный, степени $n\ge 2$. Докажи, что $\Delta(f)=0$ тогда и только тогда, когда существует $\alpha\in\overline{\mathbb{Q}}$ с $f(\alpha)=f'(\alpha)=0$.

4. Пусть $a,b\in\mathbb{Z}$, $a\ne 0$, $n\ge 2$. Установи необходимое и достаточное условие на $a,b$ для того, чтобы $f(x)=x^n+ax+b$ имел кратный корень.

5. Покажи, что для любого $n\ge 3$ и $\zeta=e^{2\pi i/n}$
$$
\prod_{k=1}^{n-1}\bigl(2-2\cos\tfrac{2\pi k}{n}\bigr)=n^2.
$$

6. Многочлены $f(x)=x^2+ax+b$ и $g(x)=x^2+cx+d$ имеют общий комплексный корень. Найди компактное полиномиальное соотношение между $a,b,c,d$.

7. Пусть $f\in\mathbb{Z}[x]$ моничный неприводимый степени $n\ge 2$. Докажи, что $\Delta(f)\ne 0$. (Этот факт делает discriminant корректно определённым инвариантом числового поля $\mathbb{Q}(\alpha)$.)

## Решения

1. $\Delta=-4p^3-27q^2$. Один real $\iff \Delta<0\iff 4p^3+27q^2>0$, т.е. $p^3>-27q^2/4$.
- $q=0$: $p^3>0\iff p\ge 1$.
- $q=\pm 1$: $p^3>-27/4$, т.е. $p\ge -1$.
- $q=\pm 2$: $p^3>-27$, т.е. $p\ge -2$ (при $p=-3, q=\pm 2$: $\Delta=108-108=0$ — кратный корень, два различных вещественных).

2. Из $f(\alpha)-g(\alpha)=0$: $(a-c)\alpha+(b-d)=0$, при $a\ne c$ получаем $\alpha=(d-b)/(a-c)\in\mathbb{Q}$. Если $a=c$, то $b=d$ (общий корень даёт $b=d$), но это противоречит $(a,b)\ne(c,d)$.

3. $\Leftarrow$: $f(\alpha)=f'(\alpha)=0\Rightarrow\operatorname{Res}(f,f')=0\Rightarrow\Delta(f)=(-1)^{n(n-1)/2}\operatorname{Res}(f,f')=0$.
$\Rightarrow$: $\Delta=a_n^{2n-2}\prod_{i<j}(\alpha_i-\alpha_j)^2=0\Rightarrow\exists i\ne j: \alpha_i=\alpha_j$, тогда $\alpha=\alpha_i$ — кратный корень $f$, и $f'(\alpha)=0$.

4. По E5: $\Delta(f)=(-1)^{n(n-1)/2}\bigl((1-n)^{n-1}a^n+n^n b^{n-1}\bigr)$. Кратный корень $\iff\Delta(f)=0\iff(1-n)^{n-1}a^n+n^n b^{n-1}=0\iff n^n b^{n-1}=(n-1)^{n-1}(-1)^n a^n$. Для $n=2$: $b=a^2/4$ (т.е. $a^2=4b$). Для $n=3$: $27 b^2=-4 a^3$ (требует $a\le 0$), классическое условие $4a^3+27b^2=0$.

5. $\prod_{k=1}^{n-1}(1-\zeta^k)=n$: формально $x^n-1=(x-1)\prod_{k=1}^{n-1}(x-\zeta^k)$, делим на $(x-1)$ и подставляем $x=1$ через L'Hopital / производную, получаем $n=\prod(1-\zeta^k)$. Тогда $|1-\zeta^k|^2=(1-\zeta^k)(1-\bar\zeta^k)=2-2\cos(2\pi k/n)$. Перемножая: $\prod_{k=1}^{n-1}(2-2\cos\tfrac{2\pi k}{n})=\bigl|\prod_{k=1}^{n-1}(1-\zeta^k)\bigr|^2=n^2$.

6. $\operatorname{Res}(f,g)=0$ при общем корне. По формуле Sylvester для двух квадратичных:
$$
\operatorname{Res}(f,g)=\det\begin{pmatrix}1 & a & b & 0\\ 0 & 1 & a & b\\ 1 & c & d & 0\\ 0 & 1 & c & d\end{pmatrix}=(b-d)^2+(a-c)(ad-bc)=0.
$$
Эквивалентно: $(b-d)^2=(a-c)(bc-ad)$. Sanity-check: $f=x^2-1, g=x^2-3x+2$ имеют общий корень $1$, $(a,b,c,d)=(0,-1,-3,2)$, $(b-d)^2=9$, $(a-c)(bc-ad)=3\cdot 3=9$. ✓

7. От противного: $f$ неприводим и $\Delta(f)=0$, значит $\gcd(f,f')\ne 1$ в $\mathbb{Q}[x]$. Но $\deg f'<\deg f$ и $f$ неприводим, поэтому $\gcd(f,f')\in\{1,f\}$. Если $\gcd=f$, то $f\mid f'$, что невозможно по степеням (кроме $f'=0$ — невозможно в char $0$ для непостоянного $f$). Значит $\gcd=1$, $\operatorname{Res}(f,f')\ne 0$, $\Delta(f)\ne 0$.
