<style scoped>
.analytics-container {
    display: flex;
    gap: 1em
}
</style>

<template>
    <Header />
    <v-spacer></v-spacer>
    <!-- Analytics Start -->
    <div class="analytics-container">
        <v-card v-for="analytic in analytics" :title="analytic.title" :subtitle="analytic.sub"
            :text="analytic.text"></v-card>
    </div>
    <!-- Analytics End -->

    <v-spacer></v-spacer>
    <!-- Data table start -->

    <v-data-table :headers="headers" :items="desserts" :sort-by="[{ key: 'status', order: 'asc' }]">
        <template v-slot:top>
            <v-toolbar flat>
                <v-toolbar-title>Daftar jadwal</v-toolbar-title>
                <v-divider class="mx-4" inset vertical></v-divider>
                <v-spacer></v-spacer>
                <v-dialog v-model="dialog" max-width="500px">
                    <template v-slot:activator="{ props }">
                        <v-btn class="mb-2" color="primary" dark v-bind="props">
                            Tambah jadwal baru
                        </v-btn>
                    </template>
                    <v-card>
                        <v-card-title>
                            <span class="text-h5">{{ formTitle }}</span>
                        </v-card-title>

                        <v-card-text>
                            <v-container>
                                <v-row>
                                    <v-col cols="12" md="4" sm="6">
                                        <v-text-field v-model="editedItem.status" label="Status"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="4" sm="6">
                                        <v-text-field v-model="editedItem.console_name"
                                            label="Nama konsol"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="4" sm="6">
                                        <v-text-field v-model="editedItem.console_number"
                                            label="Nomor konsol"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="4" sm="6">
                                        <v-text-field v-model="editedItem.start" label="Jam mulai"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="4" sm="6">
                                        <v-text-field v-model="editedItem.end" label="Jam berakhir"></v-text-field>
                                    </v-col>
                                    <v-col cols="12" md="4" sm="6">
                                        <v-text-field v-model="editedItem.customer_name" label="Pemesan"></v-text-field>
                                    </v-col>
                                </v-row>
                            </v-container>
                        </v-card-text>

                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue-darken-1" variant="text" @click="close">
                                Cancel
                            </v-btn>
                            <v-btn color="blue-darken-1" variant="text" @click="save">
                                Save
                            </v-btn>
                        </v-card-actions>
                    </v-card>
                </v-dialog>
                <v-dialog v-model="dialogDelete" max-width="500px">
                    <v-card>
                        <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>
                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn color="blue-darken-1" variant="text" @click="closeDelete">Cancel</v-btn>
                            <v-btn color="blue-darken-1" variant="text" @click="deleteItemConfirm">OK</v-btn>
                            <v-spacer></v-spacer>
                        </v-card-actions>
                    </v-card>
                </v-dialog>
            </v-toolbar>
        </template>
        <template v-slot:item.actions="{ item }">
            <!-- <v-icon class="me-2" size="small" @click="editItem(item)">
                mdi-pencil
            </v-icon>
            <v-icon size="small" @click="deleteItem(item)">
                mdi-delete
            </v-icon> -->
            <v-btn color="primary" variant="elevated" size="small" @click="editItem(item)">Aktifkan</v-btn>
            <v-btn color="error" size="small" @click="deleteItem(item)">Non-aktifkan</v-btn>
        </template>
        <template v-slot:no-data>
            <v-btn color="primary" @click="initialize">
                Reset
            </v-btn>
        </template>
    </v-data-table>
    <!-- Data table end -->
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
            ], dialog: false,
            dialogDelete: false,
            headers: [
                {
                    title: 'Status',
                    align: 'start',
                    sortable: false,
                    key: 'status',
                },
                { title: 'Nama konsol', key: 'console_name' },
                { title: 'Nomor konsol', key: 'console_number' },
                { title: 'Jam mulai', key: 'start' },
                { title: 'Jam berakhir', key: 'end' },
                { title: 'Pemesan', key: 'customer_name' },
                { title: 'Aksi', key: 'actions', sortable: false },
            ],
            desserts: [],
            editedIndex: -1,
            editedItem: {
                name: '',
                calories: 0,
                fat: 0,
                carbs: 0,
                protein: 0,
            },
            defaultItem: {
                name: '',
                calories: 0,
                fat: 0,
                carbs: 0,
                protein: 0,
            },
        }
    },
    computed: {
        formTitle() {
            return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
        },
    },

    watch: {
        dialog(val) {
            val || this.close()
        },
        dialogDelete(val) {
            val || this.closeDelete()
        },
    },

    created() {
        this.initialize()
    },

    methods: {
        initialize() {
            this.desserts = [
                {
                    status: 'Tersedia',
                    console_name: "Playstation 5",
                    console_number: 1,
                    start: "11:30",
                    end: "12:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Dipesan',
                    console_name: "Xbox One",
                    console_number: 2,
                    start: "12:30",
                    end: "13:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Dipesan',
                    console_name: "Playstation 5",
                    console_number: 3,
                    start: "13:30",
                    end: "14:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Dipesan',
                    console_name: "Xbox One",
                    console_number: 4,
                    start: "14:30",
                    end: "15:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Tersedia',
                    console_name: "PC",
                    console_number: 1,
                    start: "15:30",
                    end: "16:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Non-aktif',
                    console_name: "Playstation 5",
                    console_number: 2,
                    start: "16:30",
                    end: "17:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Tersedia',
                    console_name: "PC",
                    console_number: 4,
                    start: "17:30",
                    end: "18:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Dipesan',
                    console_name: "Playstation 5",
                    console_number: 5,
                    start: "11:30",
                    end: "12:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Non-aktif',
                    console_name: "PC",
                    console_number: 3,
                    start: "11:30",
                    end: "12:30",
                    customer_name: "Alief"
                },
                {
                    status: 'Tersedia',
                    console_name: "Playstation 5",
                    console_number: 4,
                    start: "11:30",
                    end: "12:30",
                    customer_name: "Alief"
                },
            ]
        },

        editItem(item) {
            this.editedIndex = this.desserts.indexOf(item)
            this.editedItem = Object.assign({}, item)
            this.dialog = true
        },

        deleteItem(item) {
            this.editedIndex = this.desserts.indexOf(item)
            this.editedItem = Object.assign({}, item)
            this.dialogDelete = true
        },

        deleteItemConfirm() {
            this.desserts.splice(this.editedIndex, 1)
            this.closeDelete()
        },

        close() {
            this.dialog = false
            this.$nextTick(() => {
                this.editedItem = Object.assign({}, this.defaultItem)
                this.editedIndex = -1
            })
        },

        closeDelete() {
            this.dialogDelete = false
            this.$nextTick(() => {
                this.editedItem = Object.assign({}, this.defaultItem)
                this.editedIndex = -1
            })
        },

        save() {
            if (this.editedIndex > -1) {
                Object.assign(this.desserts[this.editedIndex], this.editedItem)
            } else {
                this.desserts.push(this.editedItem)
            }
            this.close()
        },
    },
}
</script>
