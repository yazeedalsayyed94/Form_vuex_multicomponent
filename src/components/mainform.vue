<template>
  <!--  eslint-disable  -->
    <h1>Form</h1>
    <form @submit="Submitform">
      <p>
        <label for="alphabetic">Alphabetic</label>
        <input_field
        class="inputtext"
        v-model="formdata.alphabetic"
        :alpha="formdata.alphabetic"
        :placeHolder="Object.keys(formdata)[0]"
        :class="{errorborder : this.$store.state.errorsdata.alphabetic.errors}"
        @change="this.$store.state.errorsdata.alphabetic.touched = true"/>
        <span class="errormsg">{{this.$store.state.errorsdata.alphabetic.errors}}</span>
      </p>
      <p>
        <label for="alphanumeric">Alphanumeric</label>
        <input_field
        class="inputtext"
        v-model="formdata.alphanumeric"
        :alphanum="formdata.alphanumeric"
        :placeHolder="Object.keys(formdata)[1]"
        :class="{errorborder : this.$store.state.errorsdata.alphanumeric.errors}"
        @change="this.$store.state.errorsdata.alphanumeric.touched = true"/>
        <span class="errormsg">{{this.$store.state.errorsdata.alphanumeric.errors}}</span>
      </p>
      <p>
        <label for="alphaDash">Alphanumeric Dash</label>
        <input_field
        class="inputtext"
        v-model="formdata.alphaDash"
        :alphdash="formdata.alphaDash"
        :placeHolder="Object.keys(formdata)[2]"
        :class="{errorborder : this.$store.state.errorsdata.alphaDash.errors}"
        @change="this.$store.state.errorsdata.alphaDash.touched = true"/>
        <span class="errormsg">{{this.$store.state.errorsdata.alphaDash.errors}}</span>
      </p>
      <p>
        <label for="alphaSpace">Alphanumeric Space</label>
        <input_field
        class="inputtext"
        v-model="formdata.alphaSpace"
        :alphspc="formdata.alphaSpace"
        :placeHolder="Object.keys(formdata)[3]"
        :class="{errorborder : this.$store.state.errorsdata.alphaSpace.errors}"
        @change="this.$store.state.errorsdata.alphaSpace.touched = true"/>
        <span class="errormsg">{{this.$store.state.errorsdata.alphaSpace.errors}}</span>
      </p>
      <p>
        <label for="between">Between</label>
        <input_field
        class="inputtext"
        v-model="formdata.between"
        :btw="formdata.between"
        :placeHolder="Object.keys(formdata)[4]"
        :class="{errorborder : this.$store.state.errorsdata.between.errors}"
        @focus.once="validationtouchbetween"/>
        <span class="errormsg">{{this.$store.state.errorsdata.between.errors}}</span>
      </p>
      <p>
        <label for="decimal">Decimal</label>
        <input_field
        class="inputtext"
        v-model="formdata.decimal"
        :dec="formdata.decimal"
        :placeHolder="Object.keys(formdata)[5]"
        :class="{errorborder : this.$store.state.errorsdata.decimal.errors}"
        @change="this.$store.state.errorsdata.decimal.touched = true"/>
        <span class="errormsg">{{this.$store.state.errorsdata.decimal.errors}}</span>
      </p>
      <p>
        <label for="email">Email</label>
        <input_field
        class="inputtext"
        :eml="formdata.email"
        :placeHolder="Object.keys(formdata)[6]"
        :class="{errorborder : this.$store.state.errorsdata.email.errors}"
        v-model="formdata.email"
        @focus.once="validationtouchemail"/>
        <span class="errormsg">{{this.$store.state.errorsdata.email.errors}}</span>
      </p>
      <p>
        <label for="includes">Includes</label>
        <input_field
        class="inputtext"
        :incld="formdata.includes"
        :placeHolder="Object.keys(formdata)[7]"
        :class="{errorborder : this.$store.state.errorsdata.includes.errors}"
        v-model="formdata.includes"
        @focus.once="validationtouchincludes"/>
        <span class="errormsg">{{this.$store.state.errorsdata.includes.errors}}</span>
      </p>
      <p>
        <label for="numeric">Numeric</label>
        <input_field
        class="inputtext"
        :num="formdata.numeric"
        :placeHolder="Object.keys(formdata)[8]"
        :class="{errorborder : this.$store.state.errorsdata.numeric.errors}"
        v-model="formdata.numeric"
        @focus.once="validationtouchnumeric"/>
        <span class="errormsg">{{this.$store.state.errorsdata.numeric.errors}}</span>
      </p>
      <p>
      <label for="required">Required</label>
      <input_field
      v-model="formdata.required"
      :req="formdata.required"
      :placeHolder="Object.keys(formdata)[9]"
      :class="{errorborder : this.$store.state.errorsdata.required.errors}"
      @focus.once="validationtouchrequired"
      />
      <span class="errormsg">{{this.$store.state.errorsdata.required.errors}}</span>
      </p>
      <p>
      <label for="required" class="txt1">Details</label>
      <textarea_field
      v-model="formdata.details"
      :maxLength="40"
      :placeHolder="'Maximum number of characters are 40'"
      />
      </p>
      <p>
      <label for="required" class="txt2">Description</label>
      <textarea_field
      v-model="formdata.description"
      :maxLength="60"
      :placeHolder="'Maximum number of characters are 60'"
      />
      </p>
      <input type="submit" value="Submit" :disabled="submitted"/>
      </form>
      <h1>Data Result</h1>
      <div>{{formdata}}</div>
      <h1>Data Errors</h1>
      <div>{{this.$store.state.errorsdata}}</div>

</template>

<script>
/* eslint-disable */
import { mapMutations } from 'vuex';
import input_field from './input_field.vue';
import textarea_field from './textarea_field.vue';

export default {
  name: 'form',
  components: { input_field,textarea_field },

  data() {
    return {
      formdata: {
        alphabetic: null,
        alphanumeric: null,
        alphaDash: null,
        alphaSpace: null,
        between: null,
        decimal: null,
        email: null,
        includes: null,
        numeric: null,
        required: null,
        details: null,
        description: null,
      },
    };
  },
  computed: {
    submitted () {
      if (
        this.formdata.alphabetic !== null && this.formdata.alphabetic !== "" && 
        this.$store.state.errorsdata.alphabetic.errors == null &&
        this.formdata.alphanumeric !== null && this.formdata.alphanumeric !== "" &&
        this.$store.state.errorsdata.alphanumeric.errors == null &&
        this.formdata.alphaDash !== null && this.formdata.alphaDash !== "" &&
        this.$store.state.errorsdata.alphaDash.errors == null &&
        this.formdata.alphaSpace !== null && this.formdata.alphaSpace !== "" &&
        this.$store.state.errorsdata.alphaSpace.errors == null &&
        this.formdata.between !== null && this.formdata.between !== "" &&
        this.$store.state.errorsdata.between.errors == null &&
        this.formdata.decimal !== null && this.formdata.decimal !== "" &&
        this.$store.state.errorsdata.decimal.errors == null &&
        this.formdata.email !== null && this.formdata.email !== "" &&
        this.$store.state.errorsdata.email.errors == null &&
        this.formdata.includes !== null && this.formdata.includes !== "" &&
        this.$store.state.errorsdata.includes.errors == null &&
        this.formdata.numeric !== null && this.formdata.numeric !== "" &&
        this.$store.state.errorsdata.numeric.errors == null &&
        this.formdata.required !== null && this.formdata.required !== "" &&
        this.$store.state.errorsdata.required.errors == null &&
        this.formdata.details1 !== null && this.formdata.details1 !== "" && 
        this.$store.state.errorsdata.details1.errors == null &&
        this.formdata.details2 !== null && this.formdata.details2 !== "" && 
        this.$store.state.errorsdata.details2.errors == null )
      {return false;}
      else { return true;}
    },
  },
  methods: {
    Submitform(e) {
      e.preventDefault();
      console.log(this.formdata);
    },
    ...mapMutations ([		
    'validationtouchbetween',
    'validationtouchemail',
    'validationtouchincludes',
    'validationtouchnumeric',
    'validationtouchrequired',
	])
  },
};
</script>

<style>
.inputtext {
  position: absolute;
  left: 400px;
}
.errormsg {
  position: absolute;
  left: 580px;
  color: brown;
  font-weight: bold;
}
.errorborder {
  border: 3px solid brown;
  background-color: rgba(255, 0, 0, 0.196);
  position: absolute;
  left: 400px;
}
.txt1 {
  margin-right: 107px;
}
.txt2 {
  margin-right: 78px;
}
</style>
