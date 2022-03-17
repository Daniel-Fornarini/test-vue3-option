<template>
  <div :style="{ 'width': '30px', height: '30px', 'background-color': color }"></div>
</template>

<script lang="ts">
import {Options, Vue} from "vue-class-component";
import {Prop} from "vue-property-decorator";

@Options({})
export default class Color extends Vue {
  @Prop({ required: true }) person!: { user: string, role: string, color: string };

  get color() {
    return this.person.color;
  }
}
</script>