<template>
    <div id="serverStatus" class="inline-block mr-5">
        <p class="tooltip inline-block">
            <img v-if="!data.down" src="../assets/check-circle.svg" class="inline-block mb-1">
            <img v-else src="../assets/x-circle.svg" class="inline-block mb-1">
            <span v-if="!data.down" class="tooltip-text bg-accent p-3 -mt-10 -ml-6 rounded">Apdex: {{ data.apdex_t }}</span>
            <span v-else class="tooltip-text bg-accent p-3 -mt-10 -ml-6 rounded">Down since: {{ data.down_since }}</span>
        </p>
        <a :href="data.url" class="text-xl ml-3">{{ data.alias }}</a>
    </div>
</template>

<script>
    export default {
        name: 'ServerStatus',
        props: {
            data: {
                type: Object,
                required: true
            }
        }
    }
</script>

<style scoped>
    .tooltip .tooltip-text {
        visibility: hidden;
        text-align: center;
        padding: 2px 6px;
        position: absolute;
        z-index: 100;
    }
    .tooltip:hover .tooltip-text {
        visibility: visible;
    }
</style>
