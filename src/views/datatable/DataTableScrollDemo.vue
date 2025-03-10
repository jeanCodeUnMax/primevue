<template>
	<div>
		<div class="content-section introduction">
			<div class="feature-intro">
				<h1>DataTable <span>Scroll</span></h1>
				<p>Data scrolling is available horizontally, vertically or both with support for frozen rows and columns.</p>
			</div>
		</div>

		<div class="content-section implementation">
            <div class="card">
                <h5>Vertical</h5>
                <DataTable :value="customers1" :scrollable="true" scrollHeight="400px" :loading="loading">
                    <Column field="name" header="Name" style="min-width:200px"></Column>
                    <Column field="country.name" header="Country" style="min-width:200px"></Column>
                    <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                    <Column field="status" header="Status" style="min-width:200px"></Column>
                </DataTable>
            </div>

           <div class="card">
                <h5>Flexible Scroll</h5>
                <p>Flex scroll feature makes the scrollable viewport section dynamic insteaf of a fixed value so that it can grow or shrink relative to the parent size of the table.
                   Click the button below to display a maximizable Dialog where data viewport adjusts itself according to the size changes.</p>

                <Button label="Show" icon="pi pi-external-link" @click="openDialog" />
            </div>

            <Dialog header="Flex Scroll" v-model:visible="dialogVisible" :style="{width: '75vw'}" :maximizable="true" :modal="true" :contentStyle="{height: '300px'}">
                <DataTable :value="customers1" :scrollable="true" scrollHeight="flex">
                    <Column field="name" header="Name" style="min-width:200px"></Column>
                    <Column field="country.name" header="Country" style="min-width:200px"></Column>
                    <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                    <Column field="status" header="Status" style="min-width:200px"></Column>
                </DataTable>
                <template #footer>
                    <Button label="Ok" icon="pi pi-check" @click="closeDialog" />
                </template>
            </Dialog>

            <div class="card">
                <h5>Horizontal and Vertical with Footer</h5>
                <DataTable :value="customers2" :scrollable="true" scrollHeight="400px" :loading="loading" scrollDirection="both">
                    <Column field="id" header="Id" footer="Id" style="width:100px"></Column>
                    <Column field="name" header="Name" footer="Name" style="width:200px"></Column>
                    <Column field="country.name" header="Country" footer="Country" style="width:200px"></Column>
                    <Column field="date" header="Date" footer="Date" style="width:200px"></Column>
                    <Column field="balance" header="Balance" footer="Balance" style="width:200px">
                        <template #body="{data}">
                            {{formatCurrency(data.balance)}}
                        </template>
                    </Column>
                    <Column field="company" header="Company" footer="Company" style="width:200px"></Column>
                    <Column field="status" header="Status" footer="Status" style="width:200px"></Column>
                    <Column field="activity" header="Activity" footer="Activity" style="width:200px"></Column>
                    <Column field="representative.name" header="Representative" footer="Representative" style="width:200px"></Column>
                </DataTable>
            </div>

            <div class="card">
                <h5>Frozen Rows</h5>
                <DataTable :value="unlockedCustomers" :frozenValue="lockedCustomers" :scrollable="true" scrollHeight="400px" :loading="loading">
                    <Column field="name" header="Name" style="min-width:200px"></Column>
                    <Column field="country.name" header="Country" style="min-width:200px"></Column>
                    <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                    <Column field="status" header="Status" style="min-width:200px"></Column>
                    <Column style="flex: 0 0 4rem">
                        <template #body="{data,frozenRow,index}">
                            <Button type="button" :icon="frozenRow ? 'pi pi-lock-open' : 'pi pi-lock'" :disabled="frozenRow ? false : lockedCustomers.length >= 2"
                            class="p-button-sm p-button-text" @click="toggleLock(data,frozenRow,index)"/>
                        </template>
                    </Column>
                </DataTable>
            </div>

            <div class="card">
                <h5>Frozen Columns</h5>
                <ToggleButton v-model="balanceFrozen" onIcon="pi pi-lock" offIcon="pi pi-lock-open" onLabel="Unfreeze Balance" offLabel="Freeze Balance" style="width: 12rem" />

                <DataTable :value="customers2" :scrollable="true" scrollHeight="400px" :loading="loading" scrollDirection="both" class="p-mt-3">
                    <Column field="name" header="Name" style="width:160px" frozen></Column>
                    <Column field="id" header="Id" style="width:100px"></Column>
                    <Column field="name" header="Name" style="width:200px"></Column>
                    <Column field="country.name" header="Country" style="width:200px"></Column>
                    <Column field="date" header="Date" style="width:200px"></Column>
                    <Column field="company" header="Company" style="width:200px"></Column>
                    <Column field="status" header="Status" style="width:200px"></Column>
                    <Column field="activity" header="Activity" style="width:200px"></Column>
                    <Column field="representative.name" header="Representative" style="width:200px"></Column>
                    <Column field="balance" header="Balance" style="width:120px" alignFrozen="right" :frozen="balanceFrozen">
                        <template #body="{data}">
                             <span class="p-text-bold">{{formatCurrency(data.balance)}}</span>
                        </template>
                    </Column>
                </DataTable>
            </div>

            <div class="card">
                <h5>Subheader Grouping</h5>
                <DataTable :value="customersGrouped" rowGroupMode="subheader" groupRowsBy="representative.name"
                    sortMode="single" sortField="representative.name" :sortOrder="1" scrollable scrollHeight="400px">
                    <Column field="representative.name" header="Representative"></Column>
                    <Column field="name" header="Name" style="min-width:200px"></Column>
                    <Column field="country" header="Country" style="min-width:200px">
                        <template #body="slotProps">
                            <img src="../../assets/images/flag_placeholder.png" :class="'flag flag-' + slotProps.data.country.code" width="30" />
                            <span class="image-text">{{slotProps.data.country.name}}</span>
                        </template>
                    </Column>
                    <Column field="company" header="Company" style="min-width:200px"></Column>
                    <Column field="status" header="Status" style="min-width:200px">
                        <template #body="slotProps">
                            <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                        </template>
                    </Column>
                    <Column field="date" header="Date" style="min-width:200px"></Column>
                    <template #groupheader="slotProps">
                        <img :alt="slotProps.data.representative.name" :src="'demo/images/avatar/' + slotProps.data.representative.image" width="32" style="vertical-align: middle" />
                        <span class="image-text">{{slotProps.data.representative.name}}</span>
                    </template>
                    <template #groupfooter="slotProps">
                        <td style="text-align: right" class="p-text-bold p-pr-6">Total Customers: {{calculateCustomerTotal(slotProps.data.representative.name)}}</td>
                    </template>
                </DataTable>
            </div>
		</div>

        <AppDoc name="DataTableScrollDemo" :sources="sources" :service="['CustomerService']" :data="['customers-medium', 'customers-large']" />
	</div>
</template>

<script>
import CustomerService from '../../service/CustomerService';

export default {
    data() {
        return {
            customers1: null,
            customers2: null,
            customersGrouped: null,
            lockedCustomers: [],
            unlockedCustomers: null,
            loading: false,
            dialogVisible: false,
            balanceFrozen: false,
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
	<div>
        <div class="card">
            <h5>Vertical</h5>
            <DataTable :value="customers1" :scrollable="true" scrollHeight="400px" :loading="loading">
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country.name" header="Country" style="min-width:200px"></Column>
                <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px"></Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Flexible Scroll</h5>
            <Button label="Show" icon="pi pi-external-link" @click="openDialog" />
        </div>

        <Dialog header="Flex Scroll" v-model:visible="dialogVisible" :style="{width: '75vw'}" :maximizable="true" :modal="true" :contentStyle="{height: '300px'}">
            <DataTable :value="customers1" :scrollable="true" scrollHeight="flex">
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country.name" header="Country" style="min-width:200px"></Column>
                <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px"></Column>
            </DataTable>
            <template #footer>
                <Button label="Ok" icon="pi pi-check" @click="closeDialog" />
            </template>
        </Dialog>

        <div class="card">
            <h5>Horizontal and Vertical with Footer</h5>
            <DataTable :value="customers2" :scrollable="true" scrollHeight="400px" :loading="loading" scrollDirection="both">
                <Column field="id" header="Id" footer="Id" style="width:100px"></Column>
                <Column field="name" header="Name" footer="Name" style="width:200px"></Column>
                <Column field="country.name" header="Country" footer="Country" style="width:200px"></Column>
                <Column field="date" header="Date" footer="Date" style="width:200px"></Column>
                <Column field="balance" header="Balance" footer="Balance" style="width:200px">
                    <template #body="{data}">
                        {{formatCurrency(data.balance)}}
                    </template>
                </Column>
                <Column field="company" header="Company" footer="Company" style="width:200px"></Column>
                <Column field="status" header="Status" footer="Status" style="width:200px"></Column>
                <Column field="activity" header="Activity" footer="Activity" style="width:200px"></Column>
                <Column field="representative.name" header="Representative" footer="Representative" style="width:200px"></Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Frozen Rows</h5>
            <DataTable :value="unlockedCustomers" :frozenValue="lockedCustomers" :scrollable="true" scrollHeight="400px" :loading="loading">
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country.name" header="Country" style="min-width:200px"></Column>
                <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px"></Column>
                <Column style="flex: 0 0 4rem">
                    <template #body="{data,frozenRow,index}">
                        <Button type="button" :icon="frozenRow ? 'pi pi-lock-open' : 'pi pi-lock'" :disabled="frozenRow ? false : lockedCustomers.length >= 2"
                        class="p-button-sm p-button-text" @click="toggleLock(data,frozenRow,index)"/>
                    </template>
                </Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Frozen Columns</h5>
            <ToggleButton v-model="balanceFrozen" onIcon="pi pi-lock" offIcon="pi pi-lock-open" onLabel="Unfreeze Balance" offLabel="Freeze Balance" style="width: 12rem" />

            <DataTable :value="customers2" :scrollable="true" scrollHeight="400px" :loading="loading" scrollDirection="both" class="p-mt-3">
                <Column field="name" header="Name" style="width:160px" frozen></Column>
                <Column field="id" header="Id" style="width:100px"></Column>
                <Column field="name" header="Name" style="width:200px"></Column>
                <Column field="country.name" header="Country" style="width:200px"></Column>
                <Column field="date" header="Date" style="width:200px"></Column>
                <Column field="company" header="Company" style="width:200px"></Column>
                <Column field="status" header="Status" style="width:200px"></Column>
                <Column field="activity" header="Activity" style="width:200px"></Column>
                <Column field="representative.name" header="Representative" style="width:200px"></Column>
                <Column field="balance" header="Balance" style="width:120px" alignFrozen="right" :frozen="balanceFrozen">
                    <template #body="{data}">
                         <span class="p-text-bold">{{formatCurrency(data.balance)}}</span>
                    </template>
                </Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Subheader Grouping</h5>
            <DataTable :value="customersGrouped" rowGroupMode="subheader" groupRowsBy="representative.name"
                sortMode="single" sortField="representative.name" :sortOrder="1" scrollable scrollHeight="400px">
                <Column field="representative.name" header="Representative"></Column>
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country" header="Country" style="min-width:200px">
                    <template #body="slotProps">
                        <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="30" />
                        <span class="image-text">{{slotProps.data.country.name}}</span>
                    </template>
                </Column>
                <Column field="company" header="Company" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px">
                    <template #body="slotProps">
                        <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                    </template>
                </Column>
                <Column field="date" header="Date" style="min-width:200px"></Column>
                <template #groupheader="slotProps">
                    <img :alt="slotProps.data.representative.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png"  width="32" style="vertical-align: middle" />
                    <span class="image-text">{{slotProps.data.representative.name}}</span>
                </template>
                <template #groupfooter="slotProps">
                    <td style="text-align: right" class="p-text-bold p-pr-6">Total Customers: {{calculateCustomerTotal(slotProps.data.representative.name)}}</td>
                </template>
            </DataTable>
        </div>
	</div>
</template>

<script>
import CustomerService from './service/CustomerService';

export default {
    data() {
        return {
            customers1: null,
            customers2: null,
            customersGrouped: null,
            lockedCustomers: [],
            unlockedCustomers: null,
            loading: false,
            dialogVisible: false,
            balanceFrozen: false
        }
    },
    customerService: null,
    created() {
        this.customerService = new CustomerService();
    },
    mounted() {
        this.loading = true;

        this.customerService.getCustomersLarge().then(data => {
            this.customers1 = data;
            this.loading = false;
        });
        this.customerService.getCustomersMedium().then(data => this.customers2 = data);
        this.customerService.getCustomersMedium().then(data => this.unlockedCustomers = data);
        this.customerService.getCustomersMedium().then(data => this.customersGrouped = data);

        this.lockedCustomers = [
            {
                id: 5135,
                name: "Geraldine Bisset",
                country: {
                    name: "France",
                   code: "fr"
                },
                company: "Bisset Group",
                status: "proposal",
                date: "2019-05-05",
                activity: 0,
                representative: {
                    name: "Amy Elsner",
                    image: "amyelsner.png"
                }
            }
        ];
    },
    methods: {
        openDialog() {
            this.dialogVisible = true;
        },
        closeDialog() {
            this.dialogVisible = false;
        },
        formatCurrency(value) {
            return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
        },
        calculateCustomerTotal(name) {
            let total = 0;

            if (this.customersGrouped) {
                for (let customer of this.customersGrouped) {
                    if (customer.representative.name === name) {
                        total++;
                    }
                }
            }

            return total;
        },
        toggleLock(data, frozen, index) {
            if (frozen) {
                this.lockedCustomers = this.lockedCustomers.filter((c, i) => i !== index);
                this.unlockedCustomers.push(data);
            }
            else {
                this.unlockedCustomers = this.unlockedCustomers.filter((c, i) => i !== index);
                this.lockedCustomers.push(data);
            }

            this.unlockedCustomers.sort((val1, val2) => {
                return val1.id < val2.id ? -1 : 1;
            });
        }
    }
}
<\\/script>

<style lang="scss" scoped>
::v-deep(.p-datatable-frozen-tbody) {
    font-weight: bold;
}

::v-deep(.p-datatable-scrollable .p-frozen-column) {
    font-weight: bold;
}
</style>                    
`
                },
                'composition-api': {
                    tabName: 'Composition API',
                    content: `
<template>
	<div>
        <div class="card">
            <h5>Vertical</h5>
            <DataTable :value="customers1" :scrollable="true" scrollHeight="400px" :loading="loading">
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country.name" header="Country" style="min-width:200px"></Column>
                <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px"></Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Flexible Scroll</h5>
            <Button label="Show" icon="pi pi-external-link" @click="openDialog" />
        </div>

        <Dialog header="Flex Scroll" v-model:visible="dialogVisible" :style="{width: '75vw'}" :maximizable="true" :modal="true" :contentStyle="{height: '300px'}">
            <DataTable :value="customers1" :scrollable="true" scrollHeight="flex">
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country.name" header="Country" style="min-width:200px"></Column>
                <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px"></Column>
            </DataTable>
            <template #footer>
                <Button label="Ok" icon="pi pi-check" @click="closeDialog" />
            </template>
        </Dialog>

        <div class="card">
            <h5>Horizontal and Vertical with Footer</h5>
            <DataTable :value="customers2" :scrollable="true" scrollHeight="400px" :loading="loading" scrollDirection="both">
                <Column field="id" header="Id" footer="Id" style="width:100px"></Column>
                <Column field="name" header="Name" footer="Name" style="width:200px"></Column>
                <Column field="country.name" header="Country" footer="Country" style="width:200px"></Column>
                <Column field="date" header="Date" footer="Date" style="width:200px"></Column>
                <Column field="balance" header="Balance" footer="Balance" style="width:200px">
                    <template #body="{data}">
                        {{formatCurrency(data.balance)}}
                    </template>
                </Column>
                <Column field="company" header="Company" footer="Company" style="width:200px"></Column>
                <Column field="status" header="Status" footer="Status" style="width:200px"></Column>
                <Column field="activity" header="Activity" footer="Activity" style="width:200px"></Column>
                <Column field="representative.name" header="Representative" footer="Representative" style="width:200px"></Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Frozen Rows</h5>
            <DataTable :value="unlockedCustomers" :frozenValue="lockedCustomers" :scrollable="true" scrollHeight="400px" :loading="loading">
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country.name" header="Country" style="min-width:200px"></Column>
                <Column field="representative.name" header="Representative" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px"></Column>
                <Column style="flex: 0 0 4rem">
                    <template #body="{data,frozenRow,index}">
                        <Button type="button" :icon="frozenRow ? 'pi pi-lock-open' : 'pi pi-lock'" :disabled="frozenRow ? false : lockedCustomers.length >= 2"
                        class="p-button-sm p-button-text" @click="toggleLock(data,frozenRow,index)"/>
                    </template>
                </Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Frozen Columns</h5>
            <ToggleButton v-model="balanceFrozen" onIcon="pi pi-lock" offIcon="pi pi-lock-open" onLabel="Unfreeze Balance" offLabel="Freeze Balance" style="width: 12rem" />

            <DataTable :value="customers2" :scrollable="true" scrollHeight="400px" :loading="loading" scrollDirection="both" class="p-mt-3">
                <Column field="name" header="Name" style="width:160px" frozen></Column>
                <Column field="id" header="Id" style="width:100px"></Column>
                <Column field="name" header="Name" style="width:200px"></Column>
                <Column field="country.name" header="Country" style="width:200px"></Column>
                <Column field="date" header="Date" style="width:200px"></Column>
                <Column field="company" header="Company" style="width:200px"></Column>
                <Column field="status" header="Status" style="width:200px"></Column>
                <Column field="activity" header="Activity" style="width:200px"></Column>
                <Column field="representative.name" header="Representative" style="width:200px"></Column>
                <Column field="balance" header="Balance" style="width:120px" alignFrozen="right" :frozen="balanceFrozen">
                    <template #body="{data}">
                         <span class="p-text-bold">{{formatCurrency(data.balance)}}</span>
                    </template>
                </Column>
            </DataTable>
        </div>

        <div class="card">
            <h5>Subheader Grouping</h5>
            <DataTable :value="customersGrouped" rowGroupMode="subheader" groupRowsBy="representative.name"
                sortMode="single" sortField="representative.name" :sortOrder="1" scrollable scrollHeight="400px">
                <Column field="representative.name" header="Representative"></Column>
                <Column field="name" header="Name" style="min-width:200px"></Column>
                <Column field="country" header="Country" style="min-width:200px">
                    <template #body="slotProps">
                        <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="30" />
                        <span class="image-text">{{slotProps.data.country.name}}</span>
                    </template>
                </Column>
                <Column field="company" header="Company" style="min-width:200px"></Column>
                <Column field="status" header="Status" style="min-width:200px">
                    <template #body="slotProps">
                        <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                    </template>
                </Column>
                <Column field="date" header="Date" style="min-width:200px"></Column>
                <template #groupheader="slotProps">
                    <img :alt="slotProps.data.representative.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png"  width="32" style="vertical-align: middle" />
                    <span class="image-text">{{slotProps.data.representative.name}}</span>
                </template>
                <template #groupfooter="slotProps">
                    <td style="text-align: right" class="p-text-bold p-pr-6">Total Customers: {{calculateCustomerTotal(slotProps.data.representative.name)}}</td>
                </template>
            </DataTable>
        </div>
	</div>
</template>

<script>
import { ref, onMounted } from 'vue';
import CustomerService from './service/CustomerService';

export default {
    setup() {
        onMounted(() => {
            loading.value = true;

            customerService.value.getCustomersLarge().then(data => {
                customers1.value = data;
                loading.value = false;
            });
            customerService.value.getCustomersMedium().then(data => customers2.value = data);
            customerService.value.getCustomersMedium().then(data => unlockedCustomers.value = data);
            customerService.value.getCustomersMedium().then(data => customersGrouped.value = data);

            lockedCustomers.value = [
                {
                    id: 5135,
                    name: "Geraldine Bisset",
                    country: {
                        name: "France",
                       code: "fr"
                    },
                    company: "Bisset Group",
                    status: "proposal",
                    date: "2019-05-05",
                    activity: 0,
                    representative: {
                        name: "Amy Elsner",
                        image: "amyelsner.png"
                    }
                }
            ];
        })

        const customers1 = ref();
        const customers2 = ref();
        const customersGrouped = ref();
        const lockedCustomers = ref([]);
        const unlockedCustomers = ref();
        const loading = ref(false);
        const dialogVisible = ref(false);
        const balanceFrozen = ref(false);
        const customerService = ref(new CustomerService());

        const openDialog = () => {
            dialogVisible.value = true;
        };
        const closeDialog = () => {
            dialogVisible.value = false;
        };
        const formatCurrency = (value) => {
            return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
        };
        const calculateCustomerTotal = (name) => {
            let total = 0;

            if (customersGrouped.value) {
                for (let customer of customersGrouped.value) {
                    if (customer.representative.name === name) {
                        total++;
                    }
                }
            }

            return total;
        };

        const toggleLock = (data, frozen, index) => {
            if (frozen) {
                lockedCustomers.value = lockedCustomers.value.filter((c, i) => i !== index);
                unlockedCustomers.value.push(data);
            }
            else {
                unlockedCustomers.value = unlockedCustomers.value.filter((c, i) => i !== index);
                lockedCustomers.value.push(data);
            }

            unlockedCustomers.value.sort((val1, val2) => {
                return val1.id < val2.id ? -1 : 1;
            });
        }

        return { customers1, customers2, customersGrouped, lockedCustomers, unlockedCustomers, 
            loading, dialogVisible, balanceFrozen, openDialog, closeDialog, formatCurrency, 
            calculateCustomerTotal, toggleLock }
    }
}
<\\/script>

<style lang="scss" scoped>
::v-deep(.p-datatable-frozen-tbody) {
    font-weight: bold;
}

::v-deep(.p-datatable-scrollable .p-frozen-column) {
    font-weight: bold;
}
</style>                    
`
                }
            }
        }
    },
    customerService: null,
    created() {
        this.customerService = new CustomerService();
    },
    mounted() {
        this.loading = true;

        this.customerService.getCustomersLarge().then(data => {
            this.customers1 = data;
            this.loading = false;
        });
        this.customerService.getCustomersMedium().then(data => this.customers2 = data);
        this.customerService.getCustomersMedium().then(data => this.unlockedCustomers = data);
        this.customerService.getCustomersMedium().then(data => this.customersGrouped = data);

        this.lockedCustomers = [
            {
                id: 5135,
                name: "Geraldine Bisset",
                country: {
                    name: "France",
                   code: "fr"
                },
                company: "Bisset Group",
                status: "proposal",
                date: "2019-05-05",
                activity: 0,
                representative: {
                    name: "Amy Elsner",
                    image: "amyelsner.png"
                }
            }
        ];
    },
    methods: {
        openDialog() {
            this.dialogVisible = true;
        },
        closeDialog() {
            this.dialogVisible = false;
        },
        formatCurrency(value) {
            return value.toLocaleString('en-US', {style: 'currency', currency: 'USD'});
        },
        calculateCustomerTotal(name) {
            let total = 0;

            if (this.customersGrouped) {
                for (let customer of this.customersGrouped) {
                    if (customer.representative.name === name) {
                        total++;
                    }
                }
            }

            return total;
        },
        toggleLock(data, frozen, index) {
            if (frozen) {
                this.lockedCustomers = this.lockedCustomers.filter((c, i) => i !== index);
                this.unlockedCustomers.push(data);
            }
            else {
                this.unlockedCustomers = this.unlockedCustomers.filter((c, i) => i !== index);
                this.lockedCustomers.push(data);
            }

            this.unlockedCustomers.sort((val1, val2) => {
                return val1.id < val2.id ? -1 : 1;
            });
        }
    }
}
</script>

<style lang="scss" scoped>
::v-deep(.p-datatable-frozen-tbody) {
    font-weight: bold;
}

::v-deep(.p-datatable-scrollable .p-frozen-column) {
    font-weight: bold;
}
</style>