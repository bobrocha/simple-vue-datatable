<template>
	<div class="data-table-container">
		<table class="data-table">
			<thead>
				<tr>
					<th
						@click="sortTableByFieldId(field.id)"
						class="field-title"
						v-for="(field, id) in fields"
						:key="id"
					>{{ field.title }}</th>
					<th class="control">
						<button class="filter-row-button" @click="toggleFilterRow">{{ filter_row_button_text }}</button>
					</th>
				</tr>
				<tr v-show="filter_row_toggle" class="filter-row">
					<slot name="filter-row"></slot>
					<th></th>
				</tr>
				<tr class="insert-row">
					<slot name="insert-row"></slot>
					<th class="control">
						<button type="submit">Add Row</button>
						<button>Clear</button>
					</th>
				</tr>
			</thead>
			<tbody>
				<tr
					v-for="(row, i) in displayed_rows"
					:key="i"
				>
				<td
					v-for="(value, i) in Object.values(row)"
					:key="i"
				>{{ value }}</td>
				<td class="control">
					<button>Edit</button>
					<button>Delete</button>
				</td>
				</tr>
			</tbody>
		</table>
		<ul v-show="pages.length > 1" class="pagination">
			<li class="pagination-item"><button :disabled="isFirstPage" @click="switchPage(first_page_number)" class="pagination-control">First</button></li>
			<li class="pagination-item"><button :disabled="isFirstPage" @click="previousPage" class="pagination-control">Previous</button></li>
			<li class="pagination-item"><input v-model.trim="input_page_number" :min="first_page_number + 1" :max="last_page_number + 1" class="pagination-control page-number-input" type="number"></li>
			<li class="pagination-item"><button @click="enterPageNumber" class="pagination-control">Enter</button></li>
			<li class="pagination-item">{{ pagoLocation }}</li>
			<li class="pagination-item"><button :disabled="isLastPage" @click="nextPage" class="pagination-control">Next</button></li>
			<li class="pagination-item"><button :disabled="isLastPage" @click="switchPage(last_page_number)" class="pagination-control">Last</button></li>
		</ul>
	</div>
</template>
<script>

export default {
	props : {
		fields     : Array,
		filter_row : Object,
		rows       : Array,
	},
	data() {
		return {
			displayed_rows         : null,
			sort_key               : false,
			filter_row_toggle      : false,
			filter_row_button_text : 'Show Filter',
			total_pages            : null,
			page_size              : null,
			pages                  : null,
			page                   : null,
			page_number            : 0,
			first_page_number      : null,
			last_page_number       : null,
			input_page_number      : null,
		}
	},
	created() {
		this.setPageSize(12);

		this.paginate(this.rows);
		this.displayed_rows = this.getPage();
	},
	methods : {
		sortTableByFieldId(id) {
			const copy_rows = this.rows;

			copy_rows.sort((a, b) => {

				if(a[id] === b[id]) {
					return 0;
				}

				// Ascending
				if(this.sort_key === false) {
					return a[id] < b[id] ? -1 : 1;
				}

				// Descending
				return a[id] > b[id] ? -1 : 1;
			});

			this.sort_key = !this.sort_key;

			this.paginate(copy_rows);

			this.displayed_rows = this.getPage();
		},
		toggleFilterRow() {
			this.filter_row_toggle = !this.filter_row_toggle;

			if(this.filter_row_toggle) {
				this.filter_row_button_text = 'Hide Filter Row';
			} else {
				this.filter_row_button_text = 'Show Filter Row';
				this.$emit('clearFilterRow');
			}
		},
		filterRows(filter_row_obj) {
			const object_keys = Object.keys(filter_row_obj);

			const filtered = this.rows.filter(row => {
				return object_keys.every(key => {
					const found_value = String(row[key]).toLowerCase();
					const input_value = String(filter_row_obj[key]).toLowerCase();

					return found_value.includes(input_value);
				});
			});

			this.page_number = 0;
			this.paginate(filtered);
			this.displayed_rows = this.page;
		},
		setPageSize(size) {
			this.page_size = size;
		},
		paginate(rows = null) {
			this.total_pages = Math.ceil(rows.length / this.page_size);

			const pages = [];
			let page    = [];

			for(let i = 0; i < rows.length; i++) {
				const is_page    = (i + 1) % this.page_size === 0;
				const is_the_end = i === rows.length -1;

				page.push(rows[i]);

				/**
				 * If we have a full page, clear out the
				 * pages array and push page to pages
				 */
				if(is_page) {
					pages.push(page);
					page = [];
				}

				/**
				 * If we have reached the end of the array and the page is not empty
				 * push the ramaining push elements to pages.
				 */
				if(is_the_end && page.length) {
					pages.push(page);
					page = [];
				}
			}

			this.first_page_number = 0;
			this.last_page_number  = pages.length -1;
			this.pages             = pages;
			this.page              = pages[this.page_number];
		},
		getPage() {
			return this.page;
		},
		nextPage() {
			this.page_number++;

			if(this.page_number > this.last_page_number) {
				this.page_number = this.last_page_number
			}
			this.switchPage(this.page_number);
		},
		previousPage() {
			this.page_number--;

			if(this.page_number < this.first_page_number) {
				this.page_number = this.first_page_number;
			}

			this.switchPage(this.page_number);
		},
		switchPage(page_number) {
			this.displayed_rows = this.pages[page_number];
			this.page_number    = page_number;
		},
		enterPageNumber() {
			if(this.input_page_number) {
				this.switchPage(this.input_page_number - 1);
			}
		},
	},
	computed : {
		isFirstPage() {
			return this.page_number == this.first_page_number;
		},
		isLastPage() {
			return this.page_number == this.last_page_number;
		},
		pagoLocation() {
			return `Page ${this.page_number + 1} of ${this.last_page_number + 1}`;
		},
	},
	watch : {
		filter_row : {
			handler(filter_row_obj) {
				this.filterRows(filter_row_obj);
			},
			deep: true
		},
	}
}
</script>
<style>
*,
*::before,
*::after {
	box-sizing: border-box;
}

table.data-table {
	width: 100%;
	border-collapse: collapse;
	border: 1px solid #ddd;
}

.data-table tr {
	border-top: 1px solid #ddd;
}

.data-table tr:nth-child(odd) td {
	background-color: #F3F3F3;
}

.data-table td, .data-table th {
	padding: 8px 10px;
	border: 1px solid #ddd;
}

.data-table .field-title {
	cursor: pointer;
}

.data-table input {
	width: 100%;
}

.data-table .control {
	text-align: center;
	padding: 0;
}

.data-table .control button {
	border-radius: 3px;
	border: 1px solid #ddd;
	background-color: #dedcdc;
	cursor: pointer;
}

.data-table .control button:hover {
	background-color: #b1b0b0;
}

.data-table .filter-row {
	background-image: linear-gradient(rgb(189, 188, 188), rgb(131, 130, 130));
}

.data-table .insert-row-button,
.data-table .filter-row-button {
	display: block;
	margin: 0.5rem auto;
}

.pagination {
	text-align: center;
	background-color: #F3F3F3;
	list-style-type: none;
	padding: 0.5rem;
	margin: 0;
	border: 1px solid #ddd;
}

.pagination .pagination-item {
	display: inline-block;
	margin : 0 0.5rem;
}

.pagination .page-number-input {
	width: 75px;
}
</style>