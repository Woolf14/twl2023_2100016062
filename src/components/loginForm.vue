<template>
    <div>
        <h2 class="text-2xl font-semibold text-center mb-6">Sign In</h2>
        <form @submit.prevent="loginUser">
            <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="username">Username</label>
                <input v-model="username"
                    class="appearance-none border rounded w-full py-3 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    id="username" type="text" placeholder="Enter your username" />
            </div>
            <div class="mb-6">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="password">Password</label>
                <Password placeholder="Enter your password" v-model="password" class="rounded text-gray-700 text-sm font-bold mb-2" 
                    :feedback="false" toggleMask ></Password>
<!-- 
                <input v-model="password"
                    class="appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                    id="password" type="password" placeholder="Enter your password" /> -->
            </div>
            <div class="pb-3">
                <button
                    class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
                    type="submit">
                    Log In
                </button>
            </div>
            <span class="text-gray-600 text-sm">Don't have an account?</span>
            <a class="text-blue-500 hover:underline cursor-pointer" @click="switchToRegistration">
                Sign up</a>
        </form>
    </div>
</template>


<script>
import axios from 'axios';
import jwtDecode from 'jwt-decode';
import { useToast } from "primevue/usetoast";
import Password from 'primevue/password';

export default {
    components: {
        Password
    },
    name: 'LoginForm',
    data() {
        return {
            username: '',
            password: '',
        };
    },

    setup() {
        const toast = useToast();
        const success = () => {
            toast.add({ severity: 'success', summary: 'Success Message', detail: 'Login Sucessfull', life: 5000 });
        };
        const failed = (Message) => {
            toast.add({ severity: 'error', summary: 'Login Failed', detail: Message, life: 5000 });
        };

        return {
            success,
            failed
        };
    },

    methods: {
        async loginUser() {
            try {
                const response = await axios.post('http://localhost:3008/login', {
                    username: this.username,
                    password: this.password,
                });

                // Save the token to localStorage
                const token = response.data.token;
                localStorage.setItem('token', token);

                // Extract the expiration date from the token
                const decodedToken = jwtDecode(token);
                const expirationDate = new Date(decodedToken.exp * 1000); // Convert seconds to milliseconds

                // Save the expiration date to localStorage
                localStorage.setItem('expirationDate', expirationDate.toISOString());

                // Reset the form fields
                this.username = '';
                this.password = '';

                // Refresh the page
                window.location.reload();


            } catch (error) {
                // Handle the error
                const errorMessage = error.response.data.message;
                this.failed(errorMessage);
            }
        },

        switchToRegistration() {
            this.$emit('switch-mode', 'registration');
        },

    },
};

</script>

<style >
/* write code to change backround with image in local */
</style>
