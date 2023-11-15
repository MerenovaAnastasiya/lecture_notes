# Пул соединений/ коннектов
Без использования пула соединений по умолчанию используется модель 1 клиент = 1 процесс, что приводит к деградации сситемы, тк

- Создание соединения обходится дорого
- Большон кол-во соединений замедляет работу сервера
- Каждое соединение расходует память
- Создание кеша = авторизация/аутентификация/наполнение кешей


Менеджер Пула соединений - программа, которая для СУБД притворяется клиентом, а для клиента - СУБД, фактические
являясь прослойкой между ними

PgBouncer - стандарт де-факто, предоставляет только менеджер пула соединений, нет доп функций

PgPool 2 - не только пул, но и балансировщик

## Режимы работы 

_**Пул сеансов**_ может иметь смысл только в том случае, если сеансы очень короткие

Чаще всего используется _**пул транзакций**_ - разные транзакции одного клиентского сеанса могут выполняться
в разных соединениях с сервером

Новый пул соединений создается на каждую пару БАЗА ДАННЫХ + РОЛЬ, поэтому пул соединений будет эффективно работать тогда,
когда таких пар будет не очень много

## Аутентификация

Менеджер пула соединений должен так же, как и pg, проводить аутентификацию клиентов, иначе, тк соединение уже создано, 
какой-то пользователь может выполнить запрос без прохождения аутентификации.
Поэтому на стороне менеджера также есть механизм, обеспечивающий аутентификацию пользователей, он хранит у себя пароли и тд


## Особенности

При использовании пула соединений в транзакционном режиме могут возникнуть проблемы при выполнении действий, локализованных
в сеансе, а не в транзакции

Например:
- подготовленные операторы (PREPARE/EXECUTE), можно использовать pgpsql, но вот **явно преподготовленные функции могут привести к ошибкам**
- временные таблиц, кроме ON COMMIT DROP
- функция curval
- установка конфигурационных параметром (SET/RESET) на уровне сеанса
- блокировки на уровне сеанса
- межпроцессные уведомления (LISTEN/ NOTIFY)
- курсор с фразой WITH HOLD
- загрузка разделяемых библиотек
- расширения, сохраняющие состояние на уровне сеанса