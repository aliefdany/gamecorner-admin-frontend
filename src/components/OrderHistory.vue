<template>
    <v-container>
        <v-card>
            <v-card-title>
                <v-row>
                    <v-col cols="6">
                        <v-text-field v-model="date" label="Date" prepend-icon="mdi-calendar" readonly
                            @click:append="showDatePicker = true"></v-text-field>
                        <v-menu v-model="showDatePicker" :close-on-content-click="false" :nudge-right="40"
                            transition="scale-transition" offset-y min-width="290px">
                            <v-date-picker v-model="date" @input="showDatePicker = false"></v-date-picker>
                        </v-menu>
                    </v-col>
                </v-row>
            </v-card-title>
            <v-data-table :headers="headers" :items="orders" class="elevation-1">
                <template v-slot:top>
                    <v-toolbar flat>
                        <v-toolbar-title>Order History</v-toolbar-title>
                    </v-toolbar>
                </template>
            </v-data-table>
        </v-card>
    </v-container>
</template>

<script>
export default {
    data() {
        return {
            date: '2024-05-01',
            showDatePicker: false,
            headers: [
                { text: 'Nama Peminjam', value: 'name' },
                { text: 'Jumlah Controller', value: 'controllers' },
                { text: 'Nomor Konsol', value: 'consoleNumber' },
                { text: 'Nama Konsol', value: 'consoleName' },
                { text: 'Tanggal', value: 'date' },
                { text: 'Jam Mulai', value: 'startTime' },
                { text: 'Jam Berakhir', value: 'endTime' },
            ],
            orders: [
                { name: 'Jennie Kim Putri', controllers: 2, consoleNumber: 5, consoleName: 'Playstation 5', date: '2024-05-01', startTime: '11:30', endTime: '12:30' },
                { name: 'Byeon Satria Wooseok', controllers: 1, consoleNumber: 3, consoleName: 'Xbox One', date: '2024-05-01', startTime: '11:30', endTime: '12:30' },
                { name: 'Sun Jae Permana', controllers: 1, consoleNumber: 2, consoleName: 'Playstation 5', date: '2024-05-01', startTime: '11:30', endTime: '12:30' },
                { name: 'Woo Do Hwan Santoso', controllers: 2, consoleNumber: 1, consoleName: 'Playstation 5', date: '2024-05-01', startTime: '12:30', endTime: '13:30' },
                { name: 'Choi Hyun Wook Saputra', controllers: 2, consoleNumber: 2, consoleName: 'Playstation 5', date: '2024-05-01', startTime: '14:30', endTime: '15:30' },
                { name: 'Nobita Pratama', controllers: 2, consoleNumber: 1, consoleName: 'Playstation 5', date: '2024-05-01', startTime: '14:30', endTime: '15:30' },
                { name: 'Naruto Wijayanto', controllers: 2, consoleNumber: 3, consoleName: 'Xbox One', date: '2024-05-01', startTime: '14:30', endTime: '15:30' },
                { name: 'Sakura Ayu', controllers: 2, consoleNumber: 4, consoleName: 'Xbox One', date: '2024-05-01', startTime: '15:30', endTime: '16:30' },
                { name: 'Sasuke Hadi', controllers: 1, consoleNumber: 2, consoleName: 'Playstation 5', date: '2024-05-01', startTime: '15:30', endTime: '16:30' },
            ],
        };
    },
};
</script>

<style scoped>
.v-card-title {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>