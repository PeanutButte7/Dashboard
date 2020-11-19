<template>
    <div id="serverStatus" class="inline-block mr-5">
        <img v-if="!data.down" src="../assets/check-circle.svg" class="inline-block mb-1">
        <img v-else src="../assets/x-circle.svg" class="inline-block">
        <a :href="data.url" target="_blank" class="text-xl ml-3">{{ data.alias }}</a>
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
