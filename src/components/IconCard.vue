<template>
    <div @click="redirect" id="iconCard" class="bg-accent py-12 px-20 shadow-xl rounded-lg hover:bg-opacity-75 cursor-pointer transition duration-200 ease-in-out">
        <a>
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
        },
        methods: {
            redirect() {
                window.location.href = this.link;
            }
        }
    }
</script>
