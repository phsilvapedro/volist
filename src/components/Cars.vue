<template>
    <v-container>
        <v-layout
        text-center
        wrap
        >
            <v-flex mb-6>
                <v-col class="d-flex" cols="12" sm="6">
                    <v-select
                    :items="brands"
                    label="Brands"
                    v-model="brand"
                    v-on:change="getModels"
                    dense
                    ></v-select>
                </v-col>
            </v-flex>

            <v-flex mb-6>
                <v-col class="d-flex" cols="12" sm="6">
                    <v-select
                    :items="models"
                    label="Models"
                    v-model="modelCar"
                    v-on:change="getYears"
                    dense
                    ></v-select>
                </v-col>
            </v-flex>

            <v-flex mb-6>
                <v-col class="d-flex" cols="12" sm="6">
                    <v-select
                    :items="years"
                    label="Years"
                    v-model="yearCar"
                    v-on:change="getVersions"
                    dense
                    ></v-select>
                </v-col>
            </v-flex>

            <v-flex mb-4>
                <v-col class="d-flex" cols="12" sm="6">
                    <v-select
                    :items="versions"
                    label="Versions"
                    v-model="versionCar"
                    v-on:change="getCars"
                    item-text="version"
                    item-value="versionId"
                    dense
                    ></v-select>
                </v-col>
            </v-flex>
        </v-layout>
        <v-layout>
            <v-card
                class="mx-auto"
                max-width="400"
                v-show=car
            >
                <v-img
                    class="white--text align-end"
                    height="200px"
                    :src="require('../assets/car2.jpg')"
                >
                    <v-card-title>{{car.brand}} {{car.model}} - {{car.modelYear}}</v-card-title>
                </v-img>

                <v-card-subtitle class="pb-0"> {{ car.precoMedio | currency}}</v-card-subtitle>

                <v-card-text class="text--primary">
                    <div>{{car.version}}</div>

                    <div>Kms Rodados: {{car.kmMedio}}</div>
                </v-card-text>
            </v-card>
        </v-layout>
  </v-container>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'Cars',
    data() {
      return {
        brands: [],
        models: [],
        years: [],
        versions: [],
        brand: "",
        modelCar: "",
        yearCar: "",
        versionCar: "",
        car: ""
      };
    },
    created: function() {
      axios
        .get('https://volanty-price-api.herokuapp.com/brands')
        .then(res => {
          this.brands = res.data;
        });
    },
    methods: {
        getModels() {
            axios
                .get('https://volanty-price-api.herokuapp.com/brands/' + this.brand + '/models')
                .then(res => {
                this.models = res.data;
                this.years = [];
                this.version = "";
                this.versions = [];
                this.car = "";
            });
        },

        getYears() {
            axios
                .get('https://volanty-price-api.herokuapp.com/brands/' + this.brand + '/models/' + this.modelCar + '/years')
                .then(res => {
                this.years = res.data;
                this.version = "";
                this.versions = [];
                this.car = "";
            });
        },

        getVersions() {
            axios
                .get('https://volanty-price-api.herokuapp.com/brands/' + this.brand + '/models/' + this.modelCar + '/years/' + this.yearCar + '/versions')
                .then(res => {
                this.versions = res.data;
                this.car = "";
            });
        },

        getCars() {
            axios
                .get('https://volanty-price-api.herokuapp.com/brands/' + this.brand + '/models/' + this.modelCar + '/years/' + this.yearCar + '/versions/' + this.versionCar)
                .then(res => {
                this.car = res.data;
            });
        },

    }
  }
</script>