# [Best Practices](../../README.md)

## [JS](../README.md)

### React

###### Закрыто валидатором

- Компоненты объявляются в файле с расширением `.jsx`.
- Для каждого компонента должен быть описан тип `props`.

  **Плохо:**
  ```js
  const MyComponent = ({text}) => <div>{text}</div>;
  ```
  **Хорошо:**
  ```js
  const MyComponent = ({text}) => <div>{text}</div>;

  MyComponent.propTypes = {
    text: PropTypes.string,
  };
  ```
  **Хорошо:**
  ```flow js
  type TProps = {
    text: string,
  };
  const MyComponent = ({text}: TProps) => <div>{text}</div>;
  ```

- Нельзя объявлять функции в `render` для обработчиков, нужно выносить в стрелочные методы.

  **Плохо:**
  ```js
  class MyComponent extends React.Component {
    render() {
      return <div onClick={() => console.log('click')}>{this.props.children}</div>;
    }
  }
  ```
  **Хорошо:**
  ```js
  class MyComponent extends React.Component {
    handleClick = () => {
      console.log('click');
    }

    render() {
      return <div onClick={this.handleClick}>{this.props.children}</div>;
    }
  }
  ```

- Не использовать индексы массива в качестве свойства `key`.

  **Плохо:**
  ```js
  const MyComponent = ({itemList}) => itemList.map(({name}, index) => <div key={index}>{name}</div>);
  ```
  **Хорошо:**
  ```js
  const MyComponent = ({itemList}) => itemList.map(({id, name}) => <div key={id}>{name}</div>);
  ```

- Не использовать `deprecated` и `unsafe` методы (UNSAFE_componentWillMount(), UNSAFE_componentWillReceiveProps(),
   UNSAFE_componentWillUpdate()).

###### Можно закрыть валидатором

- Верстка описывается с помощью `JSX`.
- Если нужно изменить `state` на основе старого `state` - использовать коллбэк.

  **Плохо:**
  ```js
  setState({
    counter: this.state.counter + 1,
  });
  ```
  **Хорошо:**
  ```js
  setState((state) => ({
    counter: state.counter + 1,
  }));
  ```

###### Частично можно закрыть валидатором

- В одном файле может быть объявлен только 1 компонент.

  **Плохо:**
  ```js
  // MyComponents.jsx
  const MyComponent1 = () => ({...});

  const MyComponent2 = () => ({...});
  ```
  **Хорошо:**
  ```js
  // MyComponent1.jsx
  const MyComponent1 = () => ({...});

  // MyComponent2.jsx
  const MyComponent2 = () => ({...});
  ```

- Название React-компонента должно соответствовать стилю **PascalCase**.

  **Плохо:**
  ```js
  class myComponent {
    // ...
  }

  class my_component {
    // ...
  }

  class MY_COMPONENT {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  class MyComponent {
    // ...
  }
  ```
  **Хорошо:**
  ```js
  const MyComponent = () => ({...});
  ```

- События должны быть отменены в `componentWillUnmount`.

  **Плохо:**
  ```js
  class MyComponent extends React.Component {
    componentDidMount() {
      window.addEventListener('resize', this.handleResize);
      setTimeout({...});
    }
  }
  ```
  **Хорошо:**
  ```js
  class MyComponent extends React.Component {
    timeout = null;

    componentDidMount() {
      window.addEventListener('resize', this.handleResize);
        this.timeout = setTimeout({...});
    }

    componentWillUnmount() {
      window.removeEventListener('resize', this.handleResize);
      clearTimeout(this.timeout);
    }
  }
  ```

- `defaultProps` использовать только как статик. При деструктуризации нельзя.

  **Плохо:**
  ```js
  class MyComponent extends React.Component {
    render() {
      const {prop1 = 'prop1'} = this.props;
    }
  }
  ```
  **Хорошо:**
  ```js
  class MyComponent extends React.Component {
    static defaultProps = {prop1: 'prop1'};

    render() {
      const {prop1} = this.props;
    }
  }
  ```

###### Нельзя закрыть валидатором

- Слоты должны соответствовать стилю **camelCase**.

  **Плохо:**
  ```js
  const MyComponent = ({Item1, Item2}) => {
    return [
      <div key="1">{Item1}</div>,
      <div key="1">{Item2}</div>
    ];
  };

  <MyComponent Item1={<div>Item</div>} Item2={<MyOtherComponent />} />
  ```

  **Хорошо:**
  ```js
  const MyComponent = ({item1, item2}) => {
    return [
      <div key="1">{item1}</div>,
      <div key="1">{item2}</div>
    ];
  };

  <MyComponent item1={<div>Item</div>} item2={<MyOtherComponent />} />
  ```

- Стили описываются в отдельном файле `styles.less` рядом с компонентом (`styles.local.less` для **css-modules**).
- Для описания стилей используется **БЭМ** или **css-modules**.

  **Плохо:**
  ```js
  <button class="button active">OK</button>
  <button class="btn m-t-0 d-i-b">OK</button>
  ```
  **Хорошо:**
  ```js
  <button class="button button_active">OK</button>
  ```
  **Хорошо:**
  ```js
  import bemCn from 'bem-cn';
  import './styles.less'; // файл css
  const b = bemCn('button');

  function CustomButton() {
    return (
      <button className={b({active: true})()}>OK</button>
    );
  }
  ```
  **Хорошо:**
  ```js
  import styles from './styles.local.less'; // файл css-modules

  function CustomButton() {
    return (
      <button className={styles.buttonActive}>OK</button>
    );
  }
  ```

- Для булевых `props` значение по-умолчанию - `false`.

  **Плохо:**
  ```js
  const MyComponent = ({show, text}) => <div>{show ? text : null}</div>;

  MyComponent.defaulProps = {
    show: true,
  };

  <MyComponent text="text" />
  <MyComponent text="text" show={false} />
  ```
  **Хорошо:**
  ```js
  const MyComponent = ({show, text}) => <div>{show ? text : null}</div>;

  MyComponent.defaulProps = {
    show: false,
  };

  <MyComponent text="text" show />
  <MyComponent text="text" />
  ```

- Для загрузки данных использовать метод `componentDidMount`.

  **Плохо:**
  ```js
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);
      this.props.loadData();
    }
  }
  ```
  **Плохо:**
  ```js
  class MyComponent extends React.Component {
    componentWillMount() {
      this.props.loadData();
    }
  }
  ```
  **Хорошо:**
  ```js
  class MyComponent extends React.Component {
    componentDidMount() {
      this.props.loadData();
    }
  }
  ```

- Если нужно перезапросить данные на изменения `props` - использовать `componentDidUpdate`.

  **Хорошо:**
  ```js
  class MyComponent extends React.Component {
    componentDidMount() {
      const {id, loadData} = this.props;

      loadData(id);
    }

    componentDidUpdate(props) {
      const {id} = this.props;

      if (props.id !== id) {
        this.props.loadData(id);
      }
    }
  }
  ```

- Все общие DOM атрибуты (`className`, `data атрибуты` и т.д.) должны быть необязательными.

  **Плохо:**
  ```flow js
  type TProps = {
    children: React.Node,
    className: string,
  };

  const MyComponent = ({children, className}: TProps) => (
    <div className={className}>{children}</div>
  );
  ```
  **Хорошо:**
  ```flow js
  type TProps = {
    children?: React.Node,
    className?: string,
  };

  const MyComponent = ({children = null, className = ''}: TProps) => (
    <div className={className}>{children}</div>
  )
  ```
