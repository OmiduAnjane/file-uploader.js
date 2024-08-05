# FileUploader

File upload support for multiple storage backends provides flexibility by allowing uploads to be handled across different platforms like local filesystems, AWS S3, or Google Cloud Storage. This feature ensures secure, scalable, and efficient file storage tailored to users' needs.

## Features

- Middleware for handling file uploads in Express.
- Support for multiple file storage backends (local filesystem, AWS S3, Google Cloud Storage).
- File validation (size, type, etc.).
- Chunked uploads for large files.
- Image processing and resizing utilities.

## Installation

```bash
npm install file-uploader-js3
```
# Usage
## Middleware
```js
const express = require('express');
const { fileUpload } = require('file-uploader-js3');

const app = express();

// Local storage
const upload = fileUpload('local', { destination: 'uploads/' });

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('File uploaded successfully');
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});

// AWS S3 storage
const upload = fileUpload('s3', {
  bucket: 'your-bucket-name',
});

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('File uploaded successfully');
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});

// Google Cloud Storage (GCS) storage
const upload = fileUpload('gcs', {
  bucket: 'your-bucket-name',
});

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('File uploaded successfully');
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```
## File Validation
```js
const { validateFile } = require('file-uploader-js3');

const options = {
  maxSize: 1024 * 1024, // 1 MB
  allowedTypes: ['image/jpeg', 'image/png'],
};

try {
  validateFile(req.file, options);
  // Continue processing the file
} catch (error) {
  res.status(400).send(error.message);
}
```
## Image Processing
```js
const { resizeImage } = require('file-uploader-js3');
const fs = require('fs');

const buffer = fs.readFileSync('path/to/image.jpg');

resizeImage(buffer, 200, 200)
  .then((resizedBuffer) => {
    fs.writeFileSync('path/to/resized_image.jpg', resizedBuffer);
  })
  .catch((error) => {
    console.error(error);
  });
  ```
  ### AWS S3 storage .env
  ```env
  AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_REGION=
``` 
### Google Cloud Storage (GCS) storage .env
```env
GCP_PROJECT_ID=
GCP_KEY_FILE=
```
# License
## GNU GENERAL PUBLIC LICENSE


**The GNU General Public License (GPL) is a widely used free software license that guarantees end users the freedom to run, study, share, and modify the software. Key features of the GPL include:**

Freedom to Use: Users can run the software for any purpose.
Freedom to Study and Modify: Users can study how the program works and change it to suit their needs. Access to the source code is required.
Freedom to Distribute Copies: Users can redistribute the original software to others.

reedom to Distribute Modified Versions: Users can distribute copies of the modified software, allowing the community to benefit from improvements. Access to the source code of modified versions is required.
The GPL aims to promote and protect software freedom by ensuring that software remains free and open. Any derivative work must also be licensed under the GPL, ensuring that the same freedoms are preserved.**

**For the full text of the GPL, you can refer to the GNU General Public License website.**