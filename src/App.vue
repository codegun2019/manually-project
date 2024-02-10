<template>
  <div><h1>CODEGUN</h1></div>
  <h2>#Debug:{{ count }}</h2>
  <h2>#Ref:{{ refcount }}</h2>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    let count = 20; //เปลี่ยนแปลงค่าได้
    const refcount   = ref<number>(2)

    return {
      count,
      refcount

    };
  },
});
</script>
