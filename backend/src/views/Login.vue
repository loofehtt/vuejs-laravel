<template>
    <GuestLayout title="Sign in to your account">
        <form class="space-y-6" action="#" method="POST" @submit.prevent="login">
            <div>
                <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>
                <div class="mt-2">
                    <input id="email" name="email" type="email" autocomplete="email" v-model="user.email"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                </div>
            </div>

            <div>
                <div class="flex items-center justify-between">
                    <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
                </div>
                <div class="mt-2">
                    <input id="password" name="password" type="password" autocomplete="current-password" v-model="user.password"
                        class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6" />
                </div>
            </div>
            <div class="flex">
                <div class="flex flex-1">
                    <input name="remember" id="remember" type="checkbox" v-model="user.remember"
                        class="appearance-none checked:bg-blue-500 rounded-md mt-0.5" />
                    <p class="text-sm ml-1">Remember me</p>
                </div>
                <div class="text-sm">
                    <router-link :to="{ name: 'requestPassword' }"
                        class="font-medium text-indigo-600 hover:text-indigo-500">
                        Forgot your password?
                    </router-link>
                </div>
            </div>

            <div>
                <button type="submit"
                    class="flex w-full justify-center rounded-md bg-indigo-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">
                    Sign in
                </button>
            </div>
        </form>
        <p class="mt-10 text-center text-sm text-gray-500">
            Not a member?
            {{ " " }}
            <router-link :to="{ name: 'requestPassword' }"
                class="font-semibold leading-6 text-indigo-600 hover:text-indigo-500">
                Sign up
            </router-link>
        </p>
    </GuestLayout>
</template>

<script setup>
import GuestLayout from "../components/GuestLayout.vue";
import store from "../store";
import { useRouter } from "vue-router";

const router = useRouter();

const user = {
    email: '',
    password: '',
    remember: false,
}

function login(ev) {
    ev.preventDefault();
    store.dispatch('login', user)
        .then(() => {
            router.push({
                name: 'Dashboard'
            })
        })

}

</script>

<style scoped></style>
