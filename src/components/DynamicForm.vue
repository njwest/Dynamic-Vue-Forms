<template>
  <div class="card">
    <div class="card-body">
      <b-form
        v-on:submit.prevent="onSubmit"
      >
        <template v-for="question in questions">
          <b-form-group
            :label="question.label"
            v-bind:key="question.model">
              <b-form-input
                v-if="question.type === 'TEXT'"
                type="text"
                :v-model="question.model"
                :id="question.model"
                @input="formInput(question.model, $event)"
                class="mb-4 border"
                size="lg"
                autocomplete="off"
                :required="question.required ? true : false"
              >
              </b-form-input>

              <b-form-input
                v-if="question.type === 'NUMBER'"
                type="number"
                :v-model="question.model"
                :id="question.model"
                @input="formInput(question.model, $event)"
                :min="question.min ? question.min : 0"
                size="lg"
                :required="question.required ? true : false"
              >
            </b-form-input>
          </b-form-group>
        </template>

        <slot name="buttons">
        </slot>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DynamicForm',
  props: {
    questions: Array,
    onSubmit: Function
  },
  methods: {
    formInput(key, value) {
      console.log(`Key: ${key}, Value: ${value}`)
      this.$emit(`update:${key}`, value)
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card{
  max-width: 700px;
  margin: 0em auto;
}
.card-body{
  max-width: 400px;
  margin: 0em auto;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
