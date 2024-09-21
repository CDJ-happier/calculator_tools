<template>
  <div>
    <h2>卷积层输出特征大小计算器</h2>
    <label>
      输入大小 H/W:
      <input
        type="number"
        v-model="inputSize"
        placeholder="输入特征大小"
      />
    </label>
    <label>
      卷积核大小 (K):
      <input
        type="number"
        v-model="kernelSize"
        placeholder="卷积核大小"
      />
    </label>
    <label>
      步长 (S):
      <input type="number" v-model="stride" placeholder="步长" />
    </label>
    <label>
      填充 (P):
      <input type="number" v-model="padding" placeholder="填充大小" />
    </label>
    <label>
      膨胀 (D):
      <input type="number" v-model="dilation" placeholder="膨胀大小" />
    </label>
    <h3 v-if="outputSize !== null">输出大小: {{ outputSize }}</h3>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const inputSize = ref(0);
    const kernelSize = ref(0);
    const padding = ref(0);
    const stride = ref(1);
    const dilation = ref(1);

    // 使用计算属性实时计算输出大小
    const outputSize = computed(() => {
      if (stride.value <= 0) return null; // 防止除零错误

      const effectiveKernelSize = kernelSize.value + (kernelSize.value - 1) * (dilation.value - 1);

      return Math.floor((inputSize.value + 2 * padding.value - effectiveKernelSize) / stride.value) + 1;
    });

    return {
      inputSize,
      kernelSize,
      padding,
      stride,
      outputSize,
    };
  },
};
</script>

<style scoped>
label {
  display: block;
  margin: 10px 0;
}
input {
  margin-left: 10px;
}
button {
  margin-top: 10px;
}
</style>