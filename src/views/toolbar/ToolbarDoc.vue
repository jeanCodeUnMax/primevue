<template>
	<AppDoc name="ToolbarDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import Toolbar from 'primevue/toolbar';

</code></pre>

		<h5>Getting Started</h5>
		<p>Toolbar provides <i>left</i> and <i>right</i> templates to place content at these sections.</p>
<pre v-code><code>
&lt;Toolbar&gt;
    &lt;template #left&gt;
        &lt;Button label="New" icon="pi pi-plus" class="p-mr-2" /&gt;
        &lt;Button label="Upload" icon="pi pi-upload" class="p-button-success" /&gt;
        &lt;i class="pi pi-bars p-toolbar-separator p-mr-2" /&gt;
        &lt;SplitButton label="Save" icon="pi pi-check" :model="items" class="p-button-warning"&gt;&lt;/SplitButton&gt;
    &lt;/template&gt;

    &lt;template #right&gt;
        &lt;Button icon="pi pi-search" class="p-mr-2" /&gt;
        &lt;Button icon="pi pi-calendar" class="p-button-success p-mr-2" /&gt;
        &lt;Button icon="pi pi-times" class="p-button-danger" /&gt;
    &lt;/template&gt;
&lt;/Toolbar&gt;

</code></pre>

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
                        <td>left</td>
                        <td>-</td>
                    </tr>
                    <tr>
                        <td>right</td>
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
						<td>p-toolbar</td>
						<td>Main container element.</td>
					</tr>
					<tr>
						<td>p-toolbar-group-left</td>
						<td>Left content container.</td>
					</tr>
					<tr>
						<td>p-toolbar-group-right</td>
						<td>Right content container.</td>
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
        <Toolbar>
            <template #left>
                <Button label="New" icon="pi pi-plus" class="p-mr-2" />
                <Button label="Upload" icon="pi pi-upload" class="p-button-success" />
                <i class="pi pi-bars p-toolbar-separator p-mr-2" />
                <SplitButton label="Save" icon="pi pi-check" :model="items" class="p-button-warning"></SplitButton>
            </template>

            <template #right>
                <Button icon="pi pi-search" class="p-mr-2" />
                <Button icon="pi pi-calendar" class="p-button-success p-mr-2" />
                <Button icon="pi pi-times" class="p-button-danger" />
            </template>
        </Toolbar>
    </div>
</template>

<script>
export default {
    data() {
        return {
            items: [
                {
                    label: 'Update',
                    icon: 'pi pi-refresh'
                },
                {
                    label: 'Delete',
                    icon: 'pi pi-times'
                },
                {
                    label: 'Vue Website',
                    icon: 'pi pi-external-link',
                    command: () => {
                        window.location.href = 'https://vuejs.org/'
                    }
                },
                {   label: 'Upload',
                    icon: 'pi pi-upload',
                    command: () => {
                        window.location.hash = "/fileupload"
                    }
                }
            ]
        }
    }
}
<\\/script>

<style scoped>
.p-button,
.p-splitbutton {
    margin-bottom: 0.5rem;
}
</style>`
                },
                'composition-api': {
                    tabName: 'Composition API',
                    content: `
<template>
    <div>
        <Toolbar>
            <template #left>
                <Button label="New" icon="pi pi-plus" class="p-mr-2" />
                <Button label="Upload" icon="pi pi-upload" class="p-button-success" />
                <i class="pi pi-bars p-toolbar-separator p-mr-2" />
                <SplitButton label="Save" icon="pi pi-check" :model="items" class="p-button-warning"></SplitButton>
            </template>

            <template #right>
                <Button icon="pi pi-search" class="p-mr-2" />
                <Button icon="pi pi-calendar" class="p-button-success p-mr-2" />
                <Button icon="pi pi-times" class="p-button-danger" />
            </template>
        </Toolbar>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const items = ref([
            {
                label: 'Update',
                icon: 'pi pi-refresh'
            },
            {
                label: 'Delete',
                icon: 'pi pi-times'
            },
            {
                label: 'Vue Website',
                icon: 'pi pi-external-link',
                command: () => {
                    window.location.href = 'https://vuejs.org/'
                }
            },
            {   label: 'Upload',
                icon: 'pi pi-upload',
                command: () => {
                    window.location.hash = "/fileupload"
                }
            }
        ]);

        return { items }
    }
}
<\\/script>

<style scoped>
.p-button,
.p-splitbutton {
    margin-bottom: 0.5rem;
}
</style>`
                }
            }
        }
    }
}
</script>