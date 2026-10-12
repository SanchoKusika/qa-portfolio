# QA Portfolio

Ручное тестирование веб-приложения [Swag Labs](https://www.saucedemo.com/): тест-план, чек-лист, тест-кейсы, техники тест-дизайна и баг-репорты.

> **EN:** Manual QA portfolio built around the Swag Labs demo store (saucedemo.com): a test plan, a checklist, test cases, test design techniques (equivalence partitioning, boundary values, decision table, state transitions) and bug reports with screenshots. The documentation is written in Russian.

## Содержание

| Раздел | Что внутри |
|---|---|
| [Тест-план](docs/test-plan.md) | Объект и границы тестирования, подход, окружение, критерии входа и выхода, риски |
| [Чек-лист](checklists/saucedemo-checklist.md) | 70 проверок по 9 разделам, включая сравнение тестовых пользователей |
| [Тест-кейсы](test-cases/saucedemo-test-cases.md) | 22 тест-кейса: логин, каталог, корзина, оформление заказа, меню |
| [Тест-дизайн](test-design/README.md) | Классы эквивалентности, граничные значения, таблица решений, диаграмма состояний |
| [Баг-репорты](bug-reports/README.md) | Дефекты со скриншотами, severity и priority |

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

## Подход

- Требований к приложению нет, поэтому ожидаемый результат определяется по поведению `standard_user`, по тексту интерфейса и по общепринятому поведению интернет-магазинов. Подробнее в [тест-плане](docs/test-plan.md#5-источник-ожидаемого-результата).
- Тест-кейсы построены с помощью техник тест-дизайна, а не перебором.
- Каждый баг-репорт описывает одну проблему и воспроизводится по шагам без уточняющих вопросов.

## Инструменты

- Chrome DevTools: Console, Network, Application, Device Mode
- Git, GitHub, Markdown, Mermaid

## Структура репозитория

```
qa-portfolio/
├── docs/            тест-план
├── checklists/      чек-лист
├── test-cases/      тест-кейсы
├── test-design/     техники тест-дизайна
└── bug-reports/     баг-репорты
    └── img/         скриншоты
```
