<template>
    <v-card class="mx-auto mt-10" width="400">
        <v-card-title>
            <v-img :src="logo" alt="GameCorner Logo" />
            <h2 class="ml-3">Login</h2>
        </v-card-title>
        <v-card-text>
            <v-text-field label="Email" required type="email" outlined v-model="email" />
            <v-text-field label="Password" required type="password" outlined v-model="password" />
            <v-checkbox label="Remember me" hide-details v-model="rememberMe" />
        </v-card-text>
        <v-card-actions>
            <v-spacer />
            <v-btn color="primary" type="submit" @click="login">LOGIN</v-btn>
            <v-btn text href="/forgot-password">Forgot your password?</v-btn>
        </v-card-actions>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            logo: '@/assets/logo.png',
            email: '',
            password: '',
            rememberMe: false,
            error: '',
        };
    },
    methods: {
        login() {
            // Mock login logic - replace with your actual login call
            if (this.email === 'user@example.com' && this.password === 'password') {
                // Login successful
                console.log('Login successful!');
                // Simulate redirection to a different route (replace with your logic)
                this.$router.push('/dashboard');
            } else {
                // Login failed - show error message
                this.error = 'Invalid email or password';
            }
        },
    },
};
</script>

<style scoped>
/* Login card styling */
</style>