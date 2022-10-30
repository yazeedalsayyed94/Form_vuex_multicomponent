<!--  eslint-disable  -->
<template>
    <textarea
    name="required" type="text"
    :value="modelValue"
    :placeholder="placeHolder"
    :maxlength="maxLength"
    @input="$emit('update:modelValue', $event.target.value)"></textarea>
</template>

<script>
/* eslint-disable */
export default {
  props: ['modelValue','placeHolder','maxLength'],
  emits: ['update:modelValue'],
};
</script>

<style>
textarea {
    width: 200px;
    height: 30px;
}
</style>