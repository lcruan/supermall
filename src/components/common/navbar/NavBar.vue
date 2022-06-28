<template>
    <div class="nav-bar">
        <div class="left"><slot name="left"></slot></div>
        <div class="center"><slot name="center"></slot></div>
        <div class="right"><slot name="right"></slot></div>
    </div>
</template>

<script>
export default {
    name: 'NavBar'
}
</script>

<style>
 .nav-bar {
    display: flex;
    height: 44px;
    line-height: 44px;
    text-align: center;
    box-shadow: 0 1px 1px rgba(100, 100, 100, .1);
 }
 .left, .right {
    width: 60px;
 }
 .center {
    /* 其他有确定宽度，只剩下一个，它会占据整个部分 */
    flex: 1;
 }
</style>