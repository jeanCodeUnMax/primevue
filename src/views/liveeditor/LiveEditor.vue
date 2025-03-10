<template>
    <span v-if="showEditor">
        <SplitButton :model="items" label="Edit in CodeSandbox" class="liveEditorSplitButton" @click="openDefaultCSB" />
    </span>
</template>

<script>
import { services, data } from './LiveEditorData';
export default {
    data() {
        return {
            sandbox_id: null,
            showCodeHighlight: false,
            items: [
                {label: "Options API", command: () => { this.postSandboxParameters('options-api') }},
                {label: "Composition API", command: () => { this.postSandboxParameters('composition-api') }}
            ]
        }
    },
    props: {
        name: {
            type: String,
            default: null
        },
        sources: {
            type: Object,
            default: null
        },
        service: {
            type: Array,
            default: null
        },
        data: {
            type: Array,
            default: null
        },
        extPages: {
            type: Array,
            default: null
        },
        dependencies: {
            type: Object,
            default: null
        },
        extFiles: {
            type: Object,
            default: null
        }
    },
    methods: {
        postSandboxParameters(sourceType) {
            fetch('https://codesandbox.io/api/v1/sandboxes/define?json=1', {
                method: "POST",
                headers: {
                    'Content-Type': 'application/json',
                    'Accept': 'application/json'
                },
                body: JSON.stringify(this.getSandboxParameters(sourceType))
            })
            .then(response => response.json())
            .then(data => window.open(`https://codesandbox.io/s/${data.sandbox_id}`, '_blank'))
            .catch(() => this.showCodeHighlight = true );
        },

        createSandboxParameters(nameWithExt, files, extDependencies) {
            const boolExtFiles = !this.extFiles;
            let extFiles = !boolExtFiles ? {...this.extFiles} : {};
            let extIndexCSS = extFiles['index.css'] || '';
            delete extFiles['index.css'];

            const dependencies = require('../../../package.json') ? require('../../../package.json').devDependencies : {};

            return {
                files: {
                    'package.json': {
                        content: {
                            main: `src/demo/${nameWithExt}`,
                            dependencies: {
                                ...extDependencies,
                                'vue': dependencies['vue'],
                                'axios': dependencies['axios'],
                                'primevue': 'latest',
                                'primeflex': dependencies['primeflex'],
                                'primeicons': 'latest',
                                '@babel/cli': dependencies['@babel/cli'],
                                'core-js': dependencies['core-js'],
                                'vue-router': dependencies['vue-router']
                            },
                            devDependencies: {
                                '@vue/cli-plugin-babel': dependencies['@vue/cli-plugin-babel'],
                                '@vue/cli-plugin-eslint': dependencies['@vue/cli-plugin-eslint'],
                                '@vue/cli-service': dependencies['@vue/cli-service'],
                                '@vue/compiler-sfc': dependencies['@vue/compiler-sfc'],
                                'eslint': dependencies['eslint'],
                                'eslint-plugin-vue': dependencies['eslint-plugin-vue']
                            }
                        }
                    },
                    'babel.config.js': {
                content: `module.exports = {
    presets: [
        '@vue/cli-plugin-babel/preset'
    ]
}`
                    },
                    '.eslintrc.js': {
                        content: `module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    'plugin:vue/vue3-essential',
    'eslint:recommended'
  ],
  parserOptions: {
    parser: 'babel-eslint'
  }
}`
                    },
                    'src/index.css': {
                        content: `html {
    font-size: 14px;
}

body {
    background-color: #ffffff;
    font-family: -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, Helvetica, Arial, sans-serif, Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol;
    font-weight: normal;
    color: #495057;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    padding: .5em;
    margin-bottom: 50px;
}

h1, h2, h3, h4, h5, h6 {
    margin: 1.5rem 0 1rem 0;
    font-family: inherit;
    font-weight: 600;
    line-height: 1.2;
    color: inherit;
}

h1 { font-size: 2.5rem; }
h2 { font-size: 2rem; }
h3 { font-size: 1.75rem; }
h4 { font-size: 1.5rem; }
h5 { font-size: 1.25rem; }
h6 { font-size: 1rem; }
p {
    line-height: 1.5;
    margin: 0 0 1rem 0;
}

.card {
    margin-bottom: 2rem;
}

input[type="number"] {
    -moz-appearance: textfield;
}

input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
}

@keyframes pulse {
    0% {
        background-color: rgba(165, 165, 165, 0.1)
    }
    50% {
        background-color: rgba(165, 165, 165, 0.3)
    }
    100% {
        background-color: rgba(165, 165, 165, 0.1)
    }
}

.customer-badge {
    border-radius: 2px;
    padding: .25em .5rem;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: .3px;
}

.customer-badge.status-qualified {
    background-color: #C8E6C9;
    color: #256029;
}

.customer-badge.status-unqualified {
    background-color: #FFCDD2;
    color: #C63737;
}

.customer-badge.status-negotiation {
    background-color: #FEEDAF;
    color: #8A5340;
}

.customer-badge.status-new {
    background-color: #B3E5FC;
    color: #23547B;
}

.customer-badge.status-renewal {
    background-color: #ECCFFF;
    color: #694382;
}

.customer-badge.status-proposal {
    background-color: #FFD8B2;
    color: #805B36;
}

.product-badge {
    border-radius: 2px;
    padding: .25em .5rem;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: .3px;
}

.product-badge.status-instock {
    background: #C8E6C9;
    color: #256029;
}

.product-badge.status-outofstock {
    background: #FFCDD2;
    color: #C63737;
}

.product-badge.status-lowstock {
    background: #FEEDAF;
    color: #8A5340;
}

.order-badge {
    border-radius: 2px;
    padding: .25em .5rem;
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    letter-spacing: .3px;
}

.order-badge.order-delivered {
    background: #C8E6C9;
    color: #256029;
}

.order-badge.order-cancelled {
    background: #FFCDD2;
    color: #C63737;
}

.order-badge.order-pending {
    background: #FEEDAF;
    color: #8A5340;
}

.order-badge.order-returned {
    background: #ECCFFF;
    color: #694382;
}

.image-text {
    margin-left: .5rem;
}

.p-multiselect-representative-option {
    display: inline-block;
    vertical-align: middle;
}

.p-multiselect-representative-option img {
    vertical-align: middle;
    width: 24px;
}

.p-multiselect-representative-option span {
    margin-top: .125rem;
}

.country-item {
    display: flex;
    align-items: center;
}

.country-item img.flag {
    width: 18px;
    margin-right: .5rem;
}

.flag {
    vertical-align: middle;
}

span.flag {
    width:44px;
    height:30px;
    display:inline-block;
}

img.flag {
    width:30px
}

.true-icon {
    color: #256029;
}

.false-icon {
    color: #C63737;
}
${extIndexCSS}
`
                    },
                    ...files,
                    ...extFiles
                }
            }
        },

        getSandboxParameters(sourceType) {
            /* eslint-disable */
            let name = this.name;
            let extension = '.vue';
            let extDependencies = this.dependencies || {};
            let extImport = '';
            let extElement = '';
            let content = this.sources[sourceType].content.replace('<\\/script>', '<\/script>');
            let pages = this.extPages ? this.extPages : '';
            let _files = {}, element = '';

            if(this.dependencies) {
                extImport += `import ${name.slice(0, -4)} from 'primevue/${name.slice(0, -4).toLowerCase()}';`
                extElement += `app.component('${name.slice(0, -4)}', ${name.slice(0, -4)});`;
            }

            if (this.service) {
                let dataArr = [], serviceArr = [];
                
                this.service.forEach(el => {
                    serviceArr.push(el.split(','))
                })

                if(this.data) {
                    this.data.forEach(el => {
                        dataArr.push(el.split(','))
                    })

                    if(dataArr) {
                        dataArr.forEach(el => {
                            _files[`public/data/${el}.json`] = {
                                content: data[el]
                            };
                        });
                    }
                }

                serviceArr.forEach(serv => {
                     _files[`src/service/${serv}.js`] = {
                            content: `${services[serv]}`
                    };
                })
            }

            element += `import ${name} from "./${name}.vue"`;

            _files['src/main.js'] = {
                content: `import "primeflex/primeflex.css";
import "primevue/resources/themes/saga-blue/theme.css";
import "primevue/resources/primevue.min.css";
import "primeicons/primeicons.css";
import "./index.css";

import { createApp } from "vue";
${element}
import { router } from "./router";
import PrimeVue from "primevue/config";
import AutoComplete from 'primevue/autocomplete';
import Accordion from 'primevue/accordion';
import AccordionTab from 'primevue/accordiontab';
import Avatar from 'primevue/avatar';
import AvatarGroup from 'primevue/avatargroup';
import Badge from 'primevue/badge';
import BadgeDirective from "primevue/badgedirective";
import BlockUI from 'primevue/blockui';
import Button from 'primevue/button';
import Breadcrumb from 'primevue/breadcrumb';
import Calendar from 'primevue/calendar';
import Card from 'primevue/card';
import CascadeSelect from 'primevue/cascadeselect';
import Carousel from 'primevue/carousel';
import Checkbox from 'primevue/checkbox';
import Chip from 'primevue/chip';
import Chips from 'primevue/chips';
import ColorPicker from 'primevue/colorpicker';
import Column from 'primevue/column';
import ColumnGroup from 'primevue/columngroup';
import ConfirmDialog from 'primevue/confirmdialog';
import ConfirmPopup from 'primevue/confirmpopup';
import ConfirmationService from 'primevue/confirmationservice';
import ContextMenu from 'primevue/contextmenu';
import DataTable from 'primevue/datatable';
import DataView from 'primevue/dataview';
import DataViewLayoutOptions from 'primevue/dataviewlayoutoptions';
import DeferredContent from 'primevue/deferredcontent';
import Dialog from 'primevue/dialog';
import Divider from 'primevue/divider';
import Dropdown from 'primevue/dropdown';
import Fieldset from 'primevue/fieldset';
import FileUpload from 'primevue/fileupload';
import Galleria from 'primevue/galleria';
import InlineMessage from 'primevue/inlinemessage';
import Inplace from 'primevue/inplace';
import InputSwitch from 'primevue/inputswitch';
import InputText from 'primevue/inputtext';
import InputMask from 'primevue/inputmask';
import InputNumber from 'primevue/inputnumber';
import Knob from 'primevue/knob';
import Listbox from 'primevue/listbox';
import MegaMenu from 'primevue/megamenu';
import Menu from 'primevue/menu';
import Menubar from 'primevue/menubar';
import Message from 'primevue/message';
import MultiSelect from 'primevue/multiselect';
import OrderList from 'primevue/orderlist';
import OrganizationChart from 'primevue/organizationchart';
import OverlayPanel from 'primevue/overlaypanel';
import Paginator from 'primevue/paginator';
import Panel from 'primevue/panel';
import PanelMenu from 'primevue/panelmenu';
import Password from 'primevue/password';
import PickList from 'primevue/picklist';
import ProgressBar from 'primevue/progressbar';
import ProgressSpinner from 'primevue/progressspinner';
import Rating from 'primevue/rating';
import RadioButton from 'primevue/radiobutton';
import Ripple from 'primevue/ripple';
import Row from 'primevue/row';
import SelectButton from 'primevue/selectbutton';
import ScrollPanel from 'primevue/scrollpanel';
import ScrollTop from 'primevue/scrolltop';
import Skeleton from 'primevue/skeleton';
import Slider from 'primevue/slider';
import Sidebar from 'primevue/sidebar';
import SplitButton from 'primevue/splitbutton';
import Splitter from 'primevue/splitter';
import SplitterPanel from 'primevue/splitterpanel';
import Steps from 'primevue/steps';
import TabMenu from 'primevue/tabmenu';
import TieredMenu from 'primevue/tieredmenu';
import Textarea from 'primevue/textarea';
import Toast from 'primevue/toast';
import ToastService from 'primevue/toastservice';
import Toolbar from 'primevue/toolbar';
import TabView from 'primevue/tabview';
import TabPanel from 'primevue/tabpanel';
import Tag from 'primevue/tag';
import Terminal from 'primevue/terminal';
import Timeline from 'primevue/timeline';
import ToggleButton from 'primevue/togglebutton';
import Tooltip from 'primevue/tooltip';
import Tree from 'primevue/tree';
import TreeTable from 'primevue/treetable';
import TriStateCheckbox from 'primevue/tristatecheckbox';
${extImport}

const app = createApp(${name});

app.use(PrimeVue, { ripple: true });
app.use(ConfirmationService);
app.use(ToastService);
app.use(router);

app.directive('tooltip', Tooltip);
app.directive('badge', BadgeDirective);
app.directive('ripple', Ripple);

app.component('Accordion', Accordion);
app.component('AccordionTab', AccordionTab);
app.component('AutoComplete', AutoComplete);
app.component('Avatar', Avatar);
app.component('AvatarGroup', AvatarGroup);
app.component('Badge', Badge);
app.component('BlockUI', BlockUI);
app.component('Breadcrumb', Breadcrumb);
app.component('Button', Button);
app.component('Calendar', Calendar);
app.component('Card', Card);
app.component('Carousel', Carousel);
app.component('CascadeSelect', CascadeSelect);
app.component('Checkbox', Checkbox);
app.component('Chip', Chip);
app.component('Chips', Chips);
app.component('ColorPicker', ColorPicker);
app.component('Column', Column);
app.component('ColumnGroup', ColumnGroup);
app.component('ConfirmDialog', ConfirmDialog);
app.component('ConfirmPopup', ConfirmPopup);
app.component('ContextMenu', ContextMenu);
app.component('DataTable', DataTable);
app.component('DataView', DataView);
app.component('DataViewLayoutOptions', DataViewLayoutOptions);
app.component('DeferredContent', DeferredContent);
app.component('Dialog', Dialog);
app.component('Divider', Divider);
app.component('Dropdown', Dropdown);
app.component('Fieldset', Fieldset);
app.component('FileUpload', FileUpload);
app.component('InlineMessage', InlineMessage);
app.component('Inplace', Inplace);
app.component('InputMask', InputMask);
app.component('InputNumber', InputNumber);
app.component('InputSwitch', InputSwitch);
app.component('InputText', InputText);
app.component('Galleria', Galleria);
app.component('Knob', Knob);
app.component('Listbox', Listbox);
app.component('MegaMenu', MegaMenu);
app.component('Menu', Menu);
app.component('Menubar', Menubar);
app.component('Message', Message);
app.component('MultiSelect', MultiSelect);
app.component('OrderList', OrderList);
app.component('OrganizationChart', OrganizationChart);
app.component('OverlayPanel', OverlayPanel);
app.component('Paginator', Paginator);
app.component('Panel', Panel);
app.component('PanelMenu', PanelMenu);
app.component('Password', Password);
app.component('PickList', PickList);
app.component('ProgressBar', ProgressBar);
app.component('ProgressSpinner', ProgressSpinner);
app.component('RadioButton', RadioButton);
app.component('Rating', Rating);
app.component('Row', Row);
app.component('SelectButton', SelectButton);
app.component('ScrollPanel', ScrollPanel);
app.component('ScrollTop', ScrollTop);
app.component('Slider', Slider);
app.component('Sidebar', Sidebar);
app.component('Skeleton', Skeleton);
app.component('SplitButton', SplitButton);
app.component('Splitter', Splitter);
app.component('SplitterPanel', SplitterPanel);
app.component('Steps', Steps);
app.component('TabMenu', TabMenu);
app.component('TabView', TabView);
app.component('TabPanel', TabPanel);
app.component('Tag', Tag);
app.component('Textarea', Textarea);
app.component('Terminal', Terminal);
app.component('TieredMenu', TieredMenu);
app.component('Timeline', Timeline);
app.component('Toast', Toast);
app.component('Toolbar', Toolbar);
app.component('ToggleButton', ToggleButton);
app.component('Tree', Tree);
app.component('TreeTable', TreeTable);
app.component('TriStateCheckbox', TriStateCheckbox);
${extElement}

app.mount("#app");
`
            }

            _files['public/index.html'] = {
                content: `<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0" />
    <link href="https://unpkg.com/primeicons/primeicons.css" rel="stylesheet">
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
`
            }

            _files[`src/${name}${extension}`] = {       
                    content: `${content}
`
            }

            if(pages) {
                let routes = [], routeImports = '';

                pages.forEach((page, i) => {
                    _files[`src/components/${page.tabName}.vue`] = {
                        'content': `${page.content.replace('<\\/script>', '<\/script>')}`
                    }

                    let route = '';

                    routeImports += `import ${page.tabName} from './components/${page.tabName}.vue';
`;

                    if(i === 0) {
                        route += `{
    path: "/",
    component: ${page.tabName}
}`;
                    }
                    else {
                        route += `{
    path: "/${page.tabName.slice(0, -4).toLowerCase()}",
    component: ${page.tabName}
}`;
                    }

                    routes.push(route);
                })

                _files['src/router.js'] = {
                    'content': `import { createRouter, createWebHistory } from "vue-router";
${routeImports}
export const router = createRouter({
    history: createWebHistory(),
    routes: [
        ${routes}
    ]
});
`
                }
            }
            else {
                _files[`src/router.js`] = {
                    content: `import { createRouter, createWebHistory } from "vue-router";
${element}

export const router = createRouter({
  history: createWebHistory(),
  routes: [{ path: "/", component: ${name} }]
});`
                }
            }

            return this.createSandboxParameters(`${name}${extension}`, _files, extDependencies);
        },

        openDefaultCSB() {
            this.postSandboxParameters(this.defaultSourceType);
        }
    },
    computed: {
        showEditor() {
            return this.$appState.codeSandbox;
        },
        defaultSourceType() {
            return this.$appState.sourceType;
        }
    }
}
</script>
