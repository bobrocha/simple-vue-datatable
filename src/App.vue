<template>
	<div id="app">
		<data-table
			:fields="fields"
			:filter_row="filter_row"
			@clearFilterRow="clearFilterRow"
			:rows="rows"
			:items_per_page="12"
		>
			<template v-slot:filter-row>
				<td><input v-model="filter_row.month"></td>
				<td><input v-model="filter_row.amount"></td>
				<td><input v-model="filter_row.year"></td>
			</template>
		</data-table>
	</div>
</template>

<script>
import DataTable from './DataTable.vue';

// Fields used to build table header with
const fields = [
	{
		id    : 'month',
		title : 'Month'
	},
	{
		id    : 'amount',
		title : 'Amount'
	},
	{
		id    : 'year',
		title : 'Year'
	},
];

// Dummy rows
const rows = [
	///////////////////////////////// 2013
	{
		month  : 'January',
		amount : 3.49,
		year   : 2013,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2013,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2013,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2013,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2013,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2013,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2013,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2013,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2013,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2013,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2013,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2013,
	},
	///////////////////////////////// 2014
	{
		month  : 'January',
		amount : 3.49,
		year   : 2014,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2014,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2014,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2014,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2014,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2014,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2014,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2014,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2014,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2014,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2014,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2014,
	},
	///////////////////////////////// 2015
	{
		month  : 'January',
		amount : 3.49,
		year   : 2015,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2015,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2015,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2015,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2015,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2015,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2015,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2015,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2015,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2015,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2015,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2015,
	},
	///////////////////////////////// 2016
	{
		month  : 'January',
		amount : 3.49,
		year   : 2016,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2016,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2016,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2016,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2016,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2016,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2016,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2016,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2016,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2016,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2016,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2016,
	},
	///////////////////////////////// 2017
	{
		month  : 'January',
		amount : 3.49,
		year   : 2017,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2017,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2017,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2017,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2017,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2017,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2017,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2017,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2017,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2017,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2017,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2017,
	},
	///////////////////////////////// 2018
	{
		month  : 'January',
		amount : 3.49,
		year   : 2018,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2018,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2018,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2018,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2018,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2018,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2018,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2018,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2018,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2018,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2018,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2018,
	},
	///////////////////////////////// 2019
	{
		month  : 'January',
		amount : 3.49,
		year   : 2019,
	},
	{
		month  : 'February',
		amount : 3.50,
		year   : 2019,
	},
	{
		month  : 'March',
		amount : 3.51,
		year   : 2019,
	},
	{
		month  : 'April',
		amount : 3.52,
		year   : 2019,
	},
	{
		month  : 'May',
		amount : 3.53,
		year   : 2019,
	},
	{
		month  : 'June',
		amount : 3.54,
		year   : 2019,
	},
	{
		month  : 'July',
		amount : 3.55,
		year   : 2019,
	},
	{
		month  : 'August',
		amount : 3.56,
		year   : 2019,
	},
	{
		month  : 'September',
		amount : 3.57,
		year   : 2019,
	},
	{
		month  : 'October',
		amount : 3.58,
		year   : 2019,
	},
	{
		month  : 'November',
		amount : 3.59,
		year   : 2019,
	},
	{
		month  : 'December',
		amount : 3.60,
		year   : 2019,
	},
	///////////////////////////////// 2020
	{
		month  : 'January',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'February',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'March',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'April',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'May',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'June',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'July',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'August',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'September',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'October',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'November',
		amount : 3.49,
		year   : 2020,
	},
	{
		month  : 'December',
		amount : 3.49,
		year   : 2020,
	},
];
export default {
	components :{
		DataTable,
	},
	data() {
		return {
			fields     : fields,
			insert_row : {},
			filter_row : {},
			rows       : rows,
		}
	},
}
</script>