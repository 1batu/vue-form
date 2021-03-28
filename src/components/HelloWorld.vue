<template>
  <div class="hello">
    <div class="col-md-12">
      <div class="row">
        <div class="col-md-6">
          <div class="col-md-12 d-flex justify-content-center">
            <h2>DEMO FORM BUILD</h2>
          </div>
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
          <div class="card" style="margin-top: 3px" v-if="formStatus">
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
                        placeholder="Başlık"
                      />
                    </div>
                    <div class="form-group">
                      <label for="exampleInputEmail1"
                        >{{ index }}. Form Elemanı İçerik</label
                      >
                      <select
                        class="form-control"
                        :id="'icerik' + index"
                        @change="
                          dataTypeChange('icerik' + index, index, 'type')
                        "
                      >
                        <option
                          v-for="data in dataType"
                          :key="data.name"
                          :value="data.name"
                        >
                          {{ data.value }}
                        </option>
                      </select>
                    </div>
                  </div>
                </div>
              </div>
              <div class="col-md-12" v-if="schema.length > 1">
                <div class="card">
                  <div class="card-body">
                    <button class="btn btn-primary" @click="formButtonAdd">
                      Formu Tamamla
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <div class="col-md-12 d-flex justify-content-center">
            <h2>DEMO FORM VIEW</h2>
          </div>
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
      formStatus: true,
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
      dataType: [
        {
          name: "text",
          value: "Yazı",
        },
        {
          name: "password",
          value: "Şifre",
        },
        {
          name: "email",
          value: "Mail",
        },
        {
          name: "date",
          value: "Tarih",
        },
        {
          name: "textarea",
          value: "Uzun Metin",
        },
        {
          name: "checkbox",
          value: "Seçme İsteği",
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
          type: "text",
        });
        count++;
      }
    },
    dataChange(key, id, type) {
      let idChangeValue = document.getElementById(key).value;
      this.schema[id][type] = idChangeValue;
      this.schema[id]["name"] = idChangeValue;
    },
    dataTypeChange(key, id, type) {
      let idChangeValue = document.getElementById(key).value;
      this.schema[id][type] = idChangeValue;
    },
    formButtonAdd() {
      let verson = prompt("Form Submit Button Text", "Buton Adı");
      if (verson != null) {
        this.schema.push({
          name: "submit",
          type: "submit",
          label: verson,
        });
        this.formStatus = false;
      }
    },
  },
};
</script>
