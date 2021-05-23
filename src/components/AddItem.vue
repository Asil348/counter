<template>
  <div class="add-new-item">
    <!-- Button trigger modal -->
    <div class="add-item-button">
      <button class="btn btn-lg btn-success" type="button" data-bs-toggle="modal" data-bs-target="#addModal">Add New
        Item</button>
    </div>

    <!-- Modal -->
    <div class="modal fade" id="addModal" tabindex="-1" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="modalLabel">New Item</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <form @submit="onSubmit">
            <div class="modal-body">
              <div class="mb-3 form-floating">
                <input type="text" class="form-control" id="inputName" placeholder="Name" v-model="text" required>
                <label for="inputName">Name</label>
              </div>
              <div class="mb-3 form-floating">
                <input type="text" class="form-control" id="inputCount" placeholder="Count" v-model="count" required>
                <label for="inputCount">Count</label>
              </div>
              <div class="mb-3 form-floating">
                <input type="text" class="form-control" id="inputIncrementBy" placeholder="Increment By"
                  v-model="config.increment" required>
                <label for="inputIncrementBy">Increment By</label>
              </div>
              <div class="row mb-3">
                <div class="col-sm-10">
                  <div class="form-check">
                    <label class="form-check-label" for="gridCheck">
                      Reminder
                    </label>
                    <input class="form-check-input" type="checkbox" id="gridCheck" v-model="config.reminder">
                  </div>
                </div>
              </div>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
              <button type="submit" class="btn btn-success">Save</button>
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
      items: Object
    },
    data() {
      return {
        text: '',
        config: {
          increment: 1,
          reminder: false
        },
        count: 0,
        addItemModal: ""
      }
    },
    mounted() {
      let modal = new bootstrap.Modal(document.getElementById('addModal'));
      this.addItemModal = modal;
    },
    methods: {
      onSubmit(e) {
        e.preventDefault();

        var newID = this.items.length;

        const newItem = {
          id: newID,
          text: this.text,
          config: {
            increment: this.config.increment,
            reminder: this.config.reminder
          },
          count: this.count
        }

        this.$emit('add-item', newItem);

        this.text = ''
        this.config.increment = 1
        this.config.reminder = false
        this.count = 0

        this.addItemModal.hide();
      }
    }
  }
</script>

<style scoped>
  .add-new-item .add-item-button {
    text-align: center;
  }
</style>