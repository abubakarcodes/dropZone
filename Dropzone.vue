<template>
    <div>
        <label for="">Upload Images</label>
        <div class="dropzone dz-clickable" id="mydropzone"></div>
        <input type="text" name="dropzoneFiles" id="mydropzone-files" />
    </div>
</template>
<script>
import Dropzone from "dropzone";
export default {
    mounted() {
        this.intializeDropzone();
    },
    methods: {
        intializeDropzone() {
            let myDropzone = new Dropzone("#mydropzone", {
                url: "/api/upload-file",
            });
            myDropzone.on("success", (file) => {
                let fileInput = document.getElementById("mydropzone-files");
                let files = fileInput.value;
                let newFiles =
                    file.xhr.response.replace(/"/g, "") + "," + files;
                fileInput.value = newFiles;
                // console.log(file.xhr.response);
                console.log("A file has been completed");
            });
        },
    },
};
</script>
