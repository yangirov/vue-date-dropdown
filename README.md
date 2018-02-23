# Vue Date Dropdown

> A Vue date dropdown component

[![npm version](https://badge.fury.io/js/vue-date-dropdown.svg)](https://badge.fury.io/js/vue-date-dropdown)

![Example](./assets/vue-date-dropdown.gif)

## Contents

 - [Installing](https://github.com/yangirov/vue-date-dropdown#installing)
 - [Examples](https://github.com/yangirov/vue-date-dropdown#examples)
 - [API](https://github.com/yangirov/vue-date-dropdown#api)

## Installing

```bash
npm install vue-date-dropdown --save

yarn add vue-date-dropdown
```

```js
import DateDropdown from 'vue-date-dropdown'

export default {
	...
	components: {
		DateDropdown
	},
	data () {
		return {
			selectedDate: '',
			...
		}
	}
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
	data() {
		return {
			selectedDate: '',
			...
		}
	}
	...
});
<script>
```

## Examples

See the demo in the [example](https://github.com/yangirov/vue-date-dropdown/tree/master/example) folder.

Setting a default date

```html
<date-dropdown default="1995-01-10" v-model="selectedDate" />
```

Setting a min date

```html
<date-dropdown min="1960" v-model="selectedDate" />
```

Setting a max date

```html
<date-dropdown max="2018" v-model="selectedDate" />
```

Setting a range of dates

```html
<date-dropdown min="1960" max="2017" v-model="selectedDate" />
```

Setting Russian names of months

```html
<date-dropdown
	v-model="selectedDate" 
	months-names="Январь, Февраль, Март, Апрель, Май, Июнь, Июль, Август, Сентябрь, Октябрь, Ноябрь, Декабрь">
<date-dropdown>
```

## API

### Props

| Name         | Type     | Description                                      |
| :------------| :------- | :------------------------------------------------|
| default      | String   | Set default date.                                |
| min          | String   | Limits the year to a minimum specified value.    |
| max          | String   | Limits the year to a maximum specified value.    |
| months-names | String   | The alternative names of month.                  |