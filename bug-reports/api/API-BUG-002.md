# API-BUG-002. [GET /pet/findByStatus] Недопустимый статус возвращает 200 и пустой массив вместо 400

| Поле | Значение |
|---|---|
| Severity | Minor |
| Priority | Low |
| Endpoint | `GET /v2/pet/findByStatus` |
| Окружение | https://petstore.swagger.io/v2, Newman 6.2.1, cURL |
| Дата | 2026-10-12 |
| Воспроизводимость | Всегда |
| Автотест | `4. Known defects / API-BUG-002 Find pets by invalid status` |

## Шаги воспроизведения

```bash
curl -i "https://petstore.swagger.io/v2/pet/findByStatus?status=qwerty"
```

## Фактический результат

```
HTTP/1.1 200 OK
Content-Type: application/json

[]
```

## Ожидаемый результат

По спецификации параметр `status` принимает только `available`, `pending`, `sold`, а для другого значения описан ответ `400 Invalid status value`.

## Дополнительно

Клиент не может отличить опечатку в статусе от ситуации «питомцев с таким статусом нет»: в обоих случаях пустой массив. Severity Minor, потому что данные не портятся.
