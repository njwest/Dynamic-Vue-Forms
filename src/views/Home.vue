<template>
  <div class="home container">
    <div class="row">
      <div class="col-8">
        <DynamicForm
          v-bind.sync="form"
          :questions="questions"
          :answers="answers"
          :onSubmit="onSubmit"
        >
          <template slot="buttons">
            <b-button
              variant="info"
              type="submit"
              size="lg"
              block
            >
              Submit
            </b-button>
          </template>
        </DynamicForm>
      </div>

      <div class="col-4">
        {{form}}
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import DynamicForm from '@/components/DynamicForm.vue'

export default {
  name: 'home',
  components: {
    DynamicForm
  },
  data(){
    return {
      form: {},
      questions: [
        {
          "type": "TEXT",
          "label": "Name",
          "model": "name"
        },
        {
          "type": "NUMBER",
          "label": "Age",
          "model": "age"
        }
      ],
      answers: {
        "name": "Chan Tai Man"
      }
    }
  },
  beforeMount(){
    let questionArray = this.questions

    for(var i = 0; i < questionArray.length; i++){
      var valueToSet;
      // var

      if(this.answers[questionArray[i].model]){
        valueToSet = this.answers[questionArray[i].model]
      } else{
        valueToSet = questionArray[i].defaultValue ? questionArray[i].defaultValue : ''
      }

      this.$set(this.form, questionArray[i].model, valueToSet)
    }
  },
  methods: {
    onSubmit(){
      console.log(this.form)
    }
  }
}
</script>
