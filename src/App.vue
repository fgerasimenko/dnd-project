  
<template>
  <div class="container" ref="container">
    <div class="depth-chart">
      <div 
        class="field drop-zone"
        @drop="onDrop($event, 1)"
        @dragenter.prevent
        @dragover.prevent
      >
        <div
          class="player"
          v-for="item in getList(1)"
          :id="item.id"
          :key="item.id"
          draggable="true"
          @dragstart="startDrag($event, item)"
        >
        </div>
      </div>
      <div
        class="bench drop-zone"
        @drop="onDrop($event, 2)"
        @dragenter.prevent
        @dragover.prevent
      >
      <div
        class="player"
        v-for="item in getList(2)"
        :key="item.id" 
        draggable="true"
        @dragstart="startDrag($event, item)"
      >
      </div>
      </div>
    </div>
    
  </div>
</template>
<script setup>
import { ref } from 'vue'

const items = ref([
    {
      id: 1,
      name: "Jogador um",
      position: null,
      list: 1
    },
    {
      id: 2,
      name: "Jogador dois",
      position: null,
      list: 1
    },
    {
      id: 3,
      name: "Jogador três",
      position: null,
      list: 1
    },
    {
      id: 4,
      name: "Jogador quatro",
      position: null,
      list: 2
    },
  ]
)

const getList = (list) => {
  return items.value.filter((item) => item.list == list)
}

const startDrag = (e, item) => {
  // itemRefs.value.find((refItem) => item.id == refItem.id)
  // console.log(item)
  e.dataTransfer.dropEffect = 'move'
  e.dataTransfer.effectAllowed = 'move'
  e.dataTransfer.setData('itemId', item.id)
}

const onDrop = (e, list) => {
  console.log(e)
  const itemID = e.dataTransfer.getData('itemID')
  const item = items.value.find((item) => item.id == itemID)
  const screenPosition = [e.screenX, e.screenY];
  item.position = screenPosition
  item.list = list
}

</script>

<style scoped>
  .container{
    display: grid;
    width: 100%;
    height: 100vh;
  }

  .drop-zone {
    position: relative;
    width: 100%;
    margin: 50px;
    background-color: brown;
    padding: 10px;
    min-height: 10px;
  }

  .field {
    width: 100%;
    margin: 10px;
    background-color: brown;
    padding: 10px;
    min-height: 200px;
  }

  .drag-el {
    background-color: black;
    color: white;
    padding: 5px;
    margin-bottom: 10px;
    border-radius: 100%;
  }
  .player {
    background-color: black;
    color: white;
    padding: 5px;
    margin-bottom: 10px;
    height: 50px;
    width: 50px;
    border-radius: 50%;
  }

  .drag-el:last-of-type{
    margin-bottom: 0;
  }
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  .container{
    display: grid;
    width: 100%;
    height: 100vh;
  }

  .drop-zone {
    position: relative;
    width: 100%;
    margin: 50px;
    background-color: brown;
    padding: 10px;
    min-height: 10px;
  }

  .field {
    width: 100%;
    margin: 10px;
    background-color: brown;
    padding: 10px;
    min-height: 600px;
  }

  .drag-el {
    background-color: black;
    color: white;
    padding: 5px;
    margin-bottom: 10px;
  }

  .drag-el:last-of-type{
    margin-bottom: 0;
  }
}
</style>
