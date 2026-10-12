# Баг-репорты: Swag Labs

Каждый файл описывает один дефект. Скриншоты лежат в [img](img/).

## Список дефектов

| ID | Заголовок | Пользователь | Severity | Priority |
|---|---|---|---|---|
| [BUG-001](BUG-001.md) | [Каталог] У всех товаров одно и то же изображение | `problem_user` | Major | High |
| [BUG-002](BUG-002.md) | [Каталог] Сортировка товаров не применяется | `problem_user` | Major | Medium |
| [BUG-003](BUG-003.md) | [Каталог] Клик по товару открывает карточку другого товара | `problem_user` | Critical | High |
| [BUG-004](BUG-004.md) | [Корзина] Три товара из шести не добавляются в корзину | `problem_user` | Critical | High |
| [BUG-005](BUG-005.md) | [Каталог] Кнопка Remove в каталоге не удаляет товар из корзины | `problem_user` | Major | Medium |
| [BUG-006](BUG-006.md) | [Оформление] Ввод в поле Last Name перезаписывает First Name, заказ оформить невозможно | `problem_user` | Blocker | High |
| [BUG-007](BUG-007.md) | [Каталог] Любая сортировка вызывает системное окно «Sorting is broken!» | `error_user` | Major | Medium |
| [BUG-008](BUG-008.md) | [Корзина] Три товара не добавляются в корзину, в Console ошибка «Failed to add item to the cart» | `error_user` | Critical | High |
| [BUG-009](BUG-009.md) | [Каталог] Remove в каталоге не удаляет товар, в Console ошибка «Failed to remove item from cart» | `error_user` | Major | Medium |
| [BUG-010](BUG-010.md) | [Оформление] Поле Last Name не принимает ввод | `error_user` | Major | High |
| [BUG-011](BUG-011.md) | [Оформление] Форма пропускает пустое обязательное поле Last Name | `error_user` | Major | Medium |
| [BUG-012](BUG-012.md) | [Оформление] Кнопка Finish не завершает заказ, в Console TypeError | `error_user` | Blocker | High |
| [BUG-013](BUG-013.md) | [Каталог] Цены в каталоге случайные и не совпадают с ценами в корзине | `visual_user` | Critical | High |
| [BUG-014](BUG-014.md) | [Каталог] Цена отображается с одним знаком после точки | `visual_user` | Minor | Low |
| [BUG-015](BUG-015.md) | [Каталог] У Sauce Labs Backpack чужое изображение, и оно шире остальных | `visual_user` | Major | Medium |
| [BUG-016](BUG-016.md) | [Шапка] Иконка корзины смещена вниз из шапки к списку сортировки | `visual_user` | Minor | Medium |
| [BUG-017](BUG-017.md) | [Каталог] Названия двух товаров сдвинуты вправо | `visual_user` | Trivial | Low |
| [BUG-018](BUG-018.md) | [Каталог] Кнопка Add to cart у Test.allTheThings() T-Shirt (Red) выходит за край карточки | `visual_user` | Minor | Low |
| [BUG-019](BUG-019.md) | [Корзина] Кнопка Checkout отображается в правом верхнем углу шапки | `visual_user` | Minor | Medium |
| [BUG-020](BUG-020.md) | [Каталог] Каталог открывается около 5 секунд: страницу блокирует синхронный цикл ожидания | `performance_glitch_user` | Major | High |
| [BUG-021](BUG-021.md) | [Мониторинг] Отчеты об ошибках не доходят до Backtrace: в URL незаполненные UNIVERSE и TOKEN | `locked_out_user` | Major | Medium |

## Шкала severity

| Severity | Значение |
|---|---|
| Blocker | Блокирует работу с приложением, обходного пути нет |
| Critical | Не работает ключевая функция (вход, корзина, оформление заказа) |
| Major | Функция работает неправильно, но есть обходной путь |
| Minor | Незначительное нарушение логики или интерфейса |
| Trivial | Косметический дефект: опечатка, сдвиг на несколько пикселей |

Priority (High, Medium, Low) показывает срочность исправления с точки зрения бизнеса и не зависит от severity. Например, опечатка в названии магазина на главной: severity Trivial, priority High.

## Шаблон

Новый баг-репорт создается по [TEMPLATE.md](TEMPLATE.md).
