<template>
    <span class="text-xs mt-0.5 mr-2 text-gray-400 dark:text-gray-100">Light</span>

    <input type="checkbox" id="toggle" class="hidden" :checked="lightMode">
    <div class="w-9 h-5 flex items-center bg-gray-300 rounded-full">
        <label
            for="toggle"
            @click="toggleDarkMode()"
            class="dark:translate-x-4 w-5 h-5 bg-white rounded-full shadow-md hover:cursor-pointer duration-300 ease-in-out">
        </label>
    </div>

    <span class="text-xs mt-0.5 ml-2 text-gray-900 dark:text-gray-600">Dark</span>
</template>

<script>
export default {
    name: "DarkModeComponent",
    data() {
        return {
            lightMode: localStorage.theme,
            html: document.querySelector('html'),
        }
    },
    methods: {
        initDarkMode() {
            if (localStorage.theme === 'dark' || (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
                this.lightMode = false;
                document.documentElement.classList.add('dark');
            } else {
                this.lightMode = true;
                document.documentElement.classList.remove('dark')
            }
            // Whenever the user explicitly chooses to respect the OS preference
            localStorage.removeItem('theme')
        },
        toggleDarkMode() {
            const checkbox = document.getElementById('toggle');
            checkbox.checked
                ? this.html.classList.add('dark')
                : this.html.classList.remove('dark');

            checkbox.checked
                ? localStorage.theme = 'dark' // Whenever the user explicitly chooses dark mode
                : localStorage.theme = 'light'; // Whenever the user explicitly chooses light mode
        },
    },
    mounted() {
        this.initDarkMode()
    },
}
</script>

<style scoped>

</style>
