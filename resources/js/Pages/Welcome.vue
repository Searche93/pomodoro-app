<script setup>
import { Head, Link } from '@inertiajs/inertia-vue3';

defineProps({
    canLogin: Boolean,
    canRegister: Boolean,
    laravelVersion: String,
    phpVersion: String,
});
</script>

<script>
let lightMode;

if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    lightMode = false;
    document.documentElement.classList.add('dark');
} else {
    lightMode = true;
    document.documentElement.classList.remove('dark')
}

// Whenever the user explicitly chooses to respect the OS preference
localStorage.removeItem('theme')

// When the user uses the toggle switch
const html = document.querySelector('html');
const toggleDarkMode = () => {
    const checkbox = document.getElementById('toggle');

    checkbox.checked
        ? html.classList.add('dark')
        : html.classList.remove('dark');

    checkbox.checked
        ? localStorage.theme = 'dark' // Whenever the user explicitly chooses dark mode
        : localStorage.theme = 'light'; // Whenever the user explicitly chooses light mode
}
</script>

<template>
    <Head title="Pomodoro app" />

    <div class="justify-center flex min-h-screen bg-gray-100 text-gray-900 dark:bg-gray-900 dark:text-gray-100 sm:items-center sm:pt-0">
        <div class="relative items-top">
            <div class="fixed top-0 left-0 px-6 py-4">
                <div class="flex">
                    <span class="text-xs mt-0.5 mr-2 text-gray-400 dark:text-gray-100">
                        Light
                    </span>
                    <input type="checkbox" id="toggle" class="hidden" :checked="lightMode">
                    <div class="w-9 h-5 flex items-center bg-gray-300 rounded-full">
                        <label
                            for="toggle"
                            @click="toggleDarkMode()"
                            class="dark:translate-x-4 w-5 h-5 bg-white rounded-full shadow-md hover:cursor-pointer duration-300 ease-in-out">
                        </label>
                    </div>
                    <span class="text-xs mt-0.5 ml-2 text-gray-900 dark:text-gray-600">
                        Dark
                    </span>
                </div>
            </div>

            <div class="fixed top-0 right-0 px-6 py-4">
                <div v-if="canLogin">
                    <Link v-if="$page.props.user" :href="route('dashboard')" class="text-sm text-gray-700 underline">
                        Dashboard
                    </Link>

                    <template v-else>
                        <Link :href="route('login')" class="text-sm text-gray-700 underline dark:text-white">
                            Log in
                        </Link>

                        <Link v-if="canRegister" :href="route('register')" class="ml-4 text-sm text-gray-700 underline dark:text-white">
                            Register
                        </Link>
                    </template>
                </div>
            </div>
        </div>

        <div class="relative max-w-6xl mx-auto sm:px-6 lg:px-8">
            [TIMER]
        </div>
    </div>
</template>

<style scoped>

</style>
