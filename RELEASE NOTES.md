# Release 1.0.0.8.414

# Major Features and Improvements

## Fingerprint Modality is Now Operational
[Fingerprint](https://github.com/openinfer/PrivateIdentity/wiki#fingerprint-identification) works with touchless fingerprints (optical scan using a phone or Webcam) as well as fingerprints from a touch scanner (capacitive scan).  

## Face w/ Mask Modality
The [Face w/ Mask DNN](https://github.com/openinfer/PrivateIdentity/wiki#face--mask-recognition) is now the default model for facial recognition. Enroll using a face or face w/ mask. Then predict with a face or face w/ mask. We recommend enrolling without a mask (to provide more data to the model) and then predicting with or without a mask. 
The Face DNN (that does not work with mask) can be accessed using the URL parameter _face=true&faceMask=false._ 

## Face Modality
A new release of [Face DNN](https://github.com/openinfer/PrivateIdentity/wiki#facial-recognition) reduces the size to 1.3MB without a loss in accuracy.  

## Video and Photo Detection (Anti-spoofing) 
This release turns on [video and photo anti-spoofing](v) functionality by default. 
Use the URL parameter _antiVideospoof=false_ to turn off anti-spoofing.

# Release 1.0.0.8.244

## Major Features and Improvements

### Video and Photo Detection (Anti-spoofing) 
**Face Validation DNN** 
The Face Validation DNN provides real-time passive facial liveness to prevent photo and video presentation attacks (photo and video spoofing). This algorithm mitigates risk of a video or photo spoofing attack during unattended operation. The DNN receives video input and outputs a validation score between 0 and 1, where 0 is a human face and 1 is a video or image presentation attack. The requested action cannot proceed until the detection of a live face.

To enable the anti-spoofing in the application, use the URL parameter  antiVideoSpoof=true when launching the application. This enables the application to check whether the stream of images captured from the webcam is recorded or live. 

The next release will include video and photo anti-spoofing functionality by default without the need for a URL parameter. 

## New Enrollment Workflow
The enrollment workflow now includes an introduction, request for user consent and informs users as to the progress of the enrollment (biometrics encrypted, biometrics deleted, enrollment complete, and account creation is finished).  (With many thanks and credit to BNG!) 

## Minor Features Implemented 
* Added documentation for Customer Integrations 

* Enhanced JavaScript Encryption Engine API 

* Added Silhouette Image to gray screen & blurry screen enhancement 

* Added Metadata and Cert download to Wiki documentation for Okta

* Enhanced Log management server 

* Enhanced security of API key feature 

## Bug Fixes
* Fixed Spoof Icon during video spoof detection 

* Edited documentation to correct setup link

* Repaired enroll function for Okta and PING (SAML) 

* Repaired voice authentication for Okta

* Repaired Photo ID enrollment 

* Fixed IPad Pro is opening rear-facing camera bug


# Release 1.0.0.8.244 #


## Major Features and Improvements ##

### 1. Improved User Interface
  * Increased speed of image acquisition by 300%. Updated Model View Controller to React.js.  This resulted in a performance increase of 300 percent on image acquisition.
  * Improved stability of Verified ID in Demo application.  We reduced the possibility of user error by limiting the choices available for Verified ID.  Now, when the Verified ID button is active, the user is only allowed to choose “Enroll.”  

### 2. Improved Face and Voice Accuracy
  * Improved face recognition model’s accuracy and boundary cases.  For images using modern cameras (phone, Webcam, etc.) and images on legacy cameras (> 0.25MP) we now have an overlap of 0 percent. The last model was 3.6% overlap. This translates to 0% false positive or negatives on all testing.  On legacy images (blurry photos, and images pre-1990), the overlap is 1%.  These legacy image probes did not generate false positives but yield 1 percent false negatives.  
  * The face model is also now trained to accommodate two additional boundary cases: (1) faces in motion and (2) up to 30% occlusions without loss of accuracy.  This model can handle face mask occlusions that cover less than 30% of the face. The next iteration on July 1 will handle full face masks.
  * Improved Voice Identification Performance.  We integrated a more accurate voice model. This model has an overlap of 8%, which results in 8 percent false negatives, across the test sets with no false positives.  The last model was reported 11% overlap.
  * Fully separated the Demo and the production applications.  The demo url http://www.private.id/demo offers a simple interface to test basic functionality without the need to understand the design details. The new url http://www.private.id/a  hosts the production application running entirely on url parameters. This is sufficient for all production applications.  All URL parameters are posted here: https://github.com/openinfer/PrivateIdentity/wiki/Client-URL-Parameters. 

### 3. Third-Party Integrations
  * PING Identity Integration.  We have fully integrated Private Identity into PING Identity.  PING Identity no longer needs to use username/password.  The PING integration includes enrollment, verified enrollment using Photo ID, 1:many login with face, voice, face+voice, account recovery, “forget me,” and forget user.
  * Okta Integration.  We have fully integrated Private Identity as an “Okta IdP Factor Authentication” on the Okta platform.  This allows customers to use Private Identity face, voice, or face+voice as an MFA. 






# Release 1.0.0.8.212 #

## Major Features and Improvements ##

1. The release introduces two new URLs. 
The release split the main application into two, one that demonstrates the application, and the other that is in compliance with OKTA, PING and any SAML provider. 
   * private.id/demo/index.htm?apiKey=1962 addresses the software containing the new User Interface Panel. 
   * private.id/a/?apiKey=1962 contains this new software. This is compliant with Saml, Ping and Okta. The new features, and anything else to be noted, can be found in section 3.
  
2. The demonstration application’s functionality.
   * Modalities: The new Interface portrays the 3 modalities and a verified enrollment feature. A single click on the face and voice button enables that modality, and a double click enables liveness for that modality.
   * Enrollment, and Prediction: At the bottom part of the panel, from left to right you see a user+, a  user-, and an arrow icon. Respectively, the first button allows you to enroll using the modality you have selected, the second button deletes an enrollment of the selected modality, and the third button performs a prediction of the selected modality.
  
3. The Main App Functionality.
   * The application is now in compliance with PING, and OKTA. It can utilize the parameter mentioned in section 3)b)ii) to call any SAML provider that is supported. 
   * We introduced a few new parameters to add support for SAML providers.
     - action=predict& attempts=# 
       When the action=predict, the number of prediction attempts defaults to 3, before realizing an error condition.  The URL parameter, attempts, allows the caller to specify a different values before realizing an error condition.
     - action=enroll& email=_emailID_  
       When action=enroll, the user specifies an email parameter associated with a given enroll .
     - idp=<ping/okta> 
        This supports PING and OKTA usage by setting the SAML destination.	


# Release 1.0.0.7.94 #

## Major Features and Improvements ##

1. GlassCheck requires users to remove eyeglasses & sunglasses.
GlassCheck now detects (using a tiny DNN on the local device) when users are wearing eyeglasses or sunglasses.  Users are required to remove eyeglasses during Enroll and when using Matt’s passive liveness feature (faceLiveness=true).  

2. Private Verified Enroll 
Using a browser and a Webcam or phone, we display a square video window on the browser to request the user show his/her drivers license or passport to the camera.  We then automatically acquire the image, extract and compare the face in the photograph on the document to the enrolled user’s face, OCR the document, verify the text on the document matches the user’s mobile phone record, send SMS to request confirmation from the user’s mobile phone number, and then return a verified score.
   * User must be Enrolled (Level 1) prior to Verified Enroll workflow.
   * To start, the user Predicts using face recognition 
   * If no phone number  exists in PII data, ask user for mobile phone number 
   * An API call to TeleSign returns mobile phone registration data. 
   * The user is then asked to show the front side of the driver's license or passport. The type of document is verified using a DNN running on the browser. 
   * No fraud check is performed. We can add a fraud step here if needed.
   * The face from the document is extracted, homomorphically encrypted and sent to the server for comparison.  The process stops if the faces do not match.
   * The document is OCR’d (using a DNN on the browser) and the text is then compared to the mobile phone registration data. The process stops if the text does not match. 
   * SMS is sent to user’s phone to request user to confirm his/her intent to enroll.
   * If the enrolled face and document match, OCR data from document and the phone registration match, and the user’s intent is confirmed using SMS, the user’s Enroll is promoted to Level 2. 
   * Privacy is preserved by performing all PII processing on the user’s local device. No PII data is transmitted, processed or saved to the server.



# Release 1.0.0.6.04 #

## Major Features and Improvements ##

1. Added Local Mode
Added ability to Predict without a network connection present.  For this to function to work properly, the user must first predict or enroll (at least once) on the local device with a network connection present in order for embeddings to be stored locally.  If the device then loses network connectivity, the software automatically moves to “local mode” and performs a local predicts.

2. Use Node server to process all embeddings on iOS. 
Embeddings are now being fully processed on Node.js on Predict and Enroll to improve user performance on all iOS devices.  

3. Reject Unsupported Browsers and Devices
Added a user message for old browsers and devices.  We plan to add Samsung Galaxy Tab support next week.  

4. Improved “Camera not available” messaging.  
Added message that camera is unavailable and may be in use by another app.

5. Added “spinner” to GUI on iOS to hold user during Enroll and Predict action.
The user now sees a graphic spinner while embeddings are generated on device (instead of frozen video).

6. Optimized Bulk Enroll
Bulk enroll function enables legacy biometrics to be enrolled in a single process.  

## Statistics ##

* Phase 1 of Facial Recognition Evaluation & Test (FRET) = 99.77% accurate. 
University College London (UCL) tested our recognition algorithm against six standard facial recognition algorithms: (1) MIT Center for Biological & Computational Learning’s “MIT-CBCL Face Recognition Database”, (2) University of Massachusetts Computer Vision Laboratory’s “Labeled Faces in the Wild,” (3) AT&T Laboratories Cambridge’s “AT&T Database of Faces,” (4) Georgia Institute of Technology Center for Signal and Image Processing’s “Georgia Tech Face Database,” (5) University of Essex, UK “Face Recognition Data,” and (6) Microsoft’s MS-Celeb-1M dataset.

* The California Institute of Technology’s “Frontal Face Database” was used to test the “Unknown case” against all datasets. No probe images of unenrolled test subjects matched to an incorrect identity (False Positive Identification Rate (FPIR) = 0%).Overall accuracy across all databases (combined) was 99.77%

## Next Release ##
1. Voice DNN v1
The voice model is currently training.

2. Face DNN v3
We started the next iteration of the Private Identity face model using MobileNetV2, which will improve accuracy, better handle legacy B&W and gray-scale images, and reduce the model size from 5MB to less than 1MB.

3. Verified Enrollment 
We are adding functionality to capture government identification documents, capture the facial biometric from the document, and pass the documents to a verification vendor.  We are using computer vision to stitch multiple photographs together in order to reduce glare and produce a single 600dpi image of each document.

# Release 1.0001 #
Initial Release of PrivateIdentity


## Major Features and Improvements ##

1. Improved iOS Safari browser performance.  
We refactored the iOS Safari code to enable the iPhone now predict and enroll without the need to move any processing to the NodeJS server.  

2. Added new URL parameter to allow isolated enrollment 
URL parameter 'action=enroll' now only performs the enroll function.

3. Added new URL parameter to allow isolated predict.  
URL parameter 'action=predict' added for the purpose of predict only. This will run the predict function until a person is found or the user stops the process.

4. Bulk Enroll 
Introduced a NodeJS script for performing bulk enrolls.  
This script offers three capabilities.
   * The ability to take a single face dataset, perform data augmentation to produce enroll sets, and then enroll the sets.
   * The ability to take full face dataset that does not need data augmentation and enroll the set.  
   * The ability to test the predict function using a large face dataset based on the content in directories. 
  

