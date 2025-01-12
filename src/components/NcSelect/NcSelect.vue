<!--
	- @copyright 2022 Christopher Ng <chrng8@gmail.com>
	-
	- @author Christopher Ng <chrng8@gmail.com>
	-
	- @license AGPL-3.0-or-later
	-
	- This program is free software: you can redistribute it and/or modify
	- it under the terms of the GNU Affero General Public License as
	- published by the Free Software Foundation, either version 3 of the
	- License, or (at your option) any later version.
	-
	- This program is distributed in the hope that it will be useful,
	- but WITHOUT ANY WARRANTY; without even the implied warranty of
	- MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
	- GNU Affero General Public License for more details.
	-
	- You should have received a copy of the GNU Affero General Public License
	- along with this program. If not, see <http://www.gnu.org/licenses/>.
	-
-->

<docs>
### Description

General purpose multiselect component.

### Basic examples

```vue
<template>
	<div class="grid">
		<div v-for="{ title, props } in selectArray"
			class="container">
			<label :for="props.inputId">{{ title }}</label>
			<NcSelect v-bind="props"
				v-model="props.value" />
		</div>
	</div>
</template>

<script>
import GenRandomId from '../../utils/GenRandomId.js'

const getRandomId = () => {
	return `select-${GenRandomId()}`
}

const selectArray = [
	{
		title: 'Simple',
		props: {
			inputId: getRandomId(),
			options: [
				'foo',
				'bar',
				'baz',
				'qux',
				'quux',
			],
		},
	},

	{
		title: 'Multiple (with placeholder)',
		props: {
			inputId: getRandomId(),
			multiple: true,
			placeholder: 'Select multiple options',
			options: [
				'foo',
				'bar',
				'baz',
				'qux',
				'quux',
			],
		},
	},

	{
		title: 'Multiple (objects, pre-selected, stay open on select)',
		props: {
			inputId: getRandomId(),
			multiple: true,
			closeOnSelect: false,
			options: [
				{
					id: 'foo',
					label: 'Foo',
				},
				{
					id: 'bar',
					label: 'Bar',
				},
				{
					id: 'baz',
					label: 'Baz',
				},
				{
					id: 'qux',
					label: 'Qux',
				},
				{
					id: 'quux',
					label: 'Quux',
				},
				{
					id: 'corge',
					label: 'Corge',
				},
				{
					id: 'grault',
					label: 'Grault',
				},
				{
					id: 'garply',
					label: 'Garply',
				},
				{
					id: 'waldo',
					label: 'Waldo',
				},
				{
					id: 'fred',
					label: 'Fred',
				},
			],
			value: [
				{
					id: 'foo',
					label: 'Foo',
				},
				{
					id: 'bar',
					label: 'Bar',
				},
			],
		},
	},
]

export default {
	data() {
		return {
			selectArray,
		}
	},
}
</script>

<style>
.grid {
	display: grid;
	grid-template-columns: repeat(2, 1fr);
	gap: 10px;
}

.container {
	display: flex;
	flex-direction: column;
	gap: 2px 0;
}
</style>
```

### No wrap example

The `noWrap` prop is set to `true` and the `max-width` of the multiselect
parent container is limited to `350px`

```vue
<template>
	<div class="grid">
		<div class="container">
			<label :for="data1.props.inputId">{{ data1.title }}</label>
			<NcSelect :no-wrap="false"
				v-bind="data1.props"
				v-model="data1.props.value" />
		</div>
		<div class="container">
			<label :for="data2.props.inputId">{{ data2.title }}</label>
			<NcSelect :no-wrap="true"
				v-bind="data2.props"
				v-model="data2.props.value" />
		</div>
	</div>
</template>

<script>
import GenRandomId from '../../utils/GenRandomId.js'

const getRandomId = () => {
	return `select-${GenRandomId()}`
}

const data1 = {
	title: 'Wrapped (Default)',
	props: {
		inputId: getRandomId(),
		multiple: true,
		closeOnSelect: false,
		options: [
			'foo',
			'bar',
			'baz',
			'qux',
			'quux',
			'corge',
			'grault',
			'garply',
			'waldo',
			'fred',
		],
		value: [
			'foo',
			'bar',
			'baz',
			'qux',
			'quux',
			'corge',
			'grault',
			'garply',
			'waldo',
			'fred',
		],
	},
}

const data2 = {
	title: 'Not wrapped',
	props: {
		inputId: getRandomId(),
		multiple: true,
		closeOnSelect: false,
		options: [
			'foo',
			'bar',
			'baz',
			'qux',
			'quux',
			'corge',
			'grault',
			'garply',
			'waldo',
			'fred',
		],
		value: [
			'foo',
			'bar',
			'baz',
			'qux',
			'quux',
			'corge',
			'grault',
			'garply',
			'waldo',
			'fred',
		],
	},
}

export default {
	data() {
		return {
			data1,
			data2,
		}
	},
}
</script>

<style>
.grid {
	display: grid;
	grid-template-columns: repeat(1, 1fr);
	gap: 10px;
}

.container {
	max-width: 350px;
	display: flex;
	flex-direction: column;
	gap: 2px 0;
}
</style>
```

### User select examples

```vue
<template>
	<div class="grid">
		<div v-for="{ title, props } in selectArray"
			class="container">
			<label :for="props.inputId">{{ title }}</label>
			<NcSelect v-bind="props"
				v-model="props.value" />
		</div>
	</div>
</template>

<script>
import AccountGroup from '@mdi/svg/svg/account-group.svg?raw'
import Email from '@mdi/svg/svg/email.svg?raw'

import GenRandomId from '../../utils/GenRandomId.js'

const getRandomId = () => {
	return `select-${GenRandomId()}`
}

const selectArray = [
	{
		title: 'User select',
		props: {
			inputId: getRandomId(),
			userSelect: true,
			options: [
				{
					id: '0-john',
					displayName: 'John',
					isNoUser: false,
					subtitle: 'john@example.org',
					icon: '',
				},
				{
					id: '0-emma',
					displayName: 'Emma',
					isNoUser: false,
					subtitle: 'emma@example.org',
					icon: '',
				},
				{
					id: '0-olivia',
					displayName: 'Olivia',
					isNoUser: false,
					subtitle: 'olivia@example.org',
					icon: '',
				},
				{
					id: '0-noah',
					displayName: 'Noah',
					isNoUser: false,
					subtitle: 'noah@example.org',
					icon: '',
				},
				{
					id: '0-oliver',
					displayName: 'Oliver',
					isNoUser: false,
					subtitle: 'oliver@example.org',
					icon: '',
				},
				{
					id: '1-admin',
					displayName: 'Admin',
					isNoUser: true,
					subtitle: null,
					iconSvg: AccountGroup,
					iconTitle: 'Group icon',
				},
				{
					id: '2-org@example.org',
					displayName: 'Organization',
					isNoUser: true,
					subtitle: 'org@example.org',
					iconSvg: Email,
					iconTitle: 'Email icon',
				},
			],
		},
	},

	{
		title: 'Multiple user select (stay open on select)',
		props: {
			inputId: getRandomId(),
			userSelect: true,
			multiple: true,
			closeOnSelect: false,
			options: [
				{
					id: '0-john',
					displayName: 'John',
					isNoUser: false,
					subtitle: 'john@example.org',
					icon: '',
				},
				{
					id: '0-emma',
					displayName: 'Emma',
					isNoUser: false,
					subtitle: 'emma@example.org',
					icon: '',
				},
				{
					id: '0-olivia',
					displayName: 'Olivia',
					isNoUser: false,
					subtitle: 'olivia@example.org',
					icon: '',
				},
				{
					id: '0-noah',
					displayName: 'Noah',
					isNoUser: false,
					subtitle: 'noah@example.org',
					icon: '',
				},
				{
					id: '0-oliver',
					displayName: 'Oliver',
					isNoUser: false,
					subtitle: 'oliver@example.org',
					icon: '',
				},
				{
					id: '1-admin',
					displayName: 'Admin',
					isNoUser: true,
					subtitle: null,
					iconSvg: AccountGroup,
					iconTitle: 'Group icon',
				},
				{
					id: '2-org@example.org',
					displayName: 'Organization',
					isNoUser: true,
					subtitle: 'org@example.org',
					iconSvg: Email,
					iconTitle: 'Email icon',
				},
			],
		},
	},
]

export default {
	data() {
		return {
			selectArray,
		}
	},
}
</script>

<style>
.grid {
	display: grid;
	grid-template-columns: repeat(1, 500px);
	gap: 10px;
}

.container {
	display: flex;
	flex-direction: column;
	gap: 2px 0;
}
</style>
```
</docs>

<template>
	<VueSelect class="select"
		:class="{
			'select--no-wrap': noWrap,
		}"
		v-bind="propsToForward"
		v-on="$listeners"
		@search="searchString => search = searchString">
		<template #open-indicator="{ attributes }">
			<ChevronDown v-bind="attributes"
				fill-color="var(--vs-controls-color)"
				:size="26" />
				<!-- Set size to 26 to make up for the increased padding of this icon -->
		</template>
		<template #option="option">
			<NcListItemIcon v-if="userSelect"
				v-bind="option"
				:title="option[localLabel]"
				:search="search" />
			<NcEllipsisedOption v-else
				:name="String(option[localLabel])"
				:search="search" />
		</template>
		<template #selected-option="selectedOption">
			<NcListItemIcon v-if="userSelect"
				v-bind="selectedOption"
				:title="selectedOption[localLabel]"
				:search="search" />
			<NcEllipsisedOption v-else
				:name="String(selectedOption[localLabel])"
				:search="search" />
		</template>
		<template #spinner="spinner">
			<NcLoadingIcon v-if="spinner.loading" />
		</template>
		<template #no-options>
			{{ t('No results') }}
		</template>
		<template v-for="(_, name) in $scopedSlots" #[name]="data">
			<!-- @slot Any combination of slots from https://vue-select.org/api/slots.html -->
			<slot :name="name" v-bind="data" />
		</template>
	</VueSelect>
</template>

<script>
import VueSelect from 'vue-select'
import 'vue-select/dist/vue-select.css'

import ChevronDown from 'vue-material-design-icons/ChevronDown.vue'
import Close from 'vue-material-design-icons/Close.vue'

import NcEllipsisedOption from '../NcEllipsisedOption/index.js'
import NcListItemIcon from '../NcListItemIcon/index.js'
import NcLoadingIcon from '../NcLoadingIcon/index.js'

import l10n from '../../mixins/l10n.js'

export default {
	name: 'NcSelect',

	components: {
		ChevronDown,
		NcEllipsisedOption,
		NcListItemIcon,
		NcLoadingIcon,
		VueSelect,
	},

	mixins: [
		l10n,
	],

	props: {
		// Add VueSelect props to $props
		...VueSelect.props,

		/**
		 * Close the dropdown when selecting an option
		 *
		 * @see https://vue-select.org/api/props.html#closeonselect
		 */
		closeOnSelect: {
			type: Boolean,
			default: true,
		},

		/**
		 * Replace default vue-select components
		 *
		 * @see https://vue-select.org/api/props.html#components
		 */
		components: {
			type: Object,
			default: () => ({
				Deselect: {
					render: createElement => createElement(Close, {
						props: {
							size: 20,
							fillColor: 'var(--vs-controls-color)',
						},
						style: {
							cursor: 'pointer',
						},
					}),
				},
			}),
		},

		/**
		 * Disable the component
		 *
		 * @see https://vue-select.org/api/props.html#disabled
		 */
		disabled: {
			type: Boolean,
			default: false,
		},

		/**
		 * Callback to determine if the provided option should
		 * match the current search text. Used to determine
		 * if the option should be displayed.
		 *
		 * Defaults to the internal vue-select function documented at the link
		 * below
		 *
		 * Enabling `userSelect` will automatically set this to filter by the
		 * `displayName` and `subtitle` properties of the user option object
		 * unless this prop is set explicitly
		 *
		 * @see https://vue-select.org/api/props.html#filterby
		 */
		filterBy: {
			type: Function,
			default: null,
		},

		/**
		 * Input element id
		 *
		 * @see https://vue-select.org/api/props.html#inputid
		 */
		inputId: {
			type: String,
			default: null,
		},

		/**
		 * Key of the displayed label for object options
		 *
		 * Defaults to `'label'`
		 *
		 * Enabling `userSelect` will automatically set this to `'displayName'`
		 * unless this prop is set explicitly
		 *
		 * @see https://vue-select.org/api/props.html#label
		 */
		label: {
			type: String,
			default: null,
		},

		/**
		 * Show the loading icon
		 *
		 * @see https://vue-select.org/api/props.html#loading
		 */
		loading: {
			type: Boolean,
			default: false,
		},

		/**
		 * Allow selection of multiple options
		 *
		 * @see https://vue-select.org/api/props.html#multiple
		 */
		multiple: {
			type: Boolean,
			default: false,
		},

		/**
		 * Disable automatic wrapping when selected options overflow the width
		 */
		noWrap: {
			type: Boolean,
			default: false,
		},

		/**
		 * Array of options
		 *
		 * @type {Array<string | number | { [key: string | number]: any }>}
		 *
		 * @see https://vue-select.org/api/props.html#options
		 */
		options: {
			type: Array,
			default: () => [],
		},

		/**
		 * Placeholder text
		 *
		 * @see https://vue-select.org/api/props.html#placeholder
		 */
		placeholder: {
			type: String,
			default: '',
		},

		/**
		 * Enable the user selector with avatars
		 *
		 * Objects must contain the data expected by the
		 * [NcAvatar](#/Components/NcAvatar) component
		 */
		userSelect: {
			type: Boolean,
			default: false,
		},

		/**
		 * Currently selected value
		 *
		 * The `v-model` directive may be used for two-way data binding
		 *
		 * @type {string | number | { [key: string | number]: any } | Array<any>}
		 *
		 * @see https://vue-select.org/api/props.html#value
		 */
		value: {
			type: [String, Number, Object, Array],
			default: null,
		},

		/**
		 * Any available prop
		 *
		 * @see https://vue-select.org/api/props.html
		 */
		// Not an actual prop but needed to show in vue-styleguidist docs
		// eslint-disable-next-line
		' ': {},
	},

	emits: [
		/**
		 * All events from https://vue-select.org/api/events.html
		 */
		// Not an actual event but needed to show in vue-styleguidist docs
		' ',
	],

	data() {
		return {
			search: '',
		}
	},

	computed: {
		localFilterBy() {
			if (this.filterBy !== null) {
				return this.filterBy
			}

			if (this.userSelect) {
				return (option, label, search) => {
					return (`${label} ${option.subtitle}` || '')
						.toLocaleLowerCase()
						.indexOf(search.toLocaleLowerCase()) > -1
				}
			}
			return null
		},

		localLabel() {
			if (this.label !== null) {
				return this.label
			}

			if (this.userSelect) {
				return 'displayName'
			}
			return 'label'
		},

		propsToForward() {
			const {
				// Custom overrides of vue-select props
				filterBy,
				label,
				// Props handled by the component itself
				noWrap,
				userSelect,
				// Props to forward
				...initialPropsToForward
			} = this.$props

			const propsToForward = {
				...initialPropsToForward,
				label: this.localLabel,
			}

			if (this.localFilterBy) {
				propsToForward.filterBy = this.localFilterBy
			}

			return propsToForward
		},
	},
}
</script>

<style lang="scss" scoped>
.select {
	/* Set custom vue-select CSS variables */

	/* Search Input */
	--vs-search-input-color: var(--color-main-text);
	--vs-search-input-bg: var(--color-main-background);
	--vs-search-input-placeholder-color: var(--color-text-maxcontrast);

	/* Font */
	--vs-font-size: var(--default-font-size);
	--vs-line-height: var(--default-line-height);

	/* Disabled State */
	--vs-state-disabled-bg: var(--color-background-dark);
	--vs-state-disabled-color: var(--color-text-maxcontrast);
	--vs-state-disabled-controls-color: var(--color-text-maxcontrast);
	--vs-state-disabled-cursor: not-allowed;

	/* Borders */
	--vs-border-color: var(--color-border-dark);
	--vs-border-width: 2px;
	--vs-border-style: solid;
	--vs-border-radius: var(--border-radius-large);

	/* Component Controls: Clear, Open Indicator */
	--vs-controls-color: var(--color-text-maxcontrast);

	/* Selected */
	--vs-selected-bg: var(--color-background-dark);
	--vs-selected-color: var(--color-main-text);

	/* Dropdown */
	--vs-dropdown-bg: var(--color-main-background);
	--vs-dropdown-color: var(--color-main-text);
	--vs-dropdown-box-shadow: 0px 2px 2px 0px var(--color-box-shadow);

	/* Options */
	--vs-dropdown-option-padding: 8px 20px;

	/* Active State */
	--vs-dropdown-option--active-bg: var(--color-background-hover);
	--vs-dropdown-option--active-color: var(--color-main-text);

	/* Deselect State */
	--vs-dropdown-option--deselect-bg: var(--color-error);
	--vs-dropdown-option--deselect-color: #fff;

	/* Transitions */
	--vs-transition-duration: 0ms;

	/* Override default vue-select styles */
	min-height: $clickable-area;
	min-width: 260px;
	margin: 0;

	&--no-wrap {
		&:deep(.vs__selected-options) {
			flex-wrap: nowrap;
			overflow: auto;
		}
	}

	&:deep(.vs__selected) {
		min-height: 36px;
		padding: 0 0.5em;
	}

	&:deep(.vs__clear) {
		margin-right: 2px;
	}
}
</style>
