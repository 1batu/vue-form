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
              <div class="form-group">
                <label for="exampleInputEmail1"
                  >Form Bulunacak Eleman Sayısı</label
                >
                <input
                  type="number"
                  class="form-control"
                  v-model="formElementCount"
                  placeholder="Eleman Sayısı"
                  @change="reproduce"
                />
              </div>
            </div>
          </div>
          <div class="card" style="margin-top: 3px">
            <div class="card-body">
              <div class="col-md-12 d-flex justify-content-center">
                <h2>Form Elemanları</h2>
              </div>
              <div class="col-md-12" v-for="(i, index) in schema" :key="index">
                <div class="card" v-if="i.label">
                  <div class="card-body">
                    <div class="form-group">
                      <label for="exampleInputEmail1"
                        >{{ index }}. Form Elemanı Başlık</label
                      >
                      <input
                        type="text"
                        class="form-control"
                        :id="'baslik' + index"
                        @change="dataChange('baslik' + index, index, 'label')"
                        placeholder="baslik"
                      />
                    </div>
                  </div>
                </div>
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
      formElementCount: [],
      model: {
        values: {},
      },
      schema: [
        {
          component: "h3",
          children: "",
        },
      ],
    };
  },
  watch: {},
  methods: {
    reproduce() {
      this.formElementCount = parseInt(this.formElementCount);
      this.createFormElemet();
    },
    createFormElemet() {
      let count = 1;
      while (count <= this.formElementCount) {
        this.schema.push({
          label: "Your name",
          name: "name",
          validation: "required",
        });
        count++;
      }
    },
    dataChange(key, id, type) {
      let idChangeValue = document.getElementById(key).value;
      this.schema[id][type] = idChangeValue;
      this.schema[id]["name"] = idChangeValue;
    },
  },
};
</script>
