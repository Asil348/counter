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
            <h5 class="modal-title" :id="'modalLabel' + item.id">{{ item.text }}</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <form>
            <div class="modal-body">
              <div class="row mb-3">
                <label :for="'inputName' + item.id" class="col-sm-2 col-form-label">Name</label>
                <div class="col-sm-10">
                  <input type="text" class="form-control" :id="'inputName' + item.id" :value='item.text'>
                </div>
              </div>
              <div class="row mb-3">
                <label :for="'inputIncrementBy' + item.id" class="col-sm-3 col-form-label">Increment By</label>
                <div class="col-sm-9">
                  <input type="text" class="form-control" :id="'inputIncrementBy' + item.id"
                    :value='item.config.increment'>
                </div>
              </div>
              <div class="row mb-3">
                <div class="col-sm-10">
                  <div class="form-check">
                    <label class="form-check-label" :for="'gridCheck1' + item.id">
                      Reminder
                    </label>
                    <input class="form-check-input" type="checkbox" :id="'gridCheck1' + item.id" :checked="item.config.reminder">
                  </div>
                </div>
              </div>
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
    }
  }
</script>

<style scoped>

</style>