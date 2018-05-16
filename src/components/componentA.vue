<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <button v-on:click="onClickMe">ClickMe and 将我的信息传给父亲</button>
    </div>
</template>

<script>
export default {

    components: {},
    // 父传子 注册组件
    props: [ 'msgfromfather' ],
    data () {
        return {
            msg: '我是component中的内容'
        };
    },

    methods: {
        onClickMe: function () {
            // alert(this.msgfromfather);
            this.$emit('child-tell-me-something', this.msg);
        }
    }
}

</script>
<style lang='' scoped>
    h1 {
        color: #000;
    }
</style>