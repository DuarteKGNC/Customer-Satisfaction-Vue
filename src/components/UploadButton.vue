<template>
    <div class="text-center">
      <input class="form-control" type="file" id="formFile" @change="uploadedFile">
      <label for="formFile" class="form-label text-nowrap text-white">* Only CSV files allowed *</label>
      <div class="row">
        <div class="col-12 mt-3">
          <button class="btn btn-primary w-25" type="submit" @click="readCSV">Calculate</button>
        </div>
        <div v-if="file != null" class="d-flex text-center justify-content-center align-items-center mt-5">
          <h5>File Uploaded: </h5>
          <span class="mb-2">{{ file }}</span>
        </div>
        <div v-if="average" class="mt-5">
            <h2>Average Score:</h2>
            <h5>{{ average }}</h5>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Papa from 'papaparse';
  
  export default {
    name: 'UploadButton',
    data() {
      return {
        file: null,
        average: 0
      };
    },
    methods: {
      uploadedFile(event) {
        let name = event.target.files[0].name;
        let isValid = /\.csv$/.test(name);
  
        if (isValid) {
          this.file = name;
        } else {
          console.log('Invalid File Format');
        }
      },
      readCSV() {
        if (!this.file) {
          console.log('No file uploaded.');
          return;
        }
  
        const fileInput = document.getElementById('formFile');
        const file = fileInput.files[0];

        Papa.parse(file, {
          header: true,
          complete: (result) => {
            const satisfactionValues = result.data.map(row => row['How satisfied are you with the support you received from Kognic?']);
            console.log('Satisfaction values:', satisfactionValues);
            

            this.average = Math.abs(satisfactionValues.reduce((a,b) => parseInt(a) + parseInt(b), 0) / satisfactionValues.length).toFixed(1);


          },
          error: (error) => {
            console.error('Error parsing CSV:', error);
          },
        });
      },
    },
  };
  </script>
  
  <style scoped></style>
  