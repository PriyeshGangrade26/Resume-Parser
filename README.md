# Eden AI Resume Parser

## Introduction

Eden AI Resume Parser, a tool designed to extract text and relevant information from resumes using Node.js.

## Prerequisites

- Node.js installed (version 12.0 or higher).
- An API key from Eden AI.

## Installation

1. Initialize the Project : 
   Run the following command to initialize a new Node.js project and create a `package.json` file:
   ```sh
   npm init -y
   ```

2. Install Dependencies : 
   Install the required dependencies using the following command:
   ```sh
   npm install axios
   ```

3. API Key Configuration : 
   Create a `.env` file to store your Eden AI API key:
   ```
   EDEN_API_KEY= "KEY"
   ```

## Making API Calls

1. Import Required Modules : 
   Create a JavaScript file (e.g., `app.js`) and start by importing the necessary modules:

   ```javascript
   const axios = require('axios');
   require('dotenv').config();
   ```

2. Prepare API Request : 
   Define the API endpoint and headers in your script:

   ```javascript
   const apiUrl = 'https://api.edenai.run/v1/pretrained/vision/ocr_resume';
   const headers = {
     'Authorization': `Bearer ${process.env.EDEN_API_KEY}`,
     'Content-Type': 'application/json'
   };
   ```

3. Send API Request : 
   Create a function to send the API request and handle the response:

   ```javascript
   async function parseResume(filePath) {
     try {
       const response = await axios.post(apiUrl, {
         inputs: [filePath]
       }, { headers });

       return response.data;
     } catch (error) {
       throw new Error('Error parsing resume: ' + error.response.data.message);
     }
   }
   ```

4. Usage : 
   Use the `parseResume` function to extract text from a resume:

   ```javascript
   const resumeFilePath = '/path/to/your/resume.pdf';
   parseResume(resumeFilePath)
     .then(result => {
       console.log('Parsed Resume:', result);
     })
     .catch(error => {
       console.error('Error:', error.message);
     });
   ```

## Response Format

The response from the API call will be in JSON format and contain extracted information from the resume. The specific structure of the response will depend on the Eden AI API.
