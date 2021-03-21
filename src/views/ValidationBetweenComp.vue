<template>
  <v-countainer>
    <h1>vuetifyのバリデーションをコンポーネントをまたいで使ってみる</h1>
    <v-card class="ma-5">
        <v-toolbar
            color="cyan"
            dark
            flat
        >
            <v-app-bar-nav-icon></v-app-bar-nav-icon>
            <v-toolbar-title>Your Dashboard</v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon>
                <v-icon>mdi-magnify</v-icon>
            </v-btn>
            <v-btn icon>
                <v-icon>mdi-dots-vertical</v-icon>
            </v-btn>
            <template v-slot:extension>
                <v-tabs v-model="tab">
                    <v-tab href="#tab-1">タブ1</v-tab>
                    <v-tab href="#tab-2">タブ2</v-tab>
                </v-tabs>
            </template>
        </v-toolbar>

        <v-tabs-items v-model="tab">
            <v-tab-item value="tab-1" class="pa-8">
                <Tab1 :form_data="form_data" @validate="tab1_validate"></Tab1>
            </v-tab-item>
            <v-tab-item value="tab-2" class="pa-8">
                <Tab2 :form_data="form_data" @validate="tab2_validate"></Tab2> 
            </v-tab-item>
        </v-tabs-items>
    </v-card>
    

    <v-btn outlined color="teal" @click="save">保存</v-btn>
    <v-btn outlined color="indigo" @click="submit">送信</v-btn>
    <h2 v-if="success">バリデーションOK！送信できます</h2>
    <hr>
    <h3>{{form_data}}</h3>
    <h1>{{validation_result}}</h1>
  </v-countainer>
</template>


<script>
// @ is an alias to /src
import Tab1 from '@/components/Tab1.vue'
import Tab2 from '@/components/Tab2.vue'

export default {
  name: 'ValidationBetweenComp',
  components: {
    // HelloWorld
    Tab1,
    Tab2,
  },
  data(){
    return {
        form_data:{
            tab1:{text1:"", text2:"", text3:""},
            tab2:{text1:"", text2:""},
        },
        tab:"",
        success:false,
        text1:"",
        text2:"",
        text3:"",
        required: value => !!value || "必ず入力してください",
        limit_length: value => (value || '').length <= 3 || "3文字以内で入力してください",
        validation_result:{tab1:false, tab2:false},
    }
  },
  updated() {
    console.log("updated")
  },
  methods:{
    save(){
      console.log("save");
    },
    submit(){
      console.log("submit");
      if(this.validation_result.tab1 && this.validation_result.tab2){
          console.log("send data!!!");
          this.success = true;
      }
    
    },
    tab1_validate(value){
        this.validation_result.tab1=value;
    },
    tab2_validate(value){
        this.validation_result.tab2=value;
    }

  }
}
</script>