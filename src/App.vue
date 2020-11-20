<template>
    <div id="app" class="flex flex-col items-center mt-20 py-20 text-primary">
        <div class="flex flex-col">
            <div>
                <h1 id="day" class="inline-block text-10xl font-semibold mt-2">{{ dayOfWeek }}</h1>
                <div class="inline-block mb-5 mt-32 float-right">
                    <ServerStatus v-for="server in servers" :key="server.id" :data="server"/>
                </div>
            </div>
            <div class="flex">
                <div class="grid gap-10 grid-cols-2">
                    <IconCard icon="hard-drive" :link="iconCards.topLeft"/>
                    <IconCard icon="mail" :link="iconCards.topRight"/>
                    <IconCard icon="github" :link="iconCards.bottomLeft"/>
                    <IconCard icon="bookmark" :link="iconCards.bottomRight"/>
                </div>
                <div class="grid gap-10 grid-cols-2 ml-32">
                    <ItemCard v-for="card in cards" :key="card.id" :card="card"/>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from "axios";
    import locales from "@/locales/locales";
    import ItemCard from "@/components/ItemCard";
    import IconCard from "@/components/IconCard";
    import ServerStatus from "@/components/ServerStatus";

    export default {
        name: 'App',
        components: {
            ItemCard,
            IconCard,
            ServerStatus
        },
        data () {
            return {
                iconCards: locales.iconCards,
                cards: locales.cards,
                servers: [],
                timer: ''
            }
        },
        created () {
            this.fetchServers();
            this.timer = setInterval(this.fetchServers, 300000)
        },
        methods: {
            fetchServers () {
                if (locales.servers === "") {
                    return;
                }

                axios.get(locales.servers).then(response => {
                    this.servers = response.data
                }).catch( error => { console.log(error); });
            }
        },
        computed: {
            dayOfWeek() {
                const d = new Date();
                const weekday = new Array(7);
                weekday[0] = "Sunday";
                weekday[1] = "Monday";
                weekday[2] = "Tuesday";
                weekday[3] = "Wednesday";
                weekday[4] = "Thursday";
                weekday[5] = "Friday";
                weekday[6] = "Saturday";

                return weekday[d.getDay()];
            },
        },
        beforeDestroy () {
            clearInterval(this.timer)
        }
    }
</script>

<style>

</style>
