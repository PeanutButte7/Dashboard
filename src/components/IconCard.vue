<template>
    <div id="iconCard" class="bg-accent py-12 px-20 shadow-xl rounded-lg hover:bg-opacity-75">
        <a :href="link" target="_blank">
            <img :src="require(`@/assets/${icon}.svg`)">
        </a>
    </div>
</template>

<script>
    export default {
        name: 'IconCard',
        props: {
            icon: {
                type: String,
                required: true
            },
            link: {
                type: String,
                required: true
            }
        }
    }
</script>
