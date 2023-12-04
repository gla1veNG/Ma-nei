<template>
    <div>
      <label class="formItem">
        <span class="name">{{this.fieldName}}</span> 
        <input type="text" 
        :value="value"
        @input="onValueChange($event.target.value)"
        :placeholder="placeholder" />
      </label>
    </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop} from "vue-property-decorator";

@Component
    export default class Notes extends Vue{
     @Prop({default:''}) readonly value!:string;
      
     @Prop({required:true}) fieldName!:string;
     @Prop() placeholder?:string;

      onValueChange(value:string){
        this.$emit('update:value',value);
      }
    }
</script>

<style lang="scss" scoped>
.formItem{
  display: flex;
  font-size: 14px;
  padding-left:16px;
  align-items: center;
  .name{
    padding-right: 16px;
  }
  input{
    padding: 16px 0;
    flex-grow: 1;
    background: transparent;
    border: none;
  }
}
</style>