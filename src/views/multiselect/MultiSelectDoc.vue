<template>
	<AppDoc name="MultiSelectDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import MultiSelect from 'primevue/multiselect';

</code></pre>

		<h5>Getting Started</h5>
		<p>MultiSelect requires a value to bind and a collection of arbitrary objects along with the <i>optionLabel</i> property to specify the label property of the option.</p>
<pre v-code><code>
&lt;MultiSelect v-model="selectedCars" :options="cars" optionLabel="brand" placeholder="Select Brands" /&gt;

</code></pre>

<pre v-code.script><code>
data() {
	return {
		selectedCars: null,
		cars: [
			{brand: 'Audi', value: 'Audi'},
			{brand: 'BMW', value: 'BMW'},
			{brand: 'Fiat', value: 'Fiat'},
			{brand: 'Honda', value: 'Honda'},
			{brand: 'Jaguar', value: 'Jaguar'},
			{brand: 'Mercedes', value: 'Mercedes'},
			{brand: 'Renault', value: 'Renault'},
			{brand: 'Volkswagen', value: 'Volkswagen'},
			{brand: 'Volvo', value: 'Volvo'}
		]
	}
}

</code></pre>

        <h5>Chips Display</h5>
        <p>A comma separated list is used by default to display selected items whereas alternative chip mode is provided using the <i>display</i> property to visualize the items as tokens.</p>
<pre v-code><code>
&lt;MultiSelect v-model="selectedCars" :options="cars" optionLabel="brand" placeholder="Select Brands" display="chip"/&gt;

</code></pre>

        <h5>Grouping</h5>
		<p>Options groups are specified with the <i>optionGroupLabel</i> and <i>optionGroupChildren</i> properties.</p>
<pre v-code.script><code>
export default {
    data() {
        return {
            selectedGroupedCities: null,
            groupedCities: [{
                label: 'Germany', code: 'DE', 
                items: [
                    {label: 'Berlin', value: 'Berlin'},
                    {label: 'Frankfurt', value: 'Frankfurt'},
                    {label: 'Hamburg', value: 'Hamburg'},
                    {label: 'Munich', value: 'Munich'}
                ]
            },
            {
                label: 'USA', code: 'US', 
                items: [
                    {label: 'Chicago', value: 'Chicago'},
                    {label: 'Los Angeles', value: 'Los Angeles'},
                    {label: 'New York', value: 'New York'},
                    {label: 'San Francisco', value: 'San Francisco'}
                ]
            },
            {
                label: 'Japan', code: 'JP', 
                items: [
                    {label: 'Kyoto', value: 'Kyoto'},
                    {label: 'Osaka', value: 'Osaka'},
                    {label: 'Tokyo', value: 'Tokyo'},
                    {label: 'Yokohama', value: 'Yokohama'}
                ]
            }]
        }
    }
}
</code></pre>

<pre v-code><code><template v-pre>
&lt;MultiSelect v-model="selectedGroupedCities" :options="groupedCities" 
        optionLabel="label" optionGroupLabel="label" optionGroupChildren="items"&gt;
&lt;/MultiSelect&gt;
</template>
</code></pre>

		<h5>Filtering</h5>
		<p>Filtering allows searching items in the list using an input field at the header. In order to use filtering, enable <i>filter</i> property. By default,
        optionLabel is used when searching and <i>filterFields</i> can be used to customize the fields being utilized. Furthermore, <i>filterMatchMode</i> is available
        to define the search algorithm. Valid values are "contains" (default), "startsWith" and "endsWith".</p>

<pre v-code><code>
&lt;MultiSelect v-model="selectedCars" :options="cars" :filter="true" optionLabel="brand" placeholder="Select Brands"/&gt;

</code></pre>

		<h5>Templating</h5>
		<p>Label of an option is used as the display text of an item by default, for custom content support define an <i>option</i> template that gets the option instance as a parameter.
        In addition <i>value</i>, <i>optiongroup</i>, <i>header</i>, <i>footer</i>, <i>emptyfilter</i> and <i>empty</i> slots are provided for further customization.</p>
<pre v-code><code><template v-pre>
&lt;MultiSelect v-model="selectedCars2" :options="cars" optionLabel="brand" placeholder="Select a Car"&gt;
	&lt;template #value="slotProps"&gt;
		&lt;div class="p-multiselect-car-token" v-for="option of slotProps.value" :key="option.brand"&gt;
			&lt;img :alt="option.brand" :src="'demo/images/car/' + option.brand + '.png'" /&gt;
			&lt;span&gt;{{option.brand}}&lt;/span&gt;
		&lt;/div&gt;
		&lt;template v-if="!slotProps.value || slotProps.value.length === 0"&gt;
            Select Brands
        &lt;/template&gt;
	&lt;/template&gt;
	&lt;template #option="slotProps"&gt;
		&lt;div class="p-multiselect-car-option"&gt;
			&lt;img :alt="slotProps.option.brand" :src="'demo/images/car/' + slotProps.option.brand + '.png'" /&gt;
			&lt;span&gt;{{slotProps.option.brand}}&lt;/span&gt;
		&lt;/div&gt;
	&lt;/template&gt;
&lt;/MultiSelect&gt;
</template>
</code></pre>

		<h5>Properties</h5>
        <p>Any property as style and class are passed to the main container element. Following are the additional properties to configure the component.</p>
		<div class="doc-tablewrapper">
			<table class="doc-table">
				<thead>
                    <tr>
                        <th>Name</th>
                        <th>Type</th>
                        <th>Default</th>
                        <th>Description</th>
                    </tr>
				</thead>
				<tbody>
                    <tr>
                        <td>modelValue</td>
                        <td>any</td>
                        <td>null</td>
                        <td>Value of the component.</td>
                    </tr>
                    <tr>
                        <td>options</td>
                        <td>array</td>
                        <td>null</td>
                        <td>An array of selectitems to display as the available options.</td>
                    </tr>
                    <tr>
                        <td>optionLabel</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Property name or getter function to use as the label of an option.</td>
                    </tr>
                    <tr>
                        <td>optionValue</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Property name or getter function to use as the value of an option, defaults to the option itself when not defined.</td>
                    </tr>
                    <tr>
                        <td>optionDisabled</td>
                        <td>boolean</td>
                        <td>null</td>
                        <td>Property name or getter function to use as the disabled flag of an option, defaults to false when not defined.</td>
                    </tr>
                    <tr>
                        <td>optionGroupLabel</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Property name or getter function to use as the label of an option group.</td>
                    </tr>
                    <tr>
                        <td>optionGroupChildren</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Property name or getter function that refers to the children options of option group.</td>
                    </tr>
                    <tr>
                        <td>scrollHeight</td>
                        <td>string</td>
                        <td>200px</td>
                        <td>Height of the viewport in pixels, a scrollbar is defined if height of list exceeds this value.</td>
                    </tr>
                    <tr>
                        <td>filter</td>
                        <td>boolean</td>
                        <td>false</td>
                        <td>When specified, displays a filter input at header.</td>
                    </tr>
                    <tr>
                        <td>filterPlaceholder</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Placeholder text to show when filter input is empty.</td>
                    </tr>
                    <tr>
                        <td>filterLocale</td>
                        <td>string</td>
                        <td>undefined</td>
                        <td>Locale to use in filtering. The default locale is the host environment's current locale.</td>
                    </tr>
                    <tr>
                        <td>filterMatchMode</td>
                        <td>string</td>
                        <td>contains</td>
                        <td>Defines the filtering algorithm to use when searching the options. Valid values are "contains" (default), "startsWith" and "endsWith"</td>
                    </tr>
                    <tr>
                        <td>filterFields</td>
                        <td>array</td>
                        <td>null</td>
                        <td>Fields used when filtering the options, defaults to optionLabel.</td>
                    </tr>
                    <tr>
                        <td>placeholder</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Label to display when there are no selections.</td>
                    </tr>
                    <tr>
                        <td>disabled</td>
                        <td>boolean</td>
                        <td>false</td>
                        <td>When present, it specifies that the component should be disabled.</td>
                    </tr>
                    <tr>
                        <td>tabindex</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Index of the element in tabbing order.</td>
                    </tr>
                    <tr>
                        <td>inputId</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Identifier of the underlying input element.</td>
                    </tr>
                    <tr>
                        <td>dataKey</td>
                        <td>string</td>
                        <td>null</td>
                        <td>A property to uniquely identify an option.</td>
                    </tr>
                    <tr>
                        <td>ariaLabelledBy</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Establishes relationships between the component and label(s) where its value should be one or more element IDs.</td>
                    </tr>
                    <tr>
                        <td>appendTo</td>
                        <td>string</td>
                        <td>body</td>
                        <td>A valid query selector or an HTMLElement to specify where the overlay gets attached.</td>
                    </tr>
                    <tr>
                        <td>emptyFilterMessage</td>
                        <td>string</td>
                        <td>No results found</td>
                        <td>Text to display when filtering does not return any results. Defaults to value from PrimeVue locale configuration.</td>
                    </tr>
                    <tr>
                        <td>emptyMessage</td>
                        <td>string</td>
                        <td>No results found</td>
                        <td>Text to display when there are no options available. Defaults to value from PrimeVue locale configuration.</td>
                    </tr>
                    <tr>
                        <td>display</td>
                        <td>string</td>
                        <td>comma</td>
                        <td>Defines how the selected items are displayed, valid values are "comma" and "chip".</td>
                    </tr>
				</tbody>
			</table>
		</div>

		<h5>Events</h5>
        <div class="doc-tablewrapper">
            <table class="doc-table">
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Parameters</th>
                        <th>Description</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td>change</td>
                        <td>event.originalEvent: Original event <br />
                            event.value: Selected option value </td>
                        <td>Callback to invoke on value change.</td>
                    </tr>
                    <tr>
                        <td>before-show</td>
                        <td>-</td>
                        <td>Callback to invoke before the overlay is shown.</td>
                    </tr>
                    <tr>
                        <td>before-hide</td>
                        <td>-</td>
                        <td>Callback to invoke before the overlay is hidden.</td>
                    </tr>
                    <tr>
                        <td>show</td>
                        <td>-</td>
                        <td>Callback to invoke when the overlay is shown.</td>
                    </tr>
                    <tr>
                        <td>hide</td>
                        <td>-</td>
                        <td>Callback to invoke when the overlay is hidden.</td>
                    </tr>
                    <tr>
                        <td>filter</td>
                        <td>event.originalEvent: Original event <br />
                            event.value: Filter value </td>
                        <td>Callback to invoke on filter input.</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <h5>Methods</h5>
		<div class="doc-tablewrapper">
			<table class="doc-table">
				<thead>
                    <tr>
                        <th>Name</th>
                        <th>Parameters</th>
                        <th>Description</th>
                    </tr>
				</thead>
				<tbody>
                    <tr>
                        <td>show</td>
                        <td>-</td>
                        <td>Shows the overlay.</td>
                    </tr>
                    <tr>
                        <td>Hide</td>
                        <td>-</td>
                        <td>Hides the overlay.</td>
                    </tr>
				</tbody>
			</table>
		</div>

        <h5>Slots</h5>
		<div class="doc-tablewrapper">
            <table class="doc-table">
				<thead>
                    <tr>
                        <th>Name</th>
                        <th>Parameters</th>
                    </tr>
				</thead>
				<tbody>
                    <tr>
                        <td>option</td>
                        <td>option: Option instance <br />
                            index: Index of the option</td>
                    </tr>
                    <tr>
                        <td>optiongroup</td>
                        <td>option: OptionGroup instance <br />
                            index: Index of the option group</td>
                    </tr>
                     <tr>
                        <td>value</td>
                        <td>value: Value of the component <br />
                            placeholder: Placeholder prop value</td>
                    </tr>
                    <tr>
                        <td>header</td>
                        <td>value: Value of the component <br />
                            options: Displayed options</td>
                    </tr>
                    <tr>
                        <td>footer</td>
                        <td>value: Value of the component <br />
                            options: Displayed options</td>
                    </tr>
                    <tr>
                        <td>emptyfilter</td>
                        <td>-</td>
                    </tr>
                    <tr>
                        <td>empty</td>
                        <td>-</td>
                    </tr>
				</tbody>
			</table>
        </div>

		<h5>Styling</h5>
		<p>Following is the list of structural style classes, for theming classes visit <router-link to="/theming">theming</router-link> page.</p>
		<div class="doc-tablewrapper">
			<table class="doc-table">
				<thead>
                    <tr>
                        <th>Name</th>
                        <th>Element</th>
                    </tr>
				</thead>
				<tbody>
                    <tr>
                        <td>p-multiselect</td>
                        <td>Container element.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-label-container</td>
                        <td>Container of the label to display selected items.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-label-container</td>
                        <td>Label to display selected items.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-trigger</td>
                        <td>Dropdown button.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-filter-container</td>
                        <td>Container of filter input.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-panel</td>
                        <td>Overlay panel for items.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-items</td>
                        <td>List container of items.</td>
                    </tr>
                    <tr>
                        <td>p-multiselect-item</td>
                        <td>An item in the list.</td>
                    </tr>
				</tbody>
			</table>
		</div>

		<h5>Dependencies</h5>
		<p>None.</p>
    </AppDoc>
</template>

<script>
export default {
    data() {
        return {
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
    <div>
        <h5>Basic</h5>
        <MultiSelect v-model="selectedCities1" :options="cities" optionLabel="name" placeholder="Select Cities" />

        <h5>Chips</h5>
        <MultiSelect v-model="selectedCities2" :options="cities" optionLabel="name" placeholder="Select Cities" display="chip" />

        <h5>Grouped</h5>
        <MultiSelect v-model="selectedGroupedCities" :options="groupedCities" optionLabel="label"  optionGroupLabel="label" optionGroupChildren="items" placeholder="Select Cities">
            <template #optiongroup="slotProps">
                <div class="p-d-flex p-ai-center country-item">
                    <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" class="p-mr-2" width="18" />
                    <div>{{slotProps.option.label}}</div>
                </div>
            </template>
        </MultiSelect>

        <h5>Advanced with Templating and Filtering</h5>
        <MultiSelect v-model="selectedCountries" :options="countries" optionLabel="name" placeholder="Select Countries" :filter="true" class="multiselect-custom">
            <template #value="slotProps">
                <div class="country-item country-item-value" v-for="option of slotProps.value" :key="option.code">
                    <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" class="p-mr-2" width="18" />
                    <div>{{option.name}}</div>
                </div>
                <template v-if="!slotProps.value || slotProps.value.length === 0">
                    Select Countries
                </template>
            </template>
            <template #option="slotProps">
                <div class="country-item">
                    <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" class="p-mr-2" width="18" />
                    <div>{{slotProps.option.name}}</div>
                </div>
            </template>
        </MultiSelect>
    </div>
</template>

<script>
export default {
    data() {
        return {
            selectedCities1: null,
            selectedCities2: null,
            selectedCountries: null,
            selectedGroupedCities: null,
            cities: [
                {name: 'New York', code: 'NY'},
                {name: 'Rome', code: 'RM'},
                {name: 'London', code: 'LDN'},
                {name: 'Istanbul', code: 'IST'},
                {name: 'Paris', code: 'PRS'}
            ],
            countries: [
                {name: 'Australia', code: 'AU'},
                {name: 'Brazil', code: 'BR'},
                {name: 'China', code: 'CN'},
                {name: 'Egypt', code: 'EG'},
                {name: 'France', code: 'FR'},
                {name: 'Germany', code: 'DE'},
                {name: 'India', code: 'IN'},
                {name: 'Japan', code: 'JP'},
                {name: 'Spain', code: 'ES'},
                {name: 'United States', code: 'US'}
            ],
            groupedCities: [{
                label: 'Germany', code: 'DE', 
                items: [
                    {label: 'Berlin', value: 'Berlin'},
                    {label: 'Frankfurt', value: 'Frankfurt'},
                    {label: 'Hamburg', value: 'Hamburg'},
                    {label: 'Munich', value: 'Munich'}
                ]
            },
            {
                label: 'USA', code: 'US', 
                items: [
                    {label: 'Chicago', value: 'Chicago'},
                    {label: 'Los Angeles', value: 'Los Angeles'},
                    {label: 'New York', value: 'New York'},
                    {label: 'San Francisco', value: 'San Francisco'}
                ]
            },
            {
                label: 'Japan', code: 'JP', 
                items: [
                    {label: 'Kyoto', value: 'Kyoto'},
                    {label: 'Osaka', value: 'Osaka'},
                    {label: 'Tokyo', value: 'Tokyo'},
                    {label: 'Yokohama', value: 'Yokohama'}
                ]
            }]
        }
    }
}
<\\/script>

<style lang="scss" scoped>
.p-multiselect {
    width: 18rem;
}

::v-deep(.multiselect-custom) {
    .p-multiselect-label:not(.p-placeholder) {
        padding-top: .25rem;
        padding-bottom: .25rem;
    }

    .country-item-value {
        padding: .25rem .5rem;
        border-radius: 3px;
        display: inline-flex;
        margin-right: .5rem;
        background-color: var(--primary-color);
        color: var(--primary-color-text);

        img.flag {
            width: 17px;
        }
    }
}

@media screen and (max-width: 640px) {
    .p-multiselect {
        width: 100%;
    }
}
</style>`
                },
                'composition-api': {
                    tabName: 'Composition API',
                    content: `
<template>
    <div>
        <h5>Basic</h5>
        <MultiSelect v-model="selectedCities1" :options="cities" optionLabel="name" placeholder="Select Cities" />

        <h5>Chips</h5>
        <MultiSelect v-model="selectedCities2" :options="cities" optionLabel="name" placeholder="Select Cities" display="chip" />

        <h5>Grouped</h5>
        <MultiSelect v-model="selectedGroupedCities" :options="groupedCities" optionLabel="label"  optionGroupLabel="label" optionGroupChildren="items" placeholder="Select Cities">
            <template #optiongroup="slotProps">
                <div class="p-d-flex p-ai-center country-item">
                    <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" class="p-mr-2" width="18" />
                    <div>{{slotProps.option.label}}</div>
                </div>
            </template>
        </MultiSelect>

        <h5>Advanced with Templating and Filtering</h5>
        <MultiSelect v-model="selectedCountries" :options="countries" optionLabel="name" placeholder="Select Countries" :filter="true" class="multiselect-custom">
            <template #value="slotProps">
                <div class="country-item country-item-value" v-for="option of slotProps.value" :key="option.code">
                    <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" class="p-mr-2" width="18" />
                    <div>{{option.name}}</div>
                </div>
                <template v-if="!slotProps.value || slotProps.value.length === 0">
                    Select Countries
                </template>
            </template>
            <template #option="slotProps">
                <div class="country-item">
                    <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" class="p-mr-2" width="18" />
                    <div>{{slotProps.option.name}}</div>
                </div>
            </template>
        </MultiSelect>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const selectedCities1 = ref();
        const selectedCities2 = ref();
        const selectedCountries = ref();
        const selectedGroupedCities = ref();
        const cities = ref([
            {name: 'New York', code: 'NY'},
            {name: 'Rome', code: 'RM'},
            {name: 'London', code: 'LDN'},
            {name: 'Istanbul', code: 'IST'},
            {name: 'Paris', code: 'PRS'}
        ]);
        const countries = ref([
            {name: 'Australia', code: 'AU'},
            {name: 'Brazil', code: 'BR'},
            {name: 'China', code: 'CN'},
            {name: 'Egypt', code: 'EG'},
            {name: 'France', code: 'FR'},
            {name: 'Germany', code: 'DE'},
            {name: 'India', code: 'IN'},
            {name: 'Japan', code: 'JP'},
            {name: 'Spain', code: 'ES'},
            {name: 'United States', code: 'US'}
        ]);
        const groupedCities = ref([
            {
                label: 'Germany', code: 'DE', 
                items: [
                    {label: 'Berlin', value: 'Berlin'},
                    {label: 'Frankfurt', value: 'Frankfurt'},
                    {label: 'Hamburg', value: 'Hamburg'},
                    {label: 'Munich', value: 'Munich'}
                ]
            },
            {
                label: 'USA', code: 'US', 
                items: [
                    {label: 'Chicago', value: 'Chicago'},
                    {label: 'Los Angeles', value: 'Los Angeles'},
                    {label: 'New York', value: 'New York'},
                    {label: 'San Francisco', value: 'San Francisco'}
                ]
            },
            {
                label: 'Japan', code: 'JP', 
                items: [
                    {label: 'Kyoto', value: 'Kyoto'},
                    {label: 'Osaka', value: 'Osaka'},
                    {label: 'Tokyo', value: 'Tokyo'},
                    {label: 'Yokohama', value: 'Yokohama'}
                ]
            }
        ]);

        return { selectedCities1, selectedCities2, selectedCountries, selectedGroupedCities, cities, countries, groupedCities }
    }
}
<\\/script>

<style lang="scss" scoped>
.p-multiselect {
    width: 18rem;
}

::v-deep(.multiselect-custom) {
    .p-multiselect-label:not(.p-placeholder) {
        padding-top: .25rem;
        padding-bottom: .25rem;
    }

    .country-item-value {
        padding: .25rem .5rem;
        border-radius: 3px;
        display: inline-flex;
        margin-right: .5rem;
        background-color: var(--primary-color);
        color: var(--primary-color-text);

        img.flag {
            width: 17px;
        }
    }
}

@media screen and (max-width: 640px) {
    .p-multiselect {
        width: 100%;
    }
}
</style>`
                }
            }
        }
    }
}
</script>
