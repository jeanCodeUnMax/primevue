<template>
	<AppDoc name="SkeletonDemo" :sources="sources">
        <h5>Import</h5>
<pre v-code.script><code>
import Skeleton from 'primevue/skeleton';

</code></pre>

		<h5>Getting Started</h5>
		<p>Skeleton displays a rectangle in its simplest form.</p>
<pre v-code><code>
&lt;Skeleton /&gt;

</code></pre>

		<h5>Circle</h5>
		<p>The other option is the circle by setting <i>shape</i> property as "circle".</p>
<pre v-code><code>
&lt;Skeleton shape="circle"/&gt;

</code></pre>

		<h5>Size</h5>
		<p>In order to customize the size, use <i>width</i> and <i>height</i> properties for rectangles and <i>size</i> for Circle and Square shapes.</p>
<pre v-code><code>
&lt;Skeleton width="100%" height="2rem" /&gt;
&lt;Skeleton shape="circle" size="50px" /&gt;

</code></pre>

		<h5>Border Radius</h5>
		<p>The default border radius of a rectangle is specified by the theme and can be overriden using the <i>borderRadius</i> property.</p>
<pre v-code><code>
&lt;Skeleton borderRadius="16px" /&gt;

</code></pre>

		<h5>Animation</h5>
		<p>Animation can be turned of by setting <i>animation</i> to "none".</p>
<pre v-code><code>
&lt;Skeleton animation="none" /&gt;

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
                        <td>shape</td>
                        <td>string</td>
                        <td>rectangle</td>
                        <td>Shape of the element, options are "rectangle" and "circle".</td>
                    </tr>
					<tr>
                        <td>size</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Size of the Circle or Square.</td>
                    </tr>
					<tr>
                        <td>width</td>
                        <td>string</td>
                        <td>100%</td>
                        <td>Width of the element.</td>
                    </tr>
					<tr>
                        <td>height</td>
                        <td>string</td>
                        <td>1rem</td>
                        <td>Height of the element.</td>
                    </tr>
					<tr>
                        <td>borderRadius</td>
                        <td>string</td>
                        <td>null</td>
                        <td>Border radius of the element, defaults to value from theme.</td>
                    </tr>
					<tr>
                        <td>animation</td>
                        <td>string</td>
                        <td>wave</td>
                        <td>Type of the animation, valid options are "wave" and "none".</td>
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
                        <td>p-skeleton</td>
                        <td>Container element.</td>
                    </tr>
                    <tr>
                        <td>p-skeleton-circle</td>
                        <td>Container element of a determinate progressbar.</td>
                    </tr>
                    <tr>
                        <td>p-skeleton-animation-none</td>
                        <td>Container element of an indeterminate progressbar.</td>
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
        <div class="card">
             <div class="p-grid p-formgrid">
                <div class="p-field p-col-12 p-md-6">
                    <h5>Rectangle</h5>
                    <Skeleton class="p-mb-2"></Skeleton>
                    <Skeleton width="10rem" class="p-mb-2"></Skeleton>
                    <Skeleton width="5rem" class="p-mb-2"></Skeleton>
                    <Skeleton height="2rem" class="p-mb-2"></Skeleton>
                    <Skeleton width="10rem" height="4rem"></Skeleton>
                </div>
                <div class="p-field p-col-12 p-md-6">
                    <h5>Rounded</h5>
                    <Skeleton class="p-mb-2" borderRadius="16px"></Skeleton>
                    <Skeleton width="10rem" class="p-mb-2" borderRadius="16px"></Skeleton>
                    <Skeleton width="5rem" borderRadius="16px" class="p-mb-2"></Skeleton>
                    <Skeleton height="2rem" class="p-mb-2" borderRadius="16px"></Skeleton>
                    <Skeleton width="10rem" height="4rem" borderRadius="16px"></Skeleton>
                </div>
                <div class="p-field p-col-12 p-md-6">
                    <h5 class="p-mt-3">Square</h5>
                    <div class="p-d-flex p-ai-end">
                        <Skeleton size="2rem" class="p-mr-2"></Skeleton>
                        <Skeleton size="3rem" class="p-mr-2"></Skeleton>
                        <Skeleton size="4rem" class="p-mr-2"></Skeleton>
                        <Skeleton size="5rem"></Skeleton>
                    </div>
                </div>
                <div class="p-field p-col-12 p-md-6">
                    <h5 class="p-mt-3">Circle</h5>
                    <div class="p-d-flex p-ai-end">
                        <Skeleton shape="circle" size="2rem" class="p-mr-2"></Skeleton>
                        <Skeleton shape="circle" size="3rem" class="p-mr-2"></Skeleton>
                        <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                        <Skeleton shape="circle" size="5rem"></Skeleton>
                    </div>
                </div>
             </div>
        </div>

        <div class="card">
             <div class="p-grid p-formgrid">
                <div class="p-field p-col-12 p-md-6 p-pr-md-6 p-pr-0">
                    <h5>Card</h5>
                    <div class="custom-skeleton p-p-4">
                        <div class="p-d-flex p-mb-3">
                            <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                            <div>
                                <Skeleton width="10rem" class="p-mb-2"></Skeleton>
                                <Skeleton width="5rem" class="p-mb-2"></Skeleton>
                                <Skeleton height=".5rem"></Skeleton>
                            </div>
                        </div>
                        <Skeleton width="100%" height="150px"></Skeleton>
                        <div class="p-d-flex p-jc-between p-mt-3">
                            <Skeleton width="4rem" height="2rem"></Skeleton>
                            <Skeleton width="4rem" height="2rem"></Skeleton>
                        </div>
                    </div>
                </div>

                <div class="p-field p-col-12 p-md-6">
                    <h5>List</h5>
                    <div class="custom-skeleton p-p-4">
                        <ul class="p-m-0 p-p-0">
                            <li class="p-mb-3">
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                            <li class="p-mb-3">
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                            <li class="p-mb-3">
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                            <li>
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>

            <h5>DataTable</h5>
            <DataTable :value="products" responsiveLayout="scroll">
                <Column field="code" header="Code">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
                <Column field="name" header="Name">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
                <Column field="category" header="Category">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
                <Column field="quantity" header="Quantity">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
            </DataTable>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            products: new Array(4)
        }
    }
}
<\\/script>

<style lang="scss" scoped>
.custom-skeleton {
    border: 1px solid var(--surface-d);
    border-radius: 4px;

    ul {
        list-style: none;
    }
}
</style>`
				},
                'composition-api': {
                    tabName: 'Composition API',
					content: `
<template>
    <div>
        <div class="card">
             <div class="p-grid p-formgrid">
                <div class="p-field p-col-12 p-md-6">
                    <h5>Rectangle</h5>
                    <Skeleton class="p-mb-2"></Skeleton>
                    <Skeleton width="10rem" class="p-mb-2"></Skeleton>
                    <Skeleton width="5rem" class="p-mb-2"></Skeleton>
                    <Skeleton height="2rem" class="p-mb-2"></Skeleton>
                    <Skeleton width="10rem" height="4rem"></Skeleton>
                </div>
                <div class="p-field p-col-12 p-md-6">
                    <h5>Rounded</h5>
                    <Skeleton class="p-mb-2" borderRadius="16px"></Skeleton>
                    <Skeleton width="10rem" class="p-mb-2" borderRadius="16px"></Skeleton>
                    <Skeleton width="5rem" borderRadius="16px" class="p-mb-2"></Skeleton>
                    <Skeleton height="2rem" class="p-mb-2" borderRadius="16px"></Skeleton>
                    <Skeleton width="10rem" height="4rem" borderRadius="16px"></Skeleton>
                </div>
                <div class="p-field p-col-12 p-md-6">
                    <h5 class="p-mt-3">Square</h5>
                    <div class="p-d-flex p-ai-end">
                        <Skeleton size="2rem" class="p-mr-2"></Skeleton>
                        <Skeleton size="3rem" class="p-mr-2"></Skeleton>
                        <Skeleton size="4rem" class="p-mr-2"></Skeleton>
                        <Skeleton size="5rem"></Skeleton>
                    </div>
                </div>
                <div class="p-field p-col-12 p-md-6">
                    <h5 class="p-mt-3">Circle</h5>
                    <div class="p-d-flex p-ai-end">
                        <Skeleton shape="circle" size="2rem" class="p-mr-2"></Skeleton>
                        <Skeleton shape="circle" size="3rem" class="p-mr-2"></Skeleton>
                        <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                        <Skeleton shape="circle" size="5rem"></Skeleton>
                    </div>
                </div>
             </div>
        </div>

        <div class="card">
             <div class="p-grid p-formgrid">
                <div class="p-field p-col-12 p-md-6 p-pr-md-6 p-pr-0">
                    <h5>Card</h5>
                    <div class="custom-skeleton p-p-4">
                        <div class="p-d-flex p-mb-3">
                            <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                            <div>
                                <Skeleton width="10rem" class="p-mb-2"></Skeleton>
                                <Skeleton width="5rem" class="p-mb-2"></Skeleton>
                                <Skeleton height=".5rem"></Skeleton>
                            </div>
                        </div>
                        <Skeleton width="100%" height="150px"></Skeleton>
                        <div class="p-d-flex p-jc-between p-mt-3">
                            <Skeleton width="4rem" height="2rem"></Skeleton>
                            <Skeleton width="4rem" height="2rem"></Skeleton>
                        </div>
                    </div>
                </div>

                <div class="p-field p-col-12 p-md-6">
                    <h5>List</h5>
                    <div class="custom-skeleton p-p-4">
                        <ul class="p-m-0 p-p-0">
                            <li class="p-mb-3">
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                            <li class="p-mb-3">
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                            <li class="p-mb-3">
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                            <li>
                                <div class="p-d-flex">
                                    <Skeleton shape="circle" size="4rem" class="p-mr-2"></Skeleton>
                                    <div style="flex: 1">
                                        <Skeleton width="100%" class="p-mb-2"></Skeleton>
                                        <Skeleton width="75%"></Skeleton>
                                    </div>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
            </div>

            <h5>DataTable</h5>
            <DataTable :value="products" responsiveLayout="scroll">
                <Column field="code" header="Code">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
                <Column field="name" header="Name">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
                <Column field="category" header="Category">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
                <Column field="quantity" header="Quantity">
                    <template #body>
                        <Skeleton></Skeleton>
                    </template>
                </Column>
            </DataTable>
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const products = ref(new Array(4));

        return { products }
    }
}
<\\/script>

<style lang="scss" scoped>
.custom-skeleton {
    border: 1px solid var(--surface-d);
    border-radius: 4px;

    ul {
        list-style: none;
    }
}
</style>`
				}
			}
		}
	}
}
</script>