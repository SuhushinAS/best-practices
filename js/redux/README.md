# [Best Practices](../../README.md)

## [JS](../README.md)

### Redux

###### Можно закрыть валидатором

- Обращаться к данным в `Store` можно только через селекторы.

  **Плохо:**
  ```js
  const mapStateToProps = (state) => ({
    userName: state.user.name,
  });
  ```
  **Хорошо:**
  ```js
  const selectUserName = (state) => state.user.name;

  const mapStateToProps =(state) => ({
    userName: selectUserName(state),
  });
  ```

###### Частично можно закрыть валидатором

- Редьюсер всегда должен иметь `InitialState`.
  ```js
  const initialState = {
    // ...
  };

  const reducers = {
    // ...
  };

  export default createReducer(initialState, reducers);
  ```

- `InitialState` должен иметь все возможные поля с теми же типами.

  **Плохо:**
  ```js
  const initialState = {
    data: {},
  };

  const reducers = {
    [userActions.update]: (state, data) => ({
      data: 'string',
      isLoading: false,
    }),
    // ...
  };

  export default createReducer(initialState, reducers);
  ```
  **Хорошо:**
  ```js
  const initialState = {
    data: {},
    isLoading: false,
  };

  const reducers = {
    [userActions.update]: (state, data) => ({
      data: {
        // ...
      },
      isLoading: false,
    }),
    // ...
  };

  export default createReducer(initialState, reducers);
  ```

- Редьюсер всегда должен возвращать мерж старого и нового состояния.

  **Плохо:**
  ```js
  const reducers = {
    [userActions.update]: (state, data) => ({
      isLoading: false,
    }),
    // ...
  };
  ```
  **Хорошо:**
  ```js
  const reducers = {
    [userActions.update]: (state, data) => ({
      ...state,
      isLoading: false,
    }),
    // ...
  };
  ```

- Имя экшена должно быть вынесено в константу и описано в **camelCase** с привязкой к имени модуля.

  **Плохо:**
  ```js
  const reducers = {
    userGetList: (state, data) => {
      // ...
    },
    userUpdate: (state, data) => {
      // ...
    },
  };
  ```
  **Хорошо:**
  ```js
  // constants/index.js
  export const userActions = {
    getList: 'user__list_get',
    update: 'user__update',
  };

  // reducers/index.js
  import {userActions} from 'modules/user/constants/index.js';

  const reducers = {
    [userActions.getList]: (state, data) => {
      // ...
    },
    [userActions.update]: (state, data) => {
      // ...
    },
  };
  ```
- Название селектора должно начинаться с глагола `select` и соответствовать стилю **camelCase**.

   **Плохо:**
   ```js
    export const getUserList = (state) => state.user.list;
   ```
   **Хорошо:**
   ```js
    export const selectUserList = (state) => state.user.list;
    ```

- Если селектор возвращает новый объект/массив или производит сложные вычисления — он должен быть обернут в `reselect`.

  **Плохо:**
  ```js
  const selectUserNameList = (state) => state.usersList.map((user) => user.name);
  ```
  **Хорошо:**
  ```js
  import {createSelector} from 'reselect';

  const selectUserList = (state) => state.usersList;

  const getName = (user) => user.name;

  const selectUserNameList = createSelector(
    [selectUserList],
    (usersList) => state.usersList.map(getName)
  );
  ```

###### Нельзя закрыть валидатором

- Редьюсеры - чистые функции, нельзя мутировать данные и использовать **сайд-эффекты**, все данные приходят только через `payload`.

   **Плохо:**
  ```js
  const reducers = {
    [userActions.update]: (state, data) => {
      state.data[data.id] = data;
      return state;
    },
    // ...
  };
  ```
  **Плохо:**
  ```js
  const reducers = {
    [userActions.update]: (state, data) => ({
      ...state,
      data: JSON.parse(localStorage.getItem(LOCAL_STORAGE.CURRENT_STATE)),
    }),
    // ...
  };
  ```
  **Хорошо:**
  ```js
  const reducers = {
    [userActions.update]: (state, data) => ({
      ...state,
      data: {
        ...state.data,
        [data.id]: data,
      },
    }),
    // ...
  };
  ```

- `Initial state` не должен зависеть от `localStorage` и глобальных переменных.

  **Плохо:**
  ```js
  const initialState = {
    data: JSON.parse(localStorage.getItem('defaultData')),
    list: window.DEFAULT_LIST,
  };
  ```
   **Хорошо:**
  ```js
  const initialState = {
    data: {},
  };
  ```

- Если в селекторах нужны данные из `props`, то прокидывать их вторым аргументом в объекте.

  **Плохо:**
  ```js
  const selectUserNameList = (state, companyId, role) => {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  const selectUserNameList = (state, {companyId, role}) => {
    // ...
  }
  ```

- Данные, приходящие от бэкенда перед передачей в `store` нужно нормализовывать.

  **Плохо:**
  ```js
  console.log(state.users);

  [
    {
      id: 1,
      name: 'Name 1',
    },
    {
      id: 2,
      name: 'Name 2',
    },
  ]
  ```
  **Хорошо:**
  ```js
  console.log(state.users);

  ({
    data: {
      1: {
        id: 1,
        name: 'Name 1',
      },
      2: {
        id: 2,
        name: 'Name 2',
      },
    },
    list: [1, 2],
  })
  ```
