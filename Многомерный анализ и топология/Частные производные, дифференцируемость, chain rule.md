---
topic: Многомерный анализ и топология
subtopic: "Частные производные, дифференцируемость, chain rule"
sources:
  - "Rudin — Principles of Mathematical Analysis (ch. 9)"
  - "Spivak — Calculus on Manifolds"
  - "Zorich — Mathematical Analysis II"
  - "Fleming — Functions of Several Variables"
  - "Polya–Szegő — Problems and Theorems in Analysis I, II"
  - "Andreescu, Andrica — Putnam and Beyond"
  - "Engel — Problem-Solving Strategies"
  - "Nesterov — Introductory Lectures on Convex Optimization (Baillon–Haddad)"
  - "Federer — Geometric Measure Theory (Rademacher, Sard)"
  - "IMC Compendium"
  - "Putnam Compendium"
problems_referenced:
  - IMC-2002-DAY2-6
  - IMC-2004-DAY2-3
  - Putnam-2010-A4
  - Putnam-2005-A5
last_updated: 2026-04-27
---

# Частные производные, дифференцируемость, chain rule

## Scope
Тонкости определения Fréchet-дифференцируемости в $\mathbb{R}^n$ против поточечного существования partial derivatives и directional derivatives, симметрия смешанных производных (Schwarz / Young), цепное правило в матричной форме и Faà di Bruno, теоремы об обратной и неявной функции, многомерный Taylor с Hessian-остатком, тождество Эйлера для однородных функций, лемма Адамара, критерии выпуклости через gradient/Hessian и co-coercivity (Baillon–Haddad), а также Sard и Rademacher как «почти всюду» инструменты.

## Записи — Core

### E1. Sufficient condition for total differentiability ($C^1 \Rightarrow$ Fréchet)

Формулировка. Пусть $f: U \subset \mathbb{R}^n \to \mathbb{R}^m$, и в окрестности точки $a$ существуют все partial derivatives $\partial_i f$, причём они непрерывны в $a$. Тогда $f$ дифференцируема в $a$ по Fréchet:
$$f(a+h) = f(a) + Df(a)\,h + o(\|h\|), \quad h \to 0,$$
где $Df(a)$ — матрица Якоби $[\partial_j f_i(a)]$.

Условия применимости. Существование partials в самой точке **не достаточно** для дифференцируемости — это типичная ловушка. Ключ — непрерывность partials в *окрестности* (или хотя бы в $a$ при существовании в окрестности). Контрпримеры:
- $f(x,y) = xy/\sqrt{x^2+y^2}$ при $(x,y)\neq 0$, $f(0,0)=0$ — partials в нуле существуют и равны нулю, $f$ непрерывна, но не дифференцируема (предел $f(h, h)/\|h\|$ не равен нулю).
- $f(x,y) = x^3 y / (x^4 + y^2)$, $f(0,0)=0$ — все directional derivatives в нуле существуют (и равны 0), но $f$ не непрерывна в нуле (вдоль $y = x^2$ значение $1/2$), значит и не дифференцируема.

Идея доказательства. Пишем приращение по координатам:
$$f(a+h) - f(a) = \sum_{k=1}^{n} \bigl[f(a + h_1 e_1 + \cdots + h_k e_k) - f(a + h_1 e_1 + \cdots + h_{k-1} e_{k-1})\bigr],$$
к каждому слагаемому применяем 1D Lagrange MVT по переменной $x_k$, получаем $\partial_k f(\xi^{(k)}) h_k$. Непрерывность partials в $a$ даёт $\partial_k f(\xi^{(k)}) = \partial_k f(a) + o(1)$, что и есть искомая Fréchet-аппроксимация.

Варианты и обобщения.
- **Gâteaux differentiability**: существование $\lim_{t\to 0} (f(a+tv) - f(a))/t$ для каждого $v$ — слабее Fréchet. Gâteaux + локальная Lipschitz $\Rightarrow$ Fréchet.
- **Stepanov's theorem**: $f$ почти всюду дифференцируема на множестве $\{x: \limsup_{y\to x}|f(y)-f(x)|/|y-x| < \infty\}$.

Используется в. Базовый «атом» — без него ни одна задача с производными в $\mathbb{R}^n$ не решается. Важен в IMC/Putnam задачах, где $f \in C^1$ — это разрешает писать chain rule и Taylor без оговорок.

---

### E2. Schwarz / Clairaut theorem on equality of mixed partials (теорема о смешанных производных)

Формулировка. Пусть $f$ имеет $\partial_i f, \partial_j f$ в окрестности $a$, $\partial_i \partial_j f$ существует в окрестности $a$ и непрерывна в $a$. Тогда $\partial_j \partial_i f(a)$ также существует и
$$\partial_i \partial_j f(a) = \partial_j \partial_i f(a).$$
**Young's theorem (более слабое условие)**: если $f$ дважды дифференцируема в $a$ (Fréchet), то все смешанные partials порядка 2 в $a$ существуют и совпадают.

Условия применимости. Без непрерывности (или дифференцируемости второго порядка) равенство ломается. Канонический контрпример Peano:
$$f(x,y) = \frac{xy(x^2-y^2)}{x^2+y^2}, \quad f(0,0)=0.$$
Прямой подсчёт: $\partial_x f(0, y) = -y$, $\partial_y f(x, 0) = x$, поэтому
$$\partial_y \partial_x f(0,0) = -1, \quad \partial_x \partial_y f(0,0) = 1.$$

Идея доказательства. Рассмотреть «дискретный» аналог $\Delta(h,k) = f(a+he_i+ke_j) - f(a+he_i) - f(a+ke_j) + f(a)$. Двукратное применение 1D MVT даёт два выражения: $\Delta = h k\,\partial_i\partial_j f(\xi)$ и $\Delta = h k\,\partial_j\partial_i f(\eta)$. Непрерывность $\Rightarrow$ предел при $h,k\to 0$ один и тот же.

Варианты и обобщения.
- **Higher-order Schwarz**: при $C^k$ перестановка любых индексов $\le k$ не меняет $D^\alpha f$.
- **Distributional version**: для $L^1_{\text{loc}}$-функций смешанные слабые производные всегда коммутируют (без условий гладкости).

Используется в. Любая задача, где выписывается Hessian (нужна симметрия), либо контрпример строится через классический $f$ выше. В олимпиадах — реже как самостоятельная теорема, чаще как «техническая» предпосылка для Taylor (E5) и convexity criteria (E9).

---

### E3. Chain rule in matrix form (цепное правило)

Формулировка. Пусть $g: U \subset \mathbb{R}^n \to \mathbb{R}^m$ дифференцируема в $a$, $f: V \subset \mathbb{R}^m \to \mathbb{R}^k$ дифференцируема в $g(a)$. Тогда $f \circ g$ дифференцируема в $a$ и
$$D(f \circ g)(a) = Df(g(a)) \cdot Dg(a).$$
В координатах:
$$\partial_j (f \circ g)_i(a) = \sum_{l=1}^{m} \partial_l f_i(g(a)) \cdot \partial_j g_l(a).$$

Условия применимости. Дифференцируемость каждого звена в соответствующих точках — критично. Существования всех partials по отдельности **не достаточно**: контрпример строится через $g$ и $f$, у которых partials есть, но композиция не имеет нужного предела.

Идея доказательства. Прямо из определения:
$$f(g(a+h)) - f(g(a)) = Df(g(a))[g(a+h) - g(a)] + o(\|g(a+h)-g(a)\|),$$
$$g(a+h) - g(a) = Dg(a)h + o(\|h\|),$$
подставляем и пользуемся $\|g(a+h)-g(a)\| = O(\|h\|)$.

Варианты и обобщения.
- **Faà di Bruno's formula**: $n$-я производная композиции $f(g(t))$ — суммирование по разбиениям множества $\{1,\ldots,n\}$, обобщает $(f\circ g)' = f'(g)g'$.
- **Lipschitz chain rule (Stepanov + Rademacher)**: для Lipschitz $f, g$ chain rule справедлив почти всюду.
- **Carathéodory form**: $f(x) - f(a) = \Phi(x)(x-a)$ с $\Phi$ непрерывной в $a$ — тогда chain rule = умножение матриц $\Phi$.

Используется в. Везде, где работают с $f(\gamma(t))$, $f(g(x,y))$, ОДУ-системами, parameterized integrals (Leibniz). Прямой инструмент для тождества Эйлера (E8) и MVT inequality (E4).

---

### E4. Mean value inequality for vector-valued maps (неравенство о среднем в $\mathbb{R}^n$)

Формулировка. Пусть $f: U \to \mathbb{R}^m$ дифференцируема на отрезке $[a, b] \subset U \subset \mathbb{R}^n$ (т.е. $\{a + t(b-a): t \in [0,1]\}$). Тогда
$$\|f(b) - f(a)\| \leq \sup_{t \in [0,1]} \|Df(a + t(b-a))\| \cdot \|b - a\|,$$
где $\|Df\|$ — операторная норма.

**Векторный MVT в форме равенства не существует**: $f: [0, 2\pi] \to \mathbb{R}^2$, $f(t) = (\cos t, \sin t)$ — $f(0)=f(2\pi)$, но $\|f'(t)\| = 1$ всюду, нет $\xi$ с $f'(\xi) = 0$.

Условия применимости. Достаточно дифференцируемости вдоль отрезка + ограниченности $Df$ на нём. Выпуклости области не требуется — нужна только точечная связность через прямой отрезок.

Идея доказательства. Положим $\phi(t) = \langle f(a+t(b-a)) - f(a), v\rangle$ для $v = (f(b)-f(a))/\|f(b)-f(a)\|$. Применить 1D Lagrange MVT к $\phi$:
$$\|f(b)-f(a)\| = \phi(1) - \phi(0) = \phi'(\tau) = \langle Df(a+\tau(b-a))(b-a), v\rangle \leq \|Df\|\|b-a\|.$$

Варианты и обобщения.
- **Pompeiu для вектор-функций**: $f(b) - f(a) \in (b-a) \cdot \overline{\operatorname{conv}}\{f'(t): t \in (a,b)\}$ — даёт информацию о направлении, не только норме.
- **Lipschitz характеризация $C^1$**: $\sup \|Df\| = \operatorname{Lip}(f)$ на выпуклом множестве.

Используется в. Доказательство Banach fixed point для уравнений в $\mathbb{R}^n$, оценки решений ОДУ-систем, единственность через Gronwall в многомерном случае. [IMC-2004-DAY2-3 — выбор направления через triangle inequality, эквивалент сублинейного MVT для $\sum \|p - p_i\|$].

---

### E5. Multivariate Taylor's theorem (многомерный Taylor)

Формулировка. Пусть $f \in C^{k+1}$ в окрестности $a \in \mathbb{R}^n$. Тогда для $h$ малого
$$f(a+h) = \sum_{|\alpha| \leq k} \frac{D^\alpha f(a)}{\alpha!} h^\alpha + R_k(h),$$
где $\alpha = (\alpha_1, \ldots, \alpha_n)$ — мультииндекс, $h^\alpha = h_1^{\alpha_1} \cdots h_n^{\alpha_n}$, $\alpha! = \alpha_1! \cdots \alpha_n!$. Формы остатка:
- **Lagrange**: $R_k = \sum_{|\alpha|=k+1} \frac{D^\alpha f(a + \theta h)}{\alpha!} h^\alpha$, $\theta \in (0,1)$.
- **Integral**: $R_k = (k+1) \sum_{|\alpha|=k+1} \frac{h^\alpha}{\alpha!} \int_0^1 (1-t)^k D^\alpha f(a+th)\,dt$.
- **Peano**: $R_k = o(\|h\|^k)$ при $h\to 0$ (требует только $f \in C^k$).

Квадратичный случай ($k=1$): $f(a+h) = f(a) + \langle \nabla f(a), h\rangle + \tfrac12 h^T H f(a + \theta h) h$.

Условия применимости. Гладкость $C^{k+1}$ для Lagrange/integral; $C^k$ для Peano. На отрезке $[a, a+h]$ (нужна выпуклость только этого отрезка, а не окрестности).

Идея доказательства. Применить 1D Taylor к $\phi(t) = f(a + th)$. Производные: $\phi^{(j)}(t) = \sum_{|\alpha|=j} \binom{j}{\alpha} D^\alpha f(a+th) h^\alpha$ (multinomial по chain rule). Подстановка даёт нужную формулу.

Варианты и обобщения.
- **Hermite remainder в нескольких узлах** — обобщение для ε-сетей и приближений.
- **Taylor с Bernstein-positivity**: положительность всех $D^\alpha f$ + bounded growth $\Rightarrow$ аналитичность.

Используется в. Доказательство sufficient condition для extrema через Hessian, оценки в задачах на extremum, вывод Newton-style итераций. Putnam-2005-A5 — Taylor 2-го порядка с интегральным остатком для convex $f$.

---

### E6. Implicit Function Theorem (теорема о неявной функции)

Формулировка. $F: U \times V \subset \mathbb{R}^n \times \mathbb{R}^m \to \mathbb{R}^m$ — функция класса $C^k$ ($k \geq 1$), $F(a, b) = 0$, и якобиан по $y$-переменным $\partial_y F(a,b) \in \mathbb{R}^{m \times m}$ невырожден. Тогда существуют окрестности $U' \ni a$, $V' \ni b$ и единственная $g: U' \to V'$ класса $C^k$ с $g(a) = b$, $F(x, g(x)) \equiv 0$. Производная:
$$Dg(x) = -\bigl[\partial_y F(x, g(x))\bigr]^{-1} \partial_x F(x, g(x)).$$

Условия применимости. **Невырожденность $\partial_y F$ по «зависимым» переменным** — критично. Если только $\operatorname{rank} DF(a,b) = m$ (т.е. полный по строкам), нужно подобрать какие именно $m$ переменных делать «зависимыми» — это даёт другую перестановку IFT.

Идея доказательства. Применить Banach fixed point к $T_x(y) = y - [\partial_y F(a,b)]^{-1} F(x, y)$. Сжимаемость по $y$ через непрерывность производных + малость окрестности; зависимость от $x$ как параметра даёт $C^k$-регулярность $g$ через рекуррентное дифференцирование.

Варианты и обобщения.
- **Real-analytic IFT**: $C^\omega \Rightarrow g \in C^\omega$.
- **Submersion theorem**: если $DF$ имеет постоянный ранг $r$ на окрестности, локально $F$ сопряжена $(x_1,\ldots,x_r,0,\ldots,0)$ (rank theorem).
- **Holomorphic IFT**: для голоморфных $F$ с условием на якобиан получаем голоморфную $g$.

Используется в. Putnam-2010-A4 (locally extracting parameter from constraint); типовой инструмент в задачах с условными экстремумами и параметрическими кривыми. Базис для теории многообразий.

---

### E7. Inverse Function Theorem (теорема об обратной функции)

Формулировка. $f: U \subset \mathbb{R}^n \to \mathbb{R}^n$ класса $C^k$ ($k \geq 1$), $a \in U$, $\det Df(a) \neq 0$. Тогда существуют окрестности $U' \ni a$, $V' \ni f(a)$ такие, что $f|_{U'}: U' \to V'$ — $C^k$-диффеоморфизм, и
$$D(f^{-1})(f(a)) = [Df(a)]^{-1}.$$

Условия применимости. **Локальная** теорема: невырожденность якобиана не гарантирует глобальной обратимости. Контрпример: $f(x,y) = (e^x \cos y, e^x \sin y)$ (комплексная экспонента) — $\det Df = e^{2x} > 0$ всюду, но $f$ не инъективна (период по $y$).

**Глобальная версия (Hadamard's global inverse function theorem)**: $f: \mathbb{R}^n \to \mathbb{R}^n$ — собственное (proper) $C^1$-отображение с $\det Df \neq 0$ всюду $\Rightarrow$ $f$ — диффеоморфизм. Эквивалентное условие: $\|[Df(x)]^{-1}\|$ ограничено $\Rightarrow$ $f$ собственное.

Идея доказательства. IFT, применённая к $F(x, y) = f(x) - y$ — невырожденность $\partial_x F = Df(a)$ даёт локальный обратный. Альтернатива: contraction для $T_y(x) = x + [Df(a)]^{-1}(y - f(x))$.

Варианты и обобщения.
- **IFT $\Leftrightarrow$ Implicit FT**: эти две теоремы эквивалентны (вывод друг из друга через переформулировку).
- **Constant rank theorem**: при постоянном ранге $r$ получаем нормальную форму.
- **Lipschitz IFT (Clarke)**: для Lipschitz $f$ с обратимым обобщённым якобианом — локальная Lipschitz-биекция.

Используется в. Замены координат в кратных интегралах (E подтемы Якобиан/Fubini), параметризация многообразий. В олимпиадных задачах — для перехода в удобные локальные координаты.

---

### E8. Euler's homogeneous function theorem (тождество Эйлера)

Формулировка. $f: \mathbb{R}^n \setminus \{0\} \to \mathbb{R}$ — дифференцируемая функция, положительно однородная степени $k$:
$$f(\lambda x) = \lambda^k f(x), \quad \forall\,\lambda > 0,\,x \neq 0.$$
Тогда
$$\langle x, \nabla f(x)\rangle = k\,f(x).$$
Обратное также верно: $C^1$-функция, удовлетворяющая этому тождеству на $\mathbb{R}^n \setminus \{0\}$, — положительно однородная степени $k$.

Условия применимости. Дифференцируемость; положительная однородность (для $\lambda < 0$ требуется отдельная гипотеза о чётности/нечётности). На границе ($x = 0$) тождество тривиально, если $f$ непрерывна и $k > 0$.

Идея доказательства. Дифференцировать $f(\lambda x) = \lambda^k f(x)$ по $\lambda$ при $\lambda = 1$: левая часть по chain rule даёт $\langle x, \nabla f(x)\rangle$, правая — $k f(x)$. Обратно: положить $\phi(\lambda) = f(\lambda x)$, тогда $\phi'(\lambda) = \langle x, \nabla f(\lambda x)\rangle = (k/\lambda)f(\lambda x) = (k/\lambda)\phi(\lambda)$, ОДУ $\phi'/\phi = k/\lambda$ даёт $\phi(\lambda) = \lambda^k \phi(1)$.

Варианты и обобщения.
- **Higher-order Euler**: для однородной $f$ степени $k$ имеем $\sum_{|\alpha|=m} \binom{m}{\alpha} x^\alpha D^\alpha f(x) = k(k-1)\cdots(k-m+1) f(x)$.
- **Quasi-homogeneous**: $f(\lambda^{a_1} x_1, \ldots, \lambda^{a_n} x_n) = \lambda^k f(x)$ $\Rightarrow$ $\sum a_i x_i \partial_i f = k f$.

Используется в. Putnam-задачи про однородные многочлены и инварианты, вывод формулы Эйлера для решений PDE-классификации, классификация гармонических многочленов.

---

## Записи — Standard

### E9. Convexity criteria + Baillon–Haddad co-coercivity

Формулировка. Пусть $f: U \to \mathbb{R}$ — $C^1$ на выпуклом открытом $U \subset \mathbb{R}^n$.
- **First-order**: $f$ выпукла $\Leftrightarrow$ $f(y) \geq f(x) + \langle \nabla f(x), y-x\rangle$ для всех $x, y$.
- **Monotonicity of gradient**: $f$ выпукла $\Leftrightarrow$ $\langle \nabla f(x) - \nabla f(y), x - y\rangle \geq 0$.
- **Hessian-критерий ($C^2$)**: $f$ выпукла $\Leftrightarrow$ $H f(x) \succeq 0$ всюду; строго выпукла $\Leftarrow$ $Hf \succ 0$.
- **$L$-smooth $\Rightarrow$ co-coercive (Baillon–Haddad)**: если $f$ выпукла и $\nabla f$ $L$-Lipschitz, то
$$\langle \nabla f(x) - \nabla f(y), x - y\rangle \geq \frac{1}{L}\,\|\nabla f(x) - \nabla f(y)\|^2.$$

Условия применимости. Выпуклость области критична. Baillon–Haddad строго требует обоих: выпуклости и $L$-smooth (только Lipschitz $\nabla f$ без выпуклости не хватает). Эквивалентно: $\nabla f$ — $1/L$-firmly nonexpansive.

Идея доказательства (Baillon–Haddad). Положить $g(x) = f(x) - f(x_1) - \langle \nabla f(x_1), x - x_1\rangle$ — выпуклая, $\nabla g(x_1) = 0$, $g \geq 0$, $\nabla g$ всё ещё $L$-Lipschitz. Из quadratic upper bound (descent lemma):
$$g(y) \leq g(x_2) + \langle \nabla g(x_2), y - x_2\rangle + \tfrac{L}{2}\|y - x_2\|^2.$$
Минимизируем по $y$: $y^* = x_2 - \nabla g(x_2)/L$, получаем
$$0 \leq g(y^*) \leq g(x_2) - \tfrac{1}{2L}\|\nabla g(x_2)\|^2.$$
Расписав $g(x_2)$ обратно через $f$ и сложив с симметричным неравенством (поменяв $x_1 \leftrightarrow x_2$), получаем co-coercivity.

Варианты и обобщения.
- **$\mu$-strongly convex $+$ $L$-smooth $\Rightarrow$ оба неравенства одновременно**, что даёт линейную сходимость градиентного спуска.
- **Convex conjugate Moreau–Fenchel**: $f$ $L$-smooth + convex $\Leftrightarrow$ $f^*$ $1/L$-strongly convex.

Используется в. **IMC-2002-DAY2-6** — каноничная задача на co-coercivity, ровно эта же конструкция. Базис современной теории first-order optimization (Nesterov), bound на скорость сходимости gradient descent.

---

### E10. Hadamard's lemma (лемма Адамара)

Формулировка. Пусть $f \in C^k$ в открытой звёздной (по $0$) окрестности $U \ni 0$, $f(0) = 0$. Тогда существуют функции $g_1, \ldots, g_n \in C^{k-1}(U)$ с
$$f(x) = \sum_{i=1}^{n} x_i\,g_i(x), \quad g_i(0) = \partial_i f(0).$$

Условия применимости. Звёздность (или просто выпуклость) области относительно нуля — нужна для интегрирования по отрезку $[0, x]$. Для $f$ только $C^0$ лемма становится ложной.

Идея доказательства. Прямой расчёт через интеграл от полной производной:
$$f(x) = f(x) - f(0) = \int_0^1 \frac{d}{dt} f(tx)\,dt = \int_0^1 \sum_i x_i\,\partial_i f(tx)\,dt = \sum_i x_i\,\underbrace{\int_0^1 \partial_i f(tx)\,dt}_{g_i(x)}.$$
$g_i(0) = \partial_i f(0)$ и $g_i \in C^{k-1}$ — из дифференцирования под интегралом.

Варианты и обобщения.
- **Higher-order Hadamard**: $f \in C^k$, $f(0)=\cdots=D^{k-1}f(0)=0$ $\Rightarrow$ $f(x) = \sum_{|\alpha|=k} x^\alpha\,g_\alpha(x)$ с $g_\alpha \in C^0$.
- **Smooth division lemma**: используется при доказательстве полугладкости и в дифференциальной топологии.

Используется в. Доказательство IFT/IVT в категории $C^\infty$, вывод нормальных форм отображений (Morse lemma), задачи на «вынесение множителя $x$» из гладкой функции.

---

### E11. Gradient zero $\Rightarrow$ constant on connected open set

Формулировка. Пусть $U \subset \mathbb{R}^n$ — связное открытое множество, $f: U \to \mathbb{R}$ дифференцируема и $\nabla f(x) = 0$ для всех $x \in U$. Тогда $f$ постоянна на $U$.

**Расширение**: если $\|\nabla f(x)\| \leq \phi(x)\,\|f(x) - f(x_0)\|$ для какой-то локально интегрируемой $\phi$ и связного $U$ с $f(x_0) = c_0$, то по Gronwall в одномерных параметризациях $f \equiv c_0$.

Условия применимости. **Связность критична**: на двух disjoint компонентах $f$ может быть разными константами. Открытость нужна для существования отрезков; на множестве с «дырами» (например, $\{(x,y): xy>0\}$) теорема всё ещё работает на каждой компоненте.

Идея доказательства. Фиксируем $x_0 \in U$. Множество $\{x: f(x) = f(x_0)\}$ открыто (по локальной формуле $f(x) = f(x_0) + \int_0^1 \langle\nabla f, x-x_0\rangle\,dt$ на отрезке) и замкнуто (непрерывность $f$). По связности — это всё $U$.

Варианты и обобщения.
- **Liouville-type**: если $f$ дифференцируема на $\mathbb{R}^n$ и $\langle \nabla f, x\rangle = 0$ всюду, то $f$ постоянна на каждом луче через $0$ (E8 при $k=0$), а если $f$ непрерывна в нуле — постоянна везде.
- **Distributional version**: $f \in W^{1,1}_{\text{loc}}$, $\nabla f = 0$ почти всюду $\Rightarrow$ $f$ постоянна на каждой компоненте связности (требует абсолютной непрерывности на отрезках).

Используется в. IMC-style задачи с условиями типа «$f$ удовлетворяет PDE первого порядка» $\Rightarrow$ редуцируется к константности по характеристикам. [IMC-2004-DAY2-3 — выбор экстремального направления через $\nabla(\sum |p - p_i|)$, использует sub-gradient analysis на сфере].

---

### E12. Saddle point / second-order condition for local extrema

Формулировка. Пусть $f \in C^2$ в окрестности $a$, $\nabla f(a) = 0$.
- $H f(a) \succ 0$ (PD) $\Rightarrow$ $a$ — строгий локальный минимум.
- $H f(a) \prec 0$ (ND) $\Rightarrow$ строгий локальный максимум.
- $H f(a)$ имеет собственные значения обоих знаков $\Rightarrow$ $a$ — седловая точка (no extremum).
- $H f(a) \succeq 0$ — минимум **не гарантируется** (вырожденный случай, нужны старшие производные).

Условия применимости. **Не путать**: $Hf \succeq 0$ в окрестности $\Rightarrow$ выпуклость и минимум; $Hf \succeq 0$ в одной точке — недостаточно (контрпример $f(x,y) = x^2 - y^4$: $\nabla f(0)=0$, $Hf(0) = \operatorname{diag}(2, 0) \succeq 0$, но $f(0, t) = -t^4 < 0$, не минимум).

Идея доказательства. Taylor 2-го порядка с Lagrange-остатком: $f(a+h) = f(a) + \tfrac12 h^T Hf(\xi) h$. Непрерывность Hessian в $a$ + PD в $a$ $\Rightarrow$ PD в окрестности $\Rightarrow$ $f(a+h) > f(a)$ для $h \neq 0$ малого.

Варианты и обобщения.
- **Bordered Hessian** для условных экстремумов (см. подтему Lagrange multipliers).
- **Morse lemma**: при $Hf(a)$ невырожденной существуют локальные координаты $u_1, \ldots, u_n$, в которых $f(u) = f(a) + \sum \pm u_i^2$.

Используется в. Стандартный инструмент классификации стационарных точек. Базис теории Морса.

---

## Записи — Exotic

### E13. Sard's theorem (теорема Сарда)

Формулировка. Пусть $f: U \subset \mathbb{R}^n \to \mathbb{R}^m$ — $C^k$-отображение, $k \geq \max(1, n - m + 1)$. Множество **критических точек** $C = \{x: \operatorname{rank} Df(x) < m\}$ имеет образ $f(C)$ нулевой меры Лебега в $\mathbb{R}^m$.

Условия применимости. **Условие на $k$ обязательно**: при $n > m$ и низкой гладкости теорема ложна (Whitney построил $C^1$ контрпример при $n=2, m=1$, где $f$ непостоянна, но критические значения занимают интервал). При $n \leq m$ достаточно $C^1$. При $f \in C^\infty$ — никаких ограничений.

Идея доказательства. Локализация через покрытие куба маленькими кубами и оценка образа по Тейлору: на критическом кубе остаток порядка $\|h\|^{k+1}$ сжимает образ в множество объёма $O(\varepsilon^{k+1} \cdot \varepsilon^{n-m})$ — выбор $k$ обеспечивает суммируемость.

Варианты и обобщения.
- **Morse–Sard**: $f \in C^\infty$ $\Rightarrow$ почти все значения регулярны.
- **Smale's infinite-dimensional Sard**: для Fredholm-отображений банаховых пространств.
- **Bates extension**: понижение требования гладкости для специальных $f$.

Используется в. Доказательство существования регулярных значений в дифференциальной топологии. В олимпиадных задачах редко напрямую, но как «фон»: $f: \mathbb{R}^n \to \mathbb{R}$ $C^\infty$ $\Rightarrow$ почти все уровневые множества — гладкие гиперповерхности. Эпизодически применяется в Miklós Schweitzer (теория меры + дифференциальная геометрия).

---

### E14. Rademacher's theorem (теорема Радемахера)

Формулировка. Каждое Lipschitz-отображение $f: \mathbb{R}^n \to \mathbb{R}^m$ дифференцируемо по Fréchet почти всюду по мере Лебега в $\mathbb{R}^n$.

Условия применимости. Lipschitz — глобально или локально (на каждом компакте). На полной мере точек $a$ существует линейное отображение $Df(a)$ с
$$\lim_{h\to 0} \frac{\|f(a+h) - f(a) - Df(a)h\|}{\|h\|} = 0.$$
Множество исключительных точек имеет меру нуль, но может быть всюду плотным.

Идея доказательства. По Lebesgue's theorem на дифференцируемость монотонных функций (через Vitali-cover, см. подтему 1D) каждая координатная функция $f_i$ имеет partial derivatives $\partial_j f_i$ почти всюду. Затем — через Fubini и аппроксимацию по линейным комбинациям — доказывается существование Fréchet-предела.

Варианты и обобщения.
- **Stepanov's theorem**: $f$ дифференцируема почти всюду на $\{x: \limsup_{y\to x}|f(y)-f(x)|/|y-x| < \infty\}$ (без глобальной Lipschitz).
- **Kirchheim**: расширение для метрических пространств $\mathbb{R}^n \to X$ (метрическая Rademacher).
- **Pansu Rademacher** на группах Карно — некоммутативный аналог.

Используется в. Geometric measure theory, теория BV-функций, доказательство существования tangent plane почти всюду у Lipschitz-графика. На олимпиадах — крайне редко, но как «контекст»: Lipschitz-условие даёт почти всюду гладкость без явных предположений.

---

## Self-test

1. Найди $f: \mathbb{R}^2 \to \mathbb{R}$ непрерывную в $0$ с существующими в $0$ всеми производными по направлениям, но не дифференцируемую в $0$ по Fréchet.

2. Положим $f(x,y) = xy(x^2-y^2)/(x^2+y^2)$ при $(x,y) \neq 0$, $f(0,0)=0$. Вычисли $\partial_y \partial_x f(0,0)$ и $\partial_x \partial_y f(0,0)$.

3. Пусть $f: \mathbb{R}^n \to \mathbb{R}$ — $C^1$ выпуклая функция с $\|\nabla f(x) - \nabla f(y)\| \leq L\|x-y\|$. Докажи:
$$\langle \nabla f(x) - \nabla f(y),\,x - y\rangle \geq \tfrac{1}{L}\|\nabla f(x) - \nabla f(y)\|^2.$$

4. Пусть $f: \mathbb{R}^n \to \mathbb{R}^n$ — $C^1$, $\|Df(x) - I\|_{\text{op}} \leq 1/2$ для всех $x$. Докажи, что $f$ — глобальный $C^1$-диффеоморфизм $\mathbb{R}^n$ на $\mathbb{R}^n$.

5. Пусть $f \in C^1(\mathbb{R}^n \setminus \{0\})$, $\langle x, \nabla f(x)\rangle = 0$ для $x \neq 0$. Докажи, что $f$ постоянна на каждом луче из начала и, как следствие, $f(x) = g(x/\|x\|)$ для некоторой функции $g$ на единичной сфере.

---

## Решения

1. Стандартный пример: $f(x,y) = x^3 y / (x^4 + y^2)$ при $(x,y)\neq 0$, $f(0,0)=0$. Для направления $v = (a, b)$, $b \neq 0$: $f(ta, tb)/t = t^2 a^3 b / (t^2 a^4 + b^2) \to 0$ при $t \to 0$, значит directional derivative $= 0$. По направлению $(a,0)$ — тривиально $0$. Значит все directional derivatives в $0$ существуют и равны $0$. Но $f$ не непрерывна: вдоль $y = x^2$ имеем $f(x, x^2) = x^5 / (2x^4) = x/2 \not\to 0$ нужным образом — точнее, $f(x, x^2) = x^5/(x^4+x^4) = x/2$, и в окрестности нуля принимает любые малые значения, но при этом $\sup_{|h|<\delta} f(h) = O(\delta)$ — функция непрерывна в нуле, но не Fréchet-дифференцируема, иначе линейное приближение дало бы $f(x, x^2) = o(\sqrt{x^2 + x^4}) \sim o(|x|)$, а $f(x, x^2) = x/2$, противоречие.

2. По E2 (Schwarz counterexample): прямой расчёт. $\partial_x f(x, y) = \partial_x \bigl[xy(x^2-y^2)/(x^2+y^2)\bigr]$ для $(x,y) \neq 0$:
$$\partial_x f = y \cdot \frac{(3x^2 - y^2)(x^2+y^2) - (x^3 - xy^2) \cdot 2x}{(x^2+y^2)^2} = y \cdot \frac{x^4 + 4x^2 y^2 - y^4}{(x^2+y^2)^2}.$$
В точке $(0, y)$ при $y \neq 0$: $\partial_x f(0, y) = y \cdot (-y^4)/y^4 = -y$. Поэтому $\partial_y \partial_x f(0, 0) = -1$.

Симметрично, $\partial_y f(x, 0) = x$ при $x \neq 0$ (по антисимметрии $f(x,y) = -f(y,x)$), откуда $\partial_x \partial_y f(0, 0) = 1$.

Mixed partials в нуле существуют, но **не равны**: $\partial_y\partial_x f(0,0) = -1 \neq 1 = \partial_x\partial_y f(0,0)$. Schwarz не применима, поскольку $\partial_x \partial_y f$ разрывна в нуле.

3. **IMC-2002-DAY2-6** — каноничный Baillon–Haddad. Положим $g(x) = f(x) - f(x_1) - \langle \nabla f(x_1), x - x_1\rangle$. Свойства: $g$ выпукла, $\nabla g(x) = \nabla f(x) - \nabla f(x_1)$ — $L$-Lipschitz, $g(x_1) = 0$, $\nabla g(x_1) = 0$. Поэтому $x_1$ — глобальный минимум $g$, и $g \geq 0$.

Из descent lemma (Taylor + $L$-Lipschitz $\nabla g$): для всех $x, y$,
$$g(y) \leq g(x) + \langle \nabla g(x), y - x\rangle + \tfrac{L}{2}\|y - x\|^2.$$
Минимизируя правую часть по $y$: $y^* = x - \nabla g(x)/L$, что даёт
$$0 \leq g(y^*) \leq g(x) - \tfrac{1}{2L}\|\nabla g(x)\|^2.$$
Применим к $x = x_2$: $g(x_2) \geq \tfrac{1}{2L}\|\nabla g(x_2)\|^2$, то есть
$$f(x_2) - f(x_1) - \langle\nabla f(x_1), x_2 - x_1\rangle \geq \tfrac{1}{2L}\|\nabla f(x_2) - \nabla f(x_1)\|^2.$$
Поменяв $x_1 \leftrightarrow x_2$, получим симметричное неравенство, складываем — линейные слагаемые комбинируются в $\langle \nabla f(x_2) - \nabla f(x_1), x_2 - x_1\rangle$, левая часть обнуляется, в итоге:
$$\langle \nabla f(x_2) - \nabla f(x_1), x_2 - x_1\rangle \geq \tfrac{1}{L}\|\nabla f(x_2) - \nabla f(x_1)\|^2. \qquad\blacksquare$$

4. По E7 (global Hadamard inverse function theorem). Локально: $\det Df(x) \neq 0$, поскольку $\|Df(x) - I\| \leq 1/2$ $\Rightarrow$ $Df(x)$ обратима ($\|(Df)^{-1}\| \leq 1/(1 - 1/2) = 2$ по Neumann series). Значит $f$ — локальный диффеоморфизм всюду.

Инъективность: для $x \neq y$,
$$f(y) - f(x) = \int_0^1 Df(x + t(y-x))(y-x)\,dt = (y-x) + \int_0^1 (Df - I)(y-x)\,dt,$$
$$\|f(y) - f(x)\| \geq \|y - x\| - \tfrac{1}{2}\|y - x\| = \tfrac{1}{2}\|y - x\| > 0.$$
Сюръективность (Hadamard's global IFT): нужно показать, что $f$ — proper. Из той же оценки $\|f(x)\| \geq \|x\| - \|f(0)\| - \tfrac{1}{2}\|x\| = \tfrac{1}{2}\|x\| - \|f(0)\|$, значит $\|x\| \to \infty \Rightarrow \|f(x)\| \to \infty$. Тогда $f^{-1}$ компактных множеств компактна, $f$ — собственное. Локальный диффеоморфизм + инъективность + сюръективность $\Rightarrow$ $f: \mathbb{R}^n \to \mathbb{R}^n$ — глобальный $C^1$-диффеоморфизм.

Альтернатива (Banach FP): для фиксированного $y$ ищем $x$ с $f(x) = y$. Положим $T(x) = x - (f(x) - y)$. Тогда $T'(x) = I - Df(x)$, $\|T'\| \leq 1/2$, и $T$ — сжатие на $\mathbb{R}^n$. Banach FP даёт единственный $x$ с $T(x) = x$, т.е. $f(x) = y$.

5. По E8 (Euler) и E11 (gradient zero $\Rightarrow$ constant). Положим $\phi_x(t) = f(tx)$ для $t > 0$, $x \neq 0$. По chain rule:
$$\phi_x'(t) = \langle x, \nabla f(tx)\rangle = \tfrac{1}{t}\langle tx, \nabla f(tx)\rangle = 0$$
по условию. Значит $\phi_x$ постоянна на $(0, \infty)$, т.е. $f(tx) = f(x)$ для всех $t > 0$.

Положив $t = 1/\|x\|$, получаем $f(x) = f(x/\|x\|) = g(x/\|x\|)$, где $g := f|_{S^{n-1}}$. Гладкость $g$: $f \in C^1$ ограниченное на компактной сфере — $g$ непрерывна; на сфере $g$ не наследует $C^1$ автоматически, но $g \in C^1(S^{n-1})$ как ограничение $C^1$-функции. $\blacksquare$
