<template>
    <div><h1>{{ title }}</h1></div>
    <form>
        <label for="username"></label>
        <input type="text" name="username" id="username" v-model="states.account.username" />
        <label for="password"></label>
        <input type="text" name="password" id="password" v-model="states.account.password" />
        <br/>
        <span>#Debug : {{ states.account }}</span>
        <br/>
        <button type="button" @click="onClicklogin">submit</button>
        <button type="button" @click="onClickClearAccount" >Clear</button>
    </form>
</template>
<script lang="ts">
import { defineComponent, onMounted, reactive } from 'vue'
import  User  from '@/type/user.type'

interface LoginState{
    account: User;
}

export default defineComponent({
    emits: ["onlogin"], //> App.vue
    props: ["title"],
    //การสื่อสารระหว่าง component
    setup(props,{emit}) {

        const states = reactive<LoginState>({account: { username:"",password :""}})

        const onClickClearAccount = ()=>{
            states.account = {username:"",password:""}
        }
        const onClicklogin = () =>{
            emit("onlogin",states.account)
        }

        return {states,onClickClearAccount,onClicklogin};
    },
})
</script>
