<template>
    <nav>
        <NuxtLink to="/" style="text-decoration: none;">Home</NuxtLink>
        <hr>
    </nav>
    <slot />
</template>

<style scoped>
nav{
    text-align: center;
    font-size: 30px;
}
</style>