<template>
	<AppDoc name="SelectButtonDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import SelectButton from 'primevue/selectbutton';

</code></pre>

		<h5>Getting Started</h5>
		<p>SelectButton requires a value to bind and a collection of arbitrary objects along with the <i>optionLabel</i> property to specify the label property of the option.</p>
<pre v-code><code>
&lt;SelectButton v-model="selectedCity" :options="cities" optionLabel="name" /&gt;

</code></pre>

<pre v-code.script><code>
export default {
	data() {
		return {
			selectedCity: null,
			cities: [
				{name: 'London', code: 'LND'},
				{name: 'Paris', code: 'PRS'},
				{name: 'Rome', code: 'RM'}
			]
		}
	}
}

</code></pre>

		<h5>Multiple</h5>
		<p>SelectButton allows selecting only one item by default and setting <i>multiple</i> option enables choosing more than one item. In multiple case, model property should be an array.</p>
<pre v-code><code>
&lt;SelectButton v-model="selectedCity" :options="cities" optionLabel="brand" :multiple="true" /&gt;

</code></pre>

		<h5>Templating</h5>
		<p>Label of an option is used as the display text of an item by default, for custom content support define an <i>option</i> template that gets the option instance as a parameter.</p>
<pre v-code><code><template v-pre>
&lt;SelectButton v-model="selectedCar" :options="cars" optionLabel="brand"&gt;
	&lt;template #option="slotProps"&gt;
        &lt;div class="car-option"&gt;
            &lt;img :alt="slotProps.option.brand" :src="'demo/images/car/' + slotProps.option.brand + '.png'" /&gt;
            &lt;div&gt;{{slotProps.option.brand}}&lt;/div&gt;
        &lt;/div&gt;
	&lt;/template&gt;
&lt;/SelectButton&gt;
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
                        <td>multiple</td>
                        <td>boolean</td>
                        <td>false</td>
                        <td>When specified, allows selecting multiple values.</td>
                    </tr>
                    <tr>
                        <td>disabled</td>
                        <td>boolean</td>
                        <td>false</td>
                        <td>When present, it specifies that the element should be disabled.</td>
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
                        <td>focus</td>
                        <td>event: Browser event</td>
                        <td>Callback to invoke on focus.</td>
                    </tr>
                    <tr>
                        <td>blur</td>
                        <td>event: Browser event</td>
                        <td>Callback to invoke on blur.</td>
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
                        <td>option: Option instance<br />
                            index: Index of the option</td>
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
        <h5>Single Selection</h5>
        <SelectButton v-model="value1" :options="options" />

        <h5>Multiple Selection</h5>
        <SelectButton v-model="value2" :options="paymentOptions" optionLabel="name" multiple />

        <h5>Custom Content</h5>
        <SelectButton v-model="value3" :options="justifyOptions" dataKey="value">
            <template #option="slotProps">
                <i :class="slotProps.option.icon"></i>
            </template>
        </SelectButton>
    </div>
</template>

<script>
export default {
    data() {
        return {
            value1: 'Off',
            value2: null,
            value3: null,
            options: ['Off', 'On'],
            paymentOptions: [
                {name: 'Option 1', value: 1},
                {name: 'Option 2', value: 2},
                {name: 'Option 3', value: 3}
            ],
            justifyOptions: [
                {icon: 'pi pi-align-left', value: 'left'},
                {icon: 'pi pi-align-right', value: 'Right'},
                {icon: 'pi pi-align-center', value: 'Center'},
                {icon: 'pi pi-align-justify', value: 'Justify'}]
        }
    }
}
<\\/script>
`
                },
                'composition-api': {
                    tabName: 'Composition API',
                    content: `
<template>
    <div>
        <h5>Single Selection</h5>
        <SelectButton v-model="value1" :options="options" />

        <h5>Multiple Selection</h5>
        <SelectButton v-model="value2" :options="paymentOptions" optionLabel="name" multiple />

        <h5>Custom Content</h5>
        <SelectButton v-model="value3" :options="justifyOptions" dataKey="value">
            <template #option="slotProps">
                <i :class="slotProps.option.icon"></i>
            </template>
        </SelectButton>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const value1 = ref('Off');
        const value2 = ref();
        const value3 = ref();
        const options = ref(['Off', 'On']);
        const paymentOptions = ref([
            {name: 'Option 1', value: 1},
            {name: 'Option 2', value: 2},
            {name: 'Option 3', value: 3}
        ]);
        const justifyOptions = ref([
            {icon: 'pi pi-align-left', value: 'left'},
            {icon: 'pi pi-align-right', value: 'Right'},
            {icon: 'pi pi-align-center', value: 'Center'},
            {icon: 'pi pi-align-justify', value: 'Justify'}
        ]);

        return { value1, value2, value3, options, paymentOptions, justifyOptions }
    }
}
<\\/script>
`
                }
            }
        }
    }
}
</script>