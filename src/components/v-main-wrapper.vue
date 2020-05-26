<template>
    <div class="v-main-wrapper">
        <keep-alive>
            <router-view></router-view>
        </keep-alive>
    </div>
</template>

<script>
    // import {mapGetters} from 'vuex'

    export default {
        name: "v-main-wrapper",
        computed: {
            // ...mapGetters(['CART'])
        },
        methods: {},
        watch: {},
    }
</script>

<style lang="scss">
    .v-main-wrapper {
        width: 900px;
        margin: 0 auto;
    }
</style>
