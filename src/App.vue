<template>
    <div id="app">
        <div class="container mx-auto mt-10 px-5 md:px-0">
            <h1 class="font-light text-4xl">Resolution Finder</h1>

            <p class="mt-5">
                This tool was built to identify the best resolutions for my games, based on key factors.
            </p>

            <main class="mt-5">
            <resolution-builder/>
            </main>
        </div>
    </div>
</template>

<script>
    import ResolutionBuilder from './components/ResolutionBuilder';

    export default {
        name: 'App',
        components: {
            ResolutionBuilder
        }
    }
</script>

<style>
    @import "assets/css/app.css";

    body {
        @apply text-gray-900 mb-10;
    }

    .button {
        @apply py-2 mr-3 bg-gray-200 text-gray-700 px-5 text-sm font-medium rounded ;
    }

    .button:hover {
        @apply bg-gray-300;
    }

    .button.primary {
        @apply bg-blue-600 text-blue-100;
    }

    .button.primary:hover {
        @apply bg-blue-700;
    }

    .label {
        @apply inline-block font-semibold uppercase text-gray-700 text-sm mb-1;
    }

    .form-group {
        @apply mt-5;

        .label {
            @apply block;
        }
    }

    .input {
        @apply bg-gray-200 px-4 w-full block rounded py-2 text-gray-700;
    }

    .custom-table {
        @apply w-full;
    }

    th {
        @apply py-2;
    }

    td {
        @apply text-center py-2;
    }

    tr.even {
        @apply bg-gray-100;
    }

    tr.highlight {
        @apply bg-green-300 font-bold;
    }
</style>
