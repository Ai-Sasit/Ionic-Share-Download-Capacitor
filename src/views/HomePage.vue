<template>
  <ion-page>
    <ion-header mode="ios" :translucent="true">
      <ion-toolbar>
        <ion-title>Save & Share Plugin</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-list>
        <ion-card mode="ios">
          <img src="../assets/websiteQRCode_noFrame.png" />
        </ion-card>
        <div style=" text-align: center;">
          <ion-chip color="secondary" style="margin-right: 3rem;" @click="share">
            <ion-icon icon="share-social" color="secondary" ></ion-icon>
            <ion-label>Share</ion-label>
          </ion-chip>
          <ion-chip color="success" @click="save">
            <ion-icon icon="arrow-down" color="success"></ion-icon>
            <ion-label>Save</ion-label>
          </ion-chip>
        </div>
      </ion-list>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonList,
  IonItem,
  IonLabel,
  IonCard,
  IonChip,
  IonIcon,
} from "@ionic/vue";
import { defineComponent } from "vue";
import { Share } from "@capacitor/share";
import { Filesystem, Directory } from "@capacitor/filesystem";
/* tslint:disable no-var-requires */
/* eslint @typescript-eslint/no-var-requires: "off" */
const image = require("../assets/websiteQRCode_noFrame.png");

export default defineComponent({
  name: "HomePage",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonList,
    IonLabel,
    IonCard,
    IonChip,
    IonIcon,
  },
  data() {
    return {
      image,
    };
  },
  methods: {
    async share() {
      await Share.share({
        title: "Share This QR Code",
        text: "This is a test of the Capacitor Share Plugin",
        url: "https://capacitor.ionicframework.com",
        dialogTitle: "Share Plugin",
      });
    },
    save() {
      const downloadLink = document.createElement("a");
      downloadLink.href = image;
      downloadLink.download = "websiteQRCode_noFrame.png";
      downloadLink.click();
    },
  },
});
</script>

<style scoped>
#container {
  text-align: center;

  position: absolute;
  left: 0;
  right: 0;
  top: 50%;
  transform: translateY(-50%);
}

#container strong {
  font-size: 20px;
  line-height: 26px;
}

#container p {
  font-size: 16px;
  line-height: 22px;

  color: #8c8c8c;

  margin: 0;
}

#container a {
  text-decoration: none;
}

.center {
  display: flex;
  justify-content: center;
  align-content: center;
  align-items: center;
  width: 50%;
}
</style>
