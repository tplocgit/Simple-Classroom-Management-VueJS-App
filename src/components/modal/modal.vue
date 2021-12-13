<template>
    <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">

          <div class="modal-header">
            <slot name="header">
                Add new classroom
            </slot>
          </div>
          <div class="modal-body">
            <p v-if="isAdding" class="adding-text">Adding ...</p>
            <form class="modal-body__form form">
              <div class="modal-body__form__form-control">
                <label class="modal-body__form__form-control__label" for="in_name">Name:</label>
                <input class="modal-body__form__form-control__input" type="text" name="in_name" id="in_name">
              </div>
              <div class="modal-body__form__form-control">
                <label class="modal-body__form__form-control__label" for="in_topic">Topic:</label>
                <input class="modal-body__form__form-control__input" type="text" name="in_topic" id="in_topic">
              </div>
              <div class="modal-body__form__form-control">
                <label class="modal-body__form__form-control__label" for="in_section">Section:</label>
                <input class="modal-body__form__form-control__input" type="text" name="in_section" id="in_section">
              </div>
            </form>
          </div>
          
          <div class="modal-footer">
            <slot name="footer">
              <button class="modal-default-button modal-default-button--cancel" @click="$emit('close')">
                Cancel
              </button>
              <button class="modal-default-button modal-default-button--save" @click="addClassroom">
                Save
              </button>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>
import axios from 'axios';

export default {
  name: 'modal',
  data() {
    return {
      isAdding: false
    }
  },
  methods: {
    addClassroom() {
      if(this.isAdding) return alert("New classroom is adding please wait ...")

      let nameEl = document.getElementById("in_name")
      let topicEl = document.getElementById("in_topic")
      let sectionEl = document.getElementById("in_section")

      let postData = {
        name: nameEl.value,
        theme: topicEl.value,
        part: sectionEl.value
      }
      if(Object.values(postData).some(v => !v)) return alert("Please enter all fields.")

      this.isAdding = true
      let postURL = 'https://my-classroom-tploc1305-api.herokuapp.com/classrooms'
      axios.post(postURL, postData)
      .then(response => {
        this.isAdding = false
        if(response.status == 200 || response.status == 201) {
          alert("Add new classroom successfully.")
          this.$emit("add-classroom-success")
          this.$emit('close')
        }
        else alert(`Error ${response.status}: ${response.statusText}`)
      })
      .catch(err => console.log(err))
    }
  }
}
</script>