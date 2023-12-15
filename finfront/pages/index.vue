<template>
  <v-row justify="center" align="center">
    <v-col cols="8" sm="8" md="8">
      <li v-for="listoforg in this.listoforg" :key="listoforg.bin" style="list-style-type: none">
        <v-card style="margin-top: 20px">
          <v-row style="display: flex; justify-content: normal; background-color: aliceblue">
            <div class="img" style="margin: 10px"><img :src="listoforg.image_url"/></div>
            <div style="margin: 10px; font-size: 25px; font-family: sans-serif">{{ listoforg.full_name }}</div>
            <v-tabs
              v-model='tab'
              centered
              background-color='transparent'
              color='black'
              style='-webkit-text-fill-color: black'
            >
              <v-tabs-slider color='black'></v-tabs-slider>
              <v-tab
                v-for='item in items'
                :key='item'
                style='font-size: small'>
                {{ item }}
              </v-tab>

            </v-tabs>
            <v-tabs-items v-model='tab' style='background-color: aliceblue'>
              <v-tab-item>
                <v-div style='background-color: aliceblue; margin: 20px'>
                  <v-row style=' margin: 20px'>
                    <strong>Председатель Совета директоров:  </strong> <hr> {{ listoforg.chairman}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Совет директоров:</strong> <hr>  {{ listoforg.heads}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Члены Правления:</strong> <hr>  {{ listoforg.members}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Главный бухгалтер:</strong> <hr>  {{ listoforg.accountant}}
                  </v-row>
                </v-div>
              </v-tab-item>
              <v-tab-item>
                <v-div style='background-color: aliceblue; margin: 20px'>
                  <v-row style=' margin: 20px'>
                    <strong>Веб-Сайт:</strong> <hr>   {{ listoforg.web_site}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Телефон:</strong> <hr>   {{ listoforg.phone}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Электронная почта:</strong> <hr>   {{ listoforg.email}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Адрес:</strong> <hr>   {{ listoforg.address}}
                  </v-row>
                </v-div>
              </v-tab-item>
              <v-tab-item>
                <v-div style='background-color: aliceblue; margin: 20px'>
                  <v-row style=' margin: 20px'>
                    <strong>Веб-Сайт:</strong> <hr>  {{ listoforg.web_site}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Телефон:</strong> <hr>  {{ listoforg.phone}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Электронная почта:</strong> <hr>  {{ listoforg.email}}
                  </v-row>
                  <v-row style=' margin: 20px'>
                    <strong>Адрес:</strong> <hr>  {{ listoforg.address}}
                  </v-row>
                </v-div>
              </v-tab-item>
            </v-tabs-items>
          </v-row>
        </v-card>
      </li>
    </v-col>
  </v-row>
</template>

<script>
import {list} from "postcss";

export default {
  name: 'IndexPage',
  computed: {
    list() {
      return list
    }
  },
  data: vm => ({
    listoforg: '',
    tab: null,
    items: [
      'Кадры', 'Контактная информация', 'Банк'
    ],
  }),
  created() {
    this.getInfo()
  },
  methods: {
    async getInfo(){
      this.listoforg = await this.$axios.$get('http://localhost:8000/api/financial-organizations/')
      console.log(this.listoforg)
    }
  }
}
</script>

<style>
img {
  border-radius: 10%;
}
</style>
