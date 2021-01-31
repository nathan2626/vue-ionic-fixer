<script>
import { IonContent, IonMenuToggle, IonHeader, IonTitle, IonToolbar, IonItem, IonIcon } from '@ionic/vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Menu',
  components: {
    IonContent,
    IonHeader,
    IonTitle,
    IonToolbar,
    IonItem,
    IonIcon,
    IonMenuToggle
  }
});
</script>

<template>
  <ion-menu content-id="main-content">
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Menu</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <ion-list>
        <ion-list-header>
          Navigation
        </ion-list-header>
        <ion-menu-toggle auto-hide="false">
          <ion-item>
            <ion-icon slot="start" name='home'></ion-icon>
            <ion-label><a style="color: #333;" href="/">Home</a></ion-label>
          </ion-item>
        </ion-menu-toggle>
      </ion-list>
    </ion-content>
  </ion-menu>
</template>