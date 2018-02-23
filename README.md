# Vue Date Dropdown

> A Vue date dropdown component

![Example](./assets/vue-date-dropdown.gif)

## Contents

 - [Installing](https://github.com/yangirov/vue-date-dropdown#installing)
 - [Examples](https://github.com/yangirov/vue-date-dropdown#examples)
 - [API](https://github.com/yangirov/vue-date-dropdown#api)

## Installing

```bash
npm install vue-date-dropdown --save
```

```js
import DateDropdown from 'vue-date-dropdown'

export default {
  ...
  components: {
    DateDropdown
  },
  ...
}
```
Or if you are using CDN version

```js
<script src="vue-date-dropdown.min.js"></script>

<script>
Vue.use(DateDropdown)

new Vue({
	...
});
<script>
```

## Examples

See the demo in the [example](https://github.com/yangirov/vue-date-dropdown/tree/master/example) folder.

Setting a default date

```html
<date-dropdown default="1995-01-10" />
```

Setting a min date

```html
<date-dropdown min="1960-8-16" />
```

Setting a max date

```html
<date-dropdown max="2018-8-16" />
```

Setting a range of dates

```html
<date-dropdown min="1960-8-16" max="2017-8-16" />
```

Setting Russian names of months

```html
<date-dropdown
  months-names="Январь, Февраль, Март, Апрель, Май, Июнь, Июль, Август, Сентябрь, Октябрь, Ноябрь, Декабрь" />
```

## API

### Props

| Name         | Type     | Description                                      |
| :------------| :------- | :------------------------------------------------|
| default      | String   | Set default date.                                |
| min          | String   | Limits the year to a minimum specified value.    |
| max          | String   | Limits the year to a maximum specified value.    |
| months-names | String   | The alternative names of month.                  |