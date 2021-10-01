# [Best Practices](../../README.md)

## [JS](../README.md)

### Flow

###### Можно закрыть валидатором

- Типы объявлять с момощью префикса `"T_"`

  **Плохо:**
  ```flow js
  type User = { ... };
  ```
  **Хорошо:**
  ```flow js
  type T_User = { ... };
  ```

- Не использовать `any`, `Function`, `object`. Нужно уточнять тип.

  **Плохо:**
  ```flow js
  type TProps = {
    userList: Array,
    getUserList: Function,
  };
  ```
  **Хорошо:**
  ```flow js
  type TProps = {
    userList: [TUser],
    getUserList: typeof getUserList,
  };
  ```

- Всегда должны быть описаны типы для аргументов функции.

  **Плохо:**
  ```flow js
  function foo(bar, baz) {
    // ...
  }
  ```
  **Хорошо:**
  ```flow js
  function foo(bar: string, baz: string): string {
    // ...
  }
  ```
