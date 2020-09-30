*Public copy of the private repo. Code may not reflect the current release of the website*.

<h3>A serverless resume website with view counter using AWS. Built to participate in <a href="https://aws.amazon.com/developer/community/heroes/forrest-brazeal">Forrest Brazeal's</a> Cloud Resume <a href="https://cloudresumechallenge.dev/instructions/">Challenge</a>.</h3> 

<h4><i>Publication on <a href="https://dev.to/tolerl1/the-cloud-resume-challenge-oao">solution</a></i></h4>

This <a href="https://cloudresumechallenge.dev/instructions/">16-step challenge</a> requires the creation of a website to showcase my resume with a site view counter. It dives deeper by requiring the use of AWS Lambda, API Gateway, and DynamoDB to operate the view counter, host the site on an S3 bucket, and have the site delivered over HTTPS using CloudFront. Additionally, this all must be automated using the AWS Serverless Application Model (SAM) and a CI/CD pipeline. 

I completed the challenge by breaking the project into groups with similar tasks. 
1. I started by designing my website in HTML using Bootstrap. Next, I created a CloudFormation template to automatically deploy my CloudFront distribution linking an S3 bucket as an origin so that the site is only accessible through CloudFront. Lastly, I purchased my domain and set the CNAME to point to CloudFront.
2. I created my development environment by installing python, aws cli, aws sam cli, and httpie. I used VSCode with the AWS and Python plugins, as my IDE. 
3. Creating the API, lambda function, and DynamoDB table was the most intensive part. A few essential items that I needed to learn:

       - How these services worked in tandem
       - How to create a table that updated a single record verse a table that would generate a record per visit
       - Learn python
       - How to call an API

    For my lambda function written in Python, I used DynamoDB's atomic counter feature to update the table each time my API endpoint gets called. 
    Additionally, I included a function to serialize / deserialize the response to bypass API Gateway's decimal encoder limitation. 
    My API uses a single GET method with CORS enabled. An XMLHttpRequest written in JavaScript is used to call the API and displayed using a DOM element.

4. Lastly, I built a CI/CD pipeline for the front and back end of my site. My first pipeline uses GitHub actions and workflow 
   to push any changes in the master branch of my repo to S3. My second pipeline has the same functionality except it utilizes 
   AWS CodePiple and Code Deploy to build, test, and deploy my SAM template. Testing was performed by passing a key/value payload to the lambda function.
