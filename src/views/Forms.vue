<template>
    <div>
      <base-header type="gradient-success" class="pb-6 pb-8 pt-5">
        </base-header>
        <div class="container-fluid mt--7">
           <div class="card shadow"
            :class="type === 'dark' ? 'bg-default': ''">
            <div class="card-body">
            <tabs fill class="flex-column flex-md-row">
              <card shadow>
                  <tab-pane title="Subjective">
                      <span slot="title">
                          <i class="ni ni-circle-08" />
                          Subjective
                      </span>
                      <div>
                        <textarea class="form-control" id="subjective" rows="10" placeholder="Enter Text Here ..."></textarea>
                      </div>
                  </tab-pane>

                  <tab-pane title="Objective">
                      <span slot="title">
                          <i class="ni ni-zoom-split-in" />
                          Objective
                      </span>
                      <div>
                        <textarea class="form-control" id="subjective" rows="10" placeholder="Enter Text Here ..."></textarea>
                      </div>
                  </tab-pane>

                  <tab-pane title="Assessment">
                      <span slot="title">
                          <i class="ni ni-sound-wave" />
                          Assessment
                        </span>
                      <p>
                        <textarea class="form-control" id="Assessment" rows="10" placeholder="Enter Text Here ..."></textarea>
                      </p>
                      <base-checkbox class="mb-3" v-model="checkboxes.comorbidities">
                          Check if patient has multiple comorbitiies
                      </base-checkbox>
                  </tab-pane>
                  <tab-pane  title="Plan">
                      <span slot="title">
                          <i class="ni ni-ruler-pencil" />
                          Plan
                        </span>
                        <h4>Plan</h4>
                        <p>
                          <textarea class="form-control" id="cultures" rows="4" placeholder="Enter Text Here ..."></textarea>
                        </p>

                        <h4>ABx Start and Stop Dates</h4>
                        <base-input addon-left-icon="ni ni-calendar-grid-58">
                          <flat-picker slot-scope="{focus, blur}"
                                      @on-open="focus"
                                      @on-close="blur"
                                      :config="{allowInput: true, mode: 'range'}"
                                      class="form-control datepicker"
                                      v-model="dates.range">
                          </flat-picker>
                        </base-input>

                        <div class="row">
                          <div class="col-lg-4">

                            <h4>ABx Route</h4>
                            <base-radio name="oral" class="mb-3" v-model="radio.abxroute">
                                Oral
                            </base-radio>
                            <base-radio name="iv" class="mb-3" v-model="radio.abxroute">
                                IV
                            </base-radio>
                          </div>
                          <div class="col-lg-4">

                            <h4>Clinical Progress</h4>
                            <base-radio name="stable" class="mb-3" v-model="radio.progress" >
                                Stable
                            </base-radio>
                            <base-radio name="improving" class="mb-3" v-model="radio.progress">
                                Improving
                            </base-radio>                   
                            <base-radio name="route" class="mb-3" v-model="radio.progress">
                                Worse
                            </base-radio>   
                          </div>  
                          <div class="col-lg-4">

                            <h4>Requiring Medical Decision Making</h4>
                            <base-radio name="moderate" class="mb-3" v-model="radio.decision" >
                                Moderate
                            </base-radio>
                            <base-radio name="high" class="mb-3" v-model="radio.decision">
                                High
                            </base-radio>                     
                          </div>  
                        </div>              

                  </tab-pane>
                  <tab-pane title="Billing">
                      <span slot="title">
                          <i class="ni ni-money-coins" />
                          Billing
                        </span>
                      
                  </tab-pane>
              </card>
          </tabs>
</div>
          </div>
      </div>
    </div>
</template>
<script>

import flatPicker from "vue-flatpickr-component";
import "flatpickr/dist/flatpickr.css";
  
  export default {
    name: 'forms',
    components: {
      flatPicker
    },
    
    data() {
        return {
          dates: {
            range: "2018-07-17 to 2018-07-19"
          },
          radio: {
            abxroute: false,
            progress: false,
            decision: false
          },
          checkboxes: {
            comorbidities: false
          }
        };
      }
  };
</script>
<style></style>