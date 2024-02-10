<template>
  <div><h1>CODEGUN</h1></div>
  <span>#Debug:{{ count }}</span>
  <span>#Ref:{{ refcount }}</span>
  <button @click="onClickAdd">Add</button>
  <button @click="onClickAddref">AddRef</button>
  <hr />
  <span>#Account: {{ account }}</span>
  <button @click="onClickClearAccount">onClickClearAccount</button>
</template>
<script lang="ts">
import { defineComponent, reactive, ref ,onMounted} from "vue";

const defaultAccount = {username: "" , password:"" }

export default defineComponent({
  setup() {
    let count = 20; //เปลี่ยนแปลงค่าได้ no side effect vue ไม่ส่งใน template
    const refcount = ref<number>(2); //side effect
    //ตัวแปลแบบ reactive obj เท่านั้น ต่างจาก let
    const states = reactive({ 
        
        account : {username: "codegun", password: "password" }, //states account
        
        });

    const onClickAdd = () => {
      count = count + 1;
      console.log("count = " + count);
    };

    onMounted(() => {
        setInterval(onClickAddref, 1000) //loop callback
    });


    const onClickAddref = () => {
      refcount.value = refcount.value + 1; //.value เสมอ
      console.log("count = " + refcount.value);
    };
    const onClickClearAccount = () => {
        //reactive ไม่ต้อง .val
        //   account.username = "";
        //   account.password = "";
        states.account = defaultAccount
    };

    

    return {
      count,
      refcount,
      onClickAdd,
      onClickAddref,
      onClickClearAccount,
      states,
    };
  },
});
</script>
