<template>
    <div>
        <div class="content-section introduction">
            <div class="feature-intro">
                <h1>Tree <span>Filter</span></h1>
                <p>Filtering updates the node based on the constraints.</p>
            </div>
        </div>

        <div class="content-section implementation">
            <div class="card">
                <h5>Lenient Filter</h5>
                <Tree :value="nodes" :filter="true" filterMode="lenient"></Tree>

                <h5>Strict Filter</h5>
                <Tree :value="nodes" :filter="true" filterMode="strict"></Tree>
            </div>
        </div>

        <AppDoc name="TreeFilterDemo" :sources="sources" :service="['NodeService']" :data="['treenodes']" />
    </div>
</template>

<script>
import NodeService from '../../service/NodeService';

export default {
    data() {
        return {
            nodes: null,
            expandedKeys: {},
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
    <div>
        <h5>Lenient Filter</h5>
        <Tree :value="nodes" :filter="true" filterMode="lenient"></Tree>

        <h5>Strict Filter</h5>
        <Tree :value="nodes" :filter="true" filterMode="strict"></Tree>
    </div>
</template>

<script>
import NodeService from './service/NodeService';

export default {
    data() {
        return {
            nodes: null,
            expandedKeys: {}
        }
    },
    nodeService: null,
    created() {
        this.nodeService = new NodeService();
    },
    mounted() {
        this.nodeService.getTreeNodes().then(data => this.nodes = data);
    },
    methods: {
        expandAll() {
            for (let node of this.nodes) {
                this.expandNode(node);
            }

            this.expandedKeys = {...this.expandedKeys};
        },
        collapseAll() {
            this.expandedKeys = {};
        },
        expandNode(node) {
            this.expandedKeys[node.key] = true;
            if (node.children && node.children.length) {
                for (let child of node.children) {
                    this.expandNode(child);
                }
            }
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
        <h5>Lenient Filter</h5>
        <Tree :value="nodes" :filter="true" filterMode="lenient"></Tree>

        <h5>Strict Filter</h5>
        <Tree :value="nodes" :filter="true" filterMode="strict"></Tree>
    </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import NodeService from './service/NodeService';

export default {
    setup() {
        onMounted(() => {
            nodeService.value.getTreeNodes().then(data => nodes.value = data);
        })

        const nodes = ref(null);
        const nodeService = ref(new NodeService());
        const expandedKeys = ref({});
        const expandAll = () => {
            for (let node of nodes.value) {
                expandNode(node);
            }

            expandedKeys.value = {...expandedKeys.value};
        };
        const collapseAll = () => {
            expandedKeys.value = {};
        };
        const expandNode = (node) => {
            expandedKeys.value[node.key] = true;
            if (node.children && node.children.length) {
                for (let child of node.children) {
                    expandNode(child);
                }
            }
        };

        return { nodes, nodeService, expandedKeys, expandAll, collapseAll, expandNode }
    }
}
<\\/script>
`
                }
            }
        }
    },
    nodeService: null,
    created() {
        this.nodeService = new NodeService();
    },
    mounted() {
        this.nodeService.getTreeNodes().then(data => this.nodes = data);
    },
    methods: {
        expandAll() {
            for (let node of this.nodes) {
                this.expandNode(node);
            }

            this.expandedKeys = {...this.expandedKeys};
        },
        collapseAll() {
            this.expandedKeys = {};
        },
        expandNode(node) {
            this.expandedKeys[node.key] = true;
            if (node.children && node.children.length) {
                for (let child of node.children) {
                    this.expandNode(child);
                }
            }
        }
    }
}
</script>

<style scoped>
button {
    margin-right: .5rem;
}
</style>