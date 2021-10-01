# [Code Style](../../README.md)

## [JS](../README.md)

### Объекты

###### Можно закрыть валидатором

- Для итераций по объектам использовать методы-итераторы вместо циклов - `keys`, `values`, `entries` и тд.

  **Плохо:**
  ```js
  const users = { ... };
  const userIds = [];
  const userNames = [];

  for (const id in users) {
    userIds.push(id);
    userNames.push(users[id].name);
  }
  ```
  **Хорошо:**
  ```js
  const users = {  ... };
  const userIds = Object.keys(users);
  const userNames = Object.values(users).map((user) => user.name);
  ```

- Не переопределять нативные методы.

  **Плохо:**
  ```js
  const foo = {
    property1: 42,
  };

  foo.hasOwnProperty = () => 'customHasOwnProperty';

  console.log(foo.hasOwnProperty('property1')); // вернёт customHasOwnProperty
  ```
  **Хорошо:**
  ```js
  const foo = {
    property1: 42,
  };

  console.log(Object.hasOwnProperty.call(foo, 'property1')); // вернёт true
  ```

###### Частично можно закрыть валидатором

- Использовать деструктуризацию, если необходимо обратиться к одному свойству несколько раз.

  **Плохо:**
  ```js
  func1(obj.prop1);
  func2(obj.prop1);
  ```
  **Хорошо:**
  ```js
  const {prop1} = obj;

  func1(prop1);
  func2(prop1);
  ```
