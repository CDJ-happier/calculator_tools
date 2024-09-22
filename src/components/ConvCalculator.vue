<template>
  <div>
    <h2>卷积层输出特征大小计算器</h2>
    <div>
      \( \text{y} = \frac{\text{x} + 2 \cdot \text{p} - \text{d} \cdot (\text{k} -1) - 1 }{\text{s}} + 1 \)
    </div>
    <label>
      输入大小(x):
      <input
        type="number"
        v-model="inputSize"
        placeholder="输入特征大小"
      />
    </label>
    <label>
      卷积核大小(k):
      <input
        type="number"
        v-model="kernelSize"
        placeholder="卷积核大小"
      />
    </label>
    <label>
      步长(s):
      <input type="number" v-model="stride" placeholder="步长" />
    </label>
    <label>
      填充(p):
      <input type="number" v-model="padding" placeholder="填充大小" />
    </label>
    <label>
      膨胀(d):
      <input type="number" v-model="dilation" placeholder="膨胀大小" />
    </label>
    <h3 v-if="outputSize !== null">输出大小(y): {{ outputSize }}</h3>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const inputSize = ref(512);
    const kernelSize = ref(3);
    const padding = ref(1);
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
      dilation,
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