<script setup>
import ConvCalculator from "./ConvCalculator.vue";
import DeConvCalculator from "./DeConvCalculator.vue";
import BloomFilterCalculator from "./BloomFilterCalculator.vue";
</script>

<template>
    <div class="container">
        <div class="calculator">
            <ConvCalculator />
        </div>
        <div class="calculator">
            <DeConvCalculator />
        </div>
        <div class="calculator">
            <BloomFilterCalculator />
        </div>
    </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: space-between; /* 让组件之间的空间均匀分布 */
  align-items: center; /* 垂直居中对齐 */
  padding: 20px;
  flex-wrap: nowrap; /* 禁止换行 */
  width: 100%; /* 容器宽度占满父容器 */
}

.calculator {
  flex: 1; /* 每个计算器平分容器宽度 */
  margin: 15px; /* 外边距以增加组件之间的间距 */
  max-width: 500px; /* 限制组件最大宽度 */
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.5); /* 添加阴影效果 */
  padding: 20px; /* 内边距 */
  background-color: #ffffff; /* 背景颜色 */
  border-radius: 8px; /* 圆角 */
}

/* 响应式布局 */
@media (max-width: 768px) {
  .container {
    display: block; /* 在小屏幕上垂直排列 */
    padding: 20px 0; /* 上下内边距 */
  }

  .calculator {
    flex: none; /* 取消平分宽度 */
    max-width: 100%; /* 占满整个宽度 */
    margin: 15px 0; /* 上下外边距 */
  }
}

</style>