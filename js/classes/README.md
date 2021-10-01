# [Code Style](../../README.md)

## [JS](../README.md)

### Классы

###### Закрыто валидатором

- В одном файле может быть объявлен только 1 класс.

  **Плохо:**
  ```js
  // services.js
  class UserService {
    // ...
  }

  class CompanyService {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  // UserService.js
  class UserService {
    // ...
  }

  // CompanyService.js
  class CompanyService {
    // ...
  }
  ```

###### Можно закрыть валидатором

- Название класса должно соответствовать стилю **PascalCase**.

  **Плохо:**
  ```js
  class userView {
    // ...
  }

  class user_view {
    // ...
  }

  class USER_VIEW {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  class UserView {
    // ...
  }
  ```

###### Частично можно закрыть валидатором

- В классе должны быть объявлены все свойства с дефолтными значениями.

   **Плохо:**
   ```js
    class UserService {
        setUserId(id) {
            this.id = id;
        }
        setUserName(name) {
            this.name = name;
        }
    }
   ```
   **Хорошо:**
   ```js
    class UserService {
        constructor() {
            this.id = null;
            this.name = null;
        }
        setUserId(id) {
            this.id = id;
        }
        setUserName(name) {
            this.name = name;
        }
    }
    ```

- Использовать стрелочные методы вместо `bind`.

  **Плохо:**
  ```js
  class UserService {
    constructor() {
      this.setUserId = this.setUserId.bind(this);
    }

    setUserId(id) {
      // ...
    }
  }
  ```
  **Хорошо:**
  ```js
  class UserService {
    setUserId = (id) => {
      // ...
    };
  }
  ```

###### Нельзя закрыть валидатором

- Максимум наследований в нашем коде - 3 (не учитывается наследование в сторонних библиотеках).
