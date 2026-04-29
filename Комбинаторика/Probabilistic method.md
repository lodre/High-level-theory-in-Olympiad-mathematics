---
topic: Комбинаторика
subtopic: Probabilistic method
sources:
  - "Alon, Spencer — The Probabilistic Method, 4th ed. (Wiley, 2016)"
  - "Matoušek, Vondrák — The Probabilistic Method, lecture notes (Charles Univ. / KAM)"
  - "Yufei Zhao — Probabilistic Methods in Combinatorics (MIT 18.226 / 18.218 lecture notes, 2019/2022)"
  - "Erdős — Some remarks on the theory of graphs (Bull. AMS, 1947) — random Ramsey lower bound"
  - "Szele — Combinatorial investigations concerning directed complete graphs (1943) — Hamiltonian paths in tournaments"
  - "Erdős, Lovász — Problems and results on 3-chromatic hypergraphs (1975) — Lovász Local Lemma"
  - "Spencer — Six standard deviations suffice (Trans. AMS, 1985)"
  - "Engel — Problem-Solving Strategies, ch. 'The Probabilistic Method'"
  - "Evan Chen — Expected Uses of Probability (handout, 2014)"
  - "IMC archive — imc-math.org.uk"
  - "Putnam Archive — kskedlaya.org/putnam-archive"
problems_referenced:
  - IMC-2011-4
  - IMC-2013-DAY2-3
  - IMC-2017-4
  - IMC-2019-10
  - IMC-2022-8
  - IMC-2025-3
  - Putnam-2002-B1
  - Putnam-2005-A6
  - Putnam-2006-A4
last_updated: 2026-04-29
---

# Probabilistic method

## Scope
Доказательство существования (или несуществования) комбинаторного объекта через анализ случайной конструкции: распределение строится так, что искомое свойство выполнено с положительной вероятностью либо математическое ожидание целевой статистики достигает требуемой границы. Покрывает: бесконструктивные lower bounds (Ramsey, tournament, sum-free), оценки сверху на discrepancy, существование редких/плотных подструктур, проверку доминирования через монотонность вероятности по параметру, redукцию "экстремум $\le \mathbb{E}$" / "экстремум $\ge \mathbb{E}$". Не покрывает: задачи на распределения сами по себе (PGF, концентрация в строгом смысле — это уже теория вероятностей).

## Записи - Core

### E1. Linearity of expectation (линейность ожидания)

Формулировка. Для произвольных интегрируемых $X_1,\dots,X_n$ (зависимы или независимы):
$$\mathbb{E}\Big[\sum_i X_i\Big] = \sum_i \mathbb{E}[X_i].$$
Главный приём: $X = \sum_i \mathbb{1}_{A_i}$, тогда $\mathbb{E}[X] = \sum_i P(A_i)$ — даёт точное ожидание числа выполненных свойств.

Условия применимости. Любая зависимость допустима — единственное требование $\mathbb{E}|X_i|<\infty$. Существование исходного выбора с $X\ge\mathbb{E}[X]$ и $X\le\mathbb{E}[X]$ гарантировано (минимум/максимум $\le$/$\ge$ среднего).

Идея доказательства. Тождество $\mathbb{E}\sum=\sum\mathbb{E}$ — линейность интеграла Лебега.

Варианты и обобщения. Обусловленные ожидания: $\mathbb{E}[X\mid\mathcal{F}]$ — даёт probabilistic doubling (см. E10). Tail-sum: $\mathbb{E}[X]=\sum_{k\ge 1}P(X\ge k)$ для $\mathbb{N}$-значных $X$.

Используется в. [Putnam-2006-A4 (число локальных максимумов в случайной перестановке = $(n+1)/3$), IMC-2022-8 (E[вершин пересечения convex hulls] через индикаторы), Szele 1943 для турниров (см. E13)].

---

### E2. First moment method / averaging (метод первого момента)

Формулировка. Пусть $X\ge 0$ — целочисленная случайная величина.
- Если $\mathbb{E}[X]<1$, то $P(X=0)>0$ — существует исход без "плохих" событий.
- Если $\mathbb{E}[X]>0$, то $P(X\ge 1)>0$ — существует исход с хотя бы одним "хорошим".
- В произвольном вероятностном пространстве $\exists\omega:X(\omega)\le\mathbb{E}[X]$ и $\exists\omega:X(\omega)\ge\mathbb{E}[X]$.

Условия применимости. $X$ не обязана быть индикатором; для дискретного "$X\in\mathbb{Z}_{\ge 0}$" работает оценка $P(X\ge 1)\le\mathbb{E}[X]$ (Markov).

Идея доказательства. Markov inequality $P(X\ge a)\le\mathbb{E}[X]/a$ при $a>0$.

Варианты и обобщения. Версия Erdős для Ramsey: если $\binom{n}{k}\cdot 2^{1-\binom{k}{2}}<1$, то $R(k,k)>n$ — берём случайную раскраску $K_n$ в 2 цвета, $X$ = число монохроматических $K_k$ (E11). Sum-free множество (E12).

Используется в. [IMC-2013-DAY2-3 (existence of $\pm 1$ vector with $(u\cdot v_i)^2\le 1/d$), Erdős 1947 (lower bound для $R(k,k)\ge 2^{k/2}$), Szele 1943].

---

### E3. Alteration / deletion method (метод изменения / удаления)

Формулировка. Пусть случайная конструкция почти-удовлетворяет требуемому свойству, имея ожидаемое число $\mathbb{E}[Y]$ "дефектов" (плохих локальных нарушений). Удаляя по одному элементу из каждого дефекта, получаем чистую конструкцию размера $\ge\mathbb{E}[X-Y]$, где $X$ — исходный размер.

Условия применимости. Каждый дефект устраняется удалением $O(1)$ элементов; критично — оценить $\mathbb{E}[Y]$ снизу/сверху и оптимизировать параметр (вероятность включения, размер).

Идея доказательства. По линейности $\mathbb{E}[X-Y]=\mathbb{E}[X]-\mathbb{E}[Y]$; берём реализацию с $X-Y\ge\mathbb{E}[X-Y]$.

Варианты и обобщения.
- Ramsey lower bound: вместо $\binom{n}{k}2^{1-\binom{k}{2}}<1$ оптимизируем $n - \binom{n}{k}2^{1-\binom{k}{2}}$ — получается константный выигрыш $\sqrt{2}^k$ (см. Alon–Spencer ch. 3).
- Independent set: для графа с $n$ вершинами и $m$ рёбрами включаем каждую с вероятностью $p$, удаляем по одному из каждого ребра — получаем $\alpha(G)\ge np - mp^2 = \frac{n^2}{4m}$ (при $p=n/(2m)$), это границы Турана-типа.
- Girth + chromatic number (Erdős 1959): удаление коротких циклов в случайном графе.

Используется в. [IMC-2017-4 (random subset $S$ с probability $p$, удаление вершин с не-2 соседями в $S$ — получает $|S|\ge n/2017$ через оптимизацию $p$), independent set в треугольно-свободных графах].

---

### E4. Random subset с параметром $p$ + оптимизация

Формулировка. Каждый элемент $V$ включаем независимо в $S$ с вероятностью $p$. Для индикатора структурного свойства $f:2^V\to\mathbb{R}$ ищем оптимальное $p^*$ из $\frac{d}{dp}\mathbb{E}_p[f(S)]=0$. Часто $\mathbb{E}_p[f(S)]$ — полином от $p$, оптимум — рациональная точка.

Условия применимости. Свойство — мультипликативно по элементам ($P(\text{config}\subseteq S)=p^{|\text{config}|}$). Обычно — задачи о подграфах, покрытиях, доминирующих множествах.

Идея доказательства. По E1 ожидание разбивается в сумму по конфигурациям; оптимизация — стандартное взятие производной.

Варианты и обобщения. Параметр может быть распределение на $V$ (неравномерный), либо одновременно несколько параметров (e.g. random ordering + random subset).

Используется в. [IMC-2017-4 (выбираем $p$ так, что $np\cdot\binom{1000}{2}p^2(1-p)^{998}$ оптимально; $p^*\approx 1/1001$), dominating set bound $\gamma(G)\le n\frac{1+\ln(1+\delta)}{1+\delta}$ (Alon)].

---

### E5. Probabilistic existence через индикатор события + averaging

Формулировка. Чтобы доказать $\exists$ конфигурации со свойством $\mathcal{P}$, рассматриваем равномерное распределение на множестве $\Omega$ всех конфигураций. Если $P_{\Omega}(\mathcal{P})>0$, то $\exists$ конфигурация в $\mathcal{P}$. Эквивалентно — counting argument: $|\mathcal{P}|/|\Omega|>0$, но вероятностная подача даёт линейность.

Условия применимости. $\Omega$ — конечно или интегрируемо. Часто — $\Omega = $ все перестановки, все ориентации, все раскраски, все подмножества.

Идея доказательства. $P>0\Rightarrow$ непустота.

Варианты и обобщения.
- Random permutation argument: для inequalities на симметрических суммах ($\sum a_{\sigma(i)}b_i$ etc.) фиксированная перестановка с $\sum=\mathbb{E}_\sigma[\sum]=\frac{1}{n}\sum a_i\sum b_i$ всегда существует.
- Katona's cyclic permutation proof of Erdős–Ko–Rado: случайная циклическая перестановка $\{1,\dots,n\}\to\text{circle}$, для intersecting family $\mathcal{F}$ из $k$-подмножеств число $A\in\mathcal{F}$ образующих arc $\le k$, отсюда $|\mathcal{F}|\le\binom{n-1}{k-1}$.

Используется в. [Erdős–Ko–Rado theorem (Katona 1972), Putnam-2005-A6 (вероятность acute angle через random angles)].

---

### E6. Inclusion-exclusion via random sampling at parameter $t$

Формулировка. Для семейства множеств $A_1,\dots,A_m\subseteq U$ берём случайное $X\subseteq U$, где каждый $u\in U$ включается независимо с вероятностью $t\in[0,1]$. Тогда $P(A_i\subseteq X) = t^{|A_i|}$, и
$$P\big(\exists i:A_i\subseteq X\big) = \sum_{\emptyset\ne I}(-1)^{|I|-1}\,t^{|\bigcup_{i\in I}A_i|} =: f(t).$$
$f(t)$ — полином от $t$, нондекр на $[0,1]$ (как probability monotone в $t$ — coupling).

Условия применимости. Семейство $A_i$ — конечное; вкл-искл становится точным тождеством полиномов от $t$.

Идея доказательства. Для каждого фикса $X$ — стандартное вкл-искл; усреднение даёт identity полиномов.

Варианты и обобщения. Полученная функция $f(t)$ — полезна как probabilistic generating function-аналог: коэффициенты содержат структурную информацию о $|\bigcup A_i|$.

Используется в. [IMC-2011-4 (монотонность $f(t)$ — ключевой шаг)].

---

### E7. Pigeonhole-by-expectation (среднее $\Rightarrow\exists\ge$ среднее)

Формулировка. Для $X_1,\dots,X_n$ существует $i$ с $X_i\ge\frac{1}{n}\sum X_j$ и существует $i$ с $X_i\le\frac{1}{n}\sum X_j$. В вероятностной форме: при равномерном выборе $i$ имеем $\mathbb{E}[X_i]=\frac{1}{n}\sum X_j$ — отсюда оба экстремума.

Условия применимости. Любая конечная совокупность чисел / случайных величин. Часто — applied к "взвешенному" среднему: $X_i$ с весом $w_i$, $\sum w_i=1$.

Идея доказательства. Тривиальна.

Варианты и обобщения. Weighted version: ${X_i}$ с распределением $\pi$, $\exists i\in\text{supp}\,\pi: X_i\ge\sum\pi_j X_j$. Используется как "выбор по среднему" в дискретной оптимизации.

Используется в. [Max-cut $\ge m/2$ (random vertex partition: $\mathbb{E}[\text{cut}]=m/2\Rightarrow\exists$ cut $\ge m/2$), MAX-3SAT $\ge 7m/8$, многочисленные Putnam задачи].

---

## Записи - Standard

### E8. Random ±1 signs / sign vectors (метод случайных знаков)

Формулировка. Пусть $\varepsilon_1,\dots,\varepsilon_n\in\{\pm 1\}$ i.i.d. с $P=1/2$. Тогда:
- $\mathbb{E}[\varepsilon_i\varepsilon_j]=\delta_{ij}$, в частности $\mathbb{E}\big[(\sum\varepsilon_i v_i)\cdot w\big]^2 = \sum(v_i\cdot w)^2$.
- Для любых $v_1,\dots,v_n\in\mathbb{R}^d$ существуют $\varepsilon_i$ с $|\sum\varepsilon_i v_i|\le\sqrt{\sum|v_i|^2}$ — равенство в среднем.
- Khintchine: $\big(\mathbb{E}|\sum\varepsilon_i a_i|^p\big)^{1/p}\asymp\big(\sum a_i^2\big)^{1/2}$ для всех $p\ge 1$.

Условия применимости. Дискретная симметризация — работает для любых вещественных коэффициентов; для матриц/тензоров — даёт оценку spectral / operator нормы.

Идея доказательства. Раскрытие квадрата $\mathbb{E}|\sum\varepsilon_i v_i|^2$ через ортогональность $\mathbb{E}[\varepsilon_i\varepsilon_j]=\delta_{ij}$.

Варианты и обобщения.
- Gaussian signs: $\varepsilon_i\sim\mathcal{N}(0,1)$ — даёт те же $L^2$-оценки, плюс subgaussian tail.
- Chernoff-Hoeffding: $P(|\sum\varepsilon_i a_i|\ge t)\le 2\exp(-t^2/(2\sum a_i^2))$.
- Sign rank / Komlós conjecture для discrepancy.

Используется в. [IMC-2013-DAY2-3 (existence of $\varepsilon$: $(u\cdot v_i)^2\le 1/d\,\forall i$ для $u=\sum\varepsilon_i e_i/\sqrt{d}$), теорема Spencer "six standard deviations" (E16)].

---

### E9. Second moment method / Chebyshev for existence

Формулировка. Для $X\ge 0$:
$$P(X=0) \le \frac{\text{Var}(X)}{(\mathbb{E}[X])^2},\qquad P\big(|X-\mathbb{E}[X]|\ge a\big)\le\frac{\text{Var}(X)}{a^2}.$$
В частности, если $\text{Var}(X) = o(\mathbb{E}[X]^2)$, то $X>0$ с вероятностью $\to 1$ — отсюда existence.

Условия применимости. Нужна оценка $\text{Var}(X)$ или $\mathbb{E}[X^2]$. Для $X=\sum\mathbb{1}_{A_i}$:
$$\text{Var}(X)=\sum_i P(A_i)(1-P(A_i)) + \sum_{i\ne j}\big(P(A_i\cap A_j)-P(A_i)P(A_j)\big).$$
Сильный приём — почти-независимость пар.

Идея доказательства. Cauchy–Schwarz: $(\mathbb{E}[X])^2 = (\mathbb{E}[X\cdot\mathbb{1}_{X>0}])^2\le\mathbb{E}[X^2]\cdot P(X>0)$, отсюда $P(X>0)\ge(\mathbb{E}[X])^2/\mathbb{E}[X^2]$ (Paley–Zygmund inequality).

Варианты и обобщения. Доказательство threshold-функций для $G(n,p)$: для свойств "монотонных", таких как существование $K_4$, второй момент даёт точку $p^*$, в которой $P\to 1$.

Используется в. [Erdős–Rényi threshold для existence triangles в $G(n,p)$, разных задач "edge-density forces structure"].

---

### E10. Lovász Local Lemma (LLL, симметричная форма)

Формулировка. Пусть $A_1,\dots,A_n$ — события, $P(A_i)\le p$, и каждое $A_i$ взаимно независимо со всеми $A_j$ кроме $\le d$. Если $e p (d+1) \le 1$ ($e$ — основание натурального логарифма), то
$$P\Big(\bigcap_i \overline{A_i}\Big) > 0.$$

Условия применимости. Граф зависимостей $G$ имеет $\Delta(G)\le d$. Условие "взаимная независимость от всех вне соседства" сильнее обычной попарной независимости.

Идея доказательства. По индукции $P(\overline{A_i}\mid \bigcap_{j\in S}\overline{A_j})\ge 1-ep$ для любого $S$, не содержащего $i$ — далее цепочка условных вероятностей.

Варианты и обобщения.
- Asymmetric LLL: $\exists x_i\in(0,1)$ с $P(A_i)\le x_i\prod_{j\sim i}(1-x_j)$.
- Lopsided LLL (Erdős–Spencer): достаточно lopsidependence.
- Constructive (Moser–Tardos 2010): алгоритм поиска "хорошей" реализации за полином времени.

Используется в. [Bounded-degree hypergraph 2-coloring (Property B): $k$-uniform hypergraph с макс. degree $\le 2^{k-3}/e$ имеет proper 2-coloring; proof Erdős-Lovász 1975 через LLL].

---

### E11. Random Ramsey lower bound

Формулировка. Случайная 2-раскраска $K_n$, $X$ = число монохроматических $K_k$. $\mathbb{E}[X]=\binom{n}{k}\cdot 2^{1-\binom{k}{2}}$. Если $\mathbb{E}[X]<1$, существует раскраска без монохромного $K_k$, т.е. $R(k,k)>n$. Оптимизация даёт $R(k,k)>(1+o(1))\frac{k}{e\sqrt{2}}\cdot 2^{k/2}$ (Erdős 1947, alteration).

Условия применимости. Нужна expectation количества "плохих" подструктур $<1$ или применимы методы alteration / LLL для усиления.

Идея доказательства. Каждая фиксированная $K_k\subseteq K_n$ монохроматична с вероятностью $2\cdot 2^{-\binom{k}{2}}$; линейность ожидания.

Варианты и обобщения.
- Off-diagonal: $R(s,t)\le\binom{s+t-2}{s-1}$ верх; вероятностно $R(3,t)\ge\Omega(t^2/\log^2 t)$ (Spencer).
- Hypergraph Ramsey: аналогичные оценки для $r$-uniform.
- Constructive low bounds на $R(k,k)$ — открытая проблема (best $\Omega(2^{k/2})$, никакой полиномиальный gain не известен).

Используется в. [классический пример "first moment + alteration" в учебниках; не в IMC напрямую, но idea применяется в IMC-2017-4 и аналогичных].

---

### E12. Erdős sum-free subset

Формулировка. Любое $A\subset\mathbb{Z}_{>0}$, $|A|=n$, содержит sum-free подмножество $B$ ($x+y\ne z$ для $x,y,z\in B$) размера $|B|>n/3$.

Условия применимости. $A$ — множество ненулевых элементов в любой абелевой группе с подходящим характером (для $\mathbb{Z}$ годится отображение $a\mapsto\{a x\}\in[0,1]$, $x$ random).

Идея доказательства. Берём $x\in[0,1]$ равномерно, $B_x=\{a\in A : \{ax\}\in(1/3,2/3)\}$. $B_x$ sum-free (т.к. сумма дробных частей в $(1/3,2/3)$ не лежит в $(1/3,2/3)$). $\mathbb{E}|B_x| = n\cdot\frac{1}{3}$, отсюда $\exists x: |B_x|\ge n/3$. Строго $>$ из дискретности.

Варианты и обобщения. Для произвольной абелевой группы — оптимальная константа $2/7$ (Eberhard–Green–Manners), достигается на группах вроде $(\mathbb{Z}/3)^k$. Tightness $1/3$ для $\mathbb{Z}$: контрпримеры с почти-точно $n/3$.

Используется в. [хрестоматийный пример probabilistic existence; стиль аргумента переносим на $\sum r_i a_i\not\equiv 0$ в $\mathbb{Z}/m$].

---

### E13. Szele's tournament (нижняя оценка # Hamilton paths)

Формулировка. Существует турнир на $n$ вершинах с $\ge n!\cdot 2^{-(n-1)}$ Hamilton paths. (Szele 1943 — первое применение probabilistic method.)

Условия применимости. Random orientation каждого ребра $K_n$ независимо с вероятностью $1/2$.

Идея доказательства. Для каждой из $n!$ перестановок вершин она образует Hamilton path с вероятностью $2^{-(n-1)}$ (фиксированные $n-1$ ориентаций). Линейность: $\mathbb{E}[\#HP]=n!/2^{n-1}$, существует турнир $\ge\mathbb{E}$.

Варианты и обобщения.
- Верхняя оценка: $\#HP\le c\cdot n^{3/2}\cdot n!/2^{n-1}$ (Alon 1990) через entropy/permanent inequalities.
- Аналог для Hamilton cycles, given-length paths.

Используется в. [Putnam-2005-A6 (random angles на окружности; вероятность acute через linearity), schoolbook example linearity of expectation].

---

### E14. Random partition / random matching

Формулировка. Для графа $G=(V,E)$ случайное разбиение $V=A\sqcup B$ (каждая вершина в $A$ с вероятностью $1/2$): $\mathbb{E}[\#\text{cut edges}]=|E|/2$. Отсюда max-cut $\ge|E|/2$. Обобщение: для $k$ цветов max $k$-cut $\ge|E|(1-1/k)$.

Условия применимости. Любой граф; для weighted — ребро с весом $w_e$, ожидание $\sum w_e/2$.

Идея доказательства. Каждое ребро попадает в cut с вероятностью $1/2$ — линейность.

Варианты и обобщения.
- Goemans–Williamson: SDP relaxation + random hyperplane даёт $0.878|E|$.
- Random bisection (фиксированный $|A|$): аналогичная оценка, чуть сложнее.
- Random matching в bipartite graph $K_{n,n}$: ожидание длины LIS-cycle structure.

Используется в. [хрестоматийный max-cut, max-$k$-SAT lower bounds].

---

### E15. Random permutation / averaging over $S_n$

Формулировка. Для функционала $F:S_n\to\mathbb{R}$, $\mathbb{E}_\sigma[F(\sigma)]$ часто легко вычислимо через линейность по indicator-разложению. Применение: (a) $\exists\sigma:F(\sigma)\ge\mathbb{E}[F]$; (b) $\mathbb{E}[\#\text{fixed points}]=1$, $\mathbb{E}[\#\text{cycles}]=H_n$, $\mathbb{E}[\text{\# inversions}]=\binom{n}{2}/2$ — стандартные ожидания.

Условия применимости. $F$ — линейная комбинация индикаторов локальных событий ($\sigma(i)=j$, $\sigma(i)<\sigma(j)$, $\sigma(i)=i$ etc.). Распределение — равномерное.

Идея доказательства. $P(\sigma(i)=j)=1/n$, $P(\sigma(i)=j,\sigma(k)=l)=1/(n(n-1))$ — стандартный счёт.

Варианты и обобщения.
- Random ordering для greedy bounds: independent set $\ge\sum 1/(d_v+1)$ через random ordering, добавление вершины если все её соседи уже позади (Caro–Wei).
- Katona cyclic proof EKR (E5).

Используется в. [Putnam-2006-A4 (#локальных максимумов), Caro–Wei для $\alpha(G)\ge\sum 1/(d_v+1)$, IMC-2022-8 ($\mathbb{E}$-вершин convex hull intersection)].

---

## Записи - Exotic

### E16. Spencer's "six standard deviations suffice" (discrepancy)

Формулировка. Для $n$-точечного множества и $n$ подмножеств $S_1,\dots,S_n$, существует знаковая функция $\chi:[n]\to\{\pm 1\}$ с
$$\max_i\Big|\sum_{j\in S_i}\chi(j)\Big|\le 6\sqrt{n}.$$
Случайные $\chi(j)=\pm 1$ дают $O(\sqrt{n\log n})$ (Chernoff + union bound), Spencer-1985 убирает $\sqrt{\log}$ — нетривиально.

Условия применимости. Любая set system из $n$ множеств на $n$ элементах. Для $m\gg n$ множеств бонус не работает.

Идея доказательства. Партиальная раскраска: показать $\exists$ раскраска "большого" подмножества с малой $\ell_\infty$-discrepancy, итерировать. Современные алгоритмические доказательства (Bansal, Lovett–Meka) дают полиномиальный алгоритм; оригинал — pigeonhole + entropy.

Варианты и обобщения. Beck–Fiala theorem: discrepancy $\le 2t-1$ для систем с column degrees $\le t$. Komlós conjecture (открыта): $O(1)$ для unit-vector matrices.

Используется в. [не для IMC напрямую, но для понимания "почему случайные знаки часто оптимальны до $\sqrt{\log}$"; полезный фон для IMC-2013-DAY2-3 в его слабой форме].

---

### E17. Janson's inequality

Формулировка. Пусть $X=\sum_{i\in I}\mathbb{1}_{A_i}$, $A_i$ — "монотонные" события (включения подмножеств в random subset). Обозначим $\mu=\mathbb{E}[X]$, $\Delta=\sum_{i\sim j}P(A_i\cap A_j)$ (зависимые пары). Тогда
$$P(X=0)\le\exp\Big(-\mu+\frac{\Delta}{2}\Big).$$
В частности, при $\Delta\ll\mu$ — $P(X=0)\le e^{-(1-o(1))\mu}$.

Условия применимости. $A_i = \{B_i\subseteq R\}$ где $R$ — random subset $\Omega$; $A_i\sim A_j$ iff $B_i\cap B_j\ne\emptyset$.

Идея доказательства. Сравнение с Poisson-предельным распределением через martingale корреляционные неравенства (FKG).

Варианты и обобщения. Extended Janson: $P(X\le(1-\delta)\mu)\le\exp(-\delta^2\mu^2/(2(\mu+\Delta)))$. Используется для существования triangle-free $G(n,p)$ при subcritical $p$.

Используется в. [не появляется в IMC явно; иногда — упрощённый счёт в задачах с независимыми попарно событиями].

---

### E18. Sylvester four-point problem (Sylvester's problem)

Формулировка. Для 4 точек, выбранных независимо и равномерно из выпуклого тела $K\subset\mathbb{R}^2$, $P_4(K)=P(\text{одна точка внутри треугольника других})$. Тогда $P_4(K)$ принимает значения от $1/3$ (треугольник) до $35/(12\pi^2)\approx 0.296$ (диск). Минимум — на эллипсе/диске (Blaschke).

Условия применимости. Двумерные выпуклые тела с положительной площадью. Для $n>4$ — задача о выпуклой оболочке, $\mathbb{E}[\#\text{vertices of conv}(X_1,\dots,X_n)]\sim c_K\cdot\log n$ (smooth boundary) или $\sim c_K\cdot n^{1/3}$ (poly boundary, e.g. Rényi–Sulanke).

Идея доказательства. $P_4(K) = 1 - 4\mathbb{E}[\text{area triangle}]/\text{area}(K)$ — выражение через ожидаемую площадь случайного треугольника.

Варианты и обобщения. Бернулли-Сильвестер — большая теория random convex hulls. Для $n=2019$ — типичный размер convex hull $\sim\log 2019$ для гладких границ.

Используется в. [IMC-2019-10 (P(triangle) vs P(quadrilateral) для 2019 точек в диске — анализ через Sylvester и его обобщения)].

---

### E19. Probabilistic counting через random matrix / sign vector

Формулировка. Для подсчёта пар матриц с заданным свойством используют random sign vectors: число $\pm 1$ векторов $v\in\{\pm 1\}^n$ с $u\cdot v=0$ оценивается как $\binom{n}{n/2}\sim 2^n/\sqrt{n}$. Probabilistically: $P_v(u\cdot v=0)\sim 1/\sqrt{n}$ для random $u\in\{\pm 1\}^n$.

Условия применимости. Линейные/билинейные условия над $\mathbb{F}_2$ или $\mathbb{Z}$ для $\pm 1$ векторов. Обобщение — случайные матрицы Бернулли.

Идея доказательства. Локальная CLT: $u\cdot v\sim\sqrt{n}\cdot\mathcal{N}(0,1)$ при random $v$, далее $P(u\cdot v=0)\sim 1/\sqrt{2\pi n}$ для general position.

Используется в. [IMC-2025-3 (rank-1 ±1 matrices: $A=\pm vv^\top$, $AB=BA\Leftrightarrow v_A\cdot v_B\in\{0,\pm n\}$ — biномиальный счёт пар через probabilistic argument)].

---

## Self-test

1. Граф $G$ имеет $n$ вершин и $m$ рёбер. Доказать: существует разбиение $V=A\sqcup B$ такое, что $\ge m/2$ рёбер идут между $A$ и $B$.

2. В графе $G$ степени вершин $d_1,\dots,d_n$. Показать $\alpha(G)\ge\sum_{i=1}^{n}\frac{1}{d_i+1}$ ($\alpha$ — independence number).

3. (Putnam-style) В случайной перестановке $\sigma\in S_n$ найти $\mathbb{E}[\#\{i:\sigma(i-1)<\sigma(i)>\sigma(i+1)\}]$ для $1<i<n$, и показать, что существует перестановка с $\ge(n-2)/3$ "локальных максимумов".

4. Дано $n$ точек $v_1,\dots,v_n\in\mathbb{R}^d$ единичных. Показать: $\exists\,\varepsilon\in\{\pm 1\}^n$, что для $u=\frac{1}{\sqrt{n}}\sum\varepsilon_i v_i$ выполнено $|u|\le 1$.

5. Турнир на $n$ вершинах. Показать: существует турнир на $n$ вершинах с $\ge n!/2^{n-1}$ направленных Hamilton paths.

6. Доказать: любое множество $A\subset\mathbb{Z}_{>0}$ с $|A|=n$ содержит подмножество $B$ размера $>n/3$ такое, что $B$ не содержит решения $x+y=z$.

7. (IMC-2017-4 reduced) Граф $G$ на $n$ вершинах, каждая степени ровно $1000$. Показать: $\exists$ подмножество $S\subseteq V$, в котором $\ge n/2017$ вершин имеют ровно 2 соседей внутри $S$.

8. Случайная 2-раскраска $K_n$. Доказать: для $n=2^{k/2-1}\cdot k\cdot e^{-1}$ существует раскраска без монохромного $K_k$ ($k\ge 3$).

9. (Inclusion-exclusion via sampling) $A_1,\dots,A_m\subseteq[n]$. Случайное $X\subseteq[n]$ с $P(i\in X)=t$ независимо. Выразить $P(\exists i:A_i\subseteq X)$ как полином от $t$ и доказать его монотонность по $t$ через coupling.

---

## Решения

1. По E14 / E7. Случайное независимое включение каждой вершины в $A$ с $P=1/2$. Каждое ребро $\{u,v\}$ — в cut с вероятностью $1/2$. $\mathbb{E}[\text{cut}]=m/2$, по pigeonhole $\exists$ выбор $\ge m/2$.

2. Caro–Wei (E15). Random uniform ordering $\pi$ вершин. Алгоритм: проходим $\pi$, добавляем $v$ в $I$ если все её соседи позже неё. $I$ — independent set. $P(v\in I) = P(v$ — минимум в $\{v\}\cup N(v)) = 1/(d_v+1)$. По линейности $\mathbb{E}|I|=\sum 1/(d_i+1)$, существует ordering с $|I|\ge\sum 1/(d_i+1)$.

3. По E1: $P(\sigma(i-1)<\sigma(i)>\sigma(i+1))=1/3$ для $1<i<n$ (равная по симметрии вероятность каждого из 3 относительных порядков $\sigma(i)$ как макс/мин/средний). $\mathbb{E}=(n-2)/3$, по E7 $\exists\sigma$ с $\ge(n-2)/3$.

4. По E8: $\mathbb{E}|u|^2 = \mathbb{E}\sum_{i,j}\varepsilon_i\varepsilon_j(v_i\cdot v_j)/n = \sum_i|v_i|^2/n = 1$. Существует $\varepsilon$ с $|u|^2\le 1$.

5. По E13: random orientation $K_n$ независимо с $P=1/2$. Для каждой из $n!$ перестановок $\pi$ — она Hamilton path с вероятностью $2^{-(n-1)}$. $\mathbb{E}[\#HP]=n!/2^{n-1}$, существует турнир с $\ge\mathbb{E}$.

6. По E12: $x\in[0,1]$ равномерное, $B_x=\{a\in A:\{ax\}\in(1/3,2/3)\}$. Sum-free: если $a+b=c$, то $\{ax\}+\{bx\}\equiv\{cx\}\pmod 1$, а $(1/3,2/3)+(1/3,2/3)\not\subset(1/3,2/3)\pmod 1$. $P(\{ax\}\in(1/3,2/3))=1/3$ для каждого $a>0$ (равномерность дробной части), $\mathbb{E}|B_x|=n/3$, $\exists x$. Дискретность $|B|$ даёт $|B|>n/3$ строго.

7. По E3+E4. Случайное $S$ с $P(v\in S)=p$. По линейности $\mathbb{E}[\#\{v\in S:|N(v)\cap S|=2\}]=n\cdot p\cdot\binom{1000}{2}p^2(1-p)^{998}=n\cdot\binom{1000}{2}p^3(1-p)^{998}$. Оптимум $p^*$ из $\frac{d}{dp}\log[p^3(1-p)^{998}]=\frac{3}{p}-\frac{998}{1-p}=0$, т.е. $p^*=3/1001$. Численно $\binom{1000}{2}\cdot(3/1001)^3\cdot(998/1001)^{998}\approx 6.72\cdot 10^{-4}>1/2017\approx 4.96\cdot 10^{-4}$. Существует $S$.

8. По E11: $\mathbb{E}[\#K_k\text{ mono}]=\binom{n}{k}\cdot 2^{1-\binom{k}{2}}\le(en/k)^k\cdot 2^{1-\binom{k}{2}}$. Подстановка $n=2^{k/2-1}\cdot k/e$ даёт $\le 2^{1-k/2}<1$ для $k\ge 3$ — отсюда existence (достаточно больших $k$, для малых $k$ выражение для $n$ даёт тривиально малую границу).

9. По E6: $f(t):=P(\exists i:A_i\subseteq X)=\sum_{\emptyset\ne I}(-1)^{|I|-1}t^{|\bigcup_{i\in I}A_i|}$. Монотонность: coupling — пусть $X_t,X_{t'}$ построены через единственное $U_v\sim\text{Uniform}[0,1]$ и $X_t=\{v:U_v\le t\}$. При $t\le t'$: $X_t\subseteq X_{t'}$ а.с., следовательно $\{∃i:A_i\subseteq X_t\}\subseteq\{∃i:A_i\subseteq X_{t'}\}$, т.е. $f(t)\le f(t')$.
