  <!--  eslint-disable  -->
<template>
  <input class="inputtext"
  name="required" type="text"
  :value="modelValue"
  :placeholder="placeHolder"
  @input="$emit('update:modelValue', $event.target.value)">
</template>

<script>
/* eslint-disable */
export default {
  props: ['modelValue','alpha','alphanum','alphdash','alphspc','btw','dec','eml','incld','num','req','placeHolder'],
  emits: ['update:modelValue'],
  watch: {
    alpha: function (val) {
      this.validationalpha(val);
    },
    alphanum: function(val) {
      this.validationalphanum(val)
    },
    alphdash: function(val){
      this.validationalphdash(val)
    },
    alphspc: function(val){
      this.validationalphspc(val)
    },
    btw: function(val){
      this.validationbtw(val)
    },
    dec: function(val){
      this.validationdec(val)
    },
    eml: function(val){
      this.validationeml(val)
    },
    incld: function(val){
      this.validationincld(val)
    },
    num: function(val){
      this.validationnum(val)
    },
    req: function (val) {
      this.validationreq(val);
    },
  },
  methods: {
    validationalpha(text){
      if(text.match(/^[A-Za-z]+$/)||text=='')
        {this.$store.state.errorsdata.alphabetic.errors=null;}
      else{this.$store.state.errorsdata.alphabetic.errors='Must be a alphabetic value';}
    },
    validationalphanum(text){
      if(text.match(/^[0-9a-zA-Z]+$/)||text=='')
        {this.$store.state.errorsdata.alphanumeric.errors=null;}
      else{this.$store.state.errorsdata.alphanumeric.errors='Must only contain letters and numbers';}
    },
    validationalphdash(text){
      if(text.match(/^[a-zA-Z0-9-_]+$/)||text=='')
        {this.$store.state.errorsdata.alphaDash.errors=null;}
      else{this.$store.state.errorsdata.alphaDash.errors='Must only contain letters, numbers, underscores or dashes';}
    },
    validationalphspc(text){
      if(text.match("^[a-zA-Z0-9 ]+$")||text=='')
        {this.$store.state.errorsdata.alphaSpace.errors=null;}
      else{this.$store.state.errorsdata.alphaSpace.errors='Must only contain letters, numbers or spaces';}
    },
    validationbtw(text){
      if(0<text && text<11||text=='')
        {this.$store.state.errorsdata.between.errors=null;}
      else{this.$store.state.errorsdata.between.errors='Must be between 1 and 10';}
    },
    validationdec(text){
      if(text.match("^\\d+(\\.\\d{0,2})$") ||text.match(/^([\d]+)(?:\.([\d]{1,2}?))?$/gm)||text=='')
        {this.$store.state.errorsdata.decimal.errors=null;}
      else{this.$store.state.errorsdata.decimal.errors='Must be a decimal with 2 points';}
    },
    validationeml(text){
      if(text.match(/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/)||text=='')
        {this.$store.state.errorsdata.email.errors=null;}
      else{this.$store.state.errorsdata.email.errors='Not a valid email';}
    },
    validationincld(text){
      if(text=='foo'|| text=='bar'||text=='')
        {this.$store.state.errorsdata.includes.errors=null;}
      else{this.$store.state.errorsdata.includes.errors= text + ' is not one of the following: foo, bar';}
    },
    validationnum(text){
      if(text.match(/^\d+$/)||text=='')
        {this.$store.state.errorsdata.numeric.errors=null;}
      else{this.$store.state.errorsdata.numeric.errors='Must be a numeric value';}
    },
    validationreq(text){
      if(text.match(/^[\s\t\r\n]*\S+/ig))
        {this.$store.state.errorsdata.required.errors=null;}
      else{this.$store.state.errorsdata.required.errors='Required';}
      },
  },
};
</script>

<style>

</style>
