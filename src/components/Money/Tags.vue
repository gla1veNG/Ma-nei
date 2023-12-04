<template>
   <div class="tags"> 
      <div class="new">
        <button @click="createTag">新增标签</button>
      </div>

      <ul class="current">
        <li v-for="tag in tagList" :key="tag.id"
        :class="{selected:selectedTags.indexOf(tag)>=0}" 
        @click="toggle(tag)">{{tag.name}}</li>
      </ul>
    </div>
</template>

<script lang="ts">
import TagHelper from "@/mixins/TagHelper";
import Vue from "vue";
import { mixins } from "vue-class-component";
import { Component} from "vue-property-decorator";

@Component
  export default class Tags extends mixins(TagHelper){
    selectedTags: string[]=[];
    get tagList(){
      return  this.$store.state.tagList;
    }
    created(){
      this.$store.commit('fetchTags');
    }

    toggle(tag:string){
      const index =this.selectedTags.indexOf(tag);
      if(index>=0){
        this.selectedTags.splice(index,1);
      }else{
        this.selectedTags.push(tag);
      }
      this.$emit('update:value',this.selectedTags);
    }
  }
</script>


<style lang="scss"  scoped>
@use "sass:math";
.tags{
  font-size: 14px;
  padding: 16px;
  flex-grow: 1;
  display: flex;
  flex-direction: column-reverse;
  background: white;
  > .current{
    display: flex;
    flex-wrap: wrap;
    > li{
      color: #ffffff;
      $bg:rgb(229, 173, 174);
      background: $bg;
      $h:24px;
      height: $h;
      line-height:$h;
      border-radius: math.div($h, 2);
      padding: 0 16px;
      margin-right: 12px;
      margin-top: 8px;

      &.selected{
        background:darken($bg,20%);
        color: #fce6b0;
      }
     }

  }
  > .new{
    padding-top: 16px;
    button{
      background: transparent;
      border: none;
      color: #999;
      border-bottom: 1px solid;
      padding: 0 3px;
    }
  }
}
</style>