<script setup>
import { Head, Link } from '@inertiajs/inertia-vue3';
import DarkModeComponent from "../components/DarkModeComponent.vue";

// TODO: Opzoeken vue templating

</script>

<template>
    <div class="fixed top-0 left-0 px-6 py-4">
        <div class="flex">
            <DarkModeComponent/>
        </div>

        <div class="fixed top-0 right-0 px-6 py-4">
            <div>
                <Link href="/" class="text-sm text-gray-700 dark:text-white">
                    Home
                </Link>
                <Link v-if="this.currentPage !== route('register')" :href="route('register')" class="ml-4 text-sm text-gray-700 dark:text-white">
                    Register
                </Link>
                <Link v-else :href="route('login')" class="ml-4 text-sm text-gray-700 dark:text-white">
                    Login in
                </Link>
            </div>
        </div>
    </div>

    <div class="min-h-screen flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gray-100 text-gray-900 dark:bg-gray-900 dark:text-gray-100">
        <div class="w-full sm:max-w-md mt-6 px-6 py-4 bg-white shadow-md overflow-hidden sm:rounded-lg">
            <slot />
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            currentPage: window.location.href,
        }
    },
    methods: {

    }
}
</script>
