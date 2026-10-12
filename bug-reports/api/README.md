# Баг-репорты API: Swagger Petstore

Дефекты публичного API https://petstore.swagger.io/v2. Ожидаемый результат взят из [спецификации Swagger](https://petstore.swagger.io/v2/swagger.json). Каждый дефект покрыт автотестом в папке `4. Known defects` [коллекции Postman](../../api-tests/README.md).

| ID | Заголовок | Severity | Priority |
|---|---|---|---|
| [API-BUG-001](API-BUG-001.md) | [GET /pet/{petId}] Нечисловой id возвращает 404 и Java-исключение вместо 400 | Major | Medium |
| [API-BUG-002](API-BUG-002.md) | [GET /pet/findByStatus] Недопустимый статус возвращает 200 и пустой массив вместо 400 | Minor | Low |
| [API-BUG-003](API-BUG-003.md) | [POST /pet] Сервер принимает статус вне допустимого списка | Major | Medium |
| [API-BUG-004](API-BUG-004.md) | [POST /pet] Сервер создает питомца без обязательных полей и с id, который ломается в JavaScript | Major | High |
| [API-BUG-005](API-BUG-005.md) | [PUT /pet] Обновление несуществующего питомца создает его вместо ответа 404 | Major | Medium |
| [API-BUG-006](API-BUG-006.md) | [POST /store/order] Сервер принимает заказ с отрицательным количеством | Major | High |

Общее окружение для всех репортов: Postman 12 / Newman 6.2.1, cURL, Windows 11, дата 2026-10-12.
