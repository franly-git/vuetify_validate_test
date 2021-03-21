<template>
  <v-countainer>
    <h1>vuetifyのバリデーションを使ってみる</h1>
    <v-form ref="test">
      <v-text-field
        v-model="text1"
        label="required"
        :rules="[required]"
      ></v-text-field>

      <v-text-field
        v-model="text2"
        label="limit_length"
        :rules="[limit_length]"
        counter=3
      ></v-text-field>

      <v-text-field
        v-model="text3"
        label="required, limit_length"
        :rules="[required, limit_length]"
        counter=3
      ></v-text-field>
    </v-form>

    <v-btn outlined color="teal" @click="save">保存</v-btn>
    <v-btn outlined color="indigo" @click="submit">送信</v-btn>
    <h2 v-if="success">バリデーションOK</h2>
  </v-countainer>
</template>


<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Validation',
  components: {
    // HelloWorld
  },
  data(){
    return {
      success:false,
      text1:"",
      text2:"",
      text3:"",
      required: value => !!value || "必ず入力してください",
      limit_length: value => value.length <= 3 || "3文字以内で入力してください",
    }
  },
  methods:{
    save(){
      console.log("save");
    },
    submit(){
      console.log("submit");
      if (this.$refs.test.validate()) {
        this.success = true;
      } else {
        this.success = false;
      }
    
    }

  }
}
</script>