<template>
    <div><h1>{{ title }}</h1></div>
    <form class="mx-2 px-2">
        <label for="username"></label>
        <input class="form-control" type="text" name="username" id="username" v-model="states.account.username" />
        <label for="password"></label>
        <input class="form-control" type="text" name="password" id="password" v-model="states.account.password" />
        <br/>
        <span>#Debug : {{ states.account }}</span>
        <br/>
        <button class="bg-success text-white btn text-sm px-3 min-h-[32px] mx-1" type="button" @click="onClicklogin">submit</button>
        <button class="bg-secondary text-white btn text-sm px-3 min-h-[32px] mx-1" type="button" @click="onClickClearAccount" >Clear</button>
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
