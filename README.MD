# Тестовое задание на должность Python разработчика

Необходимо реализовать веб-сервис с использованием фреймворка Django и СУБД PostgreSQL имеющее два API метода:
1. Метод для заполнения списка остановок по URL с использованием API Яндекс.Карт.
2. Метод, возвращающий список остановок по указанному маршруту.

> **При выполнении задания не использовать библиотеки Yandex.API и Django REST.** Для получения данных из Яндекс.Карт использовать библиотеку requests метод session

> Добавить в проект Swagger - (необязательно)

## 1. Метод для заполнения списка остановок по URL Яндекс.Карт

Метод входным параметром должен получать ссылку на Яндекс.Карту, которая ведет на маршрут городского автотранспорта. Пример: [ссылка](https://yandex.ru/maps/195/ulyanovsk/?clid=2270456&ll=48.295806%2C54.283906&masstransit%5BlineId%5D=195_61_minibus_roadconsulyanovsk&masstransit%5BthreadId%5D=195A_61_minibus_roadconsulyanovsk&mode=masstransit&z=14).

Метод должен, получить данные о диапазоне маршрута и, с помощью API Яндекс.Карт, получить данные остановок маршрута и записать их в БД в таблицу `mts_routepoint`. 

## 2. Метод, возвращающий список остановок по указанному маршруту

Метод должен возвращать данные из таблицы `mts_routepoint` в виде JSON массива, в котором должны быть поля:

1. Порядковый номер остановки по маршруту 
2. Название остановки 
3. Координаты 

JSON должен реализовывать двухсвязный некольцевой список.

## Структура таблиц

### Таблица `mts_route`

```sql
CREATE TABLE public.mts_route (
	id serial NOT NULL,
	name varchar(128) NOT NULL
);
```

> Поле `name` - назваие маршрута

### Таблица `mts_routepoint`

```sql
CREATE TABLE mts_routepoint (
	id serial NOT NULL,
	name varchar(128) NOT NULL,
	route_id int4 NULL,
	next_point_id int4 NULL,
	prev_point_id int4 NULL,
	point geometry NOT NULL
	CONSTRAINT mts_routepoint_pkey PRIMARY KEY (id)
);
```

