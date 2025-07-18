Давайте разберем алгоритмическое дифференцирование (АД) прямым методом на простом примере. **Прямой метод** вычисляет производные одновременно с вычислением значения функции, продвигаясь от входных переменных к выходной.

**Суть прямого метода АД:**
1.  **Разбиваем функцию:** Представляем целевую функцию как последовательность элементарных операций (сложение, умножение, синус и т.д.) над *промежуточными переменными*.
2.  **Вычисляем значения:** Делаем "прямой проход", вычисляя значение каждой промежуточной переменной последовательно.
3.  **Вычисляем производные:** **Одновременно** с шагом 2, для *каждой* промежуточной переменной вычисляем её частные производные по всем входным переменным (или по выбранному входу). Мы делаем это, применяя правила дифференцирования (цепное правило, правило суммы, произведения и т.д.) к элементарным операциям, используя уже вычисленные производные предыдущих переменных.

**Пример:** Вычислим значение функции и её градиент (вектор частных производных) в точке `(x₀, y₀) = (1, 2)` для функции:
`f(x, y) = sin(x² + y²)`

**Шаг 1: Разобьем функцию на элементарные операции (построим вычислительный граф)**

Введем промежуточные переменные:
1.  `v₁ = x²`   (Возведение в квадрат)
2.  `v₂ = y²`   (Возведение в квадрат)
3.  `v₃ = v₁ + v₂` (Сложение)
4.  `v₄ = sin(v₃)` (Синус)
5.  `f = v₄`      (Выходная функция)

**Шаг 2: Прямой проход (вычисление значений)**
Вычислим значения промежуточных переменных для `x₀ = 1`, `y₀ = 2`:
1.  `v₁ = x² = 1² = 1`
2.  `v₂ = y² = 2² = 4`
3.  `v₃ = v₁ + v₂ = 1 + 4 = 5`
4.  `v₄ = sin(v₃) = sin(5) ≈ sin(286.48°) ≈ -0.9589` (Значение синуса берем из калькулятора)
5.  `f = v₄ ≈ -0.9589`

**Шаг 3: Прямой проход (вычисление производных - суть метода АД)**
Теперь **параллельно** с вычислением значений будем вычислять частные производные каждой промежуточной переменной `vᵢ` по входным переменным `x` и `y`. Обозначим эти производные как `∂vᵢ/∂x` и `∂vᵢ/∂y`.

*   **Для `v₁ = x²`:**
    *   Значение: `v₁ = 1`
    *   Производные (правило степенной функции):
        *   `∂v₁/∂x = 2 * x = 2 * 1 = 2`
        *   `∂v₁/∂y = 0` (так как `v₁` не зависит от `y`)

*   **Для `v₂ = y²`:**
    *   Значение: `v₂ = 4`
    *   Производные:
        *   `∂v₂/∂x = 0` (так как `v₂` не зависит от `x`)
        *   `∂v₂/∂y = 2 * y = 2 * 2 = 4`

*   **Для `v₃ = v₁ + v₂`:**
    *   Значение: `v₃ = 5`
    *   Производные (правило суммы):
        *   `∂v₃/∂x = ∂(v₁ + v₂)/∂x = ∂v₁/∂x + ∂v₂/∂x = 2 + 0 = 2`
        *   `∂v₃/∂y = ∂(v₁ + v₂)/∂y = ∂v₁/∂y + ∂v₂/∂y = 0 + 4 = 4`

*   **Для `v₄ = sin(v₃)`:**
    *   Значение: `v₄ = sin(5) ≈ -0.9589`
    *   Производные (цепное правило: производная внешней функции `sin(u)` - это `cos(u)`, умноженная на производную внутренней `u`):
        *   `∂v₄/∂x = cos(v₃) * ∂v₃/∂x ≈ cos(5) * 2 ≈ (0.2837) * 2 ≈ 0.5674`
        *   `∂v₄/∂y = cos(v₃) * ∂v₃/∂y ≈ cos(5) * 4 ≈ (0.2837) * 4 ≈ 1.1348`

*   **Для `f = v₄`:**
    *   Значение: `f ≈ -0.9589`
    *   Производные (так как `f` тождественно равно `v₄`):
        *   `∂f/∂x = ∂v₄/∂x ≈ 0.5674`
        *   `∂f/∂y = ∂v₄/∂y ≈ 1.1348`

**Результат:**
*   Значение функции в точке `(1, 2)`: `f(1, 2) ≈ -0.9589`
*   Градиент функции в точке `(1, 2)`: `∇f = (∂f/∂x, ∂f/∂y) ≈ (0.5674, 1.1348)`

**Проверка (аналитически):**
Вычислим частные производные аналитически, чтобы убедиться в правильности метода АД:
1.  `f(x, y) = sin(x² + y²)`
2.  `∂f/∂x = cos(x² + y²) * 2x`
3.  `∂f/∂y = cos(x² + y²) * 2y`
Подставляем `x=1`, `y=2`:
*   `∂f/∂x = cos(1² + 2²) * 2*1 = cos(5) * 2 ≈ 0.2837 * 2 ≈ 0.5674`
*   `∂f/∂y = cos(1² + 2²) * 2*2 = cos(5) * 4 ≈ 0.2837 * 4 ≈ 1.1348`

Результаты совпадают!

**Ключевые моменты прямого метода АД:**
1.  **Последовательность:** Вычисления идут строго от входных переменных к выходной функции.
2.  **Локальность:** На каждом шаге (для каждой элементарной операции) мы используем только:
    *   Значения непосредственных входов этой операции (вычисленные на предыдущих шагах).
    *   Производные непосредственных входов этой операции по входным переменным (вычисленные на предыдущих шагах).
    *   Производную самой элементарной операции.
3.  **Эффективность (и недостаток):** Прямой метод эффективен, когда количество входов **меньше** количества выходов (что бывает редко). Для вычисления градиента функции `f: Rⁿ -> R` (1 выход) относительно `n` входов, прямому методу нужно `O(n)` проходов (или `O(n)` дополнительной памяти при векторном подходе), так как он вычисляет производные по *одному входу за раз*. Для функций со многими входами (`n` велико) более эффективен **обратный метод АД (режим обратного распространения)**.
4.  **Точность:** Метод дает производные с *машинной точностью*, так как использует те же арифметические операции, что и вычисление функции, в отличие от численного дифференцирования.

**Итог:** Прямой метод алгоритмического дифференцирования позволяет точно вычислять производные, разбивая сложную функцию на последовательность элементарных операций и вычисляя производные параллельно со значениями функции, двигаясь от входов к выходу, используя правила дифференцирования на каждом элементарном шаге.

Разберём обратный метод алгоритмического дифференцирования (backpropagation или reverse-mode AD) на том же примере:  
`f(x, y) = sin(x² + y²)` в точке `(x₀, y₀) = (1, 2)`.

**Суть обратного метода:**
1.  **Прямой проход:** Вычисляем значение функции и **запоминаем все промежуточные результаты**.
2.  **Обратный проход:** 
    *   Начинаем с выходной переменной и движемся назад к входам.
    *   Вычисляем **сопряжённые переменные (adjoints)** `v̄_i = ∂f/∂v_i` (производная выходной функции по промежуточной переменной `v_i`).
    *   Используем цепное правило для распространения градиентов от выхода к входам.

**Шаг 1: Разбиваем функцию на элементарные операции (тот же вычислительный граф)**
1.  `v₁ = x²`
2.  `v₂ = y²`
3.  `v₃ = v₁ + v₂`
4.  `v₄ = sin(v₃)`
5.  `f = v₄`

**Шаг 2: Прямой проход (вычисляем и запоминаем значения)**
Точно такой же, как в прямом методе:
1.  `v₁ = x² = 1² = 1`
2.  `v₂ = y² = 2² = 4`
3.  `v₃ = v₁ + v₂ = 1 + 4 = 5`
4.  `v₄ = sin(v₃) = sin(5) ≈ -0.9589`
5.  `f = v₄ ≈ -0.9589`

**Шаг 3: Обратный проход (вычисление сопряжённых переменных `v̄_i = ∂f/∂v_i`)**
Идём ОТ ВЫХОДА К ВХОДАМ. **Ключевая идея:** На каждом шаге используем уже вычисленные `v̄_j` (для выходов операции) и локальные производные операции.

*   **Инициализация (выход):**
    *   `f̄ = ∂f/∂f = 1` (Производная функции по себе самой)
    *   Так как `f = v₄`, то `v̄₄ = f̄ = 1`

*   **Для операции `v₄ = sin(v₃)` (Вход: `v₃`; Выход: `v₄`):**
    *   Нам известно: `v̄₄ = 1` (сопряжённая выхода операции)
    *   Нам нужно найти: `v̄₃ = ∂f/∂v₃` (сопряжённую входа операции)
    *   Правило: `v̄₃ = v̄₄ * ∂v₄/∂v₃` (Цепное правило)
    *   `∂v₄/∂v₃ = cos(v₃)` (Производная синуса)
    *   **Значение из прямого прохода:** `v₃ = 5`
    *   `v̄₃ = 1 * cos(5) ≈ 1 * 0.2837 = 0.2837`

*   **Для операции `v₃ = v₁ + v₂` (Входы: `v₁`, `v₂`; Выход: `v₃`):**
    *   Нам известно: `v̄₃ ≈ 0.2837` (сопряжённая выхода операции)
    *   Нам нужно найти: `v̄₁ = ∂f/∂v₁` и `v̄₂ = ∂f/∂v₂` (сопряжённые входов операции)
    *   Правило суммы: `∂v₃/∂v₁ = 1`, `∂v₃/∂v₂ = 1`
    *   Правило: `v̄₁ = v̄₃ * ∂v₃/∂v₁`, `v̄₂ = v̄₃ * ∂v₃/∂v₂`
    *   `v̄₁ = 0.2837 * 1 = 0.2837`
    *   `v̄₂ = 0.2837 * 1 = 0.2837`

*   **Для операции `v₂ = y²` (Вход: `y`; Выход: `v₂`):**
    *   Нам известно: `v̄₂ ≈ 0.2837` (сопряжённая выхода операции)
    *   Нам нужно найти: `ȳ = ∂f/∂y` (сопряжённую входа операции)
    *   Правило: `ȳ = v̄₂ * ∂v₂/∂y`
    *   `∂v₂/∂y = 2y` (Производная квадрата)
    *   **Значение из прямого прохода:** `y = 2`
    *   `ȳ = 0.2837 * (2 * 2) = 0.2837 * 4 = 1.1348`

*   **Для операции `v₁ = x²` (Вход: `x`; Выход: `v₁`):**
    *   Нам известно: `v̄₁ ≈ 0.2837` (сопряжённая выхода операции)
    *   Нам нужно найти: `x̄ = ∂f/∂x` (сопряжённую входа операции)
    *   Правило: `x̄ = v̄₁ * ∂v₁/∂x`
    *   `∂v₁/∂x = 2x` (Производная квадрата)
    *   **Значение из прямого прохода:** `x = 1`
    *   `x̄ = 0.2837 * (2 * 1) = 0.2837 * 2 = 0.5674`

**Результат:**
*   `∂f/∂x = x̄ ≈ 0.5674`
*   `∂f/∂y = ȳ ≈ 1.1348`

**Проверка:** Совпадает с результатом прямого метода и аналитическим расчётом.

**Ключевые особенности обратного метода:**

1.  **Один обратный проход для всего градиента:** Весь градиент (вектор частных производных по всем входам) вычисляется за **один обратный проход**. Это главное преимущество!
2.  **Эффективность для многих входов:** Если входов `n` очень много (например, миллионы параметров в нейронной сети), а выход один (`f: Rⁿ → R`), обратный метод требует времени, пропорционального времени вычисления самой функции (`O(1)` относительно `n`). Прямой метод потребовал бы `O(n)` времени.
3.  **Требует памяти:** Необходимо хранить **все промежуточные значения** (`v₁`, `v₂`, `v₃`, ...), вычисленные во время прямого прохода. Это может стать проблемой для очень больших вычислений.
4.  **Локальность обратного прохода:** Для каждой элементарной операции на обратном проходе:
    *   Берём сопряжённую её выхода (`v̄_output`).
    *   Вычисляем локальные производные операции по её входам (используя **запомненные** значения входов из прямого прохода).
    *   Умножаем сопряжённую выхода на локальные производные, чтобы получить сопряжённые входов (`v̄_input = v̄_output * ∂output/∂input`).
    *   Передаём сопряжённые входам предыдущим операциям.
5.  **Порядок обратного прохода:** Вычисления должны идти в **строго обратном порядке** относительно прямого прохода. Нужно обрабатывать переменные от выхода к входам.
6.  **Доминирует в машинном обучении:** Обратный метод - основа алгоритма обратного распространения ошибки (backpropagation) в обучении нейронных сетей, где число параметров (входов) огромно, а функция потерь (выход) - одна скалярная величина.

**Сравнение прямого и обратного методов:**

| Характеристика          | Прямой метод (Forward-mode)                  | Обратный метод (Reverse-mode)                |
| :---------------------- | :------------------------------------------- | :------------------------------------------- |
| **Направление**         | Вперёд (от входов к выходу)                  | Назад (от выхода к входам)                   |
| **Проходов на градиент**| `n` (по одному на вход)                      | **1** (на весь градиент)                     |
| **Эффективность**       | Лучше, если `выходов >> входов` (`f: Rⁿ → Rᵐ`, `m >> n`) | **Лучше, если `входов >> выходов` (`f: Rⁿ → Rᵐ`, `n >> m`), особенно `m=1` |
| **Память**              | `O(1)` (не считая хранения градиента)        | `O(число операций)` (хранит промежуточные значения) |
| **Сложность вычислений**| `O(n) * время_функции`                       | `O(1) * время_функции` (для градиента)       |
| **Основное применение** | Неявные функции, чувствительность, `m >> n`  | **Оптимизация, ML (нейронные сети), `n >> m`** | 

**Итог:** Обратный метод AD - мощный инструмент для эффективного вычисления градиента скалярной функции по многим параметрам. Он основан на запоминании промежуточных результатов прямого прохода и применении цепного правила в обратном направлении за один проход. Это делает его незаменимым в современных задачах оптимизации и машинного обучения.
