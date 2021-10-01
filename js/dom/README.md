# [Best Practices](../../README.md)

## [JS](../README.md)

### DOM

###### Можно закрыть валидатором

- Использовать `querySelector` и `querySelectorAll`.

  **Плохо:**
  ```js
  document.getElementById('my-id');
  document.getElementsByClassName('my-class');
  document.getElementsByTagName('div');
  ```
  **Хорошо:**
  ```js
  document.queryselector('#my-id');
  document.querySelectorAll('.my-class');
  document.querySelectorAll('div');
  ```

###### Частично можно закрыть валидатором

- При использовании `addEventListener` выносить коллбэк в переменную, чтобы его можно было отменить.

  **Плохо:**
  ```js
  document.addEventListener('click', () => console.log('click'));
  document.removeEventListener('click', () => console.log('click')); // не сработает
  ```

  **Хорошо:**
  ```js
  function handleClick() {
    console.log('click');
  }

  document.addEventListener('click', handleClick);
  document.removeEventListener('click', handleClick);
  ```
