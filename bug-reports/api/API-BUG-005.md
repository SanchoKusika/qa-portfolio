# API-BUG-005. [PUT /pet] Обновление несуществующего питомца создает его вместо ответа 404

| Поле | Значение |
|---|---|
| Severity | Major |
| Priority | Medium |
| Endpoint | `PUT /v2/pet` |
| Окружение | https://petstore.swagger.io/v2, Newman 6.2.1, cURL |
| Дата | 2026-10-12 |
| Воспроизводимость | Всегда |
| Автотест | `4. Known defects / API-BUG-005 Update nonexistent pet` |

## Предусловия

Питомца с id `999000005` нет:

```bash
curl -i https://petstore.swagger.io/v2/pet/999000005
# HTTP/1.1 404 Not Found  {"code":1,"type":"error","message":"Pet not found"}
```

## Шаги воспроизведения

```bash
curl -i -X PUT https://petstore.swagger.io/v2/pet \
  -H "Content-Type: application/json" \
  -d '{"id": 999000005, "name": "qa-portfolio-ghost", "photoUrls": [], "status": "available"}'
```

## Фактический результат

```
HTTP/1.1 200 OK

{"id":999000005,"name":"qa-portfolio-ghost","photoUrls":[],"tags":[],"status":"available"}
```

После этого `GET /v2/pet/999000005` возвращает 200: питомец создан.

## Ожидаемый результат

По спецификации для `PUT /pet` описан ответ `404 Pet not found`. Обновление несуществующей записи не должно ее создавать.

## Дополнительно

Клиент, который обновляет удаленную запись, не узнает об ошибке и создаст «призрак». Если поведение «создать, если нет» (upsert) задумано, его нужно описать в спецификации и возвращать `201 Created`.
