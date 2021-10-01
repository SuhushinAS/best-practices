# [Best Practices](../../README.md)

## [JS](../README.md)

### Переменные

###### Закрыто валидатором

- Для объявления переменной использовать `const`.

  **Плохо:**
  ```js
  var userList = [];
  let userList = [];
  ```
  **Хорошо:**
  ```js
  const userList = [];
  ```

###### Можно закрыть валидатором

- Название переменной должно соответствовать стилю **camelCase**.

  **Плохо:**
  ```js
  const user_list = [];
  const UserList = [];
  const USER_LIST = [];
  ```
  **Хорошо:**
  ```js
  const userList = [];
  ```

- Каждая переменная объявляется на новой строке

  **Плохо:**
  ```js
  const first = 1, second = 2, last = 3;
  ```
  **Плохо:**
  ```js
  const first = 1,
        second = 2,
        last = 3;
  ```
  **Хорошо:**
  ```js
  const first = 1;
  const second = 2;
  const last = 3;
  ```

- Если переменную необходимо изменить, то использовать `let`.

  **Плохо:**
  ```js
  let text = 'Hello!';

  someFunction(text);
  ```
  **Хорошо:**
  ```js
  const text = 'Hello!';

  someFunction(text);
  ```
  **Хорошо:**
  ```js
  let text = 'Hello!';

  if (condition) {
    text = 'Hello, US!';
  }

  someFunction(text);
  ```

###### Частично можно закрыть валидатором

- Название констант - **UPPER_CASE**.

  **Плохо:**
  ```js
  const userRole = 'admin';
  const delay = 300;
  ```

  **Хорошо:**
  ```js
  const USER_ROLE = 'admin';
  const DELAY = 300;
  ```

###### Нельзя закрыть валидатором

- Название включает тип: массив - **entityList**, объект - **entityMap**.

  **Плохо:**
  ```js
  const usersInfo = {
    '1': {
      id: '1',
      name: 'foo',
    },
    '2': {
      id: '2',
      name: 'bar',
    }
  };
  const users = ['foo', 'bar'];
  ```
  **Хорошо:**
  ```js
  const userList = ['foo', 'bar'];
  const userMap = {
    '1': {
      id: '1',
      name: 'foo',
    },
    '2': {
      id: '2',
      name: 'bar',
    }
  };
  ```
