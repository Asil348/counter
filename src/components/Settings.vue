<template>
  <div class="settings">
    <!-- Button trigger modal -->
    <button class="btn btn-outline-white" type="button" data-bs-toggle="modal"
      :data-bs-target="'#settingsModal' + item.id"><i class="bi bi-sliders"></i></button>

    <!-- Modal -->
    <div class="modal fade" :id="'settingsModal' + item.id" tabindex="-1" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" :id="'modalLabel' + item.id">{{ text }}</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <form @submit="onSubmit">
            <div class="modal-body">
              <div class="mb-3 form-floating">
                <input type="text" class="form-control" :id="'inputName' + item.id" v-model='text'>
                <label :for="'inputName' + item.id">Name</label>
              </div>
              <div class="mb-3 form-floating">

                <!-- ##### FIX: COUNT NOT UPDATING HERE FROM ITEMS WHEN CHANGED VIA SETTINGS ##### -->
                <input type="number" class="form-control" :id="'inputCount' + item.id"
                  v-model='count'>
                <label :for="'inputCount' + item.id">Count</label>
              </div>
              <div class="mb-3 form-floating">
                <input type="number" class="form-control" :id="'inputIncrementBy' + item.id"
                  v-model='config.increment'>
                <label :for="'inputIncrementBy' + item.id">Increment By</label>
              </div>
              <div class="row mb-3">
                <div class="col-sm-10">
                  <div class="form-check">
                    <label class="form-check-label" :for="'gridCheck1' + item.id">
                      Reminder
                    </label>
                    <input class="form-check-input" type="checkbox" :id="'gridCheck1' + item.id"
                      v-model="config.reminder">
                  </div>
                </div>
              </div>
              <button type="button" class="btn btn-danger">Delete</button>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
              <button type="submit" class="btn btn-primary">Save changes</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Settings',
    props: {
      item: Object
    },
    data() {
      return {
        id: this.item.id,
        text: this.item.text,
        config: {
          increment: this.item.config.increment,
          reminder: this.item.config.reminder
        },
        count: this.item.count,
        updateModal: ''
      }
    },
    mounted() {
      let modal = new bootstrap.Modal(document.getElementById(`settingsModal${this.item.id}`));
      this.updateModal = modal;
    },
    methods: {
      onSubmit(e) {
        e.preventDefault();

        const updItem = {
          id: this.id,
          text: this.text,
          config: {
            increment: parseInt(this.config.increment),
            reminder: this.config.reminder
          },
          count: parseInt(this.count)
        }

        // ###### FIX: COUNT NOT UPDATING HERE FROM ITEMS WHEN CHANGED VIA SETTINGS ######

        this.text = updItem.text
        this.config.increment = updItem.config.increment
        this.config.reminder = updItem.config.reminder
        this.count = updItem.count

        this.$emit('update-item', updItem); // idk why it doesn't emit inline in other components, check that out later

        this.updateModal.hide();
      }
    }
  }
</script>

<style scoped>

</style>