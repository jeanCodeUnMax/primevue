<template>
    <div>
        <div class="content-section introduction">
            <div class="feature-intro">
                <h1>Tree <span>Lazy</span></h1>
                <p>Lazy loading is handy when dealing with huge datasets. This example imitates a lazy loading case with timeouts.</p>
            </div>
        </div>

        <div class="content-section implementation">
            <div class="card">
                <Tree :value="nodes" @node-expand="onNodeExpand" :loading="loading"></Tree>
            </div>
        </div>

        <AppDoc name="TreeLazyDemo" :sources="sources" :service="['NodeService']" :data="['treenodes']" />
    </div>
</template>

<script>
import NodeService from '../../service/NodeService';

export default {
    data() {
        return {
            loading: false,
            nodes: null,
            sources: {
                'options-api': {
                    tabName: 'Source',
                    content: `
<template>
    <div>
        <Tree :value="nodes" @nodeExpand="onNodeExpand" :loading="loading"></Tree>
    </div>                   
</template>

<script>
import NodeService from './service/NodeService';

export default {
    data() {
        return {
            loading: false,
            nodes: null
        }
    },
    nodeService: null,
    created() {
        this.nodeService = new NodeService();
    },
    mounted() {
        this.loading = true;

        setTimeout(() => {
            this.nodes = this.initateNodes();
            this.loading = false;
        }, 2000);
    },
    methods: {
        onNodeExpand(node) {
            if (!node.children) {
                this.loading = true;

                setTimeout(() => {
                    let _node = {...node};
                    _node.children = [];

                    for (let i = 0; i < 3; i++) {
                        _node.children.push({
                            key: node.key + '-' + i,
                            label: 'Lazy ' + node.label + '-' + i
                        });
                    }

                    let _nodes = {...this.nodes}
                    _nodes[parseInt(node.key, 10)] = _node;

                    this.nodes = _nodes;
                    this.loading = false;
                }, 500);
            }
        },
        initateNodes() {
            return [{
                key: '0',
                label: 'Node 0',
                leaf: false
            },
            {
                key: '1',
                label: 'Node 1',
                leaf: false
            },
            {
                key: '2',
                label: 'Node 2',
                leaf: false
            }];
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
        <Tree :value="nodes" @nodeExpand="onNodeExpand" :loading="loading"></Tree>
    </div>                   
</template>

<script>
import { ref, onMounted } from 'vue';
import NodeService from './service/NodeService';

export default {
    setup() {
        onMounted(() => {
            loading.value = true;

            setTimeout(() => {
                nodes.value = initateNodes();
                loading.value = false;
            }, 2000);
        })

        const loading = ref(false);
        const nodes = ref(null);
        const nodeService = ref(new NodeService());
        const onNodeExpand = (node) => {
            if (!node.children) {
                loading.value = true;

                setTimeout(() => {
                    let _node = {...node};
                    _node.children = [];

                    for (let i = 0; i < 3; i++) {
                        _node.children.push({
                            key: node.key + '-' + i,
                            label: 'Lazy ' + node.label + '-' + i
                        });
                    }

                    let _nodes = {...nodes.value}
                    _nodes[parseInt(node.key, 10)] = _node;

                    nodes.value = _nodes;
                    loading.value = false;
                }, 500);
            }
        };

        const initateNodes = () => {
            return [{
                key: '0',
                label: 'Node 0',
                leaf: false
            },
            {
                key: '1',
                label: 'Node 1',
                leaf: false
            },
            {
                key: '2',
                label: 'Node 2',
                leaf: false
            }];
        }

        return { loading, nodes, nodeService, onNodeExpand, initateNodes }
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
        this.loading = true;

        setTimeout(() => {
            this.nodes = this.initateNodes();
            this.loading = false;
        }, 2000);
    },
    methods: {
        onNodeExpand(node) {
            if (!node.children) {
                this.loading = true;

                setTimeout(() => {
                    let _node = {...node};
                    _node.children = [];

                    for (let i = 0; i < 3; i++) {
                        _node.children.push({
                            key: node.key + '-' + i,
                            label: 'Lazy ' + node.label + '-' + i
                        });
                    }

                    let _nodes = {...this.nodes}
                    _nodes[parseInt(node.key, 10)] = _node;

                    this.nodes = _nodes;
                    this.loading = false;
                }, 500);
            }
        },
        initateNodes() {
            return [{
                key: '0',
                label: 'Node 0',
                leaf: false
            },
            {
                key: '1',
                label: 'Node 1',
                leaf: false
            },
            {
                key: '2',
                label: 'Node 2',
                leaf: false
            }];
        }
    }
}
</script>

<style scoped>
button {
    margin-right: .5rem;
}
</style>