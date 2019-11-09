<template>
    <div id="app">
        <FileUpload v-if="show"></FileUpload>
    </div>
</template>

<script>
    import FileUpload from "./components/fileUpload/FileUpload";

    export default {
        name: 'app',
        data() {
            return {
                show: true
            }
        },
        components: {
            FileUpload
        }

    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: black;
        margin-top: 60px;
    }

    body {
        background-image: url("Tech-news.jpg");
        background-size: auto;
    }
</style>
