<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Makan', done: true },
  { id: id++, text: 'Gosok Gigi', done: true },
  { id: id++, text: 'Cuci Motor', done: false },
  { id: id++, text: 'Meeting Jam 18:00', done: false }
])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <div class="containerblue">
    <div class="purple">
      <h2 class="addtitle">TAMBAHKAN LIST ANDA</h2>
      <form @submit.prevent="addTodo">
        <input class="box" v-model="newTodo" required placeholder="new todo">
        <button class="button-20 buttonfirst">Tambah</button>
      </form>
    </div>
    <div class="red">
      <div class="black">
        <img class="icon" src="./assets/list.gif" alt="">
      </div>
      <div class="blue">
        <h1><span style="color: white;">MY</span><span style="color: cadetblue;">LIST</span></h1>
      </div>
      <div class="yellow">
        <div class="list">
          <ul>
            <li class="alllist" v-for="todo in filteredTodos" :key="todo.id">
              <div class="li1">
                <input type="checkbox" v-model="todo.done">
                <span :class="{ done: todo.done }" class="titillium-web-regular listtext">{{ todo.text }}</span>
              </div>
              <div class="li2">
                <button class="button-28 listbut" @click="removeTodo(todo)">Hapus</button>
              </div>
            </li>
          </ul>
          <button class="filter button-29" @click="hideCompleted = !hideCompleted">
            {{ hideCompleted ? 'Show all' : 'Hide completed' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
form{
  display: flex;
  flex-direction: column;
}
li{
  list-style-type: none;
  display: flex;
  justify-content: space-between;
}
.kanit-semibold {
  font-family: "Kanit", sans-serif;
  font-weight: 600;
  font-style: normal;
}
.addtitle{
      font-family: "IBM Plex Mono", monospace;
      font-size: 40px;
      font-weight: 400;
      font-style: normal;
}
div.li1{
  display: flex;
  margin-left: 50px;
  gap: 30px;
}
div.li2{
  padding-right: 50px;
}
.filter{
  position: relative;
  left: 25%;
  bottom: 40px;
  position: relative;
  width: 100%;
}
  .titillium-web-regular {
      font-family: "Titillium Web", sans-serif;
      font-weight: 400;
      font-size: 30px;
      font-style: normal;
    }
    input[type="checkbox"] {
     position: relative;
     right: 50px;
     top: 15px;
     scale: 2.5;
     margin-left: 10px;
    }
.list{
  position: absolute;
  height: 85%;
  width: 80%;
  top: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

}
.containerblue{
  background-image: url(./assets/2825710.gif);
  background-repeat: no-repeat;
  background-size: cover;
  height: 100vh;
  display: flex;
  justify-content: space-between;
  flex-direction: row;
}
.listtext{
  position: relative;
  top: 13px;
}
.listbut {
  position: relative;
  top: 15px;
}
h1{
      font-family: "Kanit", sans-serif;
      font-weight: 600;
      font-style: normal;
      font-size: 120px;
}
h1 span{
  margin: 40px;
}
.containerblue::before{
  content: "";
  position: absolute;
  top: 0;
  width: 100%;
  height: 120%;
  background: rgba(0, 0, 0, 0.6);
}


.red {
  position: relative;;
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 40%;
  border-radius: 20px;
}
.purple {
  top: 22%;
  left: 10%;
  position: relative;
  background: rgba(255, 255, 255, 0.6);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 20%;
  width: 30%;
  border-radius: 15px;
  justify-content: space-around;
}
.black{
  position:absolute;
  top: 0;
  left: 0;
  background-color: white;
  height: 15%;
  width: 20%;
  border-top-left-radius: 20px;
  overflow: hidden;
  
  }
.blue{
  position: absolute;
  background-color: black;
  color: white;
    top: 0;
    right: 0;
    height: 15%;
    width: 80%;
    border-top-right-radius: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 20px;
  
}

.yellow {
  position: absolute;
  bottom: 0;
  right: 0;
  height: 85%;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
  backdrop-filter: blur(10px);
  border-bottom-left-radius: 200px;
  background: rgba(255, 255, 255, 0.5) ;
  box-shadow: 0px 0px 16px 0px rgba(255,255,255, 0.5);
}
li{
  padding-top: 20px;
}
ul{
  height: 80%;
  overflow: auto;
}
img.icon{
  width: 100%;
  height: 100%;
  border-top-left-radius: 15px;
  
}
.done {
  text-decoration: line-through;
}

.button-28 {
  border: 2px solid #1A1A1A;
  border-radius: 15px;
  box-sizing: border-box;
  color: #3B3B3B;
  cursor: pointer;
  display: inline-block;
  font-family: Roobert, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  margin: 0;
  height: 40px;
  min-width: 0;
  outline: none;
  padding: 0 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 100%;
  will-change: transform;
}

.button-28:disabled {
  pointer-events: none;
}

.button-28:hover {
  color: #fff;
  background-color: #1A1A1A;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

.button-28:active {
  box-shadow: none;
  transform: translateY(0);
}

.button-29 {
  border: 2px solid #1A1A1A;
  border-radius: 15px;
  box-sizing: border-box;
  color: #3B3B3B;
  cursor: pointer;
  display: inline-block;
  font-family: Roobert, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  margin: 0;
  min-height: 60px;
  min-width: 0;
  outline: none;
  padding: 16px 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 50%;
  will-change: transform;
}

.button-29:disabled {
  pointer-events: none;
}

.button-29:hover {
  color: #fff;
  background-color: #1A1A1A;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

.button-29:active {
  box-shadow: none;
  transform: translateY(0);
}
.box{
  position: relative;
  bottom: 15px;
width: 100%;
color: rgb(36, 35, 42);
font-size: 16px;
line-height: 20px;
min-height: 28px;
border-radius: 4px;
padding: 8px 16px;
border: 2px solid transparent;
box-shadow: rgb(0 0 0 / 12%) 0px 1px 3px,
rgb(0 0 0 / 24%) 0px 1px 2px;
background: rgb(251, 251, 251);
transition: all 0.1s ease 0s;
}
.box:focus {
  border: 2px solid rgb(124, 138, 255);
}
.button-20 {
  border: 2px solid #1A1A1A;
  border-radius: 15px;
  box-sizing: border-box;
  color: #3B3B3B;
  cursor: pointer;
  display: inline-block;
  font-family: Roobert, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  font-size: 16px;
  font-weight: 600;
  line-height: normal;
  margin: 0;
  height: 40px;
  min-width: 0;
  outline: none;
  padding: 0 24px;
  text-align: center;
  text-decoration: none;
  transition: all 300ms cubic-bezier(.23, 1, 0.32, 1);
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  width: 50%;
  margin-left: 25%;
  will-change: transform;
}

.button-20:disabled {
  pointer-events: none;
}

.button-20:hover {
  color: #fff;
  background-color: #1A1A1A;
  box-shadow: rgba(0, 0, 0, 0.25) 0 8px 15px;
  transform: translateY(-2px);
}

.button-2:active {
  box-shadow: none;
  transform: translateY(0);
}
</style>