<script setup>
const logo = `${APP_NAME}/images/avatar4.png`
</script>
<template>
    <img :src="logo" alt="logo" class="imagen-agrandada">
</template>
<style>
.imagen-agrandada {
  width: 200px; /* Ancho deseado */
  height: auto; /* Altura ajustada automáticamente para mantener la proporción */
}

</style>
