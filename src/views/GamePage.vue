<script setup>
  import {reactive} from "vue";
  const state = reactive({
    width:0,
    height:0
  })

  const changeColor = () =>{
    if(event.target.className.indexOf('active') > 0 ){
      event.target.className = 'cell'
    }else{
      event.target.className = 'cell active'
    }
  }
</script>

<template>
  <div class="game">
    <v-card elevation="5" dark>
      <div class="options">
        <v-form>

          <v-text-field
              v-model="state.width"
              label="Size X"
              type="number"
          >
          </v-text-field>
          <v-text-field
              v-model.trim="state.height"
              label="Size Y"
              type="number"
          >
          </v-text-field>
        </v-form>
      </div>
      <v-divider></v-divider>
      <div class="gameField">
        <div v-for="y in ~~(state.height)" :key="y" class="row" >
          <div class="cell"
              v-for="x in ~~(state.width)"
              :onmouseenter="changeColor"
              :key="x"
          />
        </div>
      </div>
    </v-card>
  </div>
</template>

<style>
  .game{
    min-width: 600px;
    margin: 10px 10px;
    box-shadow: 0 0 2px #ccc;
    width: auto;
  }
  .gameField{
    display: flex;
    flex-direction: column;
    padding: 10px 0;
    align-items: center;
    background-color: #777;
  }
  .row{
    display: flex;
    flex-direction: row;
  }
  .cell{
    width: 36px;
    height: 36px;
    background-color: white;
    border:1px solid #999;
    border-collapse: collapse;
  }
  .cell.active{
    background-color: blue;
  }
</style>
