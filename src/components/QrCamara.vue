<template>
  <div>
    <h1>Hello World</h1>
    <h1>Camara</h1>
    <qrcode-stream @init="onInit" @decode="onDecode"/>
  </div>
</template>

<script>
import { QrcodeStream } from "vue-qrcode-reader";
export default {
  components: {
    QrcodeStream,
  },
  data(){
      return{
          result:'',
          error:''
      }
  },
  methods:{
      onDecode(result){
          this.result = result
      },
      async onInit(promise){
          try {
              await promise
          } catch (error) {
              if (error.name === 'NotAllowedError'){
                  this.error = "ERROR: you need to grant camera access permission"
              } else if(error.name === 'NotFoundError'){
                  this.error = "ERROR: no camera on this device"
              } else if(error.name === 'NotSupportedError'){
                  this.error = "ERROR: secure context required (HTTPS, localhost)"
              }
          }
      }
  }
};
</script>

<style>
</style>