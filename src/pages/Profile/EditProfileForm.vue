<template>
  <card>
    <h5 slot="header" class="title">Custom Chart</h5>
    <div class="row">
      <div class="col-md-5 pr-md-1">
        <base-input label="Title"
                  placeholder="Title"
                  >
        </base-input>
      </div>
      <div class="col-md-3 px-md-1">
        <base-input label="SubTitle"
                  placeholder="SubTitle"
                  >
        </base-input>
      </div>
      <div class="col-md-4 pl-md-1">
        <base-input label="Units of Measurement"
                  type="email"
                  placeholder="Units of Measurement">
        </base-input>
      </div>
    </div>
    <div class="row">
      <div class="col-md-6 pr-md-1">
        <base-input label="X Axis"
                  placeholder="X Axis">
        </base-input>
      </div>
      <div class="col-md-6 pl-md-1">
        <base-input label="Y Axis"
                  placeholder="Y Axis">
        </base-input>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <base-input label="Type of Chart"
                  placeholder="Line, Bar, Radar, Bubble, Doughnut, Pie, Polar">
        </base-input>
      </div>
    </div>
    <div class="row">
      <div class="col-md-4 pr-md-1">
        <base-input label="Color"
                  v-model="model.Color"
                  placeholder="ROYGBIV">
        </base-input>
      </div>
      <div class="col-md-4 px-md-1">
        <base-input label="Labels"
                  v-model="model.Labels"
                  placeholder="['example', 'list']">
        </base-input>
      </div>
      <div class="col-md-4 pl-md-1">
        <base-input label="Dataset"
                  placeholder="Z://file.repository.index">
        </base-input>
      </div>
    </div>
    <div class="row">
      <div class="col-md-8">
        <base-input>
          <label>Description</label>
          <textarea rows="4" cols="80"
                    class="form-control"
                    placeholder="Here can be your description"
                    v-model="model.about">

              </textarea>
        </base-input>
      </div>
    </div>
    <base-button slot="footer" type="primary" fill>Create</base-button>
  </card>
</template>
<script>
  export default {
    props: {
      model: {
        type: Object,
        default: () => {
          return {};
        }
      }
    }
  }
</script>
<style>
</style>
