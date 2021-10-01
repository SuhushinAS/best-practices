# [Code Style](../../README.md)

## [JS](../README.md)

### Общее

- Нельзя менять другой компонент напрямую. Можно создать событие.
- Логика и функционал должны соответствовать компоненту (например, в форме не должно быть логики изменения инпута).
- Названия функций:
  - `getFunction` — если что-то получаем/запрашиваем,
  - `onFunction` — обработка события,
  - `renderFunction` — отрисовка.
- Методы, выполняющие разные задачи также следует деструктурировать, не громоздить все в одной функции.
- Обработчики  `on...`, вместо `handle...`, Например: `onClick`, ...
- Отдельный метод `bind` не делаем, `init` - только по необходимости.
- Все, что может быть написано на чистых html+css в рамках тех свойств, что дают заявленные браузеры — должно быть написано без применения JS.
- Все кнопки `submit` должны быть внутри `<form>` вместе со всеми соответствующими инпутами. Обработку завершения заполнения вешать на событие `submit` формы, а не клик по кнопке.
- Все проверки содержащие более одного условия должны быть вынесены в переменную или функцию.
- Нужно избегать неявного приведения типов в JS.
- Все изменения в стилях, которые можно сделать через переключение классов у элемента, надо делать через добавление/удаление классов, а не добавление инлайн стилей.
- Вся работа со службами браузера (`navigator` `services`, `cookie`, `localStorage`) должна быть обернута в `try/catch`.
  > В сафари если включен режим инкогнито или если в браузере стоит блокировка cookie, то можно получить ошибку.

###### Закрыто валидатором

- Стилизацией кода занимается `Prettier` (отступы, пробелы, переносы).
- Код должен проходить проверку `ESLint`.
- Для конкатенации строк и переменных использовать шаблонные строки.

  **Плохо:**
  ```js
  const fullName = firstName + ' ' + lastName;
  ```
  **Хорошо:**
  ```js
  const fullName = `${firstName} ${lastName}`;
  ```

- Можно использовать только 1 уровень вложенности тернарных операторов.

  **Плохо:**
  ```js
  return a ? a : b ? b : c;                             
  ```
  **Хорошо:**
  ```js
  if (a) {
    return a;
  }

  return b ? b : c;
  ```

- Магические числа выносить в константы.

  **Плохо:**
  ```js
  setInterval(cb, 16);
  ```
  **Хорошо:**
  ```js
  const MILLISECONDS_PER_FRAME = 16;

  setInterval(cb, MILLISECONDS_PER_FRAME);
  ```
  **Хорошо:**
  ```js
  const FRAMES_PER_SECOND = 60;
  const ONE_SECOND = 1000;

  setInterval(cb, ONE_SECOND / FRAMES_PER_SECOND);
  ```

###### Частично можно закрыть валидатором

- При использовании браузерной фичи проверять **caniuse.com** (посмотреть `eslint`)

###### Нельзя закрыть валидатором

- Из имени переменной/функции/класса должно быть понятно назначение. Имя должно быть на английском языке, без ошибок и без транслита.

  **Плохо:**
  ```js
  const var1 = [1, 3, 5];

  function slozhenie(a, b) {
    return a + b;
  }
  ```
  **Хорошо:**
  ```js
  const oddNumbers = [1, 3, 5];
  function sum(a, b) {
    return a + b;
  }
  ```