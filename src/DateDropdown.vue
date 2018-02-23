<template>
	<div class="date-dropdown-container">

		<!-- Day -->
		<div class="date-dropdown-select-wrapper">
			<select v-model="selectedDay" class="date-dropdown-select day">
				<option v-for="day in days" :key="day.day">
					{{ day.day }}
				</option>
			</select>
		</div>

		<!-- Month -->
		<div class="date-dropdown-select-wrapper">
			<select v-model="selectedMonth" @change="updateDays()" class="date-dropdown-select month">
				<option v-for="(month, index) in months" :value="index" :key="month.month">
					{{ month.month }}
				</option>
			</select>
		</div>

		<!-- Year -->
		<div class="date-dropdown-select-wrapper">
			<select v-model="selectedYear" @change="updateDays()" class="date-dropdown-select year">
				<option v-for="year in years" :key="year.year">
					{{ year.year }}
				</option>
			</select>
		</div>

	</div>
</template>

<script>
	const defaultMonths = {
		0: 'January',
		1: 'February',
		2: 'March',
		3: 'April',
		4: 'May',
		5: 'June',
		6: 'July',
		7: 'August',
		8: 'September',
		9: 'October',
		10: 'November',
		11: 'December'
	}

	export default {
		name: "DateDropdown",
		props: {
			default: {
				type: String,
				required: false
			},
			min: {
				type: String,
				required: false
			},
			max: {
				type: String,
				required: false
			},
			monthsNames: {
				type: String,
				required: false
			}
		},

		data () {
			return {
				days: [],
				selectedDay: '',
				selectedMonth: '',
				selectedYear: ''
			}
		},

		computed: {
			// Returns if there are default date settings.
			initialDate() {
				return !! (this.default || this.min)
			},

			// The date property, converted to a date.
			specifiedDate() {
				return new Date(this.default)
			},

			// The minimum date the will allow user to select.
			minDate() {
				if (this.min)
					return new Date(this.min)

				return
			},

			// The maximum date the will allow user to select.
			maxDate() {
				if (this.max)
					return new Date(this.max)

				return
			},

			// Returns a formatted date e.g. 01.02.2018.
			calculatedDate() {
				const day = this.selectedDay >= 10 ? this.selectedDay : `0${this.selectedDay}`
				const month = this.selectedMonth + 1 >= 10 ? this.selectedMonth + 1 : `0${this.selectedMonth + 1}`

				return `${day}.${month}.${this.selectedYear}`
			},

			// The alternative names of months
			dividedNamesOfMonths() {
				if (this.monthsNames)
					return this.monthsNames.replace(/\s/g, '').split(',')

				return
			},

			// Computes a list of month.
			months() {
				let months = []

				for (let i = 0; i < 12; i++) {
					if (this.dividedNamesOfMonths)
						months.push(this.dividedNamesOfMonths[i])
					else
						months.push(defaultMonths[i])
				}

				return months.map((month, index) => {
					return { month, selected: index === this.selectedMonth }
				})
			},

			// Computes a list of years.
			years() {
				// Set the first year of the array.
				let firstYear

				if (this.min) {
					firstYear = this.minDate.getFullYear()
				} else if (this.default) {
					firstYear = this.specifiedDate.getFullYear()
				} else {
					firstYear = (new Date).getFullYear()
				}

				// Create a range of years to loop through which is either the maximum
				// date minus the first year, or simply 100.
				let through = this.max ? (this.maxDate.getFullYear() + 1) - firstYear : 101
				let years = []

				for (let i = firstYear, len = firstYear + through; i < len; i++)
					years.push(i)

				return years.map((year) => {
					return { year, selected: year === this.selectedYear }
				})
			}
		},

		methods: {
			getDays() {
				let days = []
				let daysNumberOfMonth = new Date(this.selectedYear, this.selectedMonth + 1, 0).getDate()

				for (let i = 1; i < daysNumberOfMonth + 1; i++)
					days.push(i)

				return days.map((day) => {
					return { day, selected: days === this.selectedDay }
				})
			},

			updateDays() {
				this.days = this.getDays()
			},

			// Send data to upper component.
			sendDate() {
				const date = this.format ? this.format(this.calculatedDate) : this.calculatedDate

				this.$emit('input', date)
			},

			// Set the initial date.
			setDate() {
				this.updateDays()

				// If a value property has been passed to the component, that will be
				// used instead of the current day.
				let date

				if (this.min && this.max && !this.default) {
					date = new Date(this.min)
				} else if (this.default) {
					date = new Date(this.default)
				} else {
					date = new Date()
				}

				if (this.initialDate)
					this.selectedDay = date.getDate() + 1
				else
					this.selectedDay = date.getDate()

				this.selectedDay = date.getDate()
				this.selectedMonth = date.getMonth()
				this.selectedYear = date.getFullYear()

				this.sendDate()
			}
		},

		created() {
			// Set the date when the component was created
			this.setDate()
		},

		updated() {
			// Send the data on change
			this.sendDate()
		},
	}
</script>

<style scoped>
	.date-dropdown-container {
		display: flex;
	}
	.date-dropdown-select {
		display: inline-block;
		border: 1px solid #e0e0e0;
		border-radius: 3px;
		padding: 8px;
		margin-right: 10px;
	}
</style>