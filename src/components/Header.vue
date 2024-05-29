<style scoped>
.global-pad {
    padding-left: 6em;
    padding-right: 6em;
}
</style>

<template>
    <v-app-bar :elevation="2">
        <v-app-bar-title>FILKOM GameCorner</v-app-bar-title>

        <!-- <template v-slot:append>

            <v-btn icon="mdi-dots-vertical"></v-btn>
        </template> -->

        <v-menu>
            <template v-slot:activator="{ props }">
                <v-btn v-bind="props">
                    <v-icon>mdi-menu</v-icon>
                </v-btn>
            </template>
            <v-list>
                <v-list-item v-for="item in menuItems" :key="item.title" @click="subItemClick">
                    <v-list-item-title>{{ item.title }}</v-list-item-title>
                </v-list-item>
            </v-list>
        </v-menu>



        <template v-slot:extension>
            <v-tabs v-model="tab" align-tabs="title">
                <v-tab :to="item" v-for="item in items" :key="item" :text="item" :value="item"></v-tab>
            </v-tabs>
        </template>
    </v-app-bar>
</template>

<script>
import { ref } from 'vue';

export default {
    setup() {
        const menu = ref(false);
        const items = [
            { title: 'Profile' },
            { title: 'Logout' },
        ];

        const subItemClick = (item) => {
            // Perform action based on the clicked item
            console.log(item.title);
        };

        return { menu, items, subItemClick };
    },
    data() {
        return {
            tab: null,
            menuItems: [{ title: 'Profile' },
            { title: 'Logout' },],
            items: [
                'dashboard', 'peminjaman', 'riwayat'
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