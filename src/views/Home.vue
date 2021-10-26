<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
      </ion-toolbar>
    </ion-header>
<ion-content class="ion-padding">
    <v-form v-slot="{ values, errors }" @submit="onSubmit">
        <ion-item>
          <ion-label>author</ion-label>
          <v-field name="author" v-slot="{field}" :rules="email">
            <ion-input v-bind="field" name="author"></ion-input>
          </v-field>
        </ion-item>
        <v-error-message name="author" class="error" />
        <ion-item>
          <ion-label>title</ion-label>
          <v-field name="title" v-slot="{field}" :rules="isRequired">
            <ion-input v-bind="field" name="title"></ion-input>
          </v-field>
        </ion-item>
        <v-error-message name="title" class="error" />
        <ion-item>
          <ion-label>body</ion-label>
          <v-field name="body" v-slot="{field}" :rules="isRequired">
            <ion-textarea rows="4" v-bind="field" name="body"></ion-textarea>
          </v-field>
        </ion-item>
        <v-error-message name="body" class="error" />
        <p>
          <ion-button type="submit">Save Data</ion-button>
        </p>

        <div>
          <h3>values</h3>
          <pre>{{values}}</pre>
          <h3>errors</h3>
          <pre>{{errors}}</pre>
        </div>
      </v-form>
     
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import {
  IonContent,
  IonHeader,
  IonLabel,
  IonPage,IonButton,
  IonTextarea,
  IonTitle,
  IonToolbar,IonInput,IonItem,
} from "@ionic/vue";
import { defineComponent, ref } from "vue";
import * as V from "vee-validate/dist/vee-validate";
import { defineRule } from "vee-validate/dist/vee-validate";
import { email } from '@vee-validate/rules';

export default defineComponent({
  name: "Home",
  components: {
    IonContent,
    IonHeader,
    IonPage,
    IonTitle,
    IonToolbar,
    IonInput,
    IonTextarea,IonItem,
    IonLabel,IonButton,
    VField: V.Field,
    VForm: V.Form,
    VErrorMessage: V.ErrorMessage,

  },
setup()
{ 

// const formvalues = ref<any>({
//     title: "Aaron",
//     body: null,
//   });

const isRequired=(value: any) => {
  if(value){
    console.log("value is there",value);
  }
  if(!value){
    return "The value is required";
  }
  return true;
}
  const onSubmit =(data: any) => {
    alert("on submit"+JSON.stringify(data,null,2));
    console.log("Data submitted",data);
  }
  defineRule("email",email);
  return {
    onSubmit,isRequired,email,
  };
 }





});
</script>

<style scoped>
.error {
  color: red;
  font-size: smaller;
  font-style: italic;
  font-weight: 500;
  margin-top: 4px;
}
ion-item {
  --padding-start: 0px;
}
pre {
  font-size: smaller;
}
</style>
