<template>
    <div id="app" class="flex flex-col items-center mt-32 py-20 text-primary">
        <div class="flex flex-col">
            <div>
                <p class="tooltip inline-block">
                    <span id="day" class="inline-block text-10xl font-semibold mt-2">{{ dayOfWeek }} </span>
                    <span class="tooltip-text text-xl bg-accent p-3 -mt-6 rounded">{{ advice }}</span>
                </p>
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
<!--            <div id="article-box" class="mt-10">-->
<!--                <div class="flex flex-wrap">-->
<!--                    <span v-for="(article, index) in articles" :key="index" id="articles" class="flex-grow text-center font-light rounded py-1 px-2 mb-4 mr-4 bg-accent hover:bg-opacity-75 transition duration-200 ease-in-out">-->
<!--                        <a :href="article.url" target="_blank">{{ article.title }}</a>-->
<!--                    </span>-->
<!--                </div>-->
<!--            </div>-->
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
                advice: "",
                timer: '',
                covidData: {},
                // articles: []
            }
        },
        created () {
            this.fetchServers();
            this.fetchAdviceData();
            // this.fetchNewsData();
            this.covidData = this.fetchCovidData();
            this.timer = setInterval(this.fetchServers, 300000);
        },
        methods: {
            fetchServers () {
                if (locales.servers === "") {
                    return;
                }

                axios.get(locales.servers).then(response => {
                    this.servers = response.data
                }).catch( error => { console.log(error); });
            },
            fetchCovidData() {
                if (locales.covidApiLink === "") {
                    return;
                }

                axios.get(locales.covidApiLink).then(response => {
                  console.log(response.data)
                    return response.data
                }).catch( error => { console.log(error); });
            },
            // fetchNewsData() {
            //     if (locales.newsApiLink === "") {
            //         return;
            //     }
            //
            //     axios.get(locales.newsApiLink).then(response => {
            //         console.log(response.data.articles)
            //         this.articles = response.data.articles.slice(0, 4);
            //     }).catch( error => { console.log(error); });
            // },
            fetchAdviceData() {
                if (locales.adviceApiLink === "") {
                    return;
                }

                axios.get(locales.adviceApiLink).then(response => {
                    let advice = "Life tip " + response.data.slip.id + ": " + response.data.slip.advice
                    this.advice = advice.slice(0, -1);
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

<style scoped>
    #article-box {
        max-width: 84.5rem;
    }

    .tooltip .tooltip-text {
        visibility: hidden;
        text-align: center;
        margin-left: -43rem;
        padding: 8px 20px;
        position: absolute;
        z-index: 100;
    }
    .tooltip:hover .tooltip-text {
        visibility: visible;
    }
</style>
