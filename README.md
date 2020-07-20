# Simple Vue DataTable

This simple Vue datatable can be used to display paginated data. 

Features include:

* Pagination
* Sorting
* Filtering


## Usage

In your app import the Datatable. The fields property is your table columns/fields, typically this maps to set of columns belonging to a schema relation/table. The rows property should be in json format and is what will display on your table, this should match the fields property described above as they will be your html table  column headers. The last property "items_per_page" will dictate how many items/rows are displayed per page.

The slot "filter_row" is where you will define what filter columns will be included.

```
<data-table
	:fields="fields"
	:filter_row="filter_row"
	:rows="rows"
	:items_per_page="12"
>
	<template v-slot:filter-row>
		<td><input v-model="filter_row.month"></td>
		<td><input v-model="filter_row.amount"></td>
		<td><input v-model="filter_row.year"></td>
	</template>
</data-table>
```
https://youtu.be/eWzW1oE0IV0
