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
        <div style="text-align: center">
          <ion-chip color="secondary" @click="share">
            <ion-icon icon="share-social" color="secondary"></ion-icon>
            <ion-label>Share Capacitor</ion-label>
          </ion-chip>
        </div>
        <div style="text-align: center">
          <ion-chip color="warning" @click="shareViaWebShare">
            <ion-icon icon="share-social" color="warning"></ion-icon>
            <ion-label>Web Share API</ion-label>
          </ion-chip>
        </div>
        <div style="text-align: center">
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
  IonLabel,
  IonCard,
  IonChip,
  IonIcon,
} from "@ionic/vue";
import { defineComponent } from "vue";
import { Share } from "@capacitor/share";

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
  computed: {
    webShareApiSupported() {
      return navigator.share;
    },
  },
  methods: {
    async share() {
      Share.canShare().then((canShare) => {
        if (canShare) {
          Share.share({
            title: "Save & Share Plugin",
            text: "Save & Share Plugin",
            url: "https://capacitor.ionicframework.com",
            dialogTitle: "Save & Share Plugin",
          });
        } else {
          alert("Share API not supported");
        }
      });
    },
    save() {
      const downloadLink = document.createElement("a");
      downloadLink.href = image;
      downloadLink.download = "websiteQRCode_noFrame.png";
      downloadLink.click();
    },
    shareViaWebShare() {
      let data = {
          title: "Web Share API",
          text: "Supported",
          url: "URL to be shared",
        }
      if (navigator.canShare(data)) {
        navigator.share(data)
      } else {
        alert("Not supported for this browser");
      }
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
