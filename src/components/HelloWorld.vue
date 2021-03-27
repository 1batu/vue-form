<template>
  <div class="hello">
    <div class="col-md-12">
      <div class="row">
        <div class="col-md-6">
          <div class="card">
            <div class="card-body">
              <div class="form-group">
                <label for="exampleInputEmail1">Form Adı</label>
                <input
                  type="text"
                  class="form-control"
                  v-model="schema[0].children"
                  placeholder="Form Adı"
                />
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="card">
            <div class="card-body">
              <FormulateForm v-model="model.values" :schema="schema" />
              {{ model.values }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {},
  data() {
    return {
      model: {
        values: {},
      },
      schema: [
        {
          component: "h3",
          children: "",
        },
        {
          label: "Your name",
          name: "name",
          validation: "required",
        },
        {
          label: "Your email",
          name: "email",
          help: "Please use your student email address",
          validation: "bail|required|email|ends_with:.edu",
          "validation-messages": {
            ends_with: "Please use a .edu email address",
          },
        },
        {
          label: "Student ID",
          name: "student_id",
          help: "Your 6 digit student ID (ex. ST-123421)",
          placeholder: "ST-",
          validation: "^required|matches:/^ST-[\\d]{6}$/",
          "validation-name": "Student ID",
        },
        {
          type: "submit",
        },
      ],
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
