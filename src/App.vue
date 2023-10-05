<script setup>
// 7
import {onMounted, reactive, ref,watch,provide} from 'vue'
import {computed} from 'vue'
import SonCom from './components/SonCom.vue';

const list = ref([1,2,3,4,5,6,7,8])
const computedList = computed(()=>list.value.filter(item=>item>2))
setTimeout(()=>{
  list.value.push(9,10)
},3000)

// 8
const num = ref(0)
const addNum = ()=>{
  num.value++
}
const gender = ref("male")
const changeGender = ()=>{gender.value = (gender.value === "male"?"female":"male")}
watch([num,gender],([newNum,newGender],[oldNum,oldGender])=>{
  console.log("Num or Gender is changed: " + oldNum + " ⇒ " + newNum + " || "  + oldGender + " ⇒ " + newGender)
},{immediate:true})

// 9-1
const person = ref({name:"Anna",age:18})
const changeName = () => {person.value.name = "Ken"}
const changeAge = () => {person.value.age = 20}
watch(
  () => person.value.age,
  () => console.log("Age is changed!")
)
// 9-2
const animal = reactive({name:"Wang",age:2})
const turnName = () => {animal.name = "Miao"}
const turnAge = () => {animal.age = 4}
watch(()=>animal.age,(newAge,oldAge)=>{console.log("The animal's age is changed: " + oldAge + " ⇒ " + newAge)})

// 11
const plant = ref(["rose","white",12])
setTimeout(() => {
  plant.value = ["lily","pink",9]
},3000)

// 12
const getMsg = (msg) => {
  console.log(msg)
}

// 13
const h3Ref = ref(null)
const pRef = ref(null)
onMounted(() => {
  console.log(h3Ref.value)
  console.log(pRef.value)
})

// 14
const week = ref({sunday:0,monday:1,tuesday:2})
setTimeout(()=>{
  week.value.wednesday=3
},3000)
const commited = () => {
  setTimeout(() => {
    console.log("Commited successfully!")
  },3000)
}
provide('topMsg','A message from Top!')
provide('topWeek',week)
provide('commited',commited)
</script>

<template>
  <!-- 7 -->
  <div>
    Original Arrya : {{ list }}
  </div>
  <div>
    New Array : {{ computedList }}
  </div>
  <!-- 8 -->
  <div>
    <button @click="addNum">{{ num }}</button>
  </div>
  <div>
    <button @click="changeGender">{{ gender }}</button>
  </div>
    <!-- 9-1 -->
  <div>
    <button @click="changeName">{{ person.name }}</button>
    <button @click="changeAge">{{ person.age }}</button>
  </div>
    <!-- 9-2 -->
  <div>
    <button @click="turnName">{{ animal.name }}</button>
    <button @click="turnAge">{{ animal.age }}</button>
  </div>

    <!-- 11 --><!-- 12 -->
  <div>
    <h3>App's Space</h3>
    <SonCom :msg="plant" title="I love NANA!" @get-msg="getMsg" ref="pRef"/>
  </div>

    <!-- 13 -->
  <div>
    <h3 class="life" ref="h3Ref">Life is beautiful!</h3>
  </div>
</template>



<style scoped>
.life{
  color:red
}
</style>
