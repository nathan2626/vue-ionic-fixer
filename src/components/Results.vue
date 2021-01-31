<script>
// import { IonButton, IonInput, IonItem, IonIcon } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Results',
  components: {
  },
  data () {
    return {
      result: "",
      displayResult: false,
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
    }
  },
  mounted(){
    this.$bus.on('result', (result) => {
      this.displayResult = true;
      this.result = result;
    })
  },
});

</script>

<template>
  <div class="error" style="display: none;"></div>
  <div  v-if="displayResult === true" class="contentResults" id="display-div" style="display: block;">
    <div class="card-body text-center">
      <h1>{{ result }}</h1>
    </div>
  </div>
</template>