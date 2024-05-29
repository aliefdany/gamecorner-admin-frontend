<template>
    <v-card class="mx-auto mt-10" width="400">
        <v-card-title>
            <v-img :src="logo" alt="GameCorner Logo" />
            <h2 class="ml-3">Register</h2>
        </v-card-title>
        <v-card-text>
            <v-text-field label="Name" required outlined v-model="name" />
            <v-text-field label="Email" required type="email" outlined v-model="email" />
            <v-text-field label="Password" required type="password" outlined v-model="password" />
            <v-text-field label="Confirm Password" required type="password" outlined v-model="confirmPassword" />
            <v-checkbox label="Remember me" hide-details v-model="rememberMe" />
        </v-card-text>
        <v-card-actions>
            <v-spacer />
            <v-btn color="primary" type="submit" @click="register">REGISTER</v-btn>
            <v-btn text href="/login">Already have an account?</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            logo: 'path/to/your/logo.png',
            name: '',
            email: '',
            password: '',
            confirmPassword: '',
            rememberMe: false,
            error: '',
        };
    },
    methods: {
        register() {
            // Mock register logic - replace with your actual registration call
            if (this.password !== this.confirmPassword) {
                this.error = 'Passwords do not match';
                return;
            }
            console.log('Registration successful!');
            // Simulate redirection to a different route (replace with your logic)
            this.$router.push('/login');
        },
    },
};
</script>

<style scoped>
/* Register card styling */
</style>