<template>
	<div>
		<div class="content-section introduction">
			<div class="feature-intro">
				<h1>DataTable <span>ContextMenu</span></h1>
				<p>CDataTable has exclusive integration with ContextMenu.</p>
			</div>
		</div>

		<div class="content-section implementation">
            <div class="card">
                <DataTable :value="products" contextMenu v-model:contextMenuSelection="selectedProduct" @row-contextmenu="onRowContextMenu" responsiveLayout="scroll">
                    <Column field="code" header="Code"></Column>
                    <Column field="name" header="Name"></Column>
                    <Column field="category" header="Category"></Column>
                    <Column field="price" header="Price">
                        <template #body="slotProps">
                            {{formatCurrency(slotProps.data.price)}}
                        </template>
                    </Column>
                </DataTable>
            </div>

            <ContextMenu :model="menuModel" ref="cm" />
		</div>

        <AppDoc name="DataTableContextMenuDemo" :sources="sources" :service="['ProductService']" :data="['products-small']" />
	</div>
</template>

<script>
import ProductService from '../../service/ProductService';

export default {
    data() {
        return {
            products: null,
            selectedProduct: null,
            menuModel: [
                {label: 'View', icon: 'pi pi-fw pi-search', command: () => this.viewProduct(this.selectedProduct)},
                {label: 'Delete', icon: 'pi pi-fw pi-times', command: () => this.deleteProduct(this.selectedProduct)}
            ],
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
    <div>
        <Toast />
        <DataTable :value="products" contextMenu v-model:contextMenuSelection="selectedProduct" @rowContextmenu="onRowContextMenu" responsiveLayout="scroll">
            <Column field="code" header="Code"></Column>
            <Column field="name" header="Name"></Column>
            <Column field="category" header="Category"></Column>
            <Column field="price" header="Price">
                <template #body="slotProps">
                    {{formatCurrency(slotProps.data.price)}}
                </template>
            </Column>
        </DataTable>

        <ContextMenu :model="menuModel" ref="cm" />
    </div>
</template>

<script>
import ProductService from './service/ProductService';

export default {
    data() {
        return {
            products: null,
            selectedProduct: null,
            menuModel: [
                {label: 'View', icon: 'pi pi-fw pi-search', command: () => this.viewProduct(this.selectedProduct)},
                {label: 'Delete', icon: 'pi pi-fw pi-times', command: () => this.deleteProduct(this.selectedProduct)}
            ]
        }
    },
    productService: null,
    created() {
        this.productService = new ProductService();
    },
    mounted() {
        this.productService.getProductsSmall().then(data => this.products = data);
    },
    methods: {
        onRowContextMenu(event) {
            this.$refs.cm.show(event.originalEvent);
        },
        viewProduct(product) {
            this.$toast.add({severity: 'info', summary: 'Product Selected', detail: product.name});
        },
        deleteProduct(product) {
            this.products = this.products.filter((p) => p.id !== product.id);
            this.$toast.add({severity: 'error', summary: 'Product Deleted', detail: product.name});
            this.selectedProduct = null;
        },
        formatCurrency(value) {
            return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
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
        <Toast />
        <DataTable :value="products" contextMenu v-model:contextMenuSelection="selectedProduct" @rowContextmenu="onRowContextMenu" responsiveLayout="scroll">
            <Column field="code" header="Code"></Column>
            <Column field="name" header="Name"></Column>
            <Column field="category" header="Category"></Column>
            <Column field="price" header="Price">
                <template #body="slotProps">
                    {{formatCurrency(slotProps.data.price)}}
                </template>
            </Column>
        </DataTable>

        <ContextMenu :model="menuModel" ref="cm" />
    </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { useToast } from 'primevue/usetoast';
import ProductService from './service/ProductService';

export default {
    setup() {
        onMounted(() => {
            productService.value.getProductsSmall().then(data => products.value = data);
        })

        const cm = ref();
        const toast = useToast();
        const products = ref();
        const productService = ref(new ProductService());
        const selectedProduct = ref();
        const menuModel = ref([
            {label: 'View', icon: 'pi pi-fw pi-search', command: () => viewProduct(selectedProduct)},
            {label: 'Delete', icon: 'pi pi-fw pi-times', command: () => deleteProduct(selectedProduct)}
        ]);
        const onRowContextMenu = (event) => {
            cm.value.show(event.originalEvent);
        };
        const viewProduct = (product) => {
            toast.add({severity: 'info', summary: 'Product Selected', detail: product.name});
        };
        const deleteProduct = (product) => {
            products.value = products.value.filter((p) => p.id !== product.value.id);
            toast.add({severity: 'error', summary: 'Product Deleted', detail: product.name});
            selectedProduct.value = null;
        };
        const formatCurrency = (value) => {
            return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
        };

        return { cm, products, selectedProduct, menuModel, onRowContextMenu, viewProduct, deleteProduct, formatCurrency }
    }
}
<\\/script>
`
                }
            }
        }
    },
    productService: null,
    created() {
        this.productService = new ProductService();
    },
    mounted() {
        this.productService.getProductsSmall().then(data => this.products = data);
    },
    methods: {
        onRowContextMenu(event) {
            this.$refs.cm.show(event.originalEvent);
        },
        viewProduct(product) {
            this.$toast.add({severity: 'info', summary: 'Product Selected', detail: product.name});
        },
        deleteProduct(product) {
            this.products = this.products.filter((p) => p.id !== product.id);
            this.$toast.add({severity: 'error', summary: 'Product Deleted', detail: product.name});
            this.selectedProduct = null;
        },
        formatCurrency(value) {
            return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
        }
    }
}
</script>