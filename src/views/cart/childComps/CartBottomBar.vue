<template>
    <div class="bottom-bar">
       <div class="check-content">
             <check-button :is-checked="isSelectAll" @click.native="checkClick" class="check-button"/>
             <span>全选</span>
       </div>
       <div class="price">
        合计：{{totalPrice}}
       </div>
       <div class="calculate">
        去计算({{checkLength}})
       </div>
    </div>
</template>

<script>

import CheckButton from 'components/content/checkButton/CheckButton'

import { mapGetters } from 'vuex';
export default {
    name: 'CartBottom',
    components: {
        CheckButton
    },
    computed: {
        ...mapGetters(['cartList']),
        totalPrice() {
            return '￥' + this.cartList.filter(item => {
                return item.checked
            }).reduce((preValue, item) => {
                return preValue + item.price * item.count;
            }, 0).toFixed(2);
        },
        checkLength() {
            return this.cartList.filter(item => item.checked).length;
        },
        isSelectAll() {
            // 不选中 有长度
            //1. 使用filter
            // return !(this.cartList.filter(item => !item.checked).length)
            if(this.cartList.length === 0) return false;
            //2.使用find
            return !this.cartList.find(item => !item.checked)
        }
    },
    methods: {
        checkClick() {
            // 全部选中
            if(this.isSelectAll) {
                this.cartList.forEach(item => item.checked = false)
            }else {// 部分或全部不选中
                this.cartList.forEach(item => item.checked = true)
            }

            //这里不能做简化
            // this.cartList.forEach(item => item.checked = !this.isSelectAll)
        }
    }
}
</script>

<style scoped>
    .bottom-bar {
        height: 40px;
        background-color: #eee;
        position: relative;
        line-height: 40px;
        display: flex;
        font-size: 14px;
    }
    .check-content {
        display: flex;
        align-items: center;
        margin-left: 10px;
        width: 60px;
    }
    .check-button {
        width: 20px;
        height: 20px;
        line-height: 20px;
        margin-right: 5px;
    }
    .price {
        margin-left: 20px;
        flex: 1;
    }
    .calculate {
        width: 90px;
        background-color: red;
        color: #fff;
        text-align: center;
    }
</style>