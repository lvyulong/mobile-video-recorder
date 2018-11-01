<template>
    <div>
        <router-view/>
    </div>
</template>

<script>
    import authApi from 'api/authApi';
    import axios from 'axios';
    export default {
        name: "app",
        data() {
            return {
                tip: '主应用部分'
            }
        },
        created: function () {

        }
    };
</script>
<style lang="less" scoped>
</style>
