<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Perfil</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Perfil</ion-title>
        </ion-toolbar>
      </ion-header>
      <IonGrid>
        <IonRow>
        <IonCol size="4 "  v-for="post in imagens">
        <img class="imgPost" :src="post.url" :alt="post.name" />
        </IonCol> 
        </IonRow>
      </IonGrid>
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
  IonGrid,
  IonRow,
  IonCol,
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
    IonGrid,
    IonRow,
    IonCol,
  },
  setup() {
    const imagens = ref();

    async function pegarImagens() {
      let resp = await fetch("https://api.imgflip.com/get_memes");
      let respJson = await resp.json();
      imagens.value = respJson.data.memes;
    }
    return {
      imagens,
      pegarImagens,
    };
  },

  mounted() {
    this.pegarImagens();
  },
}
</script>
<style scoped>
.imgPost{
  height:150px;
  width:100%;
  object-fit:cover;
  margin:0;
}
</style>