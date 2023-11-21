<script setup>
import { ref } from 'vue'
const showModal = ref(false)
const newNote = ref('')
const errorMessage = ref('')
const notes = ref([])

function getRandomColor(){
  return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
}

const addNote =()=>{
  if (newNote.value.length < 10){
    errorMessage.value = 'Note must be at least 10 characters long'
    return
  }
  notes.value.push(
    {
      id: Math.floor(Math.random() * 100000),
      text: newNote.value,
      date: new Date().toLocaleDateString(),
      backgroundColor:getRandomColor()
    }
  );
  showModal.value = false;
  newNote.value = '';
  errorMessage.value = '';
}
</script>

<template>
  <main>
    <div v-show="showModal" class="overlay">
      <div class="modal">
          <textarea v-model.trim="newNote" placeholder="Note"></textarea>
          <p v-if="errorMessage" style="color:red">{{errorMessage}}</p>
          <button @click="addNote()">Add note</button>
          <button @click="showModal=false;" class="close">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>🗿Notes🗿</h1>
        <button @click="showModal=true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in notes"
        :key="note.id" 
        class="card" 
        :style="{backgroundColor:note.backgroundColor}">
          <p class="main-text">{{note.text}}</p>
          <p class="date">{{note.date}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>

  main{
    height: 100vh;
    width: 100vw;
  }

  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }

  header{
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1{
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  header button{
  border: none;
  padding: 10px;
  width: 50px;
  height: 50px;
  cursor: pointer;
  background-color: rgb(21,20,20);
  border-radius: 100%;
  color: white;
  font-size: 20px;
  transition: background-color 0.25s ease, color 0.5s ease;
}

header button:hover{
  background-color: rgb(212, 212, 212);
  color: black;
}


  .card{
    width:225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 2.5%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin:10px 20px;
  }

  .date{
    font-size: 12px;
    font-weight: bold;
    color: rgb(21,20,20);
  }

  .cards-container{
    display: flex;
    flex-wrap: wrap;
  }

  .overlay{
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(21,20,20,0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 10;
  }

  .modal{
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button{
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
  }
  .modal .close{
    background-color: red;
    margin-top: 7px;
  }

  .modal textarea{
    height: 200px;
    font-size: 20px;
    padding: 10px;
    border-radius: 5px;
    border: 1px solid rgb(21,20,20);
    margin-bottom: 15px;
  }
</style>