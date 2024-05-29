<template>
    <v-container>
        <v-form>
            <v-row>
                <v-col cols="12">
                    <v-menu ref="menu" v-model="menu" :close-on-content-click="false" :nudge-right="40"
                        transition="scale-transition" offset-y min-width="290px">
                        <template v-slot:activator="{ on, attrs }">
                            <v-text-field v-model="date" label="Tanggal Peminjaman" prepend-icon="mdi-calendar" readonly
                                v-bind="attrs" v-on="on"></v-text-field>
                        </template>
                        <v-date-picker v-model="date" @input="menu = false" no-title scrollable>
                            <v-spacer></v-spacer>
                            <v-btn text color="primary" @click="menu = false">Cancel</v-btn>
                            <v-btn text color="primary" @click="$refs.menu.save(date)">OK</v-btn>
                        </v-date-picker>
                    </v-menu>
                </v-col>
            </v-row>
            <v-row v-for="console in consoles" :key="console.id">
                <v-col cols="12">
                    <p>{{ console.name }}</p>
                    <v-checkbox-group class="checkbox-group" v-model="console.timeslots" column>
                        <v-checkbox v-for="timeslot in timeslots" :key="timeslot" :label="timeslot"
                            :value="timeslot"></v-checkbox>
                    </v-checkbox-group>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12">
                    <v-checkbox v-model="allSchedules" label="MAKE ALL SCHEDULE AVAILABLE"
                        @change="makeAllSchedulesAvailable"></v-checkbox>
                </v-col>
            </v-row>
            <v-row>
                <v-col cols="12">
                    <v-btn color="primary" @click="submitForm">Tambahkan</v-btn>
                </v-col>
            </v-row>
        </v-form>
    </v-container>
</template>

<script>
export default {
    data() {
        return {
            date: null,
            menu: false,
            consoles: [
                { id: 1, name: 'Konsol 1', timeslots: [] },
                { id: 2, name: 'Konsol 2', timeslots: [] },
                { id: 3, name: 'Konsol 3', timeslots: [] },
                { id: 4, name: 'Konsol 4', timeslots: [] },
                { id: 5, name: 'Konsol 5', timeslots: [] },
            ],
            timeslots: [
                '09.30 - 10.30',
                '10.30 - 11.30',
                '11.30 - 12.30',
                '12.30 - 13.30',
                '13.30 - 14.30',
                '14.30 - 15.30',
                '15.30 - 16.30',
                '16.30 - 17.30',
            ],
            allSchedules: false,
        };
    },
    methods: {
        makeAllSchedulesAvailable() {
            this.consoles.forEach((console) => {
                if (this.allSchedules) {
                    console.timeslots = [...this.timeslots];
                } else {
                    console.timeslots = [];
                }
            });
        },
        submitForm() {
            // Handle form submission
            console.log('Date:', this.date);
            console.log('Consoles:', this.consoles);
        },
    },
};
</script>

<style scoped>
/* Add any custom styles here */
.checkbox-group {
    display: flex;
    gap: 0.5em
}
</style>