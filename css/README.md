# [Code Style](../README.md)

## CSS

- Использовать `space-between`, только в крайних случаях, когда без него не обойтись.
- Если в макете используется цвет не из палитры, сообщить дизайнеру, чтобы использовал цвет из палитры, или добавил цвет в палитру.
- Все размеры должны быть целыми, если задаются в абсолютных единицах. В случае несовпадения отступов - сообщить дизайнеру, чтобы исправил отступ.
- Адаптив: для любых свойств, которые имеют линейную размерность лучше использовать `fluid-prop` и `font-fluid`.
- Избегать дубляжа стилей.
- У компонента не должно быть своих размеров, он должен заполнять предоставленную ему область.
- Деление только по БЭМ-сущностям.
- Отступы только вверх. Исключение — `padding-bottom` у контейнера.
- Псевдоселекторы `first-child`, ... используем только в крайнем случае.
- Не подключать стили с удаленных источников.
- Каждое CSS-правило должно быть на отдельной строке.
- ??? Дизайнеры могут ошибаться — иногда надо делать запросы на изменение макета, если они нарисовали что-то переусложненное.
- Футер страницы должен быть всегда прижат к низу страницы, даже если на странице мало контента.
- Использовать `!important` только в крайних случаях.
- Использовать `transform: translate()` для выравнивания элементов только в крайних случаях.
- Если клиент предоставил макеты с кастомными шрифтами, проверить, свободные ли они и, если нет, то запросить купленные файлы шрифтов.
- Если не требуется поддержка старых браузеров, шрифты должны быть в форматах `.woff2`, `.woff`. Сначала подключать `.woff2` шрифты, затем — `.woff`
  ```css
  @font-face {
    font-family: "Lato";
    src: url("../fonts/lato-regular.woff2"), url("../fonts/lato-regular.woff");
    font-weight: 400;
    font-style: normal;
  }
  ```
- Разные начертания одного и того же шрифта подключайте под одним именем, но для разных `font-weight` и `font-style`.
  ```css
  @font-face {
    font-family: "Lato";
    src: url("../fonts/lato-regular.woff2"), url("../fonts/lato-regular.woff");
    font-weight: 400;
    font-style: normal;
  }
  @font-face {
    font-family: "Lato";
    src: url("../fonts/lato-italic.woff2"), url("../fonts/lato-italic.woff");
    font-weight: 400;
    font-style: italic;
  }
  ```
- Всегда использовать как минимум один запасной шрифт и одно запасное семейство.
  ```css
  h1 {
    font-family: Кастомный шрифт, Arial, sans-serif;
  }
  ```
- Названия шрифтов, содержащие пробелы, цифры или знаки пунктуации, кроме дефисов, заключать в кавычки.
  ```css
  h1 {
    font-family: "Times New Roman", serif;
  }
  ```
- Не использовать простой `:hover` для отображения новых элементов, которые нелегко достигнуть мышкой (например для отображения пунктов меню).