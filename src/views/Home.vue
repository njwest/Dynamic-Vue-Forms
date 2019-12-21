<template>
  <div class="home container">
    <div class="row">
      <div class="col-8">
        <DynamicForm
          v-bind.sync="form"
          :questions="questions"
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
      ]
    }
  },
  beforeMount(){
    let questionArray = this.questions

    for(var i = 0; i < questionArray.length; i++){
      this.form[questionArray[i].model] = questionArray[i].defaultValue ? questionArray[i].defaultValue : ''
    }
  },
  methods: {
    onSubmit(){
      console.log(this.form)
    }
  }
}
</script>
