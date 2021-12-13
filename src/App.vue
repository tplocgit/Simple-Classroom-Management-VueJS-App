<template>
  <div id="app" class="container">
    <div class="top-bar">
      <span class="top-bar__title">Classrooms</span>
      <button class="top-bar__button top-bar__button--add" @click="showModal = true">Add</button>
    </div>
    <Modal
      @add-classroom-success="fetchData"
      @close="showModal = false"
      v-if="showModal"
    />
    <List :items="data" />
  </div>
</template>

<script>
import List from './components/list/list.vue'
import axios from 'axios';
import Modal from './components/modal/modal.vue'

export default {
  name: 'App',
  components: {
    List,
    Modal
  },
  methods: {
    fetchData() {
      axios.get('https://my-classroom-tploc1305-api.herokuapp.com/classrooms')
        .then(response => { 
          this.data = response.data
        })
        .catch(err => alert(err))
    },
  },
  data: function() {
     return { 
      data: [],
      showModal: false
    }  
   },
   mounted() {
     this.fetchData()
   }
}
</script>
