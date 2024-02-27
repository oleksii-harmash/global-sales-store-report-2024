## Sales Power BI Report

![image](https://github.com/oleksii-harmash/pet-power-bi-projects-2024/assets/72203364/c880243f-36ac-473b-8c77-e0e5f078db6b)

### Data Preparing
##### Дані взято з kaggle, та містять інформацію про факт замовлення товару та пов'язану з ним інформацію у вигляді однієї таблиці. (ім'я, назва товару, пункт доставки, група товару і т.д.)

##### 1. Першим кроком очищено деякі пропущених дані та не потрібні стовпці з метою зменшення навантаження моделі
##### 2. **Проектування** даних відбувалося за принципом Star Schema, де факт покупки товару виділений в центральну таблицю, яка зберігає ключі до всіх суміжних. Виділено такі таблиці: Orders (центральна), Product, Date, Location, Customers, Returns.
##### ![image](https://github.com/oleksii-harmash/pet-power-bi-projects-2024/assets/72203364/99727e2d-2498-4fff-871e-e39354715ee7)
##### 3. В кожній з таблиць присутній primary key, який посилається на foreign key центральної таблиці (зв'язок 1:*).
##### 4. Таблиця Date містила лише дату створення замовлення, чого мало для аналізу, тому вирішено на основі дати додати такі поля як Day Number Of Week, Day, Day Number Of Month і так далі.
##### 5. Створено таблицю _Measures для зберігання усіх measures репорту.

### Measures
##### Для побудови графіків порівняння продажів (та інших показників) в часі створено наступні measures:
>##### 1. Total Sales = SUM(Orders[Sales]) та Total Sales PY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Date'[Order Date]))
>##### 2. Total Sales YTD = TOTALYTD([Total Sales], 'Date'[Order Date]) та Total Sales PY YTD = TOTALYTD([Total Sales PY], 'Date'[Order Date])
>##### 3. Share Total Sales PY = DIVIDE([Total Sales], [Total Sales PY]) - 1
>##### 4. Total Sales YoY% =
>   ##### var previous_year = CALCULATE([Total Sales], DATEADD('Date'[Order Date], -1, YEAR))
>   ##### return DIVIDE([Total Sales] - previous_year, previous_year, 0)
##### Дані measures поміщені в групу Sales та відповідним чином створено measures для показників: Profit, Price, Ship Cost, Units (деякі з них не застосовувалися).
 


#### Відео-демонстрація інтерфейсу репорту:

https://github.com/oleksii-harmash/pet-power-bi-projects-2024/assets/72203364/78f36479-ccf6-4659-a5c2-33fbe4e4f355






