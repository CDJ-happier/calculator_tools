<template>
  <div>
    <h2>布隆过滤器参数 \( m \) 和 \( k \) 的计算</h2>
    <div> \( m = -\frac{n \cdot \ln(p)}{(\ln(2))^2} \) </div>
    <div> \( k = \ln(2) \cdot \frac{m}{n} \) </div>
    <label>
      预期要插入的数据量(n):
      <input
        type="number"
        v-model="n"
        placeholder="数据量n"
      />
    </label>
    <label>
      预期的错误率(p) e.g., 0.01:
      <input
        type="number"
        v-model="p"
        placeholder="错误率p"
      />
    </label>
    <h3 v-if="m !== null">布隆过滤器bitsize(m): {{ m }}</h3>
    <h3 v-if="k !== null">布隆过滤器hash个数(k): {{ k }}</h3>
  </div>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    const n = ref(300);
    const p = ref(0.01);

    // 使用计算属性实时计算输出大小
    const m = computed(() => {
      return Math.ceil(-n.value * Math.log(p.value) / Math.pow(Math.log(2), 2));
    });

    const k = computed(() => {
        return Math.ceil(Math.log(2) * m.value / n.value);
    })

    return {
      n,
      p,
      m,
      k
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