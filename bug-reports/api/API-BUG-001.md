# API-BUG-001. [GET /pet/{petId}] Нечисловой id возвращает 404 и Java-исключение вместо 400

| Поле | Значение |
|---|---|
| Severity | Major |
| Priority | Medium |
| Endpoint | `GET /v2/pet/{petId}` |
| Окружение | https://petstore.swagger.io/v2, Newman 6.2.1, cURL |
| Дата | 2026-10-12 |
| Воспроизводимость | Всегда |
| Автотест | `4. Known defects / API-BUG-001 Get pet with non-numeric id` |

## Шаги воспроизведения

```bash
curl -i https://petstore.swagger.io/v2/pet/abc
```

## Фактический результат

```
HTTP/1.1 404 Not Found
Content-Type: application/json

{"code":404,"type":"unknown","message":"java.lang.NumberFormatException: For input string: \"abc\""}
```

## Ожидаемый результат

По спецификации для некорректного id: `400 Invalid ID supplied`. Тело ошибки без внутренних деталей сервера.

## Дополнительно

В одном ответе два нарушения, причина у них одна: сервер не обрабатывает нечисловой id.

1. Неверный статус-код: 404 означает «ресурс не найден», а здесь запрос некорректен, это 400.
2. Утечка внутренней информации: в ответе имя класса Java-исключения. Это подсказывает атакующему технологию бэкенда и место, где не обрабатываются ошибки.
