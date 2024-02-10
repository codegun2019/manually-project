<template>
  <div><h1>CODEGUN</h1></div>
  <span>#Debug:{{ count }}</span>
  <span>#Ref:{{ refcount }}</span>
  <button @click="onClickAdd">Add</button>
  <button @click="onClickAddref">AddRef</button>
  <hr />
  <LoginForm title="Login" @onlogin="onlogin" />
  <span>#Account: {{ account }}</span>
  <button @click="onClickClearAccount">onClickClearAccount</button>
</template>
<script lang="ts">
import { defineComponent, reactive, ref, onMounted } from "vue";
import LoginForm from "@/components/LoginForm.vue";
import  User  from '@/type/user.type'

const defaultAccount = { username: "", password: "" };

export default defineComponent({
  components: {
    LoginForm,
  },
  setup() {
    let count = 20;
    const refcount = ref<number>(2);
    const states = reactive({
      account: { username: "codegun", password: "password" },
    });

    const onClickAdd = () => {
      count = count + 1;
      console.log("count = " + count);
    };

    const onClickAddref = () => {
      refcount.value = refcount.value + 1;
      console.log("count = " + refcount.value);
    };

    onMounted(() => {
      setInterval(onClickAddref, 1000);
    });

    const onClickClearAccount = () => {
      states.account = defaultAccount;
    };

    const onlogin  = (user:User)=> {
      alert(JSON.stringify(user))
    }

    return {
      count,
      refcount,
      onClickAdd,
      onClickAddref,
      onClickClearAccount,
      states,
      onlogin,
    };
  },
});
</script>