**1. ЧТО ТАКОЕ JDBC?**

Ответ: API JDBC(Java Database Connectivity) - стандартный прикладной интерфейс языка Java для организации взаимодействия между приложением и СУБД. Взаимодействие осуществляется с помощью драйвером JDBC, обеспечивающих реализацию общих интерфейсов для конкретных СУБД и конкретных протоколов. 

**2. ЭТАПЫ РАБОТЫ С БД С ИСПОЛЬЗОВАНИЕМ JDBC?**

Ответ: 

1. Подключение библиотеки с классов-драйвером БД;
2. Установка соединения с БД;
3. Создание объекта для передачи запросов;
4. Выполнение запроса;
5. Обработка результатов выполнения запросов;
6. Закрытие соединения.

**3. КАК СОЗДАТЬ CONNECTION?**

Ответ: Для установки соединения с БД вызывается статический метод getConnection() класса java.sql.DriverManager. В качестве параметров методу передаются URL БД, логин пользователя БД и пароль доступа. Загрузка класса драйвера БД при отсутствии ссылки на экземпляр этого класса в JDBC 4.1 происходит автоматически при установке соединения с экземпляром DriverManager. Метод возвращает объект Connection. URL БД, состоящий из типа и адреса физического расположения БД, может создаваться в виде отдельной строки или извлекаться из файла ресурсов.

![](https://4.bp.blogspot.com/-8lgYElPXZ8c/V1BRpV9dIzI/AAAAAAAAAy4/HGwyiCmZikYgOWiog8HZRmZV2m8khov5wCLcB/s1600/q003_p01.jpg)

В результате будет возвращен объект Connection и будет одно установленное соединение с БД с именем testphones. Класс DriverManager предоставляет средства для управления набором драйверов БД.

**4. ЧЕМ ОТЛИЧАЕТСЯ STATEMENT ОТ PREPAREDSTATEMENT?**

Ответ: Объект Statement используется для выполнения SQL-запросов к БД. Cуществует 3 типа объектов Statement: 
* Statement, используется для выполнения простых SQL-запросов, без параметров. Интефейс Statement предоставляет базовые методы для выполнения запросов и извлечения результатов;
* PreparedStatement, наследующий от Statement, используется для выполнения перекомпилированных SQL-запросов c/без входных параметров. Интефейс PreparedStatement добавляет методы управления входными параметрами(IN);
* CallableStatement, наследующий от PreparedStatement, используется для вызова хранимых процедур. Интефейс CallableStatement добавляет методы для манипуляции выходными параметрами(OUT).

Интерфейс PreparedStatement наследуется от Statement и отличается следующим:
* Экземпляры PreparedStatement помнят скомпилированные SQL-выражения;
* SQL-выражения в PreparedStatement могут иметь один или более входной параметр.

**5. КАК ВЫЗВАТЬ ХРАНИМУЮ ПРОЦЕДУРУ?**

Ответ: Храни́мая процеду́ра — объект базы данных, представляющий собой набор SQL-инструкций, который компилируется один раз и хранится на сервере.

![](https://4.bp.blogspot.com/-xjvPBIPLdGA/V1BTElY1ZjI/AAAAAAAAAzE/i1QbBs4u1rYTrXK15bHgZ4ustpznzbjGQCLcB/s1600/q005_p01.jpg)

**6. КАК ПРАВИЛЬНО ЗАКРЫТЬ CONNECTION?**

Ответ: 

![](https://1.bp.blogspot.com/-ztzFnRlbAF4/V1BYHhOR0aI/AAAAAAAAAzU/K0HheYxbxQkd07iduBpi_-_mmWRRuu3pwCLcB/s1600/q006_p01.jpg)

**7. КАКИЕ ЕСТЬ УРОВНИ ИЗОЛЯЦИИ ТРАНЗАКЦИЙ?**

Ответ: Уровни изоляции транзакций определены в виде констант интерфейса Connection(по возрастанию уровня ограничений):

* TRANSACTION_NONE - информирует о том, что драйвер не поддерживает транзакцию;
* TRANSACTION_READ_UNCOMMITTED - позволяет транзакциям видеть несохраненные изменения данных, что разрешает грязное, неповторяющее и фантомное чтение;
* TRANSACTION_READ_COMMITTED - означает, что любое изменение, сделанное в транзакции, не видно вне ее, пока она не сохранена. Это предотвращает грязное чтение, но разрешает неповторяющееся и фантомное;
* TRANSACTION_REPEATABLE_READ - запрещает грязное и неповторяющееся чтение,  но фантомное разрешено;
* TRANSACTION_SERIALIZABLE - определяет, что грязное, неповторяющееся и фантомное чтения запрещены.

**8. КАКИЕ ЕСТЬ ТИПЫ ЧТЕНИЯ ТРАНЗАКЦИЙ?**

Ответ: Для транзакций существует несколько типов чтения:

* грязное чтение - происходит, когда транзакциям разрешено видеть несохраненные изменения данных. Иными словами, изменения, сделанные в одной транзакции, видно вне ее до того, как она была сохранена. Если изменения не будут сохранены, то, вероятно, другие транзакции выполняли работу на основе некорректных данных;
* неповторяющееся чтение - происходит, когда транзация А читает строку, транзакция В изменяет эту строку, транзакция А читает ту же строку и получает обновленные данные;
* фантомное чтение - происходит, когда транзакция А считывает все строки, удовлетворяющие Where-условию, транзакция В вставляет новую или удаляет одну из строк, которая удовлетворяет этому условию, транзакция А еще раз считывает все строки,  удовлетворяющие Where-условию, уже вместе с новой строкой или недосчитавшись старой.
