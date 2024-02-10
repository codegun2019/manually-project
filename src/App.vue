<template>
  <div><h1>CODEGUN</h1></div>
  <span>#Debug:{{ count }}</span>
  <span>#Ref:{{ refcount }}</span>
  <button @click="onClickAdd">Add</button>
  <button @click="onClickAddref">AddRef</button>
</template>
<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  setup() {
    let count = 20; //เปลี่ยนแปลงค่าได้ no side effect vue ไม่ส่งใน template
    const refcount   = ref<number>(2) //side effect

    const onClickAdd = ()=> {
        count = count + 1
        console.log("count = " + count)
    }

    const onClickAddref = ()=> {
        refcount.value = refcount.value + 1 //.value เสมอ
        console.log("count = " + refcount.value)
    }

    return {
      count,
      refcount,
      onClickAdd,
      onClickAddref

    };
  },
});
</script>
