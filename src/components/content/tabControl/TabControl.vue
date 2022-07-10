<template>
    <div class="tab-control">
        <!-- 如果只是文字不一样，就没必要搞插槽了 -->
       <div v-for="(item,index) in titles" :key="item.index" 
       class="tab-control-item" :class="{active: index === currentIndex}"
       @click="itemClick(index)">
            <span>{{item}}</span>
       </div>
    </div>
</template>

<script>
export default {
    props: {
        titles: {
            type: Array,
            default() {
                return []
            }
        }
    },
    data() {
        return {
            currentIndex: 0
        }
    },
    methods: {
        itemClick(index) {
            this.currentIndex = index;
            this.$emit('tabClick', index);
        }
    },
    name: 'TabControl'
}
</script>

<style scoped>
    .tab-control {
        display: flex;
        text-align: center;
        font-size: 15px;
        height: 40px;
        line-height: 40px;
        background-color: #fff;
    }
    .tab-control span {
        padding: 5px;
    }
    .tab-control-item {
        flex: 1;
    }
    .active {
        color: var(--color-high-text);
    }
    .active span {
        border-bottom: 3px solid var(--color-tint);
    }
</style>