# [Best Practices](../../README.md)

## [JS](../README.md)

### Массивы

###### Закрыто валидатором

- Создавать массивы через литерал.

  **Плохо:**
  ```js
  const arr = new Array();
  ```
  **Хорошо:**
  ```js
  const arr = [];
  ```

###### Можно закрыть валидатором

- Для итераций по массивам использовать методы-итераторы вместо циклов - `forEach`, `map`, `filter`, `reduce` и тд.

  **Плохо:**
  ```js
  const userList = [ ... ];
  const userNameList = [];
  for (let i = 0; i < userList.length; i++) {
    userNamesList.push(userList[i]);
  }
  ```
  **Хорошо:**
  ```js
  const userList = [ ... ];
  const userNameList = userList.map((user) => user.name);
  ```

###### Нельзя закрыть валидатором

- Использовать читаемое название аргументов в коллбэках.

  **Плохо:**
  ```js
  userList.map((item) => item.name);
  ```
  **Хорошо:**
  ```js
  userList.map((user) => user.name);
  ```
