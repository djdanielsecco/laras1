<template>
  <div class="imgg">
    <h1>{{ msg }}</h1>
      <div v-if="!image">
    <h2>Select an image</h2>
    <input type="file" accept="video/*;capture=camcorder" @change="onFileChange">
  </div>
  <div v-else>
    <img :src="image" width="50px" height="50px"/>
    <button @click="removeImage">Remove image</button>
  </div>
    
  </div>
</template>

<script>
	var firebase = require('firebase');




	export default {
		name: 'imgg',
		data() {
			return {
				msg: 'vai',
				image: '',
				urr: ''
			}
		},
		methods: {
			onFileChange(e) {
				var files = e.target.files || e.dataTransfer.files;
				if (!files.length)
					return;
				this.createImage(files[0]);
				var file = e.target.files[0];
				var storageRef = firebase.storage().ref(file.name);

				var metadata = {
					contentType: 'image/jpeg'
				};

				// Upload file and metadata to the object 'images/mountains.jpg'
				var uploadTask = storageRef.put(file, metadata);

				// Listen for state changes, errors, and completion of the upload.
				uploadTask.on(firebase.storage.TaskEvent.STATE_CHANGED, // or 'state_changed'
					function(snapshot) {
						// Get task progress, including the number of bytes uploaded and the total number of bytes to be uploaded
						var progress = (snapshot.bytesTransferred / snapshot.totalBytes) * 100;
						console.log('Upload is ' + progress + '% done');
						switch (snapshot.state) {
							case firebase.storage.TaskState.PAUSED: // or 'paused'
								console.log('Upload is paused');
								break;
							case firebase.storage.TaskState.RUNNING: // or 'running'
								console.log('Upload is running');
								break;
						}
					},
					function(error) {

						// A full list of error codes is available at
						// https://firebase.google.com/docs/storage/web/handle-errors
						switch (error.code) {
							case 'storage/unauthorized':
								// User doesn't have permission to access the object
								break;

							case 'storage/canceled':
								// User canceled the upload
								break;



							case 'storage/unknown':
								// Unknown error occurred, inspect error.serverResponse
								break;
						}
					},
					function() {
						// Upload completed successfully, now we can get the download URL
					var ind = window.dados1.length
						var downloadURL = uploadTask.snapshot.downloadURL;
						firebase.database().ref('registro/itemcod' + (ind)).set({
							foto: downloadURL,
							index: ind,
							lat: 122,
							long: 11123123123,
							user: 5585558
						});
					
					});
				
			},
			createImage(file) {
				var image = new Image();
				var reader = new FileReader();
				var vm = this;

				reader.onload = (e) => {
					vm.image = e.target.result;
				};
				reader.readAsDataURL(file);

				// use the Blob or File API
				/*storageRef.put(reader).then(function(snapshot) {
					console.log('Uploaded a blob or file!');
				});*/
				//console.log(image.innerText + '<kkkkk>');

			},
			removeImage: function(e) {
				this.image = '';
			}
		}
	}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	h1,
	h2 {
		font-weight: normal;
	}

</style>
