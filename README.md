#Это тестовое задание в команду Trade Marketing

##Запуск контейнеров 
```bash
docker-compose up
```

Контенеры с миграциями и приложением могут не запуститься, попробуйте еще раз 
```bash
docker-compose up
```

Если миграции не применились, стоит локально примеить их , если у вас стоит утилита migrate

```bash
migrate -path ./schemas -database postgres://statistic:statistic@localhost:5436/statistic?sslmode=disable up
```

##Методы API
После запуска контейнеров , все методы будут работать по адресу localhost:8081/statistic/

###Метод добавления статистики 
по адресу localhost:8081/statistic/ отправляйте POST запрос с body
```json
{
  "date":"2018-01-03",
  "views": 13,
  "clicks":13,
  "cost":12.04
}
```
В ответ вернет json, и 201 статус

```json
{"date":"2018-01-03T00:00:00Z","views":13,"clicks":13,"cost":12.041}
```

###Метод получения статистики 
по адресу localhost:8081/statistic/ отправляйте GEt запрос параметрами в URL
обязательные параметры from,to; необязательные sortby.
Пример запроса
```url
localhost:8081/statistic/?from=1999-02-18&to=2021-02-19&sortby=date
```
в ответ получите json и 200 статус

###Метод удаление статистики 
по адресу localhost:8081/statistic/ отправляйте DELETE запрос

при успешном удалении получите ответ 

```json
"deleted"
```

###Тесты 
Для запуска теста локально введите команду 
```bash
go test ./...
```
Запустит 4 теста

Можете в контейнере, но пропишите соединение до тестовой БД