# [Code Style](../../README.md)

## [JS](../README.md)

### Функции

###### Закрыто валидатором

- complexity 10

  **Плохо:**
  ```js
  function foo(value) {
    if (1 === value) {
      return 'a';
    } else if (2 === value) {
      return 'b';
    } else if (3 === value) {
      return 'c'
    } else if (4 === value) {
      return 'd'
    } else if (5 === value) {
      return 'e'
    } else if (6 === value) {
      return 'f'
    } else if (7 === value) {
      return 'g'
    } else if (8 === value) {
      return 'h'
    } else if (9 === value) {
      return 'i'
    } else if (10 === value) {
      return 'j';
    } else {
      return null;
    }
  }
  ```
  **Плохо:**
  ```js
  function foo(value) {
    switch (value) {
      case 1:
        return 'a';
      case 2:
        return 'b';
      case 3:
        return 'c';
      case 4:
        return 'd';
      case 5:
        return 'e';
      case 6:
        return 'f';
      case 7:
        return 'g';
      case 8:
        return 'h';
      case 9:
        return 'i';
      case 10:
        return 'j';
      default:
        return null;
    }
  }
  ```
  **Хорошо:**
  ```js
  function foo(value) {
    const letterMap = {
      1: 'a',
      2: 'b',
      3: 'c',
      4: 'd',
      5: 'e',
      6: 'f',
      7: 'g',
      8: 'h',
      9: 'i',
      10: 'j',
    };

    return Object.hasOwnProperty.call(letterMap, value) ? letterMap[value] : null;
  }
  ```

###### Можно закрыть валидатором

- Название функции должно соответствовать стилю **camelCase**.

  **Плохо:**
  ```js
  function add_user () {
    // ...
  }

  function AddUser () {
    // ...
  }

  function ADD_USER () {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  function addUser () {
    // ...
  }
  ```

- ??? По возможности описывать асинхронные операции с помощью `async/await` вместо `Promise`.

  **Плохо:**
  ```js
  function loginUser () {
    return authApi.login()
      .then(({data}) => data)
      .catch((error) => console.error(error));
  }
  ```
  **Хорошо:**
  ```js
  async function loginUser () {
    try {
      const {data} = await authApi.login();
      return data;
    } catch (error) {
      console.error(error);
    }
  }
  ```
- Использовать ранний выход из функции.

  **Плохо:**
  ```js
  function convertDate(date) {
    const utcDate = moment.utc(date);

    if (utcDate.isValid()) {
      return utcDate
        .startOf('day')
        .toISOString();
    }

    return null;
  }
  ```
  **Хорошо:**
  ```js
  function convertDate(date) {
    const utcDate = moment.utc(date);

    if (!utcDate.isValid()) {
      return null;
    }

    return utcDate
      .startOf('day')
      .toISOString();
  }
  ```

###### Нельзя закрыть валидатором

- Название функции должно начинаться с глагола (нельзя закрыть валидатором).

  **Плохо:**
  ```js
  function user () {
    // ...
  }

  function userAdd () {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  function addUser () {
    // ...
  }

  function login () {
    // ...
  }

  function loginUser () {
    // ...
  }
  ```
