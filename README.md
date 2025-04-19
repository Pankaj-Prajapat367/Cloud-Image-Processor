# Cloud-Image-Processor

Project Overview
The Cloud Image Processor is a serverless application that allows users to upload images to an S3 bucket, which then triggers AWS Lambda functions to process these images (resizing, applying filters, etc.). The processed images are stored in another S3 bucket, and the application provides a frontend interface to view both original and processed images.

Key Components
Frontend: A web interface built with HTML, CSS, and JavaScript for uploading and viewing images

Backend: AWS Lambda functions (Node.js) for image processing

Storage: Amazon S3 buckets for storing original and processed images

Event Processing: AWS S3 event notifications to trigger Lambda functions

Infrastructure: Deployed using AWS SAM (Serverless Application Model)


Project Structure
Cloud-Image-Processor/
├── back/                   # Lambda function source code
│   ├── fun.js               # Main image processing Lambda
│   ├── s3.js                # s3 Bucket Invoking 
│   └── package.json         # Node.js dependencies
├── front/                   # Frontend code
│   ├── home.html           # Main page
│   ├── styles.css           # CSS styles
│   └── script.js            # Frontend JavaScript
├── template.yaml            # AWS SAM template
└── README.md                # This file


Prerequisites
Before running this project, ensure you have the following installed:
1. Node.js (v14.x or later)
2. AWS CLI (configured with your credentials)
3. AWS SAM CLI
4. An AWS account with appropriate permissions

Setup and Deployment Instructions
1. Clone the Repository
###
git clone https://github.com/Pankaj-Prajapat367/Cloud-Image-Processor.git
cd Cloud-Image-Processor
###

3. Install Dependencies
Navigate to the back folder and install the required Node.js packages:
###
cd back
npm install
cd ..
###

3. Build the Application
###
sam build
###

5. Deploy the Application
###
sam deploy --guided
###

Follow the interactive prompts to configure your deployment. Make note of the output values as they will contain important endpoints and resource names.

6. Configure the Frontend
After deployment, update the frontend configuration in front/script.js with the correct S3 bucket names and API endpoints that were output during deployment.

7. Deploy the Frontend
Upload the contents of the front folder to an S3 bucket configured for static website hosting, or deploy to your preferred hosting provider.

How It Works
1. Image Upload: Users upload images via the frontend interface, which stores them in the source S3 bucket.

2. Event Trigger: S3 bucket events trigger the Lambda functions whenever a new image is uploaded.

3. Image Processing:
fun.js applies various image transformations

4. Result Storage: Processed images are saved to the destination S3 bucket.

5. Display: The frontend retrieves and displays both original and processed images.

Lambda Functions
crop.js
Crops images according to the x,y and z coord you provide.

grayscale.js
Applies grayscale and sepia filters.
Uses Sharp library for high-performance image processing.

resize.js
Resizes images to upload it in a compact environment.
Optimized for fast loading in gallery views.

pdf.js
Converts various images into a single pdf.


Customization
You can modify the image processing parameters by editing:
1. The Lambda function code in the back folder
2. The configuration in template.yaml

Cleanup
To avoid ongoing charges, delete the AWS resources when you're done:
###
sam delete
###

Troubleshooting
1. Permission Errors: Ensure your AWS credentials have proper permissions for S3, Lambda, and CloudFormation.

2. Deployment Failures: Check CloudFormation logs for detailed error messages.

3. Image Processing Issues: Verify the Sharp library is properly installed in the Lambda environment.


Contributing
Contributions are welcome! Please fork the repository and submit a pull request with your changes.
