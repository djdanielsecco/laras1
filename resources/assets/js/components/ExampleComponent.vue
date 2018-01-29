<template>
  <div id="container">
  
 <imgg></imgg>
      
      <br />

 <br />
 <database></database>

  </div>
</template>

<script>
	
	var firebase = require('firebase');

	



import Hello from './comps/Hello.vue'
import Cam from './comps/Cam.vue'
import  Database from './comps/Database.vue'
import  Imgg from './comps/Imgg.vue'

export default {
  name: 'container',
  components: {
  

	  Database,
	  Imgg
  }
}
</script>

<style>


body, header {
  margin: 0;
  height: 56px;
  padding: 0 16px 0 24px;
  background-color: #35495E;
  color: #ffffff;
}

</style>
