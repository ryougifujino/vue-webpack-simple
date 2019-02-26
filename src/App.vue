<template>
    <div>
        <img src="../asset/logo.png">
        <h1>{{title}}</h1>
        <a :href="vueOfficial">Vue Official Website</a>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                title: 'Hello Vue',
                vueOfficial: 'https://vuejs.org'
            };
        }
    }
</script>

<style>
    * {
        text-align: center;
        margin-top: 30px;
    }
</style>
