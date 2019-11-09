<template src="./FileUpload.html"></template>
<style src="./FileUpload.css"></style>
<script>
    // import EventBus from '../../../../eventBus'
    // import axios from 'axios';
    // import MainView from "../mainView/MainView";

    import axios from "axios";
    import {url} from "../../constants";

    export default {

        name: 'FileUpload',
        data() {
            return {
                FileUpload: {
                    file: '',
                    testId: '',
                    info: '',
                    noQuestionsInTest: 0,
                    noQuestionsToSend: 0
                }
            }
        },
        methods: {
            handleFileUpload(e) {
                this.FileUpload.file = e.target.files || e.dataTransfer.files;
                // console.log(this.FileUpload.file)
            },
            setNumberOfQuestions: function (noQuestions) {
                this.FileUpload.noQuestionsToSend = noQuestions;
            },
            sendNumberOfQuestions: function () {
                if (this.FileUpload.noQuestionsToSend !== 0) {
                    axios.post(`${url}/${this.FileUpload.testId}/${this.FileUpload.noQuestionsToSend}`).then(() => {
                        alert("Pomyślnie zapisano wybór liczby pytań.")
                    }).catch(() => {
                    });
                } else {
                    alert("Wybierz liczbę pytań.")
                }

            },
            submitQuestionsFile: function () {
                let formData = new FormData();
                formData.append('file', this.FileUpload.file[0]);
                axios.post(`${url}/test`, formData,
                    {
                        headers: {
                            'Content-Type': 'multipart/form-data'
                        }
                    }
                ).then(response => {
                    this.FileUpload.testId = response.data[0];
                    this.FileUpload.noQuestionsInTest = response.data[1];
                    // console.log(response);
                    // EventBus.$emit('UPLOADED', response);
                })
                    .catch(() => {
                        // console.log('FAILURE!!');
                        // console.log(err.response);
                    });
            },
            generateResults: function () {
                axios.get(`${url}/${this.FileUpload.testId}/results`).then(() => {
                    this.FileUpload.info = `${url}/${this.FileUpload.testId}/results`;
                }).catch(() => {
                });
            }
        }
    }
</script>

