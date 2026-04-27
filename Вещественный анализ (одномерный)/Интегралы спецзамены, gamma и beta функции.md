---
topic: Вещественный анализ (одномерный)
subtopic: "Интегралы: спецзамены, специальные интегралы, gamma и beta функции, тождество Γ(x)Γ(1-x)=π/sin πx"
sources:
  - "Whittaker, Watson — A Course of Modern Analysis"
  - "Andrews, Askey, Roy — Special Functions"
  - "Lebedev — Special Functions and Their Applications"
  - "Polya, Szegő — Problems and Theorems in Analysis I"
  - "Bender, Orszag — Advanced Mathematical Methods for Scientists and Engineers"
  - "De Bruijn — Asymptotic Methods in Analysis"
  - "Andreescu, Andrica — Putnam and Beyond"
  - "Engel — Problem-Solving Strategies"
  - "Glasser — A Remarkable Property of Definite Integrals (1983)"
  - "IMC Compendium"
  - "Putnam Compendium"
problems_referenced:
  - IMC-1994-5
  - IMC-1995-4
  - IMC-1995-DAY2-5
  - IMC-1996-2
  - IMC-1996-5
  - IMC-1997-1
  - IMC-1998-6
  - IMC-2001-3
  - IMC-2003-5
  - IMC-2003-DAY2-2
  - IMC-2004-DAY2-5
  - IMC-2015-7
  - Putnam-2005-A5
  - Putnam-2009-B3
  - Putnam-2013-B2
last_updated: 2026-04-26
---

# Интегралы: спецзамены, специальные интегралы, gamma и beta функции, тождество $\Gamma(x)\Gamma(1-x)=\pi/\sin\pi x$

## Scope
Точное вычисление и асимптотики одномерных интегралов на олимпиадном уровне: тождества для $\Gamma$ и $B$, рефлексия и duplication, Frullani, Glasser, симметрии (King's rule, $x\mapsto 1/x$, $x\mapsto a+b-x$), tan-half (Weierstrass), differentiation under the integral sign, Riemann sum как способ сворачивать предел в интеграл и обратно, Laplace's method, периодическое усреднение, Wallis. Не покрывает: контурное интегрирование, Mellin-преобразование, общую теорию специальных функций.

## Записи — Core

### E1. Euler reflection formula (формула отражения Эйлера)

Формулировка. Для $x \in \mathbb{C} \setminus \mathbb{Z}$
$$\Gamma(x)\,\Gamma(1-x) = \frac{\pi}{\sin\pi x}.$$
В частности, $\Gamma(1/2) = \sqrt{\pi}$ и $\Gamma(x)\Gamma(-x) = -\pi/(x\sin\pi x)$.

Условия применимости. $x \notin \mathbb{Z}$. На действительной оси работает в интервалах между полюсами; обе стороны мероморфны и совпадают как функции комплексного переменного.

Идея доказательства. Beta-интеграл $\int_0^\infty t^{x-1}/(1+t)\,dt = B(x,1-x) = \Gamma(x)\Gamma(1-x)$ при $0<x<1$; отдельно $\int_0^\infty t^{x-1}/(1+t)\,dt = \pi/\sin\pi x$ — например, через разложение $1/(1+t) = \sum (-t)^n$ на $[0,1]$ и замену $t\mapsto 1/t$ на $[1,\infty)$, или через произведение Вейерштрасса $1/\Gamma(x) = x e^{\gamma x}\prod (1+x/n)e^{-x/n}$ и тождество $\sin\pi x = \pi x \prod (1-x^2/n^2)$.

Варианты и обобщения.
- **Beta–reflection**: $B(x, 1-x) = \pi/\sin\pi x$.
- **Hurwitz / multiplication**: $\prod_{k=0}^{n-1}\Gamma\!\left(x+\tfrac{k}{n}\right) = (2\pi)^{(n-1)/2} n^{1/2 - nx}\Gamma(nx)$ (Gauss multiplication).
- $\Gamma'(1) = -\gamma$, $\psi(x) = \Gamma'(x)/\Gamma(x)$, $\psi(x) - \psi(1-x) = -\pi\cot\pi x$ (digamma reflection — производная reflection-формулы).

Используется в. [Putnam-2005-A5, IMC-2003-DAY2-2, многочисленные задачи на $\int_0^\infty x^{p-1}/(1+x^q)\,dx$, $\int_0^{\pi/2}\ln\sin$].

---

### E2. Beta function (бета-функция Эйлера) и тригонометрическая форма

Формулировка. Для $\operatorname{Re} p, \operatorname{Re} q > 0$
$$B(p, q) = \int_0^1 t^{p-1}(1-t)^{q-1}\,dt = \frac{\Gamma(p)\Gamma(q)}{\Gamma(p+q)}.$$
Тригонометрическая форма (замена $t = \sin^2\theta$):
$$B(p, q) = 2\int_0^{\pi/2}\sin^{2p-1}\!\theta\,\cos^{2q-1}\!\theta\,d\theta.$$
Рациональная форма (замена $t = u/(1+u)$):
$$B(p,q) = \int_0^\infty \frac{u^{p-1}}{(1+u)^{p+q}}\,du.$$

Условия применимости. $\operatorname{Re} p, \operatorname{Re} q > 0$ (иначе расходится у $0$ или $1$). Не путать с $\int_0^\infty t^{p-1}/(1+t)\,dt$, который равен $B(p, 1-p)$ при $0<p<1$.

Идея доказательства. $\Gamma(p)\Gamma(q) = \int\!\!\int_{x,y>0} e^{-x-y} x^{p-1} y^{q-1} dx\,dy$, замена $x = ts$, $y = (1-t)s$ — Jacobian $s$, факторизуется в $\Gamma(p+q) B(p,q)$.

Варианты и обобщения.
- $\int_0^{\pi/2}\sin^a\theta \cos^b\theta\, d\theta = \tfrac{1}{2} B\!\left(\tfrac{a+1}{2}, \tfrac{b+1}{2}\right)$ при $a, b > -1$.
- $\int_0^\infty x^{s-1}/(1+x^n)\,dx = \tfrac{\pi}{n\sin(\pi s/n)}$ ($0 < s < n$): замена $u = x^n$ + reflection.
- **Dirichlet integral на симплексе**: $\int_{\Delta} \prod x_i^{p_i - 1} = \prod \Gamma(p_i)/\Gamma(\sum p_i)$.

Используется в. [IMC-1998-6, Putnam-2009-B3 (variant), задачи с интегралами вида $\int x^a (1-x^b)^c\,dx$].

---

### E4. King's rule / симметрия $x \mapsto a+b-x$

Формулировка. Для интегрируемой $f$ на $[a, b]$
$$\int_a^b f(x)\,dx = \int_a^b f(a + b - x)\,dx.$$
Стандартное следствие: если $f(x) + f(a+b-x) = h(x)$ — простая функция, интеграл $= \tfrac{1}{2}\int_a^b h$.

Условия применимости. Только integrability. Сила приёма — в выборе подынтегральной функции: $f(x) = g(x)/(g(x) + g(a+b-x))$ даёт $\int = (b-a)/2$.

Идея доказательства. Линейная замена $u = a + b - x$.

Варианты и обобщения.
- $\int_0^{\pi/2} f(\sin x)\,dx = \int_0^{\pi/2} f(\cos x)\,dx$.
- $\int_0^1 \ln(1+x)/(1+x^2)\,dx = \tfrac{\pi}{8}\ln 2$ — берётся через $x = \tan\theta$ + King.
- **"Sneaky" Putnam tricks**: $\int_a^b f(x)/(f(x)+f(a+b-x))\,dx = (b-a)/2$.

Используется в. [Putnam-1987-B1, IMC-1996-2, IMC-1998-6 (как $x = \sin\theta, y = \cos\theta$); один из самых частых приёмов на тригонометрические интегралы].

---

### E7. Differentiation under the integral sign (Feynman trick / правило Лейбница)

Формулировка. Если $F(\alpha) = \int_a^b f(x, \alpha)\,dx$, $f, \partial_\alpha f$ непрерывны и существует интегрируемая $g$ с $|\partial_\alpha f(x,\alpha)| \leq g(x)$ в окрестности $\alpha_0$, то
$$F'(\alpha_0) = \int_a^b \partial_\alpha f(x, \alpha_0)\,dx.$$
Для несобственных пределов — равномерная сходимость по $\alpha$.

Условия применимости. Доминирующая интегрируемая мажоранта (dominated convergence) или равномерная сходимость на компактах. Edge case: $\int_0^\infty \sin(\alpha x)/x\,dx$ требует регуляризации $e^{-\beta x}$, потому что $\sin(\alpha x)/x$ не доминируется одной интегрируемой функцией при $\alpha$, бегущем по $\mathbb{R}$.

Идея доказательства. Tonelli/Fubini для конечных интегралов; для несобственных — равномерная сходимость + замкнутость дифференцирования в $C^1$.

Варианты и обобщения.
- **Dirichlet integral**: $I(\alpha) = \int_0^\infty e^{-\alpha x}\sin x/x\,dx$, $I'(\alpha) = -\int_0^\infty e^{-\alpha x}\sin x\,dx = -1/(1+\alpha^2)$, $I(0^+) = \pi/2$.
- **Gauss integral parametрически**: $\int_0^\infty e^{-x^2}\cos(2\alpha x)\,dx = (\sqrt\pi/2) e^{-\alpha^2}$ — дифференцирование по $\alpha$ даёт ODE первого порядка.
- $\int_0^\infty (e^{-ax} - e^{-bx})/x\,dx = \ln(b/a)$ — частный случай Frullani через дифференцирование по параметру и Frullani-кэп.

Используется в. [Многие IMC/Putnam с параметрическим семейством интегралов; Putnam-2005-A5].

---

### E9. Riemann sum recognition (Riemann-сумма как мост между $\sum$ и $\int$)

Формулировка. Если $f$ интегрируема по Риману на $[a, b]$, то
$$\frac{b - a}{n}\sum_{k=1}^n f\!\left(a + \frac{k(b-a)}{n}\right) \to \int_a^b f(x)\,dx.$$
Олимпиадный фокус — узнать в "странной" сумме Riemann-сумму после нелинейной замены индекса (см. ниже).

Условия применимости. Riemann-интегрируемость. На несобственных пределах нужен sandwich или mass-control: например, для $f$ с особенностью в $0$ — отдельная оценка $\sum_{k=1}^{N(\varepsilon)}$.

Идея доказательства. Определение интеграла Римана.

Варианты и обобщения.
- **Sandwich для $\ln$**: $f = \ln$ имеет особенность в $0$, но $\tfrac{1}{n}\sum \ln(k/n) \to \int_0^1 \ln x\,dx = -1$ доказывается зажатием (см. IMC-1997-1).
- **Замена $t = e^{-h}$**: $\sum_{n\geq 1} t^n/(1 + t^n)$ при $t = e^{-h}$, $h \to 0^+$ — Riemann-сумма для $\int_0^\infty dx/(1+e^x) = \ln 2$ с шагом $h$ (IMC-2001-3).
- **Несимметричный mesh $h = 1/\sqrt x$**: $\sum nx/(n^2+x)^2 = (1/\sqrt x)\sum f(n/\sqrt x)$ — Riemann-сумма для $\int_0^\infty t/(1+t^2)^2\,dt = 1/2$.
- Связь с **Euler–Maclaurin**: $\sum f(k) - \int f = \tfrac{1}{2}(f(a)+f(b)) + \sum B_{2j} (f^{(2j-1)}(b) - f^{(2j-1)}(a))/(2j)! + R_N$ — даёт точную асимптотику остатка.

Используется в. [IMC-1997-1, IMC-2001-3, IMC-1996-DAY2-5; Putnam-2003-A3, Putnam-2010-A5].

---

### E10. Periodic averaging $\int f(x)\,g(nx)\,dx$

Формулировка. Пусть $f \in C[a, b]$, $g$ — $T$-периодична и интегрируема на периоде. Тогда
$$\int_a^b f(x)\,g(nx)\,dx \;\xrightarrow{n\to\infty}\; \left(\frac{1}{T}\int_0^T g(t)\,dt\right) \int_a^b f(x)\,dx.$$

Условия применимости. $f$ непрерывна на компакте (достаточно равномерной непрерывности); $g$ $T$-периодична, $L^1[0,T]$. Для $f \in L^1$ — нужна некоторая регулярность ($f$ — sup-метрика, или mollification).

Идея доказательства. Разбиение $[a,b]$ на куски длины $T/n$; на каждом куске $f$ почти постоянна (равномерная непрерывность $\Rightarrow$ модуль $\omega(f, T/n) \to 0$), интеграл $\int g(nx)$ по периоду $= (1/n)\int_0^T g$. Сложение даёт ответ с ошибкой $O(\omega(f, T/n))$.

Варианты и обобщения.
- **Riemann–Lebesgue lemma** ($g(t) = e^{it}$): $\int_a^b f(x) e^{inx}\,dx \to 0$ для $f \in L^1$.
- **Тестовая функция $\cos x$ или $1\pm\cos x$**: $\int f(x)(1 \pm \cos nx)\,dx \to \int f \cdot \tfrac{1}{2\pi}\int (1\pm\cos)$ — приём для доказательств отрицания/смены знака (IMC-1995-DAY2-5).
- **Несколько частот**: $\int f(x) g(nx) h(mx)$ — нужно учитывать (не)соизмеримость $n/m$.

Используется в. [IMC-1994-5, IMC-1995-DAY2-5; Putnam-2000-B4 (Riemann–Lebesgue вариант)].

---

### E11. Wallis formula and Wallis integrals (Wallis-интегралы)

Формулировка. $W_n = \int_0^{\pi/2} \sin^n x\,dx$. Рекуррентность $W_n = \tfrac{n-1}{n} W_{n-2}$ (интегрирование по частям) даёт
$$W_{2n} = \frac{(2n)!}{4^n(n!)^2}\cdot\frac{\pi}{2}, \qquad W_{2n+1} = \frac{4^n (n!)^2}{(2n+1)!}.$$
Wallis product:
$$\frac{\pi}{2} = \prod_{n=1}^\infty \frac{(2n)^2}{(2n-1)(2n+1)} = \lim_{n\to\infty}\frac{1}{2n+1}\left(\frac{4^n(n!)^2}{(2n)!}\right)^2.$$
Следствия: $W_n \sim \sqrt{\pi/(2n)}$; $\binom{2n}{n} \sim 4^n/\sqrt{\pi n}$.

Условия применимости. Чисто алгебраически; для асимптотики нужен Stirling или сам Wallis.

Идея доказательства. Рекуррентность $W_n = (n-1)/n \cdot W_{n-2}$ — IBP. Произведение получается из $W_{2n}/W_{2n+1} \to 1$ (sandwich $W_{2n+1} \leq W_{2n} \leq W_{2n-1}$).

Варианты и обобщения.
- $W_n$ через beta: $W_n = \tfrac{1}{2} B(\tfrac{n+1}{2}, \tfrac{1}{2})$, ответ через $\Gamma$ — duplication даёт явную форму.
- Coxeter / Borwein-style integrals — родственные конструкции.

Используется в. [Putnam-2013-B2, IMC-1998-6; стандартный инструмент при оценке $\int_0^{\pi/2} \sin^n$ или $\binom{2n}{n}$].

---

## Записи — Standard

### E3. Legendre duplication formula (формула удвоения Лежандра)

Формулировка.
$$\Gamma(z)\,\Gamma\!\left(z + \tfrac{1}{2}\right) = 2^{1-2z}\sqrt{\pi}\,\Gamma(2z).$$

Условия применимости. $2z \notin \{0, -1, -2, \dots\}$. Удобна для перехода между $\Gamma$-значениями в полуцелых и целых точках, для замыкания $\int \sin^{2n}$ через $(2n)!/(4^n(n!)^2)$.

Идея доказательства. Из $B(z, z) = \Gamma(z)^2/\Gamma(2z)$ и интегрального представления $B(z,z) = \int_0^1 (t(1-t))^{z-1}\,dt$; замена $t = (1+u)/2$ даёт $2^{1-2z}\int_{-1}^1 (1-u^2)^{z-1}du = 2^{1-2z} B(\tfrac12, z) = 2^{1-2z}\sqrt{\pi}\,\Gamma(z)/\Gamma(z+\tfrac12)$.

Варианты и обобщения.
- **Gauss multiplication theorem**: $\prod_{k=0}^{n-1}\Gamma(z + k/n) = (2\pi)^{(n-1)/2} n^{1/2 - nz}\Gamma(nz)$.
- **Stirling**: $\Gamma(z+1) \sim \sqrt{2\pi z}\,(z/e)^z$ — критична при подсчёте Wallis-типа произведений.

Используется в. [Wallis: $W_{2n} = \tfrac{(2n)!}{4^n(n!)^2}\cdot\tfrac{\pi}{2}$ — комбинируется с асимптотикой; Putnam-2013-B2].

---

### E5. Inversion $x \mapsto 1/x$

Формулировка. Если интеграл идёт по $(0, \infty)$ и подынтегральное выражение содержит $\ln x$, $x^a$, $x + 1/x$ — замена $x \mapsto 1/x$ часто превращает интеграл в "симметризуемую" сумму. Базовое тождество:
$$\int_0^\infty \frac{f(x)}{x}\,dx = \int_0^\infty \frac{f(1/x)}{x}\,dx,$$
а также $\int_0^\infty f(x + 1/x)\,dx/x = 2\int_0^\infty f(x+1/x)\,dx/x|_{x\geq 1}$.

Условия применимости. Сходимость интеграла; чаще всего — мера $dx/x$ инвариантна относительно $x \mapsto 1/x$ и масштабирований, что и даёт фокус.

Идея доказательства. Прямая замена $u = 1/x$, $du = -dx/x^2$, $du/u = -dx/x$.

Варианты и обобщения.
- $\int_0^1 \ln x/(1+x^2)\,dx + \int_1^\infty \ln x/(1+x^2)\,dx = 0$ (антипод).
- **Cauchy–Schlömilch**: $\int_0^\infty f(x - a/x)\,dx = \int_0^\infty f(x)\,dx$ при $a > 0$ (см. E13).
- "Полу-симметризация": $\int_0^\infty \ln x \cdot R(x)\,dx$ для рациональной $R$ с $R(1/x) = x^2 R(x)$ (или подобной симметрией) — сводится к Frullani или к производной от $\Gamma$.

Используется в. [IMC-2004-DAY2-5 (замена $y = u/x$), классическое $\int_0^\infty \ln x/(1+x^2)\,dx = 0$].

---

### E6. Weierstrass substitution $t = \tan(x/2)$

Формулировка. Замена $t = \tan(x/2)$ переводит
$$\sin x = \frac{2t}{1+t^2},\quad \cos x = \frac{1-t^2}{1+t^2},\quad dx = \frac{2\,dt}{1+t^2}.$$
Превращает любую рациональную функцию от $\sin x, \cos x$ в рациональную функцию от $t$ — далее partial fractions.

Условия применимости. Универсальна для $R(\sin x, \cos x)$, но плодит $1+t^2$ в знаменателе. Для $R$ чётной по $\sin$ или по $\cos$ часто эффективнее $u = \cos x$ или $u = \tan x$ соответственно.

Идея доказательства. Стандартная подстановка двойного угла.

Варианты и обобщения.
- $u = \tan x$ для $R(\sin^2, \cos^2)$ — даёт $du = (1+u^2) dx$.
- Гиперболический аналог: $t = \tanh(x/2)$ для $R(\sinh, \cosh)$.
- "Полусдвиг" $x = \pi/2 - y$ + Weierstrass — иногда укорачивает.

Используется в. [Стандартный приём; в IMC явно редок (тригонометрические задачи чаще решаются через симметрии E4), но часто всплывает в Putnam B-задачах].

---

### E8. Frullani integral

Формулировка. Пусть $f: [0, \infty) \to \mathbb{R}$ непрерывна, существуют конечные $f(0^+) = A$ и $\lim_{x\to\infty} f(x) = B$. Тогда для $a, b > 0$
$$\int_0^\infty \frac{f(ax) - f(bx)}{x}\,dx = (A - B)\ln\frac{b}{a}.$$

Условия применимости. Существование обоих пределов критично. Обобщение: можно заменить $\lim_{x\to\infty} f(x)$ на $\lim_{x\to\infty} \tfrac{1}{x}\int_0^x f$ (Cesàro-предел) — тогда формула сохраняется при более слабых предположениях.

Идея доказательства. Представление $\ln(b/a) = \int_a^b dt/t$ + Fubini:
$$\int_0^\infty \frac{f(ax) - f(bx)}{x}\,dx = \int_0^\infty \int_a^b \frac{-x f'(tx)}{x}\,dt\,dx \;\text{(или прямая регуляризация)}.$$

Варианты и обобщения.
- $f(x) = e^{-x}$: $\int_0^\infty (e^{-ax} - e^{-bx})/x\,dx = \ln(b/a)$.
- $f(x) = \arctan x$: $\int_0^\infty (\arctan(ax) - \arctan(bx))/x\,dx = (\pi/2)\ln(b/a)$.
- **Hardy's generalisation**: для $f$ только с $f(0^+)$ конечным и $\int_1^\infty f(x)/x\,dx$ сходящимся — формула всё ещё верна с $B = 0$ заменённым на $\lim_{R\to\infty}\int_1^R f/x \cdot 1/\ln R$.

Используется в. [Putnam-1986-B5; стандартный инструмент для интегралов вида $\int_0^\infty (g_1 - g_2)/x$].

---

### E12. Laplace's method (метод Лапласа)

Формулировка. Пусть $f \in C^2[a, b]$, $f$ имеет единственный глобальный максимум во внутренней точке $x_0 \in (a, b)$ с $f''(x_0) < 0$, $g$ непрерывна, $g(x_0) \neq 0$. Тогда при $\lambda \to +\infty$
$$\int_a^b g(x)\,e^{\lambda f(x)}\,dx \sim g(x_0)\,e^{\lambda f(x_0)}\sqrt{\frac{2\pi}{-\lambda f''(x_0)}}.$$
Для максимума на конце интервала или для $f''(x_0) = 0$ — отдельные формулы (фактор $\tfrac{1}{2}$, степень $\lambda^{-1/3}$ для plateau и т. д.).

Условия применимости. Гладкость $f$ в окрестности $x_0$, "невырожденность" — $f'' < 0$. Интеграл должен быть конечен. Для $g(x_0) = 0$ — нужно следующее не-нулевое слагаемое в Тейлоре $g$; для нескольких максимумов — суммирование вкладов.

Идея доказательства. Локализация в $\delta$-окрестности $x_0$; вне неё интеграл экспоненциально мал; локально $f(x) \approx f(x_0) + \tfrac{1}{2} f''(x_0)(x-x_0)^2$, замена $u = (x - x_0)\sqrt{-\lambda f''(x_0)}$ — Гауссов интеграл.

Варианты и обобщения.
- **Stirling из Laplace**: $\Gamma(n+1) = \int_0^\infty x^n e^{-x}\,dx = n^{n+1}\int_0^\infty e^{n(\ln s - s)}\,ds$, max в $s=1$ — даёт $\sqrt{2\pi n}\,(n/e)^n$.
- **Watson's lemma**: $\int_0^\infty e^{-\lambda t} g(t)\,dt \sim \sum a_n \Gamma(\alpha_n + 1)/\lambda^{\alpha_n + 1}$ при $g(t) \sim \sum a_n t^{\alpha_n}$, $t\to 0$.
- **Saddle point method** (комплексный аналог) — для интегралов с осциллирующей фазой.

Используется в. [IMC-1996-5, IMC-2015-7; Putnam задачи на асимптотику $\int_0^1 (1 + ax + bx^2)^n\,dx$].

---

## Записи — Exotic

### E13. Cauchy–Schlömilch / Glasser's master theorem

Формулировка. (**Cauchy–Schlömilch**) Для интегрируемой $f$ на $\mathbb{R}$ и $a > 0$
$$\int_{-\infty}^\infty f\!\left(x - \frac{a}{x}\right)\,dx = \int_{-\infty}^\infty f(x)\,dx.$$
(**Glasser, 1983**) Более общий вариант: для $\alpha_n > 0$, $\beta_n \in \mathbb{R}$ и интегрируемой $F$
$$\int_{-\infty}^\infty F\!\left(x - \sum_{n=1}^N \frac{\alpha_n}{x - \beta_n}\right)\,dx = \int_{-\infty}^\infty F(x)\,dx.$$

Условия применимости. Главное — абсолютная интегрируемость $F$. Преобразование $\varphi(x) = x - \sum \alpha_n/(x-\beta_n)$ имеет особенности в $\beta_n$, но обладает свойством "для каждого $u$ уравнение $\varphi(x) = u$ имеет ровно $N+1$ корень и $\sum 1/\varphi'(x_k) = 1$".

Идея доказательства. Замена $y = \varphi(x)$: $\varphi$ покрывает $\mathbb{R}$ $(N+1)$ раз, прообраз каждой точки имеет $N+1$ корней; ключевое тождество $\sum_k 1/\varphi'(x_k(u)) = 1$ — следует из частично-дробного разложения $1/\varphi'$.

Варианты и обобщения.
- $\int_0^\infty f(x + a/x)\,dx/x = \int_0^\infty f(x)\,dx/x$ при $a > 0$ — мультипликативная версия (логарифмическая замена).
- Применение: $\int_{-\infty}^\infty e^{-(x - a/x)^2}\,dx = \int_{-\infty}^\infty e^{-x^2}\,dx = \sqrt\pi$ (мгновенно).

Используется в. [Современные Putnam-style задачи; редко в IMC, но входит в стандартный арсенал — даёт нетривиальные интегралы за одну строчку].

---

### E14. Iterated averaging operator $T f(x) = \tfrac{1}{x}\int_0^x f(t)\,dt$

Формулировка. Оператор $T f(x) = \tfrac{1}{x}\int_0^x f(t)\,dt$ при итерации даёт
$$T^n f(x) = \frac{1}{x}\int_0^x f(t)\,\frac{(\ln(x/t))^{n-1}}{(n-1)!}\,dt.$$
Если $f$ непрерывна в $0$, то $T^n f(x) \to f(0)$ при $n \to \infty$ для каждого фиксированного $x > 0$.

Условия применимости. Непрерывность в $0$ для предела; для $T^n f$ как такового — локальная интегрируемость.

Идея доказательства. Индукция и Fubini: $T(T^{n-1}f)(x) = \tfrac{1}{x}\int_0^x \tfrac{1}{s}\int_0^s f(t)\,(\ln(s/t))^{n-2}/(n-2)!\,dt\,ds$, замена порядка интегрирования + замена $u = \ln(s/t)$ даёт ядро $(\ln(x/t))^{n-1}/(n-1)!$. Сходимость к $f(0)$ — концентрация ядра $(\ln(x/t))^{n-1}/(n-1)!$ у $t = 0$ (после $u = -\ln(t/x)$ ядро превращается в $u^{n-1}/(n-1)!$ на $[0, \infty)$ относительно меры $du$ — Gamma-распределение со средним $n$, но с экспоненциальным весом $e^{-u}$ от $dt = -x e^{-u} du$).

Варианты и обобщения.
- Связь с **Mellin-преобразованием**: $T$ диагонализуется в Mellin-мере.
- Аналогия с **Cesàro-средним** для последовательностей.

Используется в. [IMC-2003-5].

---

## Self-test

1. Вычислить $\displaystyle\int_0^\infty \frac{x^{p-1}}{1+x^q}\,dx$ для $0 < p < q$ (выразить через $\pi$ и тригонометрию).

2. Доказать, что $\displaystyle\int_0^{\pi/2}\ln\sin x\,dx = -\frac{\pi}{2}\ln 2$.

3. Найти $\displaystyle\lim_{n\to\infty} \int_0^1 f(x)\,\{nx\}\,dx$ для непрерывной $f$, где $\{y\}$ — дробная часть.

4. Найти $\displaystyle\lim_{n\to\infty} n\int_0^1 \frac{x^n}{1+x}\,dx$.

5. Вычислить $\displaystyle\int_0^\infty \frac{\ln x}{1 + x^2}\,dx$.

## Решения

1. Замена $u = x^q$: $du = q x^{q-1}dx$, $x^{p-1}dx = (1/q) u^{p/q - 1}du$. Получаем $\tfrac{1}{q}\int_0^\infty u^{p/q - 1}/(1+u)\,du = \tfrac{1}{q} B(p/q, 1 - p/q) = \tfrac{\pi}{q\sin(\pi p/q)}$ (E1, E2).

2. $I = \int_0^{\pi/2}\ln\sin x\,dx$. King's rule (E4): $I = \int_0^{\pi/2}\ln\cos x\,dx$. Сумма: $2I = \int_0^{\pi/2}\ln(\tfrac{1}{2}\sin 2x)\,dx = -\tfrac{\pi}{2}\ln 2 + \tfrac{1}{2}\int_0^\pi \ln\sin u\,du = -\tfrac{\pi}{2}\ln 2 + I$ (последнее — из периодичности и симметрии $\sin(\pi-u) = \sin u$). $\Rightarrow I = -(\pi/2)\ln 2$.

3. Periodic averaging (E10) с $g(t) = \{t\}$, $T = 1$, $\tfrac{1}{T}\int_0^T g = 1/2$. Ответ: $\tfrac{1}{2}\int_0^1 f(x)\,dx$.

4. $\int_0^1 x^n/(1+x)\,dx = \int_0^1 x^n \sum_{k\geq 0}(-1)^k x^k\,dx = \sum_{k\geq 0}(-1)^k/(n+k+1)$. Альтернативно: интегрирование по частям, либо локализация массы $x^n$ у $x=1$. У точки $x=1$ имеем $1/(1+x) \approx 1/2 + O(1-x)$, так что $n\int_0^1 x^n/(1+x)\,dx \to 1/2$ (Laplace-style на конце интервала или прямая оценка). Ответ: $1/2$.

5. Замена $x = 1/u$ (E5): $dx = -du/u^2$, $\ln x = -\ln u$, $1 + x^2 = (1 + u^2)/u^2$, в итоге $\int_0^\infty \ln x/(1+x^2)\,dx = -\int_0^\infty \ln u/(1+u^2)\,du$, т. е. $I = -I$, $I = 0$.

---

## Известные пробелы

Не покрыто из стандартного арсенала или включено сжато:
- **Контурное интегрирование** — относится к комплексному анализу, отдельная подтема.
- **Mellin transform / Plancherel** — слишком тяжёлая машина для одиночной IMC-задачи; в основном используется как мотивация для E14.
- **Watson's lemma в полном виде** — упомянута в E12 как обобщение, но без отдельной записи: для типичных IMC-задач достаточно базового Laplace's method.
- **Lobachevsky integral formula** ($\int_0^\infty f(x)\sin^2 x/x^2\,dx = \int_0^{\pi/2} f$ для $\pi$-периодической $f \geq 0$) — изящная, но в IMC не встречалась; при необходимости — Whittaker–Watson §12.
- **Coxeter integrals, Apéry's $\zeta(3)$** — слишком специфичны.
