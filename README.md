## Команда «BugAbusers»
#### Бордомыдов Аркадий Павлович студент 4 курса филиала РТУ МИРЭА в г. Ставрополе
#### Нестеренко Станислав Романович студент 4 курса филиала РТУ МИРЭА в г. Ставрополе

## Поставленные задачи:
1. Разработка веб приложения для создания, редактирования и сохранения формул в БД в формате LATEX;
2. Разработка поиска на уникальность формулы на основе заполненной базы данных.

## Трудности возникшие в результате выполнения
1. В результате выполнения поставленной задачи возникли проблемы связанные с нехваткой навыков и нехваткой времени для выполнения задачи за указанный срок;
2. В связи с этим была предложена концепция приложения без конкретной реализации.

## Описание предложенной концепции

### Предложенные для использования библиотеки для работы с форматом LATEX
Для реализации данного проекта можно использовать библиотеки JS под названием Katex и MathJax. Данные библиотеки позволяют с помощью JS отображать в браузере интерпритацию введённых в формате LATEX данных в подходящем для использования виде. 

### Предложенния для реализации Frontend разработки
При реализации интрефейса и взаимодействии пользователя с интерфейсом с дальнейшей отправкой данных в базу данных и для ускорения разработки возможно использовать фреймворк VUE.JS который прост в изучении и быстр и удобен в развёртывании. Также для него есть сторонние библиотеки для взаимодействия с Katex и MathJax.

### Предложения по реализации Backend разработки
Для реализации бизнес логики можно использовать фреймворк YII2 на базе PHP который уже имеет удобные встроенные инструменты для работы с базой данных в виде ActiveRecord и ActiveQuery. Также использование паттерна MVC (Model View Controller) позволит структурировать и упростить работу проекта, а в частности также использовать паттерны Repository и DTO для передачи и инкапсуляции данных из базы данных. Данные предложено хранить в СУБД postgresql, которая в том числе уже поддерживается фрейворком YII2.

### Предложенная реализация взаимодействия пользователя с системой
В предложенной концепции предлагается создание текстового поля с возможностью ввода данных с клавиатуры, а также наличие выпадающего меню для вставки выражений по типу: дробь, сумма и тд. Для безопасности в использовании данных и для стабильной работы предложено ограничить возможность сохранения формул в базу данных путём добавления пользовательских аккаунтов с сохранением password_hash внутри базы данных и разграничением пользователей на наличие свойства administrator. В зависимости от которого будет отображаться кнопка "Сохранить", позволяющая сохранить запись в базу данных.

Поиск предлагается осуществить нажатием соответствующей кнопки с отправкой POST запроса на Controller. В POST запросе предлагается реализовать отправку содержимого текстового поля с формулой и уникального идентификатора пользователя (uid). Ответом на запрос будет является или статус с ошибкой в случае возникновения ошибки, или массив из процентного соотношения найденных по вхождению записей ко всем записям в базе данных, а также количество найденных на вхождение записей.

### Предложение реализации базы данных
Для реализации базы данных для хранения формул предлагается создание базы данных с помощью СУБД postgresql с двумя таблицами:
1. users имеющая такие поля как:
	1.1. user_id Первичный ключ (PK) представленный в формате integer
	1.2. login text. Для хранение логина пользователя, необходимый для регистрации и авторизации.
	1.3. password_hash text. Поля хранение хеша пароля, позволяющее обеспечить безопасное хранение пароля пользователя.
	1.4. administrator bool. Поля для хранение статуса пользователя. позволяющее определить права для сохранения формул в БД.
2. formules имеющая такие поля как:
	2.1. formule_id Первичный ключ (PK) представленный в формате integer.
	2.2. user_create int внешний ключ. Используется для хранения uid пользователя - создателя.
	2.3. date_create datetime. Поля для хранения и сортировки даты сохранения формулы.
	2.4. name_formule text. Используется для хранения названия формулы в базе данных.
	2.5. value text. Поле для хранения самой формулы в форммате Latex в текстовом виде.
Ниже приведена ER (Сущность - связь) модели для наглядного отображения связи 1:м в базе данных.
![image](https://github.com/user-attachments/assets/69558cda-5ee8-405f-819e-b75fae6dcd02)
