<template>
<div class="form-container">
  <form v-on:submit.prevent="uploadFiles">
    <label for="cloudname-input" >Cloud Name:</label>
    <input id="cloudname-input" v-model="cloudName" placeholder="Enter cloud_name from dashboad"/>
    <label for="preset-input">Preset:</label>
    <input id="preset-input" v-model="preset" placeholder="Enter preset from upload settings"/>
    <label for="file-input">Upload:</label>
    <input id="file-input" type="file" multiple @change="handleFileChange($event)" />
    <button type="submit" :disabled="filesSelected < 1">Upload</button>
  </form>
  </div>
</template>

<script>
import {ref} from 'vue';
import axios from 'axios';
export default {
  setup() {
    let filesSelected = ref(0);
    const files = ref(null);
    const cloudName = ref("");
    const preset = ref("");
    const formData = ref(null)

    const handleFileChange = (event) => {
      files.value = event.target.files;
      filesSelected.value = event.target.files.length;
      console.log("uploaded files", files);
    }

    const uploadFiles = () => {
      if (preset.value.length < 1 || cloudName.value.length < 1) {
      console.log("You must enter a cloud name and preset to upload");
      return;
      }

      files.value.forEach((file) => {
      formData.value = new FormData();
      formData.value.append("upload_preset", preset.value);
      formData.value.append("tags", "browser-upload");
      formData.value.append("file", file);

      let cloudinaryUploadUrl = `https://api.cloudinary.com/v1_1/${cloudName.value}/upload`;
      axios({
        url: cloudinaryUploadUrl,
        method: "POST",
        headers: {
              'Content-Type': "application/x-www-form-urlencoded"
            },
            data: formData.value,
          }).then(res => console.log(res)).catch(error => console.log(error))
      })
    }
    return {filesSelected, cloudName, preset, handleFileChange, uploadFiles}
  }
}
</script>

<style scoped>
.form-container {
  width: 80%;
  margin: 0 auto;
}
form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: stretch;
}
input {
  margin: 5px 0 15px;
}
#file-input {
  align-self: center;
}
button {
  height: 40px;
  border-radius: 10px;
  cursor: pointer;
}

</style>