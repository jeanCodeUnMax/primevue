<template>
    <AppDoc name="CheckboxDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import Checkbox from 'primevue/checkbox';

</code></pre>

		<h5>Getting Started</h5>
		<p>Checkbox can either be used in multiple selection with other checkboxes or as a single checkbox to provide a boolean value.</p>
<pre v-code><code>
&lt;Checkbox v-model="checked" :binary="true" /&gt;

</code></pre>

		<h5>Multiple Values</h5>
		<p>Multiple mode is enabled by default, v-model property refers to an array to bind the selected values.</p>
<pre v-code><code>
&lt;Checkbox name="city" value="Chicago" v-model="cities" /&gt;
&lt;Checkbox name="city" value="Los Angeles" v-model="cities" /&gt;
&lt;Checkbox name="city" value="New York" v-model="cities" /&gt;
&lt;Checkbox name="city" value="San Francisco" v-model="cities" /&gt;

</code></pre>

<pre v-code.script><code>
export default {
	data() {
		return {
			cities: []
		}
	}
}

</code></pre>

		<p>As v-model is two-way binding enabled, prepopulating the model array with values is enough to display the related
			checkboxes as checked by default.</p>

		<h5>Properties</h5>
        <p>Any property such as name and autofocus are passed to the underlying input element. Following are the additional properties to configure the component.</p>
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
                        <td>value</td>
                        <td>any</td>
                        <td>null</td>
                        <td>Value of the checkbox.</td>
                    </tr>
                    <tr>
                        <td>modelValue</td>
                        <td>any</td>
                        <td>null</td>
                        <td>Value binding of the checkbox.</td>
                    </tr>
                    <tr>
                        <td>binary</td>
                        <td>boolean</td>
                        <td>false</td>
                        <td>Allows to select a boolean value instead of multiple values.</td>
                    </tr>
				</tbody>
			</table>
		</div>

		<h5>Events</h5>
        <p>Any valid event such as focus and blur.</p>

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
                        <td>p-checkbox</td>
                        <td>Container element</td>
                    </tr>
                    <tr>
                        <td>p-checkbox-box</td>
                        <td>Container of icon.</td>
                    </tr>
                    <tr>
                        <td>p-checkbox-icon</td>
                        <td>Icon element.</td>
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
        <div class="p-field-checkbox">
            <Checkbox id="binary" v-model="checked" :binary="true" />
            <label for="binary">{{checked}}</label>
        </div>

        <h5>Multiple</h5>
        <div class="p-field-checkbox">
            <Checkbox id="city1" name="city" value="Chicago" v-model="cities" />
            <label for="city1">Chicago</label>
        </div>
        <div class="p-field-checkbox">
            <Checkbox id="city2" name="city" value="Los Angeles" v-model="cities" />
            <label for="city2">Los Angeles</label>
        </div>
        <div class="p-field-checkbox">
            <Checkbox id="city3" name="city" value="New York" v-model="cities" />
            <label for="city3">New York</label>
        </div>
        <div class="p-field-checkbox">
            <Checkbox id="city4" name="city" value="San Francisco" v-model="cities" />
            <label for="city4">San Francisco</label>
        </div>

        <h5>Dynamic Values, Preselection, Value Binding and Disabled Option</h5>
        <div v-for="category of categories" :key="category.key" class="p-field-checkbox">
            <Checkbox :id="category.key" name="category" :value="category" v-model="selectedCategories" :disabled="category.key === 'R'"/>
            <label :for="category.key">{{category.name}}</label>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            checked: false,
            cities: [],
            categories: [{name: 'Accounting', key: 'A'}, {name: 'Marketing', key: 'M'}, {name: 'Production', key: 'P'}, {name: 'Research', key: 'R'}],
            selectedCategories: []
        }
    },
    created() {
        this.selectedCategories = this.categories.slice(1,3);
    }
}
<\\/script>`
                },
                'composition-api': {
                    tabName: 'Composition API',
                    content: `
<template>
    <div>
        <h5>Basic</h5>
        <div class="p-field-checkbox">
            <Checkbox id="binary" v-model="checked" :binary="true" />
            <label for="binary">{{checked}}</label>
        </div>

        <h5>Multiple</h5>
        <div class="p-field-checkbox">
            <Checkbox id="city1" name="city" value="Chicago" v-model="cities" />
            <label for="city1">Chicago</label>
        </div>
        <div class="p-field-checkbox">
            <Checkbox id="city2" name="city" value="Los Angeles" v-model="cities" />
            <label for="city2">Los Angeles</label>
        </div>
        <div class="p-field-checkbox">
            <Checkbox id="city3" name="city" value="New York" v-model="cities" />
            <label for="city3">New York</label>
        </div>
        <div class="p-field-checkbox">
            <Checkbox id="city4" name="city" value="San Francisco" v-model="cities" />
            <label for="city4">San Francisco</label>
        </div>

        <h5>Dynamic Values, Preselection, Value Binding and Disabled Option</h5>
        <div v-for="category of categories" :key="category.key" class="p-field-checkbox">
            <Checkbox :id="category.key" name="category" :value="category" v-model="selectedCategories" :disabled="category.key === 'R'"/>
            <label :for="category.key">{{category.name}}</label>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    setup() {
        const checked = ref(false);
        const cities = ref([]);
        const categories = ref([
            {name: 'Accounting', key: 'A'}, 
            {name: 'Marketing', key: 'M'}, 
            {name: 'Production', key: 'P'}, 
            {name: 'Research', key: 'R'}
        ]);
        const selectedCategories = ref(categories.value.slice(1,3));

        return { checked, cities, categories, selectedCategories }
    }
}
<\\/script>`
                }
            }
        }
    }
}
</script>