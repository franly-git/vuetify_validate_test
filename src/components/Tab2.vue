<template>
  <v-countainer>
    <h1>Tab2</h1>
    <v-form ref="tab2">
      <v-text-field
        v-model="form_data.tab2.text1"
        label="required"
        :rules="[required]"
      ></v-text-field>

      <v-text-field
        v-model="form_data.tab2.text2"
        label="limit_length"
        :rules="[limit_length]"
        counter=3
      ></v-text-field>
    </v-form>


  </v-countainer>
</template>


<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Tab2',
  components: {
    // HelloWorld
  },
  props:["form_data"],
  data(){
    return {
      success:false,
      required: value => !!value || "必ず入力してください",
      limit_length: value => value.length <= 3 || "3文字以内で入力してください",
    }
  },
  updated() {
    this.$emit("updated", this.form_data);
    this.$emit("validate",this.$refs.tab2.validate());
  },
  methods:{

  }
}
</script>