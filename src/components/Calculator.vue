<script setup>
import ConvCalculator from "./ConvCalculator.vue";
import BloomFilterCalculator from "./BloomFilterCalculator.vue";
</script>

<template>
    <div class="container">
        <div class="calculator">
            <ConvCalculator />
        </div>
        <div class="calculator">
            <BloomFilterCalculator />
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    justify-content: space-around; /* 让组件之间的空间均匀分布 */
    align-items: center; /* 垂直居中对齐 */
    padding: 20px;
}

.calculator {
    flex: 1; /* 每个计算器平分容器宽度 */
    margin: 10px; /* 外边距以增加组件之间的间距 */
    max-width: 500px; /* 限制组件最大宽度 */
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1); /* 添加阴影效果 */
    padding: 20px; /* 内边距 */
    background-color: #f9f9f9; /* 背景颜色 */
    border-radius: 8px; /* 圆角 */
}
</style>