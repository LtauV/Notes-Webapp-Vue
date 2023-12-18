<script setup>
  import {ref} from "vue";

  const showModal = ref(false)
  const newNote = ref("")
  const notes = ref([]) 

  function pushToLocalStorage(){
    localStorage.setItem('notes_data',JSON.stringify(notes.value));
  }

  //debug of notes initialisation state
  // console.log(notes.value.length==0)
  
  function restoreFromLocalStorage(){
    if ((notes.value.length==0) && (!JSON.parse(localStorage.getItem('notes_data')))==false) {
      console.log("History succesfully identified")
      notes.value = JSON.parse(localStorage.getItem('notes_data'));

      console.log("History succesfully restored")
    }
    else {
      console.log("History was empty or Notes is not empty")
    }
    //  console.log(JSON.parse(localStorage.getItem('notes_data')))
  }

  restoreFromLocalStorage()


  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }

  const addNote = () => {
    notes.value.push({
      id: Math.floor(Math.random() * 100000),
      text: newNote.value,
      date: new Date().toDateString(),
      backgroundColor: getRandomColor(),
    });
    showModal.value=false;
    newNote.value="";
    localStorage.clear();
    pushToLocalStorage();
  }

</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
        <div class = "modal">
          <textarea v-model="newNote" name="note" id="note" cols="30" rows="10"></textarea>
          <button @click="addNote()">Add Note</button>
          <button class = "close" @click="showModal = false">Close</button>
        </div>
      </div>

    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
    
      <div class ="cards-container">
        <div v-for="note in notes" class="card" :style="{backgroundColor :note.backgroundColor}">
          <p class="main-text">{{ note.text }}</p>
          <p class = "date">{{ note.date}}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  main {
    height: 100vh;
    width: 100vw;
  }

  .container{
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto;
  }
  
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 60px;
  }

  header button {
    border : none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: gray;
    border-radius: 100%;
    color: aliceblue;
    font-size: 20px;
  }

  .card {
    width: 225px;
    height: 225px;
    
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .date {
    font-size: 12.5px;
    font-weight: bold;
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }
  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgb(250, 234, 214,0.80);
    z-index: 10;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal {
    width: 750px;
    background-color: aliceblue;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;

  }
  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color :white;
    cursor: pointer;
    margin-top: 15px;

  }

  .modal .close {
    background-color: red;
    margin-top: 10px;
  }

</style>