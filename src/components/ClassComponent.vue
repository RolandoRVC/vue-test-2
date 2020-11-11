<template>
  <v-container class="mt-5">
    <v-card elevation="4" shaped tile>
      <v-container>
        <p>Component</p>
        <v-text-field
        label="Test Input"
        :value="Hello"
        @input="updateMyProperty($event)"
        ></v-text-field>

        <p>Watch</p>
        <v-text-field
        type="number"
        label="¿Cuando es 2 + 2?"
        :value="0"
        @input="changeSumaValue($event)"
        ></v-text-field>
      </v-container>
    </v-card>
    <br>
    <p class="mb-0">Value:</p>
    <span>{{ Hello }}</span>
    <p class="mt-2 mb-0">Props:</p>
    <span>{{ exampleProperty }}</span>
    <p class="mt-2 mb-0">Computed Props</p>
    <span>{{ myComputedProp }}</span>
    <p class="mt-2 mb-0">Watch:</p>
    <span class="pr-5" v-if="SumaValue"> Value {{ SumaValue }}</span> <br>
    <span v-if="SumaOldValue"> Old Value {{ SumaOldValue }}</span>
  </v-container>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop, Watch } from "vue-property-decorator";

@Component
export default class ClassComponent extends Vue {
  Hello = "";
  Suma = 0;
  SumaValue: any = "";
  SumaOldValue : any = "";


  @Prop({ default: "Example" })
  exampleProperty?: string;
  @Watch("Suma")
  onPropertyChanged(value: string, oldValue: string) {
    this.SumaValue = value;
    this.SumaOldValue = oldValue;
    if (parseInt(value) === 4){
      alert("Correcto");
    }
  }
  // Data property
  // Lifecycle hook

  mounted() {
    this.Hello = "Hello";
    console.log(this.Hello);
  }
  // Component method
  updateMyProperty($event?: any) {
    this.Hello = $event;
  }
  changeSumaValue($event?: any){
    this.Suma = $event
  }
  get myComputedProp() {
    return Math.random();
  }
}
</script>
