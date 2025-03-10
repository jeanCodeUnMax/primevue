<template>
	<div>
		<div class="content-section introduction">
			<div class="feature-intro">
				<h1>DataTable <span>State</span></h1>
				<p>Stateful table allows keeping the state such as page, sort and filtering either at local storage or session storage so that when the page is visited again, table would render the data using its last settings.</p>
			</div>
		</div>

		<div class="content-section implementation">
            <div class="card">
                <h5>Session Storage</h5>
                <DataTable :value="customers" :paginator="true" :rows="10" v-model:filters="filters1"
                    v-model:selection="selectedCustomer1" selectionMode="single" dataKey="id"
                    stateStorage="session" stateKey="dt-state-demo-session" responsiveLayout="scroll">
                    <template #header>
                       <span class="p-input-icon-left">
                            <i class="pi pi-search" />
                            <InputText v-model="filters1['global']" placeholder="Global Search" />
                        </span>
                    </template>
                    <Column field="name" header="Name" :sortable="true" style="width:25%">
                        <template #filter>
                            <InputText type="text" v-model="filters1['name']" class="p-column-filter" placeholder="Search by name"/>
                        </template>
                    </Column>
                    <Column header="Country" :sortable="true" sortField="country.name" filterField="country.name" filterMatchMode="contains" style="width:25%">
                        <template #body="slotProps">
                            <img src="../../assets/images/flag_placeholder.png" :class="'flag flag-' + slotProps.data.country.code" width="30" />
                            <span class="image-text">{{slotProps.data.country.name}}</span>
                        </template>
                        <template #filter>
                            <InputText type="text" v-model="filters1['country.name']" class="p-column-filter" placeholder="Search by country"/>
                        </template>
                    </Column>
                    <Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name" filterMatchMode="in" style="width:25%">
                        <template #body="slotProps">
                            <img :alt="slotProps.data.representative.name" :src="'demo/images/avatar/' + slotProps.data.representative.image" width="32" style="vertical-align: middle" />
                            <span class="image-text">{{slotProps.data.representative.name}}</span>
                        </template>
                            <template #filter>
                            <MultiSelect v-model="filters1['representative.name']" :options="representatives" optionLabel="name" optionValue="name" placeholder="All" class="p-column-filter">
                                <template #option="slotProps">
                                    <div class="p-multiselect-representative-option">
                                        <img :alt="slotProps.option.name" :src="'demo/images/avatar/' + slotProps.option.image" width="32" style="vertical-align: middle" />
                                        <span class="image-text">{{slotProps.option.name}}</span>
                                    </div>
                                </template>
                            </MultiSelect>
                        </template>
                    </Column>
                    <Column field="status" header="Status" :sortable="true" filterMatchMode="equals" style="width:25%">
                        <template #body="slotProps">
                            <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                        </template>
                        <template #filter>
                            <Dropdown v-model="filters1['status']" :options="statuses" placeholder="Select a Status" class="p-column-filter" :showClear="true">
                                <template #option="slotProps">
                                    <span :class="'customer-badge status-' + slotProps.option">{{slotProps.option}}</span>
                                </template>
                            </Dropdown>
                        </template>
                    </Column>
                    <template #empty>
                        No customers found.
                    </template>
                </DataTable>
            </div>

            <div class="card">
                <h5>Local Storage</h5>
                <DataTable :value="customers" :paginator="true" :rows="10" v-model:filters="filters2"
                    v-model:selection="selectedCustomer2" selectionMode="single" dataKey="id"
                    stateStorage="session" stateKey="dt-state-demo-local" responsiveLayout="scroll">
                    <template #header>
                       <span class="p-input-icon-left">
                            <i class="pi pi-search" />
                            <InputText v-model="filters2['global']" placeholder="Global Search" />
                        </span>
                    </template>
                    <Column field="name" header="Name" :sortable="true" style="width:25%">
                        <template #filter>
                            <InputText type="text" v-model="filters2['name']" class="p-column-filter" placeholder="Search by name"/>
                        </template>
                    </Column>
                    <Column header="Country" :sortable="true" sortField="country.name" filterField="country.name" filterMatchMode="contains" style="width:25%">
                        <template #body="slotProps">
                            <img src="../../assets/images/flag_placeholder.png" :class="'flag flag-' + slotProps.data.country.code" width="30" />
                            <span class="image-text">{{slotProps.data.country.name}}</span>
                        </template>
                        <template #filter>
                            <InputText type="text" v-model="filters2['country.name']" class="p-column-filter" placeholder="Search by country"/>
                        </template>
                    </Column>
                    <Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name" filterMatchMode="in" style="width:25%">
                        <template #body="slotProps">
                            <img :alt="slotProps.data.representative.name" :src="'demo/images/avatar/' + slotProps.data.representative.image" width="32" style="vertical-align: middle" />
                            <span class="image-text">{{slotProps.data.representative.name}}</span>
                        </template>
                            <template #filter>
                            <MultiSelect v-model="filters2['representative.name']" :options="representatives" optionLabel="name" optionValue="name" placeholder="All" class="p-column-filter">
                                <template #option="slotProps">
                                    <div class="p-multiselect-representative-option">
                                        <img :alt="slotProps.option.name" :src="'demo/images/avatar/' + slotProps.option.image" width="32" style="vertical-align: middle" />
                                        <span class="image-text">{{slotProps.option.name}}</span>
                                    </div>
                                </template>
                            </MultiSelect>
                        </template>
                    </Column>
                    <Column field="status" header="Status" :sortable="true" filterMatchMode="equals" style="width:25%">
                        <template #body="slotProps">
                            <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                        </template>
                        <template #filter>
                            <Dropdown v-model="filters2['status']" :options="statuses" placeholder="Select a Status" class="p-column-filter" :showClear="true">
                                <template #option="slotProps">
                                    <span :class="'customer-badge status-' + slotProps.option">{{slotProps.option}}</span>
                                </template>
                            </Dropdown>
                        </template>
                    </Column>
                    <template #empty>
                        No customers found.
                    </template>
                </DataTable>
            </div>
		</div>
              
        <AppDoc name="DataTableStateDemo" :sources="sources" :service="['CustomerService']" :data="['customers-medium']" />

	</div>
</template>

<script>
import CustomerService from '../../service/CustomerService';

export default {
    data() {
        return {
            customers: null,
            selectedCustomer1: null,
            selectedCustomer2: null,
            filters1: {},
            filters2: {},
            loading: true,
            representatives: [
                {name: "Amy Elsner", image: 'amyelsner.png'},
                {name: "Anna Fali", image: 'annafali.png'},
                {name: "Asiya Javayant", image: 'asiyajavayant.png'},
                {name: "Bernardo Dominic", image: 'bernardodominic.png'},
                {name: "Elwin Sharvill", image: 'elwinsharvill.png'},
                {name: "Ioni Bowcher", image: 'ionibowcher.png'},
                {name: "Ivan Magalhaes",image: 'ivanmagalhaes.png'},
                {name: "Onyama Limba", image: 'onyamalimba.png'},
                {name: "Stephen Shaw", image: 'stephenshaw.png'},
                {name: "XuXue Feng", image: 'xuxuefeng.png'}
            ],
            statuses: [
                'unqualified', 'qualified', 'new', 'negotiation', 'renewal', 'proposal'
            ],
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
	<div>
        <div class="card">
            <h5>Session Storage</h5>
            <DataTable :value="customers" :paginator="true" :rows="10" v-model:filters="filters1"
                v-model:selection="selectedCustomer1" selectionMode="single" dataKey="id"
                stateStorage="session" stateKey="dt-state-demo-session" responsiveLayout="scroll">
                <template #header>
                   <span class="p-input-icon-left">
                        <i class="pi pi-search" />
                        <InputText v-model="filters1['global']" placeholder="Global Search" />
                    </span>
                </template>
                <Column field="name" header="Name" :sortable="true" style="width:25%">
                    <template #filter>
                        <InputText type="text" v-model="filters1['name']" class="p-column-filter" placeholder="Search by name"/>
                    </template>
                </Column>
                <Column header="Country" :sortable="true" sortField="country.name" filterField="country.name" filterMatchMode="contains" style="width:25%">
                    <template #body="slotProps">
                        <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="30" />
                        <span class="image-text">{{slotProps.data.country.name}}</span>
                    </template>
                    <template #filter>
                        <InputText type="text" v-model="filters1['country.name']" class="p-column-filter" placeholder="Search by country"/>
                    </template>
                </Column>
                <Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name" filterMatchMode="in" style="width:25%">
                    <template #body="slotProps">
                        <img :alt="slotProps.data.representative.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                        <span class="image-text">{{slotProps.data.representative.name}}</span>
                    </template>
                        <template #filter>
                        <MultiSelect v-model="filters1['representative.name']" :options="representatives" optionLabel="name" optionValue="name" placeholder="All" class="p-column-filter">
                            <template #option="slotProps">
                                <div class="p-multiselect-representative-option">
                                    <img :alt="slotProps.option.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                                    <span class="image-text">{{slotProps.option.name}}</span>
                                </div>
                            </template>
                        </MultiSelect>
                    </template>
                </Column>
                <Column field="status" header="Status" :sortable="true" filterMatchMode="equals" style="width:25%">
                    <template #body="slotProps">
                        <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                    </template>
                    <template #filter>
                        <Dropdown v-model="filters1['status']" :options="statuses" placeholder="Select a Status" class="p-column-filter" :showClear="true">
                            <template #option="slotProps">
                                <span :class="'customer-badge status-' + slotProps.option">{{slotProps.option}}</span>
                            </template>
                        </Dropdown>
                    </template>
                </Column>
                <template #empty>
                    No customers found.
                </template>
            </DataTable>
        </div>

        <div class="card">
            <h5>Local Storage</h5>
            <DataTable :value="customers" :paginator="true" :rows="10" v-model:filters="filters2"
                v-model:selection="selectedCustomer2" selectionMode="single" dataKey="id"
                stateStorage="session" stateKey="dt-state-demo-local" responsiveLayout="scroll">
                <template #header>
                   <span class="p-input-icon-left">
                        <i class="pi pi-search" />
                        <InputText v-model="filters2['global']" placeholder="Global Search" />
                    </span>
                </template>
                <Column field="name" header="Name" :sortable="true" style="width:25%">
                    <template #filter>
                        <InputText type="text" v-model="filters2['name']" class="p-column-filter" placeholder="Search by name"/>
                    </template>
                </Column>
                <Column header="Country" :sortable="true" sortField="country.name" filterField="country.name" filterMatchMode="contains" style="width:25%">
                    <template #body="slotProps">
                        <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="30" />
                        <span class="image-text">{{slotProps.data.country.name}}</span>
                    </template>
                    <template #filter>
                        <InputText type="text" v-model="filters2['country.name']" class="p-column-filter" placeholder="Search by country"/>
                    </template>
                </Column>
                <Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name" filterMatchMode="in" style="width:25%">
                    <template #body="slotProps">
                        <img :alt="slotProps.data.representative.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                        <span class="image-text">{{slotProps.data.representative.name}}</span>
                    </template>
                        <template #filter>
                        <MultiSelect v-model="filters2['representative.name']" :options="representatives" optionLabel="name" optionValue="name" placeholder="All" class="p-column-filter">
                            <template #option="slotProps">
                                <div class="p-multiselect-representative-option">
                                    <img :alt="slotProps.option.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                                    <span class="image-text">{{slotProps.option.name}}</span>
                                </div>
                            </template>
                        </MultiSelect>
                    </template>
                </Column>
                <Column field="status" header="Status" :sortable="true" filterMatchMode="equals" style="width:25%">
                    <template #body="slotProps">
                        <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                    </template>
                    <template #filter>
                        <Dropdown v-model="filters2['status']" :options="statuses" placeholder="Select a Status" class="p-column-filter" :showClear="true">
                            <template #option="slotProps">
                                <span :class="'customer-badge status-' + slotProps.option">{{slotProps.option}}</span>
                            </template>
                        </Dropdown>
                    </template>
                </Column>
                <template #empty>
                    No customers found.
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
            customers: null,
            selectedCustomer1: null,
            selectedCustomer2: null,
            filters1: {},
            filters2: {},
            loading: true,
            representatives: [
                {name: "Amy Elsner", image: 'amyelsner.png'},
                {name: "Anna Fali", image: 'annafali.png'},
                {name: "Asiya Javayant", image: 'asiyajavayant.png'},
                {name: "Bernardo Dominic", image: 'bernardodominic.png'},
                {name: "Elwin Sharvill", image: 'elwinsharvill.png'},
                {name: "Ioni Bowcher", image: 'ionibowcher.png'},
                {name: "Ivan Magalhaes",image: 'ivanmagalhaes.png'},
                {name: "Onyama Limba", image: 'onyamalimba.png'},
                {name: "Stephen Shaw", image: 'stephenshaw.png'},
                {name: "XuXue Feng", image: 'xuxuefeng.png'}
            ],
            statuses: [
                'unqualified', 'qualified', 'new', 'negotiation', 'renewal', 'proposal'
            ]
        }
    },
    customerService: null,
    created() {
        this.customerService = new CustomerService();
    },
    mounted() {
        this.customerService.getCustomersMedium().then(data => this.customers = data);
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
        <div class="card">
            <h5>Session Storage</h5>
            <DataTable :value="customers" :paginator="true" :rows="10" v-model:filters="filters1"
                v-model:selection="selectedCustomer1" selectionMode="single" dataKey="id"
                stateStorage="session" stateKey="dt-state-demo-session" responsiveLayout="scroll">
                <template #header>
                   <span class="p-input-icon-left">
                        <i class="pi pi-search" />
                        <InputText v-model="filters1['global']" placeholder="Global Search" />
                    </span>
                </template>
                <Column field="name" header="Name" :sortable="true" style="width:25%">
                    <template #filter>
                        <InputText type="text" v-model="filters1['name']" class="p-column-filter" placeholder="Search by name"/>
                    </template>
                </Column>
                <Column header="Country" :sortable="true" sortField="country.name" filterField="country.name" filterMatchMode="contains" style="width:25%">
                    <template #body="slotProps">
                        <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="30" />
                        <span class="image-text">{{slotProps.data.country.name}}</span>
                    </template>
                    <template #filter>
                        <InputText type="text" v-model="filters1['country.name']" class="p-column-filter" placeholder="Search by country"/>
                    </template>
                </Column>
                <Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name" filterMatchMode="in" style="width:25%">
                    <template #body="slotProps">
                        <img :alt="slotProps.data.representative.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                        <span class="image-text">{{slotProps.data.representative.name}}</span>
                    </template>
                        <template #filter>
                        <MultiSelect v-model="filters1['representative.name']" :options="representatives" optionLabel="name" optionValue="name" placeholder="All" class="p-column-filter">
                            <template #option="slotProps">
                                <div class="p-multiselect-representative-option">
                                    <img :alt="slotProps.option.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                                    <span class="image-text">{{slotProps.option.name}}</span>
                                </div>
                            </template>
                        </MultiSelect>
                    </template>
                </Column>
                <Column field="status" header="Status" :sortable="true" filterMatchMode="equals" style="width:25%">
                    <template #body="slotProps">
                        <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                    </template>
                    <template #filter>
                        <Dropdown v-model="filters1['status']" :options="statuses" placeholder="Select a Status" class="p-column-filter" :showClear="true">
                            <template #option="slotProps">
                                <span :class="'customer-badge status-' + slotProps.option">{{slotProps.option}}</span>
                            </template>
                        </Dropdown>
                    </template>
                </Column>
                <template #empty>
                    No customers found.
                </template>
            </DataTable>
        </div>

        <div class="card">
            <h5>Local Storage</h5>
            <DataTable :value="customers" :paginator="true" :rows="10" v-model:filters="filters2"
                v-model:selection="selectedCustomer2" selectionMode="single" dataKey="id"
                stateStorage="session" stateKey="dt-state-demo-local" responsiveLayout="scroll">
                <template #header>
                   <span class="p-input-icon-left">
                        <i class="pi pi-search" />
                        <InputText v-model="filters2['global']" placeholder="Global Search" />
                    </span>
                </template>
                <Column field="name" header="Name" :sortable="true" style="width:25%">
                    <template #filter>
                        <InputText type="text" v-model="filters2['name']" class="p-column-filter" placeholder="Search by name"/>
                    </template>
                </Column>
                <Column header="Country" :sortable="true" sortField="country.name" filterField="country.name" filterMatchMode="contains" style="width:25%">
                    <template #body="slotProps">
                        <img src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="30" />
                        <span class="image-text">{{slotProps.data.country.name}}</span>
                    </template>
                    <template #filter>
                        <InputText type="text" v-model="filters2['country.name']" class="p-column-filter" placeholder="Search by country"/>
                    </template>
                </Column>
                <Column header="Representative" :sortable="true" sortField="representative.name" filterField="representative.name" filterMatchMode="in" style="width:25%">
                    <template #body="slotProps">
                        <img :alt="slotProps.data.representative.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                        <span class="image-text">{{slotProps.data.representative.name}}</span>
                    </template>
                        <template #filter>
                        <MultiSelect v-model="filters2['representative.name']" :options="representatives" optionLabel="name" optionValue="name" placeholder="All" class="p-column-filter">
                            <template #option="slotProps">
                                <div class="p-multiselect-representative-option">
                                    <img :alt="slotProps.option.name" src="https://www.primefaces.org/wp-content/uploads/2020/05/placeholder.png" width="32" style="vertical-align: middle" />
                                    <span class="image-text">{{slotProps.option.name}}</span>
                                </div>
                            </template>
                        </MultiSelect>
                    </template>
                </Column>
                <Column field="status" header="Status" :sortable="true" filterMatchMode="equals" style="width:25%">
                    <template #body="slotProps">
                        <span :class="'customer-badge status-' + slotProps.data.status">{{slotProps.data.status}}</span>
                    </template>
                    <template #filter>
                        <Dropdown v-model="filters2['status']" :options="statuses" placeholder="Select a Status" class="p-column-filter" :showClear="true">
                            <template #option="slotProps">
                                <span :class="'customer-badge status-' + slotProps.option">{{slotProps.option}}</span>
                            </template>
                        </Dropdown>
                    </template>
                </Column>
                <template #empty>
                    No customers found.
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
        const customers = ref();
        const selectedCustomer1 = ref();
        const selectedCustomer2 = ref();
        const filters1: {},
        const filters2: {},
        const loading: true,
        const representatives: [
            {name: "Amy Elsner", image: 'amyelsner.png'},
            {name: "Anna Fali", image: 'annafali.png'},
            {name: "Asiya Javayant", image: 'asiyajavayant.png'},
            {name: "Bernardo Dominic", image: 'bernardodominic.png'},
            {name: "Elwin Sharvill", image: 'elwinsharvill.png'},
            {name: "Ioni Bowcher", image: 'ionibowcher.png'},
            {name: "Ivan Magalhaes",image: 'ivanmagalhaes.png'},
            {name: "Onyama Limba", image: 'onyamalimba.png'},
            {name: "Stephen Shaw", image: 'stephenshaw.png'},
            {name: "XuXue Feng", image: 'xuxuefeng.png'}
        ],
        statuses: [
            'unqualified', 'qualified', 'new', 'negotiation', 'renewal', 'proposal'
        ]
    },
    customerService: null,
    created() {
        this.customerService = new CustomerService();
    },
    mounted() {
        this.customerService.getCustomersMedium().then(data => this.customers = data);
    }
}
<\\/script>                  
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
        this.customerService.getCustomersMedium().then(data => this.customers = data);
    }
}
</script>