# [Code Style](../../README.md)

## [JS](../README.md)

### JQuery

###### Закрыто валидатором

- Название переменной с jQuery-элементом должно начинаться с `$` и соответствовать стилю **camelCase**.

  **Плохо:**
  ```js
  const element = $('.j-element');
  ```
  **Хорошо:**
  ```js
  const $element = $('.j-element');
  ```

- Если необходимо обратиться к одному элементу несколько раз - нужно сохранить элемент в переменную.

  **Плохо:**
  ```js
  func1($('.j-element'));
  func2($('.j-element'));
  ```
  **Хорошо:**
  ```js
  const $element = $('.j-element');

  func1($element);
  func2($element);
  ```

- Все события должны быть именованными.

  **Плохо:**
  ```js
  $(document).on('click', func);
  ```
  **Хорошо:**
  ```js
  $(document).on('click.customName', func);
  ```

- Старое событие перед объявлением нового должно быть отменено.

  **Плохо:**
  ```js
  $(document).on('click.customName', func);
  ```
  **Хорошо:**
  ```js
  $(document).off('click.customName').on('click.customName', func);
  ```

###### Нельзя закрыть валидатором

- При обращении в DOM элементам использовать css класс с префиксом `"j-"`.

  **Плохо:**
  ```js
  $('.user');
  $('.user .list');
  ```
  **Хорошо:**
  ```js
  $('.j-user');
  $('.j-user-list');
  ```
