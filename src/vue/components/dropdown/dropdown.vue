<template>
  <div :class="question.cssClasses.selectWrapper">
    <select
      v-if="!question.isReadOnly"
      :id="question.inputId"
      v-model="question.renderedValue"
      v-on:click="question.onOpenedCallBack()"
      :autocomplete="question.autoComplete"
      :class="question.getControlClass()"
      :aria-required="question.ariaRequired"
      :aria-label="question.ariaLabel"
      :aria-invalid="question.ariaInvalid"
      :aria-describedby="question.ariaDescribedBy"
      :required="question.isRequired">
      <option v-if="question.showOptionsCaption" :value="undefined">{{ question.optionsCaption }}</option>
      <sv-dropdown-option-item
        v-for="item in question.visibleChoices"
        :item="item"
        :key="item.id"
      ></sv-dropdown-option-item>
    </select>
    <div disabled v-else :id="question.inputId" :class="question.getControlClass()">{{ question.readOnlyText }}</div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";
import { Question } from "survey-core";
import BaseVue from "src/vue/base";

@Component
export class DropdownComponent extends BaseVue {
  @Prop() question: Question;
}
Vue.component("sv-dropdown", DropdownComponent);
export default DropdownComponent;
</script>
