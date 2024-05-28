<style scoped>
.global-pad {
    padding-left: 6em;
    padding-right: 6em;
}
</style>

<template>
    <v-app-bar :elevation="2">
        <template v-slot:prepend>
            <v-app-bar-nav-icon></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>FILKOM GameCorner</v-app-bar-title>

        <template v-slot:append>
            <v-btn icon="mdi-heart"></v-btn>

            <v-btn icon="mdi-magnify"></v-btn>

            <v-btn icon="mdi-dots-vertical"></v-btn>
        </template>

        <template v-slot:extension>
            <v-tabs v-model="tab" align-tabs="title">
                <v-tab :to="item" v-for="item in items" :key="item" :text="item" :value="item"></v-tab>
            </v-tabs>
        </template>
    </v-app-bar>
</template>

<script>
export default {
    data() {
        return {
            tab: null,
            items: [
                'dashboard', 'peminjaman',
            ],
            text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
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