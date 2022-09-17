<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-buttons slot="start">
          <ion-icon slot="icon-only" :icon="menuOutline"></ion-icon>
        </ion-buttons>
        
        <ion-title>
          <ion-icon :icon="logoTwitter" color="primary" size="large"></ion-icon>
        </ion-title>

        <ion-buttons slot="end">
          <ion-button>
            <ion-icon slot="icon-only" :icon="pulseOutline"></ion-icon>
          </ion-button>
        </ion-buttons>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-segment v-model="segment" mode="md" @ionChange="segmentChanged($event)">
        <ion-segment-button value="home">
          <ion-label>Home</ion-label>
        </ion-segment-button>
        <ion-segment-button value="content">
          <ion-label>cr-content-suggest</ion-label>
        </ion-segment-button>
      </ion-segment>

      <swiper
        :slides-per-view="4.5"
        :space-between="10"

      >
        <swiper-slide v-for="(tweet, index) in tweets" :key="index">
          <ion-avatar>
            <img :src="tweet.img" />
          </ion-avatar>
        </swiper-slide>
      </swiper>

      <div v-if="segment === 'home'">
        <div v-for="(tweet, index) in tweets" :key="index">
          <TweetComponent :tweet="tweet" />
        </div>
      </div>

      <div v-if="segment === 'content'">
        CONTENT CONTENT!
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { onMounted, reactive, ref } from 'vue'
import {
  IonPage,
  IonHeader,
  IonToolbar,
  IonContent,
  IonTitle,
  IonButtons,
  IonButton,
  IonIcon,
  IonSegment,
  IonSegmentButton,
  IonLabel,
  IonAvatar,
} from '@ionic/vue'
import { menuOutline, logoTwitter, pulseOutline } from 'ionicons/icons'
import { Swiper, SwiperSlide } from 'swiper/vue'
import TweetComponent from '@/tweet/TweetComponent.vue'

import 'swiper/css'
import '@ionic/vue/css/ionic-swiper.css'

const tweets = reactive([])
const segment = ref('home')
const segmentChanged = (e: CustomEvent) => {
  segment.value = e.detail.value
}

onMounted(async () => {
  const res = await fetch('https://devdactic.fra1.digitaloceanspaces.com/twitter-ui/tweets.json')
  const tweetsRes = await res.json()
  tweetsRes.tweets.forEach((tweet: any) => {
    tweets.push(tweet)
  })
})
</script>

<style scoped>
ion-toolbar {
  --border-style: none;
}

ion-header {
  background: #fff;
}

.swiper {
  padding-top: 8px;
  padding-bottom: 8px;
  border-bottom: 1px solid var(--ion-color-light);
}

ion-segment-button {
  text-transform: none;
}

ion-segment {
  z-index: 10;
  background: #fff;
}

ion-avatar {
  border: 2px solid var(--ion-color-primary);
  padding: 2px;
}
</style>
