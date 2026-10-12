# API-BUG-006. [POST /store/order] Сервер принимает заказ с отрицательным количеством

| Поле | Значение |
|---|---|
| Severity | Major |
| Priority | High |
| Endpoint | `POST /v2/store/order` |
| Окружение | https://petstore.swagger.io/v2, Newman 6.2.1, cURL |
| Дата | 2026-10-12 |
| Воспроизводимость | Всегда |
| Автотест | `4. Known defects / API-BUG-006 Place order with negative quantity` |

## Шаги воспроизведения

```bash
curl -i -X POST https://petstore.swagger.io/v2/store/order \
  -H "Content-Type: application/json" \
  -d '{"id": 999000006, "petId": 1, "quantity": -5, "status": "placed", "complete": false}'
```

## Фактический результат

```
HTTP/1.1 200 OK

{"id":999000006,"petId":1,"quantity":-5,"status":"placed","complete":false}
```

Заказ создан с количеством `-5`.

## Ожидаемый результат

Заказ с количеством меньше 1 отклоняется ответом `400 Invalid Order` (описан в спецификации для этого endpoint).

## Дополнительно

Граничные значения для `quantity`: 0 и -1 должны отклоняться, 1 приниматься. В реальном магазине отрицательное количество может привести к отрицательной сумме заказа, то есть к возврату денег без покупки. Поэтому priority High.
