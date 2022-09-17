<template>
  <ion-page>
    <ion-tabs>
      <ion-router-outlet></ion-router-outlet>
      <ion-tab-bar slot="bottom">
        <ion-tab-button tab="tab1" href="/tabs/tab1">
          <ion-icon :icon="homeOutline" />
        </ion-tab-button>
          
        <ion-tab-button tab="tab2" href="/tabs/tab2">
          <ion-icon :icon="searchOutline" />
        </ion-tab-button>
        
        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-badge color="primary">11</ion-badge>
          <ion-icon :icon="notificationsOutline" />
        </ion-tab-button>

        <ion-tab-button tab="tab3" href="/tabs/tab3">
          <ion-icon :icon="mailOutline" />
        </ion-tab-button>
      </ion-tab-bar>
    </ion-tabs>
  </ion-page>
</template>

<script setup lang="ts">
import { IonTabBar, IonTabButton, IonTabs, IonIcon, IonPage, IonBadge, IonRouterOutlet } from '@ionic/vue'
import { homeOutline, searchOutline, notificationsOutline, mailOutline } from 'ionicons/icons'
</script>

<style scoped>
ion-badge {
  top: 7px;
  left: calc(50% + 1px);
  font-size: 9px;
  font-weight: 500;
  border-radius: 10px;
  padding: 2px 2px 2px;
  min-width: 18px;
  min-height: 18px;
  line-height: 14px;
}
</style>