<template>
    <div>
        <div class="content-section introduction">
            <div class="feature-intro">
                <h1>Float Label</h1>
                <p>All input text components support floating labels.</p>
            </div>
            <AppInputStyleSwitch />
        </div>

        <div class="content-section implementation">
            <div class="card">
                <div class="p-fluid p-grid">
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <InputText id="inputtext" type="text" v-model="value1" />
                            <label for="inputtext">InputText</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label p-input-icon-left">
                            <i class="pi pi-search" />
                            <InputText id="inputtext-left" type="text" v-model="valueIconLeft" />
                            <label for="inputtext-left">Left Icon</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                       <span class="p-float-label p-input-icon-right">
                            <i class="pi pi-search" />
                            <InputText id="inputtext-right" type="text" v-model="valueIconRight" />
                            <label for="inputtext-right">Right Icon</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <AutoComplete v-model="value2" :suggestions="filteredCountries" @complete="searchCountry($event)" field="name" />
                            <label for="autocomplete">AutoComplete</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <Calendar id="calendar" v-model="value3" />
                            <label for="calendar">Calendar</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <Chips id="chips" v-model="value4" />
                            <label for="chips">Chips</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <InputMask id="inputmask" v-model="value5" mask="99/99/9999" slotChar="mm/dd/yyyy" />
                            <label for="inputmask">InputMask</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <InputNumber id="inputnumber" v-model="value6" />
                            <label for="inputnumber">InputNumber</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <div class="p-inputgroup">
                            <span class="p-inputgroup-addon">
                                <i class="pi pi-user"></i>
                            </span>
                            <span class="p-float-label">
                                <InputText id="inputgroup" type="text" v-model="value7" />
                                <label for="inputgroup">InputGroup</label>
                            </span>
                        </div>
                    </div>
                     <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <CascadeSelect id="cascadeSelect" v-model="selectedCity" :options="cascadeCountries" optionLabel="cname" optionGroupLabel="name"
                                :optionGroupChildren="['states', 'cities']" />
                            <label for="multiselect">CascadeSelect</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <Dropdown id="dropdown" v-model="value8" :options="cities" optionLabel="name" />
                            <label for="dropdown">Dropdown</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <MultiSelect id="multiselect" v-model="value9" :options="cities" optionLabel="name" />
                            <label for="multiselect">MultiSelect</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <Textarea id="textarea" v-model="value10" rows="3" />
                            <label for="textarea">Textarea</label>
                        </span>
                    </div>
                    <div class="p-field p-col-12 p-md-4">
                        <span class="p-float-label">
                            <Password id="password" v-model="value11" />
                            <label for="password">Password</label>
                        </span>
                    </div>
                </div>
            </div>
        </div>

        <AppDoc name="FloatLabelDemo" :sources="sources" :service="['CountryService']" :data="['countries']" />
    </div>
</template>

<script>
import CountryService from '../../service/CountryService';

export default {
    data() {
        return {
            countries: null,
            filteredCountries: null,
            cities: [
                {name: 'New York', code: 'NY'},
                {name: 'Rome', code: 'RM'},
                {name: 'London', code: 'LDN'},
                {name: 'Istanbul', code: 'IST'},
                {name: 'Paris', code: 'PRS'}
            ],
            value1: null,
            value2: null,
            value3: null,
            value4: null,
            value5: null,
            value6: null,
            value7: null,
            value8: null,
            value9: null,
            value10: null,
            value11: null,
            valueIconLeft: null,
            valueIconRight: null,
            selectedCity: null,
            cascadeCountries: [
                {
                    name: 'Australia',
                    code: 'AU',
                    states: [
                        {
                            name: 'New South Wales',
                            cities: [
                                {cname: 'Sydney', code: 'A-SY'},
                                {cname: 'Newcastle', code: 'A-NE'},
                                {cname: 'Wollongong', code: 'A-WO'}
                            ]
                        },
                        {
                            name: 'Queensland',
                            cities: [
                                {cname: 'Brisbane', code: 'A-BR'},
                                {cname: 'Townsville', code: 'A-TO'}
                            ]
                        },
                        
                    ]
                },
                {
                    name: 'Canada', 
                    code: 'CA',
                    states: [
                        {
                            name: 'Quebec',
                            cities: [
                                {cname: 'Montreal', code: 'C-MO'},
                                {cname: 'Quebec City', code: 'C-QU'}
                            ]
                        },
                        {
                            name: 'Ontario',
                            cities: [
                                {cname: 'Ottawa', code: 'C-OT'},
                                {cname: 'Toronto', code: 'C-TO'}
                            ]
                        },
                        
                    ]
                },
                {
                    name: 'United States',
                    code: 'US',
                    states: [
                        {
                            name: 'California',
                            cities: [
                                {cname: 'Los Angeles', code: 'US-LA'},
                                {cname: 'San Diego', code: 'US-SD'},
                                {cname: 'San Francisco', code: 'US-SF'}
                            ]
                        },
                        {
                            name: 'Florida',
                            cities: [
                                {cname: 'Jacksonville', code: 'US-JA'},
                                {cname: 'Miami', code: 'US-MI'},
                                {cname: 'Tampa', code: 'US-TA'},
                                {cname: 'Orlando', code: 'US-OR'}
                            ]
                        },
                        {
                            name: 'Texas',
                            cities: [
                                {cname: 'Austin', code: 'US-AU'},
                                {cname: 'Dallas', code: 'US-DA'},
                                {cname: 'Houston', code: 'US-HO'}
                            ]
                        }
                    ]
                }
            ],
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
    <div>
        <div class="card">
            <div class="p-fluid p-grid">
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <InputText id="inputtext" type="text" v-model="value1" />
                        <label for="inputtext">InputText</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label p-input-icon-left">
                        <i class="pi pi-search" />
                        <InputText id="inputtext-left" type="text" v-model="valueIconLeft" />
                        <label for="inputtext-left">Left Icon</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                   <span class="p-float-label p-input-icon-right">
                        <i class="pi pi-search" />
                        <InputText id="inputtext-right" type="text" v-model="valueIconRight" />
                        <label for="inputtext-right">Right Icon</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <AutoComplete v-model="value2" :suggestions="filteredCountries" @complete="searchCountry($event)" field="name" />
                        <label for="autocomplete">AutoComplete</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Calendar id="calendar" v-model="value3" />
                        <label for="calendar">Calendar</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Chips id="chips" v-model="value4" />
                        <label for="chips">Chips</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <InputMask id="inputmask" v-model="value5" mask="99/99/9999" slotChar="mm/dd/yyyy" />
                        <label for="inputmask">InputMask</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <InputNumber id="inputnumber" v-model="value6" />
                        <label for="inputnumber">InputNumber</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <div class="p-inputgroup">
                        <span class="p-inputgroup-addon">
                            <i class="pi pi-user"></i>
                        </span>
                        <span class="p-float-label">
                            <InputText id="inputgroup" type="text" v-model="value7" />
                            <label for="inputgroup">InputGroup</label>
                        </span>
                    </div>
                </div>
                 <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <CascadeSelect id="cascadeSelect" v-model="selectedCity" :options="cascadeCountries" optionLabel="cname" optionGroupLabel="name"
                            :optionGroupChildren="['states', 'cities']" />
                        <label for="multiselect">CascadeSelect</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Dropdown id="dropdown" v-model="value8" :options="cities" optionLabel="name" />
                        <label for="dropdown">Dropdown</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <MultiSelect id="multiselect" v-model="value9" :options="cities" optionLabel="name" />
                        <label for="multiselect">MultiSelect</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Textarea id="textarea" v-model="value10" rows="3" />
                        <label for="textarea">Textarea</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Password id="password" v-model="value11" />
                        <label for="password">Password</label>
                    </span>
                </div>
            </div>
        </div>
    </div>                    
</template>

<script>
import CountryService from './service/CountryService';
export default {
    data() {
        return {
            countries: null,
            filteredCountries: null,
            cities: [
                {name: 'New York', code: 'NY'},
                {name: 'Rome', code: 'RM'},
                {name: 'London', code: 'LDN'},
                {name: 'Istanbul', code: 'IST'},
                {name: 'Paris', code: 'PRS'}
            ],
            value1: null,
            value2: null,
            value3: null,
            value4: null,
            value5: null,
            value6: null,
            value7: null,
            value8: null,
            value9: null,
            value10: null,
            value11: null,
            valueIconLeft: null,
            valueIconRight: null,
            selectedCity: null,
            cascadeCountries: [
                {
                    name: 'Australia',
                    code: 'AU',
                    states: [
                        {
                            name: 'New South Wales',
                            cities: [
                                {cname: 'Sydney', code: 'A-SY'},
                                {cname: 'Newcastle', code: 'A-NE'},
                                {cname: 'Wollongong', code: 'A-WO'}
                            ]
                        },
                        {
                            name: 'Queensland',
                            cities: [
                                {cname: 'Brisbane', code: 'A-BR'},
                                {cname: 'Townsville', code: 'A-TO'}
                            ]
                        },
                        
                    ]
                },
                {
                    name: 'Canada', 
                    code: 'CA',
                    states: [
                        {
                            name: 'Quebec',
                            cities: [
                                {cname: 'Montreal', code: 'C-MO'},
                                {cname: 'Quebec City', code: 'C-QU'}
                            ]
                        },
                        {
                            name: 'Ontario',
                            cities: [
                                {cname: 'Ottawa', code: 'C-OT'},
                                {cname: 'Toronto', code: 'C-TO'}
                            ]
                        },
                        
                    ]
                },
                {
                    name: 'United States',
                    code: 'US',
                    states: [
                        {
                            name: 'California',
                            cities: [
                                {cname: 'Los Angeles', code: 'US-LA'},
                                {cname: 'San Diego', code: 'US-SD'},
                                {cname: 'San Francisco', code: 'US-SF'}
                            ]
                        },
                        {
                            name: 'Florida',
                            cities: [
                                {cname: 'Jacksonville', code: 'US-JA'},
                                {cname: 'Miami', code: 'US-MI'},
                                {cname: 'Tampa', code: 'US-TA'},
                                {cname: 'Orlando', code: 'US-OR'}
                            ]
                        },
                        {
                            name: 'Texas',
                            cities: [
                                {cname: 'Austin', code: 'US-AU'},
                                {cname: 'Dallas', code: 'US-DA'},
                                {cname: 'Houston', code: 'US-HO'}
                            ]
                        }
                    ]
                }
            ]
        }
    },
    countryService: null,
    created() {
        this.countryService = new CountryService();
    },
    mounted() {
        this.countryService.getCountries().then(data => this.countries = data);
    },
    methods: {
        searchCountry(event) {
            setTimeout(() => {
                if (!event.query.trim().length) {
                    this.filteredCountries = [...this.countries];
                }
                else {
                    this.filteredCountries = this.countries.filter((country) => {
                        return country.name.toLowerCase().startsWith(event.query.toLowerCase());
                    });
                }
            }, 250);
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
        <div class="card">
            <div class="p-fluid p-grid">
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <InputText id="inputtext" type="text" v-model="value1" />
                        <label for="inputtext">InputText</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label p-input-icon-left">
                        <i class="pi pi-search" />
                        <InputText id="inputtext-left" type="text" v-model="valueIconLeft" />
                        <label for="inputtext-left">Left Icon</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                   <span class="p-float-label p-input-icon-right">
                        <i class="pi pi-search" />
                        <InputText id="inputtext-right" type="text" v-model="valueIconRight" />
                        <label for="inputtext-right">Right Icon</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <AutoComplete v-model="value2" :suggestions="filteredCountries" @complete="searchCountry($event)" field="name" />
                        <label for="autocomplete">AutoComplete</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Calendar id="calendar" v-model="value3" />
                        <label for="calendar">Calendar</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Chips id="chips" v-model="value4" />
                        <label for="chips">Chips</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <InputMask id="inputmask" v-model="value5" mask="99/99/9999" slotChar="mm/dd/yyyy" />
                        <label for="inputmask">InputMask</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <InputNumber id="inputnumber" v-model="value6" />
                        <label for="inputnumber">InputNumber</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <div class="p-inputgroup">
                        <span class="p-inputgroup-addon">
                            <i class="pi pi-user"></i>
                        </span>
                        <span class="p-float-label">
                            <InputText id="inputgroup" type="text" v-model="value7" />
                            <label for="inputgroup">InputGroup</label>
                        </span>
                    </div>
                </div>
                 <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <CascadeSelect id="cascadeSelect" v-model="selectedCity" :options="cascadeCountries" optionLabel="cname" optionGroupLabel="name"
                            :optionGroupChildren="['states', 'cities']" />
                        <label for="multiselect">CascadeSelect</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Dropdown id="dropdown" v-model="value8" :options="cities" optionLabel="name" />
                        <label for="dropdown">Dropdown</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <MultiSelect id="multiselect" v-model="value9" :options="cities" optionLabel="name" />
                        <label for="multiselect">MultiSelect</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Textarea id="textarea" v-model="value10" rows="3" />
                        <label for="textarea">Textarea</label>
                    </span>
                </div>
                <div class="p-field p-col-12 p-md-4">
                    <span class="p-float-label">
                        <Password id="password" v-model="value11" />
                        <label for="password">Password</label>
                    </span>
                </div>
            </div>
        </div>
    </div>                    
</template>

<script>
import { ref, onMounted } from 'vue';
import CountryService from './service/CountryService';

export default {
    setup() {
        onMounted(() => {
            countryService.value.getCountries().then(data => countries.value = data);
        })
        const countryService = ref(new CountryService());
        const countries = ref();
        const filteredCountries = ref();
        const cities = ref([
            {name: 'New York', code: 'NY'},
            {name: 'Rome', code: 'RM'},
            {name: 'London', code: 'LDN'},
            {name: 'Istanbul', code: 'IST'},
            {name: 'Paris', code: 'PRS'}
        ]);
        const value1 = ref();
        const value2 = ref();
        const value3 = ref();
        const value4 = ref();
        const value5 = ref();
        const value6 = ref();
        const value7 = ref();
        const value8 = ref();
        const value9 = ref();
        const value10 = ref();
        const value11 = ref();
        const valueIconLeft = ref();
        const valueIconRight = ref();
        const selectedCity = ref();
        const cascadeCountries = ref([
            {
                name: 'Australia',
                code: 'AU',
                states: [
                    {
                        name: 'New South Wales',
                        cities: [
                            {cname: 'Sydney', code: 'A-SY'},
                            {cname: 'Newcastle', code: 'A-NE'},
                            {cname: 'Wollongong', code: 'A-WO'}
                        ]
                    },
                    {
                        name: 'Queensland',
                        cities: [
                            {cname: 'Brisbane', code: 'A-BR'},
                            {cname: 'Townsville', code: 'A-TO'}
                        ]
                    },
                    
                ]
            },
            {
                name: 'Canada', 
                code: 'CA',
                states: [
                    {
                        name: 'Quebec',
                        cities: [
                            {cname: 'Montreal', code: 'C-MO'},
                            {cname: 'Quebec City', code: 'C-QU'}
                        ]
                    },
                    {
                        name: 'Ontario',
                        cities: [
                            {cname: 'Ottawa', code: 'C-OT'},
                            {cname: 'Toronto', code: 'C-TO'}
                        ]
                    },
                    
                ]
            },
            {
                name: 'United States',
                code: 'US',
                states: [
                    {
                        name: 'California',
                        cities: [
                            {cname: 'Los Angeles', code: 'US-LA'},
                            {cname: 'San Diego', code: 'US-SD'},
                            {cname: 'San Francisco', code: 'US-SF'}
                        ]
                    },
                    {
                        name: 'Florida',
                        cities: [
                            {cname: 'Jacksonville', code: 'US-JA'},
                            {cname: 'Miami', code: 'US-MI'},
                            {cname: 'Tampa', code: 'US-TA'},
                            {cname: 'Orlando', code: 'US-OR'}
                        ]
                    },
                    {
                        name: 'Texas',
                            cities: [
                                {cname: 'Austin', code: 'US-AU'},
                                {cname: 'Dallas', code: 'US-DA'},
                                {cname: 'Houston', code: 'US-HO'}
                            ]
                        }
                    ]
                }
            ]);

        const searchCountry = (event) => {
            setTimeout(() => {
                if (!event.query.trim().length) {
                    filteredCountries.value = [...countries.value];
                }
                else {
                    filteredCountries.value = countries.value.filter((country) => {
                        return country.name.toLowerCase().startsWith(event.query.toLowerCase());
                    });
                }
            }, 250);
        };

        return { countryService, countries, filteredCountries, cities, value1, value2, value3, value4, value5, value6, 
            value7, value8, value9, value10, value11, valueIconLeft, valueIconRight, selectedCity, cascadeCountries, searchCountry }
    }
}
<\\/script>
`
                }
            }
        }
    },
    countryService: null,
    created() {
        this.countryService = new CountryService();
    },
    mounted() {
        this.countryService.getCountries().then(data => this.countries = data);
    },
    methods: {
        searchCountry(event) {
            setTimeout(() => {
                if (!event.query.trim().length) {
                    this.filteredCountries = [...this.countries];
                }
                else {
                    this.filteredCountries = this.countries.filter((country) => {
                        return country.name.toLowerCase().startsWith(event.query.toLowerCase());
                    });
                }
            }, 250);
        }
    }
}
</script>

<style lang="scss" scoped>
textarea {
    resize: none;
}
</style>