<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>InstaFake2.0</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar> </ion-toolbar>
      </ion-header>

      <IonHeader />
      <IonCard v-for="img in imagens">
        <img :src="img.download_url" />
        <ion-card-title>
          {{img.author }}
        </ion-card-title>
      </IonCard>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonTitle,
  IonContent,
  IonCard,
  IonCardContent,
  IonCardHeader,
  IonCardSubtitle,
  IonCardTitle,
} from "@ionic/vue";
import { ref } from "vue";

export default {
  name: "ImagesBonitinhas ",
  components: {
    IonPage,
    IonHeader,
    IonToolbar,
    IonTitle,
    IonContent,
    IonCard,
    IonCardContent,
    IonCardHeader,
    IonCardSubtitle,
    IonCardTitle,
  },
  setup() {
    const imagens = ref();

    async function pegarImagens() {
      let resp = await fetch("https://picsum.photos/v2/list");
      let respJson = await resp.json();
      imagens.value = respJson;
    }
    return {
      imagens,
      pegarImagens,
    };
  },

  mounted() {
    this.pegarImagens();
  }
}
</script>
