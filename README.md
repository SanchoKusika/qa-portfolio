# QA Portfolio

[![API tests](https://github.com/SanchoKusika/qa-portfolio/actions/workflows/api-tests.yml/badge.svg)](https://github.com/SanchoKusika/qa-portfolio/actions/workflows/api-tests.yml)

Тестирование веб-приложения [Swag Labs](https://www.saucedemo.com/) и REST API [Swagger Petstore](https://petstore.swagger.io/): тест-план, чек-лист, тест-кейсы, техники тест-дизайна, баг-репорты и API-автотесты в Postman с запуском в CI.

> **EN:** QA portfolio built around the Swag Labs demo store (saucedemo.com) and the Swagger Petstore REST API: a test plan, a checklist, test cases, test design techniques, 33 bug reports with DevTools evidence, a test run report, and a Postman collection with 72 assertions that runs in GitHub Actions via Newman. The documentation is written in Russian.

## Содержание

| Раздел | Что внутри |
|---|---|
| [Тест-план](docs/test-plan.md) | Объект и границы тестирования, подход, окружение, критерии входа и выхода, риски |
| [Чек-лист](checklists/saucedemo-checklist.md) | 70 проверок по 9 разделам с результатами: 57 Passed, 13 Failed, 1 вопрос к требованиям |
| [Тест-кейсы](test-cases/saucedemo-test-cases.md) | 22 тест-кейса: логин, каталог, корзина, оформление заказа, меню. Прогон: 18 Passed, 4 Failed |
| [Отчет о тестировании](docs/test-report.md) | Итоги прогона, дефекты по severity и пользователям, риски, рекомендация по релизу |
| [Тест-дизайн](test-design/README.md) | Классы эквивалентности, граничные значения, таблица решений, диаграмма состояний |
| [Баг-репорты UI](bug-reports/README.md) | 27 дефектов Swag Labs со скриншотами, логами Console, записью Performance и запросами из Network |
| [API-тесты](api-tests/README.md) | Коллекция Postman: 23 запроса, 72 проверки, JSON-схемы, цепочки через переменные, запуск в GitHub Actions |
| [Баг-репорты API](bug-reports/api/README.md) | 6 расхождений Petstore со спецификацией Swagger, каждое покрыто автотестом |

## Итоги: Swag Labs

Найдено **27 дефектов** под шестью тестовыми пользователями. Прогон 22 тест-кейсов под `standard_user`: 18 Passed, 4 Failed. Подробно в [отчете о тестировании](docs/test-report.md).

| Severity | Количество | Примеры |
|---|---|---|
| Blocker | 2 | Невозможно оформить заказ: ввод в Last Name портит First Name ([BUG-006](bug-reports/BUG-006.md)); Finish падает с `TypeError` ([BUG-012](bug-reports/BUG-012.md)) |
| Critical | 4 | Цены в каталоге не совпадают с ценами в корзине ([BUG-013](bug-reports/BUG-013.md)); клик по товару открывает другой товар ([BUG-003](bug-reports/BUG-003.md)) |
| Major | 12 | Каталог зависает на 5 секунд из-за синхронного цикла ожидания ([BUG-020](bug-reports/BUG-020.md)); отчеты об ошибках не доходят до Backtrace ([BUG-021](bug-reports/BUG-021.md)); можно оформить пустой заказ ([BUG-023](bug-reports/BUG-023.md)); форма принимает поля из пробелов ([BUG-026](bug-reports/BUG-026.md)) |
| Minor | 7 | Длинное сообщение об ошибке входа обрезается ([BUG-022](bug-reports/BUG-022.md)); кнопки не сбрасываются после Reset App State ([BUG-024](bug-reports/BUG-024.md)); фокус клавиатуры не виден ([BUG-027](bug-reports/BUG-027.md)) |
| Trivial | 2 | Сдвинутые названия товаров ([BUG-017](bug-reports/BUG-017.md)) |

| Пользователь | Дефектов |
|---|---|
| `problem_user` | 6 |
| `error_user` | 6 |
| `visual_user` | 7 |
| `performance_glitch_user` | 1 |
| `locked_out_user` | 1 |
| `standard_user` | 6 |

## Итоги: Swagger Petstore API

- Папки с рабочим поведением: 17 запросов, 59 проверок, все проходят. Запускаются в GitHub Actions при каждом изменении и раз в неделю.
- Найдено **6 расхождений со спецификацией**: неверные статус-коды, утечка Java-исключения в ответе, отсутствие валидации обязательных полей и допустимых значений, отрицательное количество в заказе, id больше `Number.MAX_SAFE_INTEGER`, который искажается в JavaScript ([API-BUG-004](bug-reports/api/API-BUG-004.md)).

## Объект тестирования

**Swag Labs** — учебный интернет-магазин от Sauce Labs. Пользователь входит в систему, выбирает товары в каталоге, складывает их в корзину и оформляет заказ в три шага.

На странице входа доступны тестовые учетные записи с разным поведением, пароль у всех `secret_sauce`:

| Пользователь | Назначение |
|---|---|
| `standard_user` | Эталонное поведение, с ним сравниваются остальные |
| `locked_out_user` | Заблокированная учетная запись |
| `problem_user` | Пользователь с заложенными дефектами интерфейса |
| `performance_glitch_user` | Пользователь с задержками |
| `error_user` | Пользователь с ошибками в сценариях |
| `visual_user` | Пользователь с визуальными дефектами |

**Swagger Petstore** — учебный REST API: питомцы, заказы, пользователи. Ожидаемое поведение описано в спецификации Swagger.

## Подход

- Требований к Swag Labs нет, поэтому ожидаемый результат определяется по поведению `standard_user`, по тексту интерфейса и по общепринятому поведению интернет-магазинов. Подробнее в [тест-плане](docs/test-plan.md#5-источник-ожидаемого-результата).
- Для API источник ожидаемого результата — спецификация Swagger.
- Тест-кейсы построены с помощью техник тест-дизайна, а не перебором.
- Каждый баг-репорт описывает одну проблему и воспроизводится по шагам без уточняющих вопросов.

## Инструменты

- **Chrome DevTools:** Console (исключения и стек вызовов), Network (запросы, заголовки, статус-коды, CORS), Elements (классы и размеры элементов), Performance (запись, Bottom-up, LCP), Sources (поиск причины задержки в коде), Application (localStorage, cookies)
- **Postman:** коллекции, переменные, pre-request и post-response скрипты, `pm.test`, проверка JSON-схемы, Collection Runner
- **Newman, GitHub Actions:** запуск API-тестов в CI, отчеты JUnit
- **cURL, Git, GitHub, Markdown, Mermaid**

## Структура репозитория

```
qa-portfolio/
├── docs/                     тест-план, отчет о тестировании
├── checklists/               чек-лист
├── test-cases/               тест-кейсы
├── test-design/              техники тест-дизайна
├── bug-reports/              баг-репорты Swag Labs
│   ├── img/                  скриншоты
│   └── api/                  баг-репорты Petstore API
├── api-tests/                коллекция Postman
└── .github/workflows/        запуск API-тестов в GitHub Actions
```
