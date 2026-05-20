# Customer-Personality-Analysis
Customer Personality Analysis is an analysis of different segments of a company's customers. This analysis allows a business to better understand its customers and facilitates the process of adapting products to the specific needs, behaviors, and interests of different types of customers.

Customer profiling helps a business modify its product based on its target audience, which is divided into different segments. For example, instead of spending money on marketing a new product to all customers in the company's database, a business can analyze which customer segment is most likely to purchase the product and then focus marketing efforts on that segment only.


# 🍷 Customer Personality Analysis (Сегментація клієнтів)

Цей проект присвячений аналізу та кластеризації клієнтської бази компанії. Мета — виявити різні сегменти клієнтів на основі їхньої поведінки, демографічних даних та історії покупок. Це дозволяє бізнесу адаптувати маркетингові стратегії під конкретні групи споживачів.

## 📌 Огляд проекту

Аналіз "портрету клієнта" допомагає бізнесу зрозуміти, хто є їхнім покупцем. Замість "сліпого" маркетингу для всіх, компанія може зосередити зусилля на тих сегментах, які найімовірніше принесуть прибуток (наприклад, пропонувати елітне вино заможним клієнтам або знижки економним покупцям).

**Основні цілі:**
1. Очистити та підготувати дані.
2. Провести розвідувальний аналіз (EDA).
3. Використати алгоритми машинного навчання для кластеризації.
4. Інтерпретувати отримані сегменти.

## 📂 Опис даних

Використовується датасет `marketing_campaign.csv`. Він містить 29 ознак, які можна розділити на групи:

*   **Профіль клієнта:** `Year_Birth`, `Education`, `Marital_Status`, `Income`, `Kidhome`, `Teenhome`.
*   **Історія покупок (за 2 роки):** `MntWines`, `MntFruits`, `MntMeatProducts`, `MntFishProducts` тощо.
*   **Активність:** `NumWebPurchases`, `NumStorePurchases`, `NumWebVisitsMonth`.
*   **Реакція на кампанії:** `AcceptedCmp1`...`AcceptedCmp5`, `Response`.

## 🛠 Технології

*   **Python 3.x**
*   **Pandas & NumPy** (обробка даних)
*   **Seaborn & Matplotlib** (візуалізація)
*   **Plotly** (інтерактивна 3D візуалізація)
*   **Scikit-learn** (алгоритми кластеризації KMeans, препроцесинг)
*   **SciPy** (ієрархічна кластеризація, дендрограми)

## ⚙️ Етапи аналізу

### 1. Попередня обробка даних (Preprocessing)
*   **Робота з пропусками:** Виявлено пропуски в колонці `Income`. Заповнено медіанним значенням, а також протестовано заповнення середнім.
*   **Викиди:** Знайдено та оброблено аномальні значення (наприклад, дохід 666,666). Використано метод IQR для фільтрації викидів.
*   **Feature Engineering:**
    *   Створено нову ознаку `Customer_days`: кількість днів з моменту реєстрації клієнта.
    *   `Education`: Застосовано **Ordinal Encoding** (оскільки є логічний порядок).
    *   `Marital_Status`: Застосовано **One-Hot Encoding**.
    *   `Dt_Customer`: Перетворено у формат datetime.

### 2. Кластеризація (Modeling)
Було протестовано декілька підходів:

*   **K-Means:**
    *   Тестування на масштабованих (StandardScaler) та немасштабованих даних.
    *   Вибір оптимальної кількості кластерів ($K$) за допомогою **Elbow Method** (метод ліктя) та **Silhouette Score**.
*   **Ієрархічна кластеризація (Hierarchical Clustering):**
    *   Побудова дендрограм для методів `Single`, `Centroid` та `Ward`.
    *   Оцінка якості розбиття.

### 3. Результати та Висновки

В ході експериментів було виявлено:
*   **Масштабування:** У цьому конкретному випадку масштабування даних (StandardScaler) знизило метрику Silhouette. Це може свідчити про те, що `Income` (дохід) є настільки сильною розділовою ознакою, що її природна варіативність краще формує кластери без штучного зрівнювання з іншими ознаками.
*   **Найкращі алгоритми:**
    *   **K-Means (без масштабування):** Silhouette Score $\approx 0.54$ для $K=3$.
    *   **Hierarchical Clustering (Ward Method):** Показав найкращий результат структуризації. Silhouette Score $\approx 0.60$ для $K=2$.
*   **Ключові фактори:** Найбільший вплив на поділ клієнтів мають **Річний дохід (Income)** та **Витрати на вино (MntWines)**.

**Рекомендований поділ:**
Модель чітко виділяє 2 великі групи (Високий дохід/Високі витрати vs Низький дохід/Низькі витрати), але для більш деталізованого маркетингу має сенс використовувати розбиття на **4 кластери** (Silhouette Score $\approx 0.51$ методом Ward), що дозволяє виділити перехідні групи.

## 📊 Приклади візуалізацій

*   ![Дендрограма (Ward Method)](images/DENDROGRAM%20WARD%20METHOD.jpg)
*   ![*Elbow Method графік*](images/Elbow%20Method.jpg)
*   ![*Scatter plot: Income vs MntWines*](images/Income%20vs%20MntWines.jpg)

## 🚀 Як запустити проект

1.  Клонуйте репозиторій:
    ```bash
    git clone https://github.com/Alenushka2013/Customer-Personality-Analysis
    ```
2.  Встановіть необхідні бібліотеки:
    ```bash
    pip install pandas numpy seaborn matplotlib plotly scikit-learn scipy
    ```
3.  Відкрийте файл ноутбука (наприклад, в Jupyter Notebook або Google Colab) та запустіть комірки послідовно.
