<template>
	<AppDoc name="InputTextDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import InputText from 'primevue/inputtext';

</code></pre>

		<h5>Getting Started</h5>
		<p>A model can be bound using the standard v-model directive.</p>
<pre v-code><code>
&lt;InputText type="text" v-model="value" /&gt;

</code></pre>

		<h5>Float Label</h5>
		<p>A floating label is implemented by wrapping the input and the label inside a container having <i>.p-float-label</i> style class.</p>
<pre v-code><code>
&lt;span class="p-float-label"&gt;
	&lt;InputText id="username" type="text" v-model="value" /&gt;
	&lt;label for="username"&gt;Username&lt;/label&gt;
&lt;/span&gt;

</code></pre>

        <h5>Icons</h5>
        <p>An icon can be integrated within an input field by wrapping the input and the icon with an element having <i>p-input-icon-right</i>
        and <i>p-input-icon-left</i> classes depending on the icon location.</p>
<pre v-code><code>
&lt;span class="p-input-icon-left"&gt;
    &lt;i class="pi pi-search" /&gt;
    &lt;InputText type="text" v-model="value1" placeholder="Search" /&gt;
&lt;/span&gt;

&lt;span class="p-input-icon-right"&gt;
    &lt;InputText type="text" v-model="value2" /&gt;
    &lt;i class="pi pi-spin pi-spinner" /&gt;
&lt;/span&gt;

&lt;span class="p-input-icon-left p-input-icon-right"&gt;
    &lt;i class="pi pi-search" /&gt;
    &lt;InputText type="text" v-model="value3" /&gt;
    &lt;i class="pi pi-spin pi-spinner" /&gt;
&lt;/span&gt;

</code></pre>

        <h5>Sizes</h5>
        <p>2 more sizes are available in addition to a regular input, for a smaller input add <i>p-inputtext-sm</i> and for a larger one, use <i>p-inputtext-lg</i>.
        Note that these classes are mainly be used to change the size of a particular field, for global scaling see the <router-link to="/theming">theming</router-link> page.</p>
<pre v-code><code>
&lt;InputText type="text" class="p-inputtext-sm" placeholder="Small" /&gt;
&lt;InputText type="text" placeholder="Normal" /&gt;
&lt;InputText type="text" class="p-inputtext-lg"  placeholder="Large" /&gt;

</code></pre>

        <p>Instead of repeating the scale classes for each input, sizing can also be applied to a group by adding the
            class to a container element so that descendant inputs share the same style easier.</p>
<pre v-code><code>
&lt;div class="p-inputtext-sm"&gt;
    &lt;InputText /&gt;
    &lt;InputNumber /&gt;
    &lt;InputMask /&gt;
&lt;/div&gt;

</code></pre>

        <h5>Outlined vs Filled</h5>
        <p>Input fields come in two styles, default is <i>outlined</i> with borders around the field whereas <i>filled</i> alternative adds a background color
        to the field. Applying <i>p-input-filled</i> to an ancestor of an input enables the filled style. If you prefer
        to use filled inputs in the entire application, use a global container such as document body or the application element to apply the style class.</p>

<pre v-code><code>
&lt;div class="p-input-filled"&gt;
    &lt;InputText type="text" /&gt;
    &lt;InputText type="text" /&gt;
    &lt;InputText type="text" /&gt;
&lt;/div&gt;

</code></pre>

		<h5>Properties</h5>
		<p>InputText passes any valid attribute to the underlying input element, additional attribute is the following.</p>
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
				</tbody>
			</table>
		</div>

        <h5>Events</h5>
        <p>Any valid event such as focus, blur and input are passed to the underlying input element.</p>

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
                        <td>p-inputtext</td>
                        <td>Input element</td>
                    </tr>
                    <tr>
                        <td>p-inputtext-sm</td>
                        <td>Smaller input element</td>
                    </tr>
                    <tr>
                        <td>p-inputtext-lg</td>
                        <td>Larger input element</td>
                    </tr>
                    <tr>
                        <td>p-inputtext-filled</td>
                        <td>Filled input style.</td>
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
                    content:`
<template>
    <div>
        <h5>Basic</h5>
        <InputText type="text" v-model="value1" />
        <span :style="{marginLeft: '.5em'}">{{value1}}</span>

        <h5>Floating Label</h5>
        <span class="p-float-label">
            <InputText id="username" type="text" v-model="value2" />
            <label for="username">Username</label>
        </span>

        <h5>Left Icon</h5>
        <span class="p-input-icon-left">
            <i class="pi pi-search" />
            <InputText type="text" v-model="value3" placeholder="Search" />
        </span>

        <h5>Right Icon</h5>
        <span class="p-input-icon-right">
            <i class="pi pi-spin pi-spinner" />
            <InputText type="text" v-model="value4" />
        </span>

        <h5>Help Text</h5>
        <div class="p-field">
            <label for="username1">Username</label>
            <InputText id="username1" type="username" aria-describedby="username1-help" />
            <small id="username1-help">Enter your username to reset your password.</small>
        </div>

        <h5>Invalid</h5>
        <div class="p-field">
            <label for="username2">Username</label>
            <InputText id="username2" type="username" aria-describedby="username2-help" class="p-invalid" />
            <small id="username2-help" class="p-error">Username is not available.</small>
        </div>

        <h5>Disabled</h5>
        <InputText type="text" v-model="value5" disabled />

        <h5>Sizes</h5>
        <div class="sizes">
            <InputText type="text" class="p-inputtext-sm" placeholder="Small" />
            <InputText type="text" placeholder="Normal" />
            <InputText type="text" class="p-inputtext-lg"  placeholder="Large" />
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            value1: null,
            value2: null,
            value3: null,
            value4: null,
            value5: 'PrimeVue'
        }
    }
}
<\\/script>

<style lang="scss" scoped>
.sizes {
    .p-inputtext {
        display: block;
        margin-bottom: .5rem;

        &:last-child {
            margin-bottom: 0;
        }
    }
}

.p-field * {
    display: block;
}
</style>`
                },
                'composition-api': {
                    tabName: 'Composition API',
                    content:`
<template>
    <div>
        <h5>Basic</h5>
        <InputText type="text" v-model="value1" />
        <span :style="{marginLeft: '.5em'}">{{value1}}</span>

        <h5>Floating Label</h5>
        <span class="p-float-label">
            <InputText id="username" type="text" v-model="value2" />
            <label for="username">Username</label>
        </span>

        <h5>Left Icon</h5>
        <span class="p-input-icon-left">
            <i class="pi pi-search" />
            <InputText type="text" v-model="value3" placeholder="Search" />
        </span>

        <h5>Right Icon</h5>
        <span class="p-input-icon-right">
            <i class="pi pi-spin pi-spinner" />
            <InputText type="text" v-model="value4" />
        </span>

        <h5>Help Text</h5>
        <div class="p-field">
            <label for="username1">Username</label>
            <InputText id="username1" type="username" aria-describedby="username1-help" />
            <small id="username1-help">Enter your username to reset your password.</small>
        </div>

        <h5>Invalid</h5>
        <div class="p-field">
            <label for="username2">Username</label>
            <InputText id="username2" type="username" aria-describedby="username2-help" class="p-invalid" />
            <small id="username2-help" class="p-error">Username is not available.</small>
        </div>

        <h5>Disabled</h5>
        <InputText type="text" v-model="value5" disabled />

        <h5>Sizes</h5>
        <div class="sizes">
            <InputText type="text" class="p-inputtext-sm" placeholder="Small" />
            <InputText type="text" placeholder="Normal" />
            <InputText type="text" class="p-inputtext-lg"  placeholder="Large" />
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const value1 = ref();
        const value2 = ref();
        const value3 = ref();
        const value4 = ref();
        const value5 = ref('PrimeVue');

        return { value1, value2, value3, value4, value5 }
    }
}
<\\/script>

<style lang="scss" scoped>
.sizes {
    .p-inputtext {
        display: block;
        margin-bottom: .5rem;

        &:last-child {
            margin-bottom: 0;
        }
    }
}

.p-field * {
    display: block;
}
</style>`
                }
            }
        }
    }
}
</script>