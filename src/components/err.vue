<template>
  <div id="error">
    <i class="iconfont icon-icon_warn_fill"></i>
    <p>获取数据失败</p>
    <p>请检查网络是否已连接</p>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
    #error{
        height: 105px;
        width:220px;
        background-color: #eee;
        border-radius: 20px;
        padding-top: 10px;
    }

    #error i{
        text-align: center;
        font-size: 45px;
        color: red;
    }

    #error p{
        font-size: 14px;
    }

</style>