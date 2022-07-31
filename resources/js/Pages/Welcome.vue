<script setup>
import { Head, Link } from '@inertiajs/inertia-vue3';
import DarkModeComponent from "../components/DarkModeComponent.vue";
import TimerComponent from "../components/TimerComponent.vue";

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: String,
    phpVersion: String,
});
</script>

<template>
    <Head title="Pomodoro app" />

    <div class="justify-center flex min-h-screen bg-gray-100 text-gray-900 dark:bg-gray-900 dark:text-gray-100 sm:items-center sm:pt-0">
        <div class="relative items-top">
            <div class="fixed top-0 left-0 px-6 py-4">
                <div class="flex">
                    <DarkModeComponent/>
                </div>
            </div>

            <div class="fixed top-0 right-0 px-6 py-4">
                <div v-if="canLogin">
                    <Link v-if="$page.props.user" :href="route('dashboard')" class="text-sm text-gray-700 dark:text-white">
                        Dashboard
                    </Link>

                    <template v-else>
                        <Link :href="route('login')" class="text-sm text-gray-700 dark:text-white">
                            Log in
                        </Link>

                        <Link v-if="canRegister" :href="route('register')" class="ml-4 text-sm text-gray-700 dark:text-white">
                            Register
                        </Link>
                    </template>
                </div>
            </div>
        </div>

        <div class="relative max-w-6xl mx-auto sm:px-6 lg:px-8">
            <TimerComponent/>
        </div>
    </div>
</template>

<style scoped>

</style>
