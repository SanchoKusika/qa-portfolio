# API-BUG-003. [POST /pet] Сервер принимает статус вне допустимого списка

| Поле | Значение |
|---|---|
| Severity | Major |
| Priority | Medium |
| Endpoint | `POST /v2/pet` |
| Окружение | https://petstore.swagger.io/v2, Newman 6.2.1, cURL |
| Дата | 2026-10-12 |
| Воспроизводимость | Всегда |
| Автотест | `4. Known defects / API-BUG-003 Create pet with status outside enum` |

## Шаги воспроизведения

```bash
curl -i -X POST https://petstore.swagger.io/v2/pet \
  -H "Content-Type: application/json" \
  -d '{"id": 999000003, "name": "qa-portfolio-invalid-status", "photoUrls": [], "status": "flying"}'
```

## Фактический результат

```
HTTP/1.1 200 OK

{"id":999000003,"name":"qa-portfolio-invalid-status","photoUrls":[],"tags":[],"status":"flying"}
```

Питомец создан со статусом `flying`.

## Ожидаемый результат

По спецификации `status` — перечисление `available`, `pending`, `sold`. Для другого значения сервер должен вернуть ошибку валидации (`405 Invalid input`), питомец не создается.

## Дополнительно

Последствия отсутствия валидации уже видны на стенде. `GET /v2/store/inventory` возвращает счетчики для статусов `string`, `bad`, `invalid`, `Not Available`, `invalidStatus?` и других значений, которых нет в спецификации. Такие питомцы не находятся через `findByStatus`, то есть «теряются» для клиента.

Тот же запрос показал, что число в поле `name` (`"name": 12345`) сервер молча превращает в строку `"12345"` вместо ошибки типа.
