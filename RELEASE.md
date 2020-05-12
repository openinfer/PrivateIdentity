# Release 1.0.0.8.212 #


## Release date ##

May 7 2020

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

## Release date ##

December 9 2019

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

## Release date ##

June 26 2019

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

## Release date ##

June 18 2019

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
  

