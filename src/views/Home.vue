<template>
  <ion-app>
    <ion-split-pane when="sm" content-id="main-content">
      <Menu/>
      <div class="ion-page" id="main-content">
        <ion-header :translucent="true">
          <ion-toolbar>
            <ion-buttons slot="start">
              <ion-menu-toggle>
                <ion-button>
                  <ion-icon slot="icon-only" name="menu"></ion-icon>
                </ion-button>
              </ion-menu-toggle>
            </ion-buttons>
            <ion-title>Fixer.io App</ion-title>
          </ion-toolbar>
        </ion-header>

        <ion-content class="ion-padding">
          <div class="container">
            <ion-text class="ion-text-center" color="danger"><h1>Fixer.io App</h1></ion-text>
            <Searchh/>
            <Results/>
          </div>
        </ion-content>
      </div>
    </ion-split-pane>
  </ion-app>
</template>

<script lang="ts">
import { IonContent, IonSplitPane, IonButtons, IonMenuToggle, IonHeader, IonApp, IonTitle, IonToolbar, IonText, IonButton, IonIcon } from '@ionic/vue';
import { defineComponent } from 'vue';
import Menu from '../components/Menu.vue'
import Searchh from '../components/Searchh.vue'
import Results from '../components/Results.vue'

export default defineComponent({
  name: 'Home',
  components: {
    Menu,
    Searchh,
    Results,
    IonContent,
    IonSplitPane,
    IonHeader,
    IonApp,
    IonTitle,
    IonToolbar,
    IonText,
    IonButton,
    IonIcon,
    IonButtons,
    IonMenuToggle
  },
});
</script>