<template>
	<AppDoc name="ElevationDemo" :sources="sources">
		<h5>Getting Started</h5>
		<p>Elevation is added to an element using the <i>.p-shadow-{level}</i> class.</p>
<pre v-code><code>
&lt;div class="p-shadow-1" /&gt;

</code></pre>

        <h5>Levels</h5>
        <p>There are 24 depths available varying from 1 to 24.</p>
<pre v-code><code>
&lt;div class="p-shadow-1" /&gt;
&lt;div class="p-shadow-24" /&gt;

</code></pre>
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
        <div class="p-grid">
            <div class="p-col" v-for="index in 24" :key="index">
                <div :class="['box', 'p-shadow-' + index]">
                    p-shadow-{{index}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
}
<\\/script>

<style lang="scss" scoped>
.box {
    min-height: 100px;
    min-width: 150px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    margin: 2rem;
    border-radius: 4px;
}
</style>                    
`
                },
				'composition-api': {
                    tabName: 'Composition API',
                    content: `
<template>
    <div>
        <div class="p-grid">
            <div class="p-col" v-for="index in 24" :key="index">
                <div :class="['box', 'p-shadow-' + index]">
                    p-shadow-{{index}}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
}
<\\/script>

<style lang="scss" scoped>
.box {
    min-height: 100px;
    min-width: 150px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: 600;
    margin: 2rem;
    border-radius: 4px;
}
</style>                    
`
                }
			}
		}
	}
}
</script>