<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator";

@Component({
  name: "BaseInput",
  model: {
    event: "update",
  },
})
export default class BaseInput extends Vue {
  @Prop({ required: true }) label!: string;
  @Prop({}) icon!: string;
  @Prop({}) identifier!: string;
}
</script>

<template>
  <fieldset :class="$style['c-base-input__container']">
    <!-- Adding a label for screen readers but hiding it because it's not needed for the UI -->
    <label :for="identifier" v-show="false">{{ label }}</label>
    <div :class="$style['u-flex']">
      <div :class="$style['c-base-input__icon-container']">
        <base-icon :iconName="icon" />
      </div>
      <input
        :class="$style['c-base-input__input']"
        ref="input"
        v-on="$listeners"
        @input="$emit('update', $event.target.value)"
        v-bind="{ ...$attrs, ...$props }"
        :name="identifier"
        :id="identifier"
      />
    </div>
  </fieldset>
</template>

<style lang="scss" module>
@import "@/styles";
.c-base-input__container {
  border: 0;
  padding: 0px;
}
.u-flex {
  display: flex;
}
.c-base-input__icon-container {
  width: 15%;
  background: $brown;
  height: 56px;
  display: flex;
  align-items: center;
  border-radius: 5px 5px 0px 0px;
  justify-content: center;
}
.c-base-input__input {
  width: 85%;
  height: 56px;
  box-sizing: border-box;
  border: transparent;
  border-radius: 0px 5px 5px 0px;
  padding-left: 25px;
}
</style>
