<script setup>
import GrandSonCom from "./GrandSonCom.vue"
const props = defineProps({
    msg:Array,
    title:String
})
setTimeout(()=>{
    console.log(props)
},3000)
const emit = defineEmits(["get-msg"])
const sendMsg = () => {
    emit("get-msg","A massage from SonCom!")
}
defineExpose({
    emit,
    sendMsg
})
</script>
<template>
    <p>{{ title }}</p>
    <ul>
        <li v-for="(item,index) of msg" :key="index">{{ item }}</li>
    </ul>
    <button @click="sendMsg">Send to App!</button>
    <GrandSonCom/>
</template>