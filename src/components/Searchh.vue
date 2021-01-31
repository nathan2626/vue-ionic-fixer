<script>
import { IonButton, IonInput, IonItem, IonIcon, IonSelectOption } from '@ionic/vue';
import { defineComponent } from 'vue';
import axios from "axios";

const api_key = process.env.VUE_APP_KEY;

export default defineComponent({
  name: 'Searchh',
  components: {
    IonItem,
    IonIcon,
    IonButton,
    IonInput,
    IonSelectOption
  },
  data () {
    return {
      devise1 : "",
      devise2 : "",
      result: "",
      allDevise: [],
      newAllDevise: [],
    }
  },
  methods: {
    displayError(msg){
      const toast = document.createElement('ion-toast');
      toast.message = msg;
      toast.duration = 3000;
      toast.color = "danger";
      document.body.appendChild(toast);
      return toast.present();
    },
    convertEURTo() {
      if (!this.devise1) {
       this.displayError("Aucune valeur rentrée en EUR !")
      }
      if (!this.devise2) {
        this.displayError("Aucune valeur rentrée en convertion !")
      }
      axios
          .get(
              `http://data.fixer.io/api/latest?access_key=${api_key}`
          )
          .then((response) => {
            this.allDeviseForComparation = response.data.rates;
            // console.log(this.allDeviseForComparation);
            for (let [key, value] of Object.entries(this.allDeviseForComparation)) {

               // console.log(key, value);
              /************************/
              //COMPARAISON
              /************************/
              if (key === this.devise2){
                 // console.log("IAIAIAIAIAIAIAIA " + key,value, this.devise2)
                 // console.log("Result = " + (value) + this.devise1);
                 this.devise2 = value + ' ' + key;
                 console.log(this.devise2);
               }

            }
            /************************/
            //RESULT
            /************************/
            // console.log(this.devise1 + ' et ' + this.devise2)

            this.result = parseFloat(this.devise1 ) * parseFloat(this.devise2);
            // console.log(this.result);
            // console.log(typeof this.result);

            /************************/
            //EMIT
            /************************/
            if (!isNaN(this.result)) {
              this.$bus.emit("result", this.result);
            }
          })
          .catch((error) => {
            console.log(error);
          })
    }
  },
  mounted () {
    axios
        .get(
            `http://data.fixer.io/api/symbols?access_key=${api_key}`
        )
        .then((response) => {
          this.allDevise = response.data.symbols;
        })
        .catch((error) => {
          console.log(error);
        })
  },
});
</script>

<template>
  <form @submit.prevent="convertEURTo">
    <ion-item style="margin-bottom: 55px;">
      <ion-input v-model="devise1" id="value1" placeholder="Montant en EUR" position="fixed" clear-input></ion-input>
    </ion-item>
    <ion-item>
      <ion-label>Choisir une devise</ion-label>
      <ion-select :value="devise2"
                  @ionChange="devise2= $event.target.value">
        <ion-select-option v-for="(deviseKey, deviseValue) in allDevise" :key="deviseKey" :value="deviseValue">{{ deviseValue + ' : ' + deviseKey }}</ion-select-option>
      </ion-select>
    </ion-item>
    <ion-button id="buttonCity" type="submit" class="button">
      <ion-icon  name="search-outline"></ion-icon>
    </ion-button>
  </form>
</template>