<template>
    <form @submit.prevent="uploadPhoto" id="uploadForm">
        <div class="form-group">
            <label for="description">Description</label>
            <textarea class="form-control" name="description" id="description"></textarea>
        
        
        <div class="upload">
            <label for="photo">Upload Photo</label>
            <input class="form-control" type="file" name="photo" id="photo" @change="selectImage">
        </div>
        <br>
        <button class="btn btn-primary" type="submit" @click="uploadPhoto">Upload</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            csrf_token: '',
            description: '',
            photo: ''
        }
    },
    created() {
 this.getCsrfToken();
},
    methods: {
        uploadPhoto(){

            let uploadForm = document.getElementById('uploadForm');
            let form_data = new FormData(uploadForm);

            fetch("/api/upload", {
                method: 'POST',
                body: form_data,
                headers: {
                    'X-CSRFToken': this.csrf_token
                }
            })
                .then(function (response) {
                    return response.json();
                })
                .then(function (data) {
                    // display a success message
                    console.log(data);
                })
                .catch(function (error) {
                    console.log(error);
                });
        },
        getCsrfToken() {
 let self = this;
 fetch('/api/csrf-token')
 .then((response) => response.json())
 .then((data) => {
 console.log(data);
 self.csrf_token = data.csrf_token;
 })
 }
    }
    
}
</script>

<style>


</style>