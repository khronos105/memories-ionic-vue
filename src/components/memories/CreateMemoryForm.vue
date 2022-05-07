<template>
    <form class="ion-padding" @submit.prevent="submitForm">
        <ion-list>
            <ion-item>
                <ion-label position="floating">Title</ion-label>
                <ion-input type="text" required v-model="title"/>
            </ion-item>
            <ion-item>
                <ion-thumbnail v-if="chosenImageUrl" slot="start">
                    <img :src="chosenImageUrl">
                </ion-thumbnail>
                <ion-button 
                    fill="clear"
                    type="button"
                    @click="takePhoto"
                >
                    <ion-icon slot="start" :icon="camera"></ion-icon>
                    Take photo
                </ion-button>
            </ion-item>
            <ion-item>
                <ion-label position="floating">Description</ion-label>
                <ion-textarea rows="5" v-model="description"/>
            </ion-item>
        </ion-list>
        <ion-button expand="block" type="submit">
            Store
        </ion-button>
    </form>
</template>

<script>
import { IonList, IonItem, IonLabel, IonInput, IonTextarea, IonButton, IonThumbnail, IonIcon } from '@ionic/vue'
import { camera } from 'ionicons/icons'
import { Camera, CameraSource, CameraResultType } from '@capacitor/camera'

export default {
    emits:['save-memory'],
    components: { 
      IonList,
      IonItem,
      IonLabel,
      IonInput,
      IonTextarea,
      IonButton,
      IonThumbnail,
      IonIcon
    },
    data(){
        return {
            title: '',
            description: '',
            chosenImageUrl: null,
            camera
        }
    },
    methods:{
        async takePhoto(){
            const photo = await Camera.getPhoto({
                resultType: CameraResultType.Uri,
                source: CameraSource.Camera,
                quality: 60                
            });
            this.chosenImageUrl = photo.webPath;
        },
        submitForm(){
            const memoryData = {
                title: this.title,
                imageUrl: this.chosenImageUrl,
                description: this.description
            };
            this.$emit('save-memory', memoryData);
        }
    }
}
</script>

<style>

</style>