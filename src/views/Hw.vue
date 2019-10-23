<template>
<div>
  <base-header type="gradient-success" class="pb-6 pb-8 pt-5"><h1 class="text-white">Hand Washing Audit</h1>
  </base-header>
  <div class="container-fluid mt--7">
    <div class="card shadow" :class="type === 'dark' ? 'bg-default': ''">
      <div class="card-body">
        <base-alert type="success" dismissible v-show="hw.success">
            <span class="alert-inner--icon"><i class="ni ni-like-2"></i> </span>
            <span class="alert-inner--text"><strong>Success!</strong> Audit Has Been Saved</span>
            <button type="button" class="close" data-dismiss="alert" aria-label="Close">
                <span aria-hidden="true">&times;</span>
            </button>
        </base-alert>
        <form @submit.prevent="hwSubmit">
            <input type="hidden" name="_token" value="keUsQYFEG8fTRw0Ach8crdupdRyhCKMZ7fDoRFyh">            <div class="form-group" id="div_discipline">
            <h3 class="control-label requiredField" for="discipline">Discipline </h3>
            <div class="fancy-radio-group inline-radios">
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Physician" id="Physician" v-model="hw.discipline"/>
                <label class="radio-inline" for="Physician">Physician</label>
              </div>
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Nurse" id="Nurse" v-model="hw.discipline"/>
                <label class="radio-inline" for="Nurse">Nurse</label>
              </div>
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Technician" id="Technician" v-model="hw.discipline"/>
                <label class="radio-inline" for="Technician">Technician</label>
              </div>
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Student" id="Student" v-model="hw.discipline"/>
                <label class="radio-inline" for="Student">Student</label>
              </div>
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Dietitian" id="Dietitian" v-model="hw.discipline"/>
                <label class="radio-inline" for="Dietitian">Dietitian</label>
              </div>
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Social Worker" id="Social Worker" v-model="hw.discipline"/>
                <label class="radio-inline" for="Social Worker">Social Worker</label>
              </div>
              <div class="fancy-radio">
                <input name="discipline" type="radio" value="Other" id="Other" v-model="hw.discipline"/>
                <label class="radio-inline" for="Other">Other</label>
              </div>
            </div>
                        </div>
            <div class="form-group ">
            <h3 class="control-label requiredField">Opportunity Type</h3>
            <div class="fancy-radio-group">
            <div class="fancy-radio">
                <input name="opportunity_type" type="radio" value="Prior to touching a patient" id="opp_1" required v-model="hw.opp"/>
                <label class="radio" for="opp_1">1. Prior to touching a patient</label>
            </div>
            <div class="fancy-radio">
                <input name="opportunity_type" type="radio" value="Prior to aseptic procedures" id="opp_2" v-model="hw.opp"/>
                <label class="radio" for="opp_2">2. Prior to aseptic procedures</label>
            </div>
            <div class="fancy-radio">
                <input name="opportunity_type" type="radio" value="After body fluid exposure risk" id="opp_3" v-model="hw.opp"/>
                <label class="radio" for="opp_3">3. After body fluid exposure risk</label>
            </div>
            <div class="fancy-radio">
                <input name="opportunity_type" type="radio" value="After touching a patient" id="opp_4" v-model="hw.opp"/>
                <label class="radio" for="opp_4">4. After touching a patient</label>
            </div>
            <div class="fancy-radio">
                <input name="opportunity_type" type="radio" value="After touching patient surroundings" id="opp_5" v-model="hw.opp"/>
                <label class="radio" for="opp_5">5. After touching patient surroundings</label>
            </div>
            </div>
                        </div>
            <div class="form-group" id="div_opportunity_performed">
            <h3 class="control-label requiredField" for="opportunity_performed">Was Opportunity Performed Correctly</h3>
            <div class="radio-yes-no fancy-radio-group">
              <div class="radio-yes fancy-radio">
                <input name="opportunity_performed" type="radio" value="Yes" id="opportunity_performed_yes" required v-model="hw.performed"/>
                <label class="radio-inline" for="opportunity_performed_yes">Yes</label>
              </div>
              <div class="radio-no fancy-radio">
                <input name="opportunity_performed" type="radio" value="No" id="opportunity_performed_no" v-model="hw.performed"/>
                <label class="radio-inline" for="opportunity_performed_no">No</label>
              </div>
            </div>
                        </div>
            <div class="form-group ">
            <h3 class="control-label " for="description">Description of Activity</h3>
            <textarea class="form-control" cols="40" id="description" name="description" rows="10" required v-model="hw.desc"></textarea>
                        </div>
            <div class="form-group">
            <div>
            <button class="btn btn-primary " name="submit" type="submit">Submit</button>
            </div>
            </div>
          </form>

      </div>
    </div>
  </div>
</div>
</template>
<script>
  export default {
    name: 'hw',
    data() {
      return {
        hw: {
          discipline: '',
          opp: '',
          performed: '',
          desc: '',
          success: ''
        }
      }
    },
    methods: {
      hwSubmit: function() {
        this.hw.discipline = '';
        this.hw.opp = '';
        this.hw.performed = '';
        this.hw.desc = '';
        this.hw.success = 1;
      }
    }
  };
</script>
<style lang="scss">

  .fancy-radio {
    padding:0 5px;
  }

  .inline-radios .fancy-radio, .radio-yes-no .fancy-radio  {
    display:inline-block;
  }

  .fancy-radio label {
    border:1px solid #aaa;
    border-radius:4px;
    padding:2px 8px;
    cursor:pointer;

    &:hover {
      box-shadow:0 0 4px #005CAC;
    }
  }

  .fancy-radio input[type=radio] {
    width: 0; height: 0; position: absolute; left: -9999px;
  }

  .fancy-radio input[type=radio]:checked + label {
    background:#005CAC;
    border-color:#005CAC;
    color:#fff;
  }

  .radio-yes-no .fancy-radio{
    padding:0;
  }

  .radio-yes-no .radio-no label {
    border-left:none;
    border-radius:0 4px 4px 0;
  }

.radio-no input[type=radio]:checked + label {
    background-color: #992626;
  }

  .radio-yes-no .radio-yes label {
    border-radius:4px 0 0 4px;
  }
</style>
