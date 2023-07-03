<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/vue3';
const fondo2 = `${APP_NAME}/images/fondo_guest.png`;
</script>

<template>
    <div class="min-h-screen flex flex-col sm:justify-center items-center pt-6 sm:pt-0 bg-gray-100" :style="`background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.1)), url(${fondo2}); background-size: cover`">
        
        <div
            class=""
        >
            <slot />
        </div>
    </div>
</template>
