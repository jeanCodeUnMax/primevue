<template>
    <AppDoc name="InputMaskDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import InputMask from 'primevue/inputmask';

</code></pre>

		<h5>Getting Started</h5>
		<p>A model can be bound using the standard v-model directive.</p>
<pre v-code><code>
&lt;InputMask v-model="value" mask="99-999999" /&gt;

</code></pre>

		<h5>Mask</h5>
        <p>Mask format can be a combination of the the following built-in definitions.</p>

        <ul>
            <li>
                a - Alpha character (A-Z,a-z)
            </li>
            <li>
                9 - Numeric character (0-9)
            </li>
            <li>
                * - Alpha numberic character (A-Z,a-z,0-9)
            </li>
        </ul>
<pre v-code><code>
&lt;InputMask v-model="value" mask="a*-999-a999" /&gt;

</code></pre>

        <h5>SlotChar</h5>
        <p>Underscore is the default placeholder for a mask and this can be customized using <i>slotChart</i> option.</p>
<pre v-code><code>
&lt;InputMask v-model="value" mask="99/99/9999" slotChar="mm/dd/yyyy" /&gt;

</code></pre>
        <h5>Optional Values</h5>
        <p>If the input does not complete the mask definition, it is cleared by default.
            Use <i>autoClear</i> property to control this behavior. In addition, certain part of
            a mask can be made optional by using ? symbol where anything after the question
            mark becomes optional.</p>
<pre v-code><code>
&lt;InputMask v-model="value" mask="(999) 999-9999? x99999" /&gt;

</code></pre>

		<h5>Properties</h5>
		<p>InputText passes any valid attribute to the underlying input element. In addition;</p>
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
                        <td>mask</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Mask pattern.</td>
                    </tr>
                    <tr>
                        <td>slotChar</td>
                        <td>string</td>
                        <td>-</td>
                        <td>Placeholder character in mask, default is underscore.</td>
                    </tr>
                    <tr>
                        <td>autoClear</td>
                        <td>boolean</td>
                        <td>true</td>
                        <td>Clears the incomplete value on blur.</td>
                    </tr>
                    <tr>
                        <td>unmask</td>
                        <td>boolean</td>
                        <td>false</td>
                        <td>Defines if model sets the raw unmasked value to bound value or the formatted mask value.</td>
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
                        <td>p-inputmask p-inputtext</td>
                        <td>Input element</td>
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
        <div class="p-fluid p-formgrid p-grid">
            <div class="p-field p-col-12 p-md-4">
                <label for="basic">Basic</label>
                <InputMask mask="99-999999" v-model="val1" placeholder="99-999999" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="ssn">SSN</label>
                <InputMask mask="999-99-9999" v-model="val2" placeholder="999-99-9999" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="date">Date</label>
                <InputMask mask="99/99/9999" v-model="val3" placeholder="99/99/9999" slotChar="mm/dd/yyyy" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="Phone">Phone</label>
                <InputMask mask="(999) 999-9999" v-model="val4" placeholder="(999) 999-9999" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="phoneext">Phone Ext</label>
                <InputMask mask="(999) 999-9999? x99999" v-model="val5" placeholder="(999) 999-9999? x99999"/>
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="serial">Serial</label>
                <InputMask mask="a*-999-a999" v-model="val6" placeholder="a*-999-a999" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            val1: null,
            val2: null,
            val3: null,
            val4: null,
            val5: null,
            val6: null
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
        <div class="p-fluid p-formgrid p-grid">
            <div class="p-field p-col-12 p-md-4">
                <label for="basic">Basic</label>
                <InputMask mask="99-999999" v-model="val1" placeholder="99-999999" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="ssn">SSN</label>
                <InputMask mask="999-99-9999" v-model="val2" placeholder="999-99-9999" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="date">Date</label>
                <InputMask mask="99/99/9999" v-model="val3" placeholder="99/99/9999" slotChar="mm/dd/yyyy" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="Phone">Phone</label>
                <InputMask mask="(999) 999-9999" v-model="val4" placeholder="(999) 999-9999" />
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="phoneext">Phone Ext</label>
                <InputMask mask="(999) 999-9999? x99999" v-model="val5" placeholder="(999) 999-9999? x99999"/>
            </div>

            <div class="p-field p-col-12 p-md-4">
                <label for="serial">Serial</label>
                <InputMask mask="a*-999-a999" v-model="val6" placeholder="a*-999-a999" />
            </div>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const val1 = ref();
        const val2 = ref();
        const val3 = ref();
        const val4 = ref();
        const val5 = ref();
        const val6 = ref();

        return { val1, val2, val3, val4, val5, val6 }
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