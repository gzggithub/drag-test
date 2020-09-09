<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <draggable v-model="myArray" draggable=".item" group="people" :move="dragMove" @start="drag=true" @end="drag=false">
      <div v-for="(element, index) in myArray" :ref="'px' + index" :key="element.id" class="item">{{element.name}}</div>
    </draggable>
    <h2>333</h2>
    <draggable v-model="myArray2" draggable=".item" group="people">
      <div v-for="(element, index) in myArray2" :ref="'pxl' + index" :key="element.id" class="item">{{element.name}}</div>
    </draggable>

    <h2>rrrr</h2>
    <div style="border:1px solid green;" draggable="true" @dragstart="dragstart($event, item.data)" @dragend="dragend">
      {{item.data}}
    </div>
    <h2>hhhh</h2>
    <div style="border:1px solid red;height: 100px;width:300px;" @drop="drop" @dragover.prevent>
      <h1 style="color:#ccc;">{{this.dropData}}</h1>
      <h2 style="color:#ccc;">{{this.dropData}}</h2>
      <h3 style="color:#ccc;">{{this.dropData}}</h3>
    </div>
  </div>
</template>

<script>
import draggable from 'vuedraggable'
export default {
  name: 'HelloWorld',
  components: {
    draggable,
  },
  props: {
    msg: String
  },
  data() {
    return {
      myArray: [
        {
          id: 1,
          name: '小郭'
        },
        {
          id: 2,
          name: '小郭2'
        },
        {
          id: 3,
          name: '小郭3'
        }
      ],
      myArray2: [
        {
          id: 11,
          name: '小郭2'
        },
        {
          id: 22,
          name: '小郭22'
        },
        {
          id: 33,
          name: '小郭23'
        }
      ],
      drag: false,
      dropData: 'uuu',
      item: {
        data: 'dd'
      }
    }
  },
  methods: {
    dragMove({ draggedContext, relatedContext}) {
      console.log(draggedContext);
      console.log(relatedContext);
      return (draggedContext.element.name!=='apple')
    },
    dragstart(event, data) {
      console.log('drag')
      event.dataTransfer.setData('item', data)
    },
    dragend(event) {
      event.dataTransfer.clearData()
    },
    drop(event) {
      console.log('drop')
      console.log(event)
      console.log(event.target)
      console.log(event.toElement)
      console.log(event.srcElement)
      let data = event.dataTransfer.getData('item')
      this.dropData = data
      console.log('data: ', data)
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.item {
  border: 1px solid #000000;
}
</style>
