---
topic: Многомерный анализ и топология
subtopic: "Якобиан, замена переменных в кратных интегралах, Fubini"
sources:
  - "Rudin — Real and Complex Analysis (ch. 7–8)"
  - "Rudin — Principles of Mathematical Analysis (ch. 10)"
  - "Spivak — Calculus on Manifolds"
  - "Zorich — Mathematical Analysis II (ch. 11)"
  - "Folland — Real Analysis (ch. 2, Fubini–Tonelli)"
  - "Stein–Shakarchi — Real Analysis (ch. 2–3)"
  - "Polya–Szegő — Problems and Theorems in Analysis I, II"
  - "Andreescu, Andrica — Putnam and Beyond"
  - "Engel — Problem-Solving Strategies"
  - "Federer — Geometric Measure Theory (Coarea formula)"
  - "Gardner — The Brunn–Minkowski Inequality (Bull. AMS, 2002)"
  - "Beukers — A note on the irrationality of ζ(2) and ζ(3) (1979)"
  - "IMC Compendium"
  - "Putnam Compendium"
problems_referenced:
  - IMC-1995-2
  - IMC-2009-DAY2-1
  - Putnam-1991-B5
  - Putnam-2005-A5
  - Putnam-2017-A5
last_updated: 2026-04-27
---

# Якобиан, замена переменных в кратных интегралах, Fubini

## Scope
Кратный интеграл Лебега в $\mathbb{R}^n$: формула замены переменных через определитель Якоби, Fubini–Tonelli как инструмент перестановки порядка интегрирования и сведения сумм к интегралам, переход в полярные / сферические / симплексные координаты, Cavalieri / layer-cake как мост между интегралом функции и мерой её супер-уровневых множеств. Включены инструменты доказательного уровня (Steinhaus, coarea, Brunn–Minkowski / Prékopa–Leindler) и стандартный набор «вычислительных» трюков, регулярно решающих задачи IMC / Putnam.

## Записи — Core

### E1. Change of Variables theorem (формула замены переменных)

Формулировка. Пусть $U \subset \mathbb{R}^n$ открыто, $\varphi : U \to V \subset \mathbb{R}^n$ — $C^1$-диффеоморфизм, $f : V \to \mathbb{R}$ Лебег-интегрируема. Тогда
$$\int_V f(y)\,dy = \int_U f(\varphi(x))\,|\det D\varphi(x)|\,dx.$$

Условия применимости. Достаточно: $\varphi$ инъективна на $U$, $C^1$, $\det D\varphi \neq 0$ п.в. (в форме Sard / Federer хватает $\varphi$ Lipschitz и инъективна). Знак — модуль, ориентация теряется. На границе или на множестве меры нуль ($\det D\varphi = 0$) условие можно ослабить.

Идея доказательства. Локально $\varphi$ аппроксимируется аффинной картой, на ней Якобиан — это ровно отношение объёмов. Глобально склейка через partition of unity и аппроксимацию интегрируемой функции простыми.

Варианты и обобщения.
- Lipschitz-замена + теорема Радемахера: $\varphi$ дифференцируема п.в., формула остаётся.
- Не-инъективная замена: справа появляется $\sum_{x \in \varphi^{-1}(y)} \frac{f(\varphi(x))}{|\det D\varphi(x)|}$ или эквивалентно area / coarea formula (см. E11).
- Линейный случай: $|\det A| = \mathrm{vol}(A([0,1]^n))$ — базовый «атом».

Используется в. [Putnam-1991-B5, IMC-2009-DAY2-1, любая задача с переходом в полярные / сферические координаты].

---

### E2. Fubini–Tonelli theorem

Формулировка. Пусть $(X, \mu)$, $(Y, \nu)$ — $\sigma$-конечные measure spaces, $f : X \times Y \to \mathbb{R}$ измерима. Тогда:
- (Tonelli) если $f \geq 0$, то
$$\int_{X \times Y} f\,d(\mu \otimes \nu) = \int_X \!\!\int_Y f(x,y)\,d\nu(y)\,d\mu(x) = \int_Y \!\!\int_X f(x,y)\,d\mu(x)\,d\nu(y),$$
все три значения совпадают (могут быть $+\infty$).
- (Fubini) если $f$ интегрируема, $\int |f| < \infty$, то порядок интегрирования меняется и iterated integrals совпадают с двойным.

Условия применимости. $\sigma$-конечность критична: на $[0,1] \times \{$считающая мера на $[0,1]\}$ Fubini ломается. Без Tonelli-проверки $\int |f|$ Fubini может дать разные ответы — классический пример $f(x,y) = (x^2-y^2)/(x^2+y^2)^2$ на $[0,1]^2$ даёт $\pi/4$ и $-\pi/4$.

Идея доказательства. Сначала для индикаторов прямоугольников, потом для индикаторов измеримых множеств через $\pi$-$\lambda$ / монотонные классы, потом — для простых функций, MCT для не-отрицательных, разбиение $f = f^+ - f^-$ для интегрируемых.

Варианты и обобщения.
- Дискретная Fubini: $\sum_i \sum_j a_{ij} = \sum_j \sum_i a_{ij}$ при $\sum |a_{ij}| < \infty$ или $a_{ij} \geq 0$.
- Fubini для рядов и интегралов смешанно: $\sum_n \int f_n = \int \sum_n f_n$ при абсолютной сходимости.
- Стохастическая Fubini (Itô).

Используется в. [IMC-1995-2 (двойной интеграл переводит $\int_x^1 f$ в $\int x f$), Putnam-2005-A5, Putnam-2017-A5, любой Frullani / Dirichlet trick].

---

### E3. Cavalieri / Layer cake representation (формула «слоёного пирога»)

Формулировка. Пусть $f : X \to [0, \infty]$ измерима, $\mu$ — $\sigma$-конечная. Тогда для $p > 0$
$$\int_X f^p\,d\mu = p \int_0^\infty t^{p-1}\,\mu(\{f > t\})\,dt.$$
В частности при $p = 1$:
$$\int_X f\,d\mu = \int_0^\infty \mu(\{f > t\})\,dt.$$

Условия применимости. $f \geq 0$ и измерима. Без неотрицательности — раскладывать на $f^+ - f^-$. На правой части интеграл обычно понимается как Lebesgue по $t$ или Riemann (совпадают: $t \mapsto \mu(\{f>t\})$ монотонно убывает, значит — функция Riemann-интегрируема на любом конечном отрезке).

Идея доказательства. Записать $f^p(x) = p \int_0^{f(x)} t^{p-1}\,dt = p \int_0^\infty t^{p-1} \mathbf{1}_{f(x) > t}\,dt$ и применить Tonelli по $(x, t)$.

Варианты и обобщения.
- Симметричное переупорядочивание: $\int f^p$ зависит только от distribution function $\mu_f(t) = \mu(\{f > t\})$ — основа теории $L^p$, weak-$L^p$, Lorentz spaces.
- Bathtub principle: при фиксированном $\mu_f$ $\int f g$ максимальна, когда $f$ и $g$ равно-распределены и сонаправлены.

Используется в. [любой подсчёт через распределение значений; задача «expected value of a non-negative random variable equals $\int_0^\infty P(X > t)\,dt$»].

---

### E4. Polar / spherical coordinates в $\mathbb{R}^n$ + объём шара

Формулировка. Замена $x = r\omega$, $r \in (0, \infty)$, $\omega \in S^{n-1}$:
$$\int_{\mathbb{R}^n} f(x)\,dx = \int_0^\infty \!\!\int_{S^{n-1}} f(r\omega)\,r^{n-1}\,d\sigma(\omega)\,dr,$$
где $d\sigma$ — surface measure на $S^{n-1}$. Полная масса: $\sigma(S^{n-1}) = \frac{2\pi^{n/2}}{\Gamma(n/2)}$.

Объём $n$-шара: $V_n(R) = \frac{\pi^{n/2}}{\Gamma(n/2 + 1)} R^n$.

Условия применимости. $f$ радиально интегрируема (Tonelli по $(r, \omega)$). Якобиан $r^{n-1}$ — следствие однородности.

Идея доказательства. Записать Gaussian integral двумя способами:
$$\pi^{n/2} = \int_{\mathbb{R}^n} e^{-\|x\|^2}\,dx = \sigma(S^{n-1}) \int_0^\infty e^{-r^2} r^{n-1}\,dr = \sigma(S^{n-1}) \cdot \tfrac{1}{2}\Gamma(n/2),$$
отсюда $\sigma(S^{n-1})$. Объём шара — $\int_0^R \sigma(S^{n-1}) r^{n-1}\,dr$.

Варианты и обобщения.
- Anisotropic scaling $x \mapsto Ax$ диффеоморфизмом сводит объём эллипсоида $\{Ax \in B\}$ к $|\det A^{-1}| V_n$.
- В $n = 2$: $r$, в $n = 3$: $r^2 \sin\theta$, в общем $n$: $r^{n-1} \prod_{k=1}^{n-2} \sin^{n-1-k}\varphi_k$.
- Обратная задача (объём $\to$ радиус): полезна когда условие на $|x|$ задаёт регион.

Используется в. [IMC-2009-DAY2-1 (после линейной замены — единичный шар), любая задача с радиально-симметричной функцией].

---

## Записи — Standard

### E5. Beukers double integral для $\zeta(2)$

Формулировка.
$$\int_0^1 \!\!\int_0^1 \frac{dx\,dy}{1 - xy} = \sum_{n=0}^\infty \frac{1}{(n+1)^2} = \zeta(2) = \frac{\pi^2}{6}.$$

Условия применимости. Подынтегральная функция неотрицательна — Tonelli работает безусловно, несмотря на singularity в $(1,1)$.

Идея доказательства. Геометрический ряд $\frac{1}{1-xy} = \sum_{n=0}^\infty (xy)^n$, Tonelli меняет $\sum$ и $\int\int$, $\int_0^1 x^n\,dx \cdot \int_0^1 y^n\,dy = \frac{1}{(n+1)^2}$. Beukers использовал подобные интегралы для доказательства иррациональности $\zeta(2)$ и $\zeta(3)$.

Варианты и обобщения.
- $\zeta(3) = \frac{1}{2}\int_0^1\!\int_0^1\!\int_0^1 \frac{dx\,dy\,dz}{1 - xyz}$ (с поправочным фактором).
- Замена $u = (1-x)/(1-xy)$, $v = y$ (Beukers' substitution) — диффеоморфизм $(0,1)^2 \to (0,1)^2$, превращает интеграл в нечто рациональное от $u, v$.
- Hadjicostas's formula: однопараметрическое семейство.

Используется в. [Beukers 1979; стандартный демо-пример «двойной интеграл $\to$ сумма ряда»].

---

### E6. Liouville–Dirichlet integral на симплексе

Формулировка. На стандартном $n$-симплексе $\Delta_n = \{x \in \mathbb{R}_+^n : \sum x_i \leq 1\}$:
$$\int_{\Delta_n} x_1^{\alpha_1 - 1} \cdots x_n^{\alpha_n - 1} (1 - x_1 - \cdots - x_n)^{\alpha_{n+1} - 1}\,dx = \frac{\Gamma(\alpha_1) \cdots \Gamma(\alpha_{n+1})}{\Gamma(\alpha_1 + \cdots + \alpha_{n+1} + 1)}\cdot \frac{1}{\Gamma(\alpha_1 + \cdots + \alpha_{n+1})}\cdot\Gamma(\alpha_1+\dots+\alpha_{n+1}),$$
проще говоря (приведённая форма):
$$\int_{\Delta_n} \prod_{i=1}^n x_i^{\alpha_i - 1}\,dx = \frac{\prod_{i=1}^n \Gamma(\alpha_i)}{\Gamma(1 + \sum_{i=1}^n \alpha_i)}.$$

В частности: $\mathrm{vol}(\Delta_n) = 1/n!$ (положить все $\alpha_i = 1$).

Условия применимости. $\alpha_i > 0$. Liouville's extension покрывает интегралы вида $\int_{\Delta} f(x_1 + \cdots + x_n) \prod x_i^{\alpha_i - 1}\,dx$ — сводится к одномерному интегралу $f$.

Идея доказательства. Сделать замену $y_k = x_1 + \cdots + x_k$ (или $x_n = (1 - \sum_{i<n})t_n$, иерархическая stick-breaking замена). Якобиан явно вычисляется, интеграл расщепляется на $n$ независимых Beta-интегралов.

Варианты и обобщения.
- Dirichlet distribution: PDF в точности интегрант после нормализации.
- Selberg integral — многомерное обобщение Beta с антисимметричным фактором $\prod_{i < j} |x_i - x_j|^{2\gamma}$.

Используется в. [Putnam-2005-A5 (объём $\{x_i \geq 0, \sum x_i \leq 1\}$ и его обобщения); базовое тождество для подсчётов на симплексе].

---

### E7. Frullani integral через Fubini

Формулировка. Пусть $f$ непрерывна на $[0, \infty)$, $f(0) = A$, $f(\infty) = B$ существует. Тогда для $a, b > 0$
$$\int_0^\infty \frac{f(ax) - f(bx)}{x}\,dx = (A - B)\ln \tfrac{b}{a}.$$

Условия применимости. Основная: $\lim_{x \to 0^+} f(x)$ и $\lim_{x \to \infty} f(x)$ существуют (конечны или одно из них $\pm\infty$ с правильным контролем). Если предел на бесконечности не существует, но $f$ ограничена, формула не работает в простом виде.

Идея доказательства. Записать $f(ax) - f(bx) = -\int_a^b \frac{d}{dt}f(tx)\,dt = -\int_a^b x f'(tx)\,dt$. Тогда
$$\int_0^\infty \frac{f(ax) - f(bx)}{x}\,dx = -\int_0^\infty \!\!\int_a^b f'(tx)\,dt\,dx \stackrel{\text{Fubini}}{=} -\int_a^b \!\!\int_0^\infty f'(tx)\,dx\,dt = -\int_a^b \frac{B - A}{t}\,dt.$$

Варианты и обобщения.
- $\int_0^\infty \frac{\arctan(ax) - \arctan(bx)}{x}\,dx = \tfrac{\pi}{2}\ln(a/b)$ — частный случай.
- Альтернативное доказательство — параметрическое дифференцирование по $a$.

Используется в. [Putnam, IMC — стандартный приём «представить как двойной интеграл»].

---

### E8. Dirichlet integral $\int_0^\infty \sin x / x$ через Fubini

Формулировка.
$$\int_0^\infty \frac{\sin x}{x}\,dx = \frac{\pi}{2}.$$

Условия применимости. Интеграл — improper, не абсолютно сходится. Поэтому буквальная Fubini для $|f|$ не работает; нужно регуляризовать $e^{-tx}\sin x$ или интегрировать по конечному отрезку и переходить к пределу.

Идея доказательства. Использовать $\frac{1}{x} = \int_0^\infty e^{-xt}\,dt$ при $x > 0$:
$$\int_0^\infty \frac{\sin x}{x}\,dx = \int_0^\infty \!\!\int_0^\infty e^{-xt} \sin x\,dt\,dx \stackrel{\text{Fubini}}{=} \int_0^\infty \frac{1}{1 + t^2}\,dt = \frac{\pi}{2}.$$
Перестановка обоснована через $\int_0^R$ и контроль остатка.

Варианты и обобщения.
- $\int_0^\infty \frac{\sin(ax)}{x}\,dx = \frac{\pi}{2}\,\mathrm{sgn}(a)$.
- $\int_0^\infty \frac{\sin^2 x}{x^2}\,dx = \frac{\pi}{2}$ (через $\sin^2 = (1-\cos 2x)/2$ и Frullani).
- $\int_0^\infty \frac{\sin x}{x} e^{-tx}\,dx = \arctan(1/t)$ — регуляризованная версия, всегда абсолютно сходится.

Используется в. [Putnam-1991-B5 (Laplace transforms); базовая «обвертка» Fubini].

---

### E9. Steinhaus theorem (теорема Штейнгауза о difference set)

Формулировка. Пусть $A \subset \mathbb{R}^n$ Lebesgue-измерим и $\lambda(A) > 0$. Тогда $A - A = \{a - b : a, b \in A\}$ содержит окрестность нуля. То же для $A + A$ при $A$ положительной меры в $\mathbb{R}$.

Условия применимости. Только Lebesgue-измеримость и положительная мера. На канторовом множестве с мерой нуль теорема не работает (контрпример — $C - C = [-1,1]$ всё-таки содержит интервал, но это совпадение). Рассматривать на $\mathbb{R}^n$ — формулировка та же.

Идея доказательства. Свёртка $\mathbf{1}_A * \mathbf{1}_{-A}(x) = \int \mathbf{1}_A(y) \mathbf{1}_A(y - x)\,dy = \lambda(A \cap (A + x))$ непрерывна по $x$ (Fubini + dominated convergence) и равна $\lambda(A) > 0$ при $x = 0$, значит положительна в окрестности — что и означает, что $A \cap (A + x) \neq \emptyset$, т.е. $x \in A - A$.

Варианты и обобщения.
- В $\mathbb{R}^n$: $A + B$ содержит open set, если $\lambda(A), \lambda(B) > 0$.
- В locally compact group: difference set измеримого множества положительной Haar-меры содержит окрестность $e$.
- Pillai–Steinhaus: для $A \subset \mathbb{R}^n$ положительной меры, $A - A$ содержит шар.

Используется в. [классические задачи о существовании рациональных / специальных точек в множествах положительной меры; «non-measurable set construction»].

---

### E10. Reduction to unit ball / canonical form через линейную замену

Формулировка. Если регион интегрирования задан квадратичной формой / линейными неравенствами, переход $x = Ay$ с $A$ — нижнетреугольной (Cholesky) или ортогональной (диагонализация) — превращает регион в единичный шар / куб / симплекс. Объём считается тривиально, обратный Якобиан — $|\det A|$.

Условия применимости. Положительная определённость квадратичной формы (для эллипсоида), невырожденность $A$. Для аффинных регионов — переход $y = A^{-1}(x - x_0)$.

Идея доказательства. $\{x : x^T M x \leq 1\}$ при $M = A^T A > 0$ переводится в $\{y : \|y\|^2 \leq 1\}$ заменой $x = A^{-1} y$, объём = $\det A^{-1} \cdot V_n = V_n / \sqrt{\det M}$.

Варианты и обобщения.
- Симметризация Steiner: на каждом шаге заменяет регион симметричным относительно гиперплоскости с тем же объёмом — используется для изопериметрических неравенств.
- Affine isoperimetric inequalities — поведение функционалов под линейным преобразованием.

Используется в. [IMC-2009-DAY2-1 (объём $\{|X\ell|^2 \geq 4|XP|^2\} = $ эллипсоид $\to$ шар, ответ $16\pi d^3/(27\sqrt 3)$)].

---

## Записи — Exotic

### E11. Coarea formula (формула коплощади, Federer)

Формулировка. Пусть $u : \mathbb{R}^n \to \mathbb{R}$ Lipschitz, $f : \mathbb{R}^n \to [0, \infty]$ измерима. Тогда
$$\int_{\mathbb{R}^n} f(x) |\nabla u(x)|\,dx = \int_{-\infty}^\infty \!\!\int_{u^{-1}(t)} f(x)\,d\mathcal{H}^{n-1}(x)\,dt,$$
где $\mathcal{H}^{n-1}$ — $(n-1)$-мерная Hausdorff measure.

Условия применимости. $u$ Lipschitz (или $W^{1,1}_{\mathrm{loc}}$). Уровневые множества $u^{-1}(t)$ для п.в. $t$ — $(n-1)$-rectifiable (Sard в Lipschitz-версии).

Идея доказательства. Локально для гладкой $u$ с $\nabla u \neq 0$ — следствие замены переменных в «прямоугольных» координатах $(t, $ касательная гиперплоскость$)$. Глобально склейка через approximation gladkimi Lipschitz-функциями.

Варианты и обобщения.
- $f \equiv 1$: $\int |\nabla u|\,dx = \int \mathcal{H}^{n-1}(\{u = t\})\,dt$ — TV-norm $u$.
- При $u(x) = |x|$ — восстановление сферической формулы.
- В размерности $u : \mathbb{R}^n \to \mathbb{R}^k$, $k < n$ — area formula с гиперплоскостями коразмерности $k$.

Используется в. [геометрический анализ, изопериметрические неравенства; в IMC напрямую — редко, но в задачах с уровневыми множествами полезна как «sanity check»].

---

### E12. Prékopa–Leindler / Brunn–Minkowski

Формулировка (Prékopa–Leindler). Пусть $f, g, h : \mathbb{R}^n \to [0, \infty)$ измеримы, $\lambda \in (0, 1)$, и для всех $x, y \in \mathbb{R}^n$
$$h(\lambda x + (1-\lambda) y) \geq f(x)^\lambda g(y)^{1-\lambda}.$$
Тогда
$$\int_{\mathbb{R}^n} h \geq \left(\int f\right)^\lambda \left(\int g\right)^{1-\lambda}.$$

Brunn–Minkowski (следствие). Для непустых компактных $A, B \subset \mathbb{R}^n$:
$$\mathrm{vol}(A + B)^{1/n} \geq \mathrm{vol}(A)^{1/n} + \mathrm{vol}(B)^{1/n}.$$

Условия применимости. Измеримость $f, g, h$. В Brunn–Minkowski достаточно компактности (можно ослабить до измеримых множеств положительной меры, тогда $A + B$ может быть не-измерим, но содержит измеримое множество с правильной оценкой).

Идея доказательства. Tensorisation: одномерный случай через перестановочное неравенство и Cavalieri-разбиение, потом индукция по $n$ с применением Fubini для разрезания на slice'ы. Brunn–Minkowski получается подстановкой $f = \mathbf{1}_A$, $g = \mathbf{1}_B$, $h = \mathbf{1}_{\lambda A + (1-\lambda) B}$ и масштабированием.

Варианты и обобщения.
- Functional form $\Rightarrow$ isoperimetric inequality в $\mathbb{R}^n$.
- Gaussian variant (Ehrhard inequality): то же с гауссовой мерой и $\Phi^{-1}$.

Используется в. [конвексная геометрия, аддитивная комбинаторика; в IMC — редко напрямую, но как мост между volume и Minkowski sums].

---

### E13. Crofton / Cauchy formula (интегральная геометрия)

Формулировка. Для выпуклого тела $K \subset \mathbb{R}^n$:
$$\mathrm{surface}(K) = c_n \int_{S^{n-1}} \mathrm{vol}_{n-1}(\pi_\omega K)\,d\sigma(\omega),$$
где $\pi_\omega$ — ортогональная проекция на гиперплоскость, перпендикулярную $\omega$, $c_n$ — явная нормировка.

Особый случай (Crofton, $n = 2$). Длина гладкой кривой $\gamma$ на плоскости равна
$$L(\gamma) = \frac{1}{2} \int_{\mathrm{lines}} \#(\gamma \cap \ell)\,d\ell,$$
интегрирование по mера на пространстве прямых, инвариантной относительно евклидовой группы.

Условия применимости. Выпуклость для Cauchy, спрямляемость (или $C^1$) для Crofton. Мера на пространстве прямых — $d\rho \, d\theta$, где прямая параметризуется $(\rho, \theta)$.

Идея доказательства. Fubini: $\#(\gamma \cap \ell) = \int_\gamma \mathbf{1}_{x \in \ell}\,ds$ — затем интегрирование $d\ell$ выделяет invariant measure, остаток — нормировка через unit segment.

Варианты и обобщения.
- Для непрямых линий — Cauchy–Crofton с тангенциальным углом.
- Многомерная Cauchy: integral geometry, Hadwiger characterization theorem.

Используется в. [олимпиадные задачи о длинах кривых, числе пересечений отрезков; контр-примеры на «среднее число пересечений»].

---

## Self-test

1. Найти $\displaystyle\int_0^1\!\!\int_0^1 \frac{dx\,dy}{1 - xy}$.

2. Найти $\mathrm{vol}\{(x_1, \ldots, x_n) \in \mathbb{R}_+^n : x_1 + x_2 + \cdots + x_n \leq 1\}$.

3. Доказать $\displaystyle\int_0^\infty \frac{\sin x}{x}\,dx = \frac{\pi}{2}$.

4. Найти $\displaystyle\int_{\mathbb{R}^n} e^{-\|x\|^2}\,dx$ двумя способами и из равенства вывести объём $S^{n-1}$.

5. Пусть $f : [0, 1] \to [0, \infty)$ измерима. Доказать
$$\int_0^1 f(x)^p\,dx = p \int_0^\infty t^{p-1}\,\lambda(\{x : f(x) > t\})\,dt \quad (p > 0).$$

6. Пусть $A \subset \mathbb{R}$ Lebesgue-измеримо, $\lambda(A) > 0$. Доказать, что $A - A$ содержит интервал $(-\delta, \delta)$ при некотором $\delta > 0$.

7. Найти $\displaystyle\int_0^{\pi/2} \ln \sin x\,dx$.

8. Найти $\displaystyle\int_0^\infty \frac{e^{-ax} - e^{-bx}}{x}\,dx$ для $a, b > 0$.

9. Пусть $X_1, \ldots, X_n$ — независимые $\mathrm{Uniform}(0, 1)$. Найти $P(X_1 + \cdots + X_n \leq 1)$.

10. Пусть $f \in L^1(\mathbb{R}^n)$, $\hat f(\xi) = \int e^{-2\pi i \langle x, \xi\rangle} f(x)\,dx$. Доказать, что $\widehat{f * g} = \hat f \cdot \hat g$ при $f, g \in L^1$.

## Решения

1. $\frac{1}{1-xy} = \sum_{n \geq 0} (xy)^n$, Tonelli даёт $\sum_{n \geq 0} \frac{1}{(n+1)^2} = \zeta(2) = \pi^2/6$.

2. По Liouville–Dirichlet (E6) с $\alpha_i = 1$, $\alpha_{n+1} = 1$: $\mathrm{vol} = \frac{1}{\Gamma(n+2)} \cdot \Gamma(n+1)$ — переписать аккуратно, получается $1/n!$. Альтернативно: индукция по $n$, $\int_0^1 \mathrm{vol}(\Delta_{n-1}^{(t)})\,dt = \int_0^1 \frac{(1-t)^{n-1}}{(n-1)!}\,dt = \frac{1}{n!}$.

3. Записать $\frac{1}{x} = \int_0^\infty e^{-tx}\,dt$, поменять порядок (через $\int_0^R$ и предел): $\int_0^\infty \frac{\sin x}{x}\,dx = \int_0^\infty \frac{1}{1+t^2}\,dt = \pi/2$.

4. $(\int e^{-x^2}\,dx)^n = \pi^{n/2}$ по Fubini. С другой стороны — полярные координаты: $\int_0^\infty e^{-r^2} r^{n-1}\,dr \cdot \sigma(S^{n-1}) = \tfrac{1}{2}\Gamma(n/2)\sigma(S^{n-1})$, отсюда $\sigma(S^{n-1}) = 2\pi^{n/2}/\Gamma(n/2)$.

5. $f^p(x) = \int_0^{f(x)} p t^{p-1}\,dt = \int_0^\infty p t^{p-1} \mathbf{1}_{\{f > t\}}(x)\,dt$. Tonelli по $(x, t)$ даёт требуемое.

6. $\varphi(x) := \lambda(A \cap (A + x)) = \int \mathbf{1}_A(y)\mathbf{1}_A(y-x)\,dy$ непрерывна (свёртка двух $L^1$-функций), $\varphi(0) = \lambda(A) > 0$, значит $\varphi(x) > 0$ при $|x| < \delta$. $\varphi(x) > 0 \Rightarrow x \in A - A$.

7. $I = \int_0^{\pi/2} \ln\sin x\,dx$. Замена $x \to \pi/2 - x$: $I = \int_0^{\pi/2} \ln \cos x\,dx$. Сумма $2I = \int_0^{\pi/2} \ln(\sin x \cos x)\,dx = \int_0^{\pi/2} \ln \frac{\sin 2x}{2}\,dx = \frac{1}{2}\int_0^{\pi}\ln\sin u\,du - \frac{\pi}{2}\ln 2 = I - \frac{\pi}{2}\ln 2$, откуда $I = -\frac{\pi}{2}\ln 2$.

8. Frullani с $f(x) = e^{-x}$, $f(0) = 1$, $f(\infty) = 0$: $I = (1 - 0) \ln(b/a) = \ln(b/a)$.

9. По Liouville–Dirichlet $P = \mathrm{vol}(\Delta_n) = 1/n!$.

10. $\widehat{f*g}(\xi) = \int\!\!\int e^{-2\pi i \langle x, \xi\rangle} f(y) g(x-y)\,dy\,dx$. Fubini (контроль через $\int |f||g| < \infty$), замена $u = x - y$: $\int e^{-2\pi i \langle y, \xi\rangle} f(y)\,dy \cdot \int e^{-2\pi i \langle u, \xi\rangle} g(u)\,du = \hat f(\xi) \hat g(\xi)$.
