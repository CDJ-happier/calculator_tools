<template>
  <div>
    <h2>转置卷积输出特征大小计算器</h2>
    <div>
      \( \text{y} = (\text{x} - 1) \cdot \text{s} - 2 \cdot \text{p} + \text{d} \cdot (\text{k} - 1) + \text{op} + 1 \)
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
      output_padding(op):
      <input type="number" v-model="output_padding" placeholder="output_padding大小" />
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
    const stride = ref(1);
    const padding = ref(1);
    const dilation = ref(1);
    const output_padding = ref(0);

    // 使用计算属性实时计算输出大小
    const outputSize = computed(() => {
        // 计算转置卷积输出特征大小
        const effectiveKernelSize = kernelSize.value + (kernelSize.value - 1) * (dilation.value - 1);
        return (inputSize.value - 1) * stride.value - 2 * padding.value + effectiveKernelSize + output_padding.value;
    });

    return {
      inputSize,
      kernelSize,
      padding,
      stride,
      dilation,
      output_padding,
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