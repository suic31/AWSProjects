[*Hosting a Static Website in S3 Bucket*]
======================================

Step 1: Access Amazon S3 from your AWS Management Console.

Step 2: Create a bucket and provide a unique name.

Step 3: Make sure ACLs are enabled.

Step 4: Also uncheck Block all public access.

Step 5: Enable Bucket versioning.

Step 6: Rest all will be default.
![image](https://github.com/user-attachments/assets/d2586919-b3a5-4093-a0de-8581554b74fb)


Make sure you check this checkbox
Step 7: Click on Create Bucket.

Step 8: Need to add a file i.e index.html (If you dont have any below i have some code written copy paste and create a index.html file) and then click on upload.

<!DOCTYPE html>
<html lang=”en”>
<head>
<meta charset=”UTF-8">
<meta name=”viewport” content=”width=device-width, initial-scale=1.0">
<title>Welcome to Our Website</title>
<style>
body {
text-align: center;
font-family: Arial, sans-serif;
margin: 0;
padding: 0;
background-color: #f0f0f0;
}
.container {
padding: 20px;
}
.gallery {
display: flex;
justify-content: center;
flex-wrap: wrap;
}
.gallery img {
width: 30%; /* Adjust based on preference */
margin: 10px;
box-shadow: 0 4px 8px rgba(0,0,0,0.1); /* Optional: Adds a shadow for better visibility */
transition: transform 0.2s; /* Smooth transition for hover effect */
}
/* Offset each image */
.gallery img:nth-child(1) { transform: translateY(20px); }
.gallery img:nth-child(2) { transform: translateY(40px); }
.gallery img:nth-child(3) { transform: translateY(60px); }

/* Hover effect to slightly enlarge images */
.gallery img:hover {
transform: scale(1.03);
}
</style>
</head>
<body>
<div class=”container”>
<h1>Welcome to Our Website!</h1>
<p>We’re glad you’re here. Check out our gallery below:</p>
<div class=”gallery”>
<img src=”YOUR_IMAGE_FILENAME_HERE” alt=”Image description 1">
<img src=”YOUR_IMAGE_FILENAME_HERE” alt=”Image description 2">
<img src=”YOUR_IMAGE_FILENAME_HERE” alt=”Image description 3">
</div>
</div>
</body>
</html>

Step 9: Now need to setup your bucket for static website hosting (In the Properties section of your bucket, enableStatic website hosting and then follow the below points.
![image](https://github.com/user-attachments/assets/3aa922aa-8011-4d97-97ee-069334966ae3)


Kindly check and write down as per the above image
Step 9: Need to make the file index.html publicly accessible to the internet need to select option Make public using ACL.
![image](https://github.com/user-attachments/assets/8f246173-ae0a-4a49-b524-66f92e071bef)


Click on Make public button.
![image](https://github.com/user-attachments/assets/ae36e781-2169-4703-b8b8-5b3b1e5632b4)


Step 10: Now you should be able to access the S3 URL link and see website.
![image](https://github.com/user-attachments/assets/de83d87a-2b63-47c4-8245-099995ebdd2f)


