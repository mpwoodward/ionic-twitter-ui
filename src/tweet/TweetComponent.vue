<template>
  <ion-row class="wrapper">
    <ion-col size="2">
      <ion-avatar>
        <ion-img :src="tweet.img"></ion-img>
      </ion-avatar>
    </ion-col>
    <ion-col size="10">
      <ion-row class="tweet-info">
        <ion-col size="12">
          <span class="name">{{ tweet.username }}</span>
          <span class="handle">@{{ tweet.handle }}</span>
          <span class="handle">- {{ formatDate(tweet.date) }}</span>
        </ion-col>
      </ion-row>
      <ion-row>
        <ion-col size="12">
          <div v-html="tweet.text"></div>
          <img v-if="tweet.attachment" :src="tweet.attachment" class="preview-img">
        </ion-col>
      </ion-row>
      <ion-row class="ion-justify-content-start">
        <ion-col>
          <ion-button fill="clear" color="medium" size="small">
            <ion-icon :icon="chatbubbleOutline" slot="start"></ion-icon>
            {{ tweet.response }}
          </ion-button>
        </ion-col>
        <ion-col>
          <ion-button
            fill="clear"
            :color="tweet.retweet ? 'primary' : 'medium'"
            size="small">
            <ion-icon :icon="repeatOutline" slot="start"></ion-icon>
            {{ tweet.retweets }}
          </ion-button>
        </ion-col>
        <ion-col>
          <ion-button
            fill="clear"
            :color="tweet.liked ? 'primary' : 'medium'"
            size="small"
          >
            <ion-icon :icon="heartOutline" slot="start"></ion-icon>
            {{ tweet.like }}
          </ion-button>
        </ion-col>
        <ion-col>
          <ion-button fill="clear" color="medium" size="small">
            <ion-icon :icon="shareOutline" slot="start"></ion-icon>
          </ion-button>
        </ion-col>
      </ion-row>
    </ion-col>
  </ion-row>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import {
  IonRow,
  IonCol,
  IonAvatar,
  IonImg,
  IonButton,
  IonIcon,
} from '@ionic/vue'
import { chatbubbleOutline, repeatOutline, heartOutline, shareOutline } from 'ionicons/icons'

defineProps({
  tweet: Object,
})

function formatDate(timestamp: number) {
  const ms = timestamp * 1000
  return new Date(ms).toLocaleDateString()
}
</script>

<style scoped>
.tweet-info {
  font-size: 0.9em;
}

.name {
  font-weight: 600;
}

.handle {
  padding-left: 4px;
  color: var(--ion-color-medium);
}

.wrapper {
  border-bottom: 1px solid var(--ion-color-light);
}

.highlight {
  color: var(--ion-color-primary);
}

.preview-img {
  border: 1px solid var(--ion-color-light);
  border-radius: 10px;
}
</style>