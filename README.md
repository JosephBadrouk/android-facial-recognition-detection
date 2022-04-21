## Coin - An Application of Facial Recognition using Augmented Reality
### Developed by @JosephB99 & @jimi487

Coin is an Android application we developed to dive into the world of augmented reality using facial detection  and recognition.
There are many ways to apply the use of this technology in diverse fields, but this serves as an excellent starting point.

### How It Works
When a registered user points at a face via the camera in the app, the app tries to detect any faces present (can be multiple), 
and for every detected face it tries to then recognize them. Facial recognition will only be successful if the detected face belongs
to a registered user in the app. 

A bounding box will be drawn around the face of each detected face, and if the user is recognized, their name and instagram handle
will be displayed at the bottom. Clicking on the handle will redirect to that user's instagram.

### Coin was built using...

* Google Firestore to store the user's basic information (name, date of birth, social media handles, etc.)
* Amazon S3 to store the user's image
* Amazon Cognito to handle user registration and authentication
* Amazon Rekonigtion for the facial detection and recognition
* Amazon Kinesis for the main video stream
* Android Studio as the IDE
* Kotlin as the main programming language

### From registration to recognizing faces 
When a new user wishes to register, they are taken to a page where they must accept the ToS. Upon agreement, they are asked to enter 
their e-mail address and password of choice. Amazon Cognito then sends a verification code to their e-mail, which they must then enter.
If successful, they are created in the Cognito User Pool as a user.

The user must then fill in a form with their basic information, and take a picture of themselves that we will use to recognize them
if another user points at their face. A face must be present in the picture, otherwise regisration won't be allowed. Once all is filled,
their image is stored into an Amazon S3 bucket and an Amazon Rekognition Collection, and their information is stored into the Firestore database.

The main part of the app is the Video Stream, redirected to from the login or after registration. Here, the user can manually start
the video stream, which is a continous live video feed of their camera. This is set up via Amazon Kinesis. From here, all faces in the
stream are sent to Rekognition for detection and recognition.

The user can stop the stream at any time. Once stopped, the images of all of the users that were recognized from the moment the stream 
started up until the point that the stream was stopped are displayed at the top left. Clicking on an image redirects to the corresponding image's associated Instagram page.

### Other small features
* Full validation of every form was taken into consideration (password lengths, existing users, no face present in registration, mandatory fields, etc.)
* Settings page - the user can view and change their information, including their image
* Account recovery incase the password was forgotten
* Registration pickup: if the user quits the app before entering their confirmation code on registration and then tries to login, they are redirected to a page that prompts them to enter another verification code.
In addition, if the user quits the app after entering their confirmation code but before filling in their registration information (taking their picture, for example), they are redirected back to the registration page.

### Screenshots of the app (face shots courtesy of Jimi)

The login page\
![main page](https://lh5.googleusercontent.com/8pP1b_jyPe6_r3t-tvA_yD-TUjeJqHA2yzo6FJol_zu9YMtGJd61vumCRQD7c4kkbmdl1OkajhIKmabzld2q1T2Ivcn1OUl6Xfo1xTB1smPrsy0km0xHb6SFYNi2Dfg7wPK_qoT1)

Forgot password page\
![main page](https://lh3.googleusercontent.com/hoJ6BfrudoYy5_AzkeFybK7sqwY0nWKERN1r4laqXQzbLk_fJxfxN-njoK9mMtRQNoQoJp4qNBWAIjyHxefd6d5VNP_5-ZjgJKvC7YlKYYcWtO1MR9t9ZBUdYhrjLw8wZMxGU59x)

Registration page step 1: ToS\
![main page](https://lh6.googleusercontent.com/uBX2zZI86pa2e7e_F7CMlzb4AG5c4NsvNimujHrnBSm5NKiR0N8bv0vLOcnQAqqJWMTXUldhEdceIE44vVOA0_1gWxv9u5MiQKCMFTygiMO60JDIUG6E5ZybjDk5fsf9uhdxX09S)

Registration page step 2: E-mail and password\
![main page](https://lh5.googleusercontent.com/70pcrLz4sFBdN-Ydz9MHnRtq7iC1ysFGkIVyWLFdGWpOibbfDWw5Coq5yCfszRS1b0qX78OCzF1lA9YnygTEArltnu4Tr76Nq-SUDOXgOzVAc56MXFzUHmJclnYqSGsgx_x651UX)

Registration page step 3: Picture and basic information\
![main page](https://lh3.googleusercontent.com/ZtJQMpKotGwLP3ZS82Z5oSYJXETovaRcGuyg_4qzLr9yPPFV7WXGQB4fa_L4U-EsNAdNkF_kQdomChEjeAP7vdaFf8pcixPxuuY1oPDo7Fj4EwNflALWm0ILzB5Ogk5Hsa1J9ohW)

Video stream: Detected and recognized face\
![main page](https://lh3.googleusercontent.com/VUxjD9xPVtKumoPxioQVbr4pWK6Cm9A0cESejbA-ki-g2xiY_udeBOwQ_8nTm3PEq3InulFC1xFrBHdqIXbAa4j_6ehXu-oUgVEgo9kXcshXBGg9_2BM21PmDfbTL7Y3t1JJkzLX)

Video stream: After stream is stopped, with image results of recognized faces (top left)\
![main page](https://lh4.googleusercontent.com/DqmFyaGc9BF4Mrtzpnu7UZOMGoVFdFHHNtSUlgT-4KwTkn2LRVFf-AgLmZ0N6a0DuJIf222e9uXONO_TIDeeVARGE8uEyNLTa-o118bFgwIJYs2-eofHe1vHAIG8zv0tTBpz-26k)

User settings page\
![main page](https://lh6.googleusercontent.com/zNe2RdiHEpxG6lcH4Gscb3EkEELNFSdcmhvQLiADp6Y5HULB0T5eR0TDCFT0yrhGOnaSi0XYgdPFTp7V6-JDF0lcQ1UIQNuJGmK1JegVwnXoCwMsFrijrfwuYiVJ8-F56_ZynzsA)
