<template>
    <div id="itemCard" class="bg-accent rounded-lg shadow-xl pt-5 pl-10 pr-32 hover:bg-opacity-75 transition duration-200 ease-in-out">
        <h2 class="text-4xl font-semibold mb-5">{{ card.name }}</h2>
        <a v-for="item in card.items" :key="item.id" :href="item.link" class="block text-2xl hover:underline font-light">{{ item.name }}</a>
    </div>
</template>

<script>
    export default {
        name: 'ItemCard',
        props: {
            card: {
                type: Object,
                required: true
            }
        }
    }
</script>

<style>
    #itemCard {
        padding-bottom: 6.5rem;
    }
</style>
