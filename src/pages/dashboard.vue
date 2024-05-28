<style scoped>
.analytics-container {
    display: flex
}
</style>

<template>
    <Header />


    <div class="analytics-container">
        <v-card v-for="analytic in analytics" :title="analytic.title" :subtitle="analytic.sub"
            :text="analytic.text"></v-card>
    </div>
    <!-- <v-tab :to="item" v-for="item in items" :key="item" :text="item" :value="item"></v-tab> -->
</template>


<script>
export default {
    data() {
        return {
            analytics: [
                {
                    title: "27 Pengunjung",
                    sub: "+30%",
                    text: "Greyhound divisively hello coldly wonderfully marginally far upon excluding. "
                },
                {
                    title: "150 Jam dimainkan",
                    sub: "-2%",
                    text: "Greyhound divisively hello coldly wonderfully marginally far upon excluding. "
                },
                {
                    title: "Rating harian 4.2",
                    sub: "+5%",
                    text: "Greyhound divisively hello coldly wonderfully marginally far upon excluding. "
                }
            ]
        }
    },
}
</script>
