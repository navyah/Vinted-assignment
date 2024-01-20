**1. Test cases:**

Please create 5 test cases for the item upload area. These test cases should show how you approach testing rather than be exhaustive test cases. Mention what you think should be given special attention. Tell us why you chose those test cases. You can use the format of your own choosing. If you find any bugs in the item upload area - create bug reports for them in a form of your own choosing.

Answer 

Sanity tests: These tests focuses on the high level and critical path of the business in the upload process

1. Verify that the user can navigate to upload area and the page is loading successfully (scroll should work with all device sizes) 
2. Ensure that the user can upload the file successfully 
3. Ensure that the user is able to enter the data in all other fields successfully
4. Verify that the upload button is displayed on the screen and it is clickable
5. Ensure Submit Feedback is working as expected and the response is recorded
6. Verify that the user is displayed with valid error messages for the missing information in the screen

Other test approaches I follow are:

UI
1. Ensure screen is scrollable until the last item in the screen is visible and accessible 
2. Ensure no spelling mistakes on the title of the fields and in any contents in the screen 
3. Verify all UI elements are visible and clickable 

Functionality
File type & size validation and error messages for invalid file format & invalid file size
Verify that the removing the uploaded file should work as expected 
Verify that the user should be able to upload more more than 1 images 
Verify that the user should not be able to upload more than 20 images 
Ensure user should be able to see the photo tips as expected and able to scroll through the screen properly 
Cancelling the upload process and navigation to back screen should work as expected and user file should be cleared 
Ensure users should not be able to submit the data without entering all mandatory values.
Ensure all the fields are accessible and user can enter the data from dropdown fields 
Ensure appropriate error messages displayed for all the fields in the screen when the user skip to enter the values
Verify Bump item checkbox functionality is working as expected and Learn more link is taking the user to correct web link 
Ensure the link to Law and sections are opening as expected 
Ensure user is able to submit the rating along with/without the appropriate tags successfully  
Verify user should be able to close the rate drawer without providing any rating by touching somewhere on the screen or by tapping X icon
Verify user should be able to save the draft version successful 
Verify the behaviour of the screen when the device is not connected to the internet 

Security
Ensure executable scripts should not be a part of the upload (both file and text fields) and proper validation should be present

Compatibility (both apk & ipa)
The app should be able to run on all devices (based on requirement) 
The app should be  able to work in all supported OS versions

___________________________________________________________________________________________________________________________________________________________________________________

**2. Bugs**
Tell us how would you approach testing (how would you try to reproduce, what should be paid special attention, what could be the causes and etc.) for the issues mentioned below:

a) User is not able to upload an item - gets an “unexpected error” when pressing “Pridėti” button in Upload form. Kibana logs show message: Rejected file upload: photo.webp (size: 0, head: )


Answer 

With the given information above I try to guess the scenario as below:


From which country is the issue reported from (Guess from ‘Pridėti’ ) 
From Kibana logs I understand that, the file name is ‘photo.webp’ 
and size is 0

Try with empty .webp file and valid .webp file
Try to break the file upload process to make sure how the empty file can be uploaded 
Test the file format and size scenario multiple times to find the root cause 
Testing with different internet speed and different network connectivity to mimic the process 

b) User sometimes does not receive push notifications when out of our app on Android.

Verify that there are no similar issues reported from any other users to make sure it is user specific or device specific issue 
Ensure the service which is handling the push notification does not have any errors and the service is 100% available

Then verify from users perspective: 

Verify that the app has notification permission enabled (apps manifest file)
Ensure ‘Do not Disturb’ mode is not active in the device 
Verify the user internet connection is enabled and Vinted app can access mobile data
Ensure vinted app is not part of any background restriction settings related to battery optimization (Android OS have mechanism to kill unnecessary background activities to save battery) 
Verifying the device log might be helpful in understanding the problem
Verify the same user account with different device to narrow down the problem
Update the app version if any 
Verify that the clearing the application cache from the settings helps in fixing the issue
Verify that the app uninstall and install helps in fixing the issue 



**3. Automated test**
At Vinted we have quite a lot of automated e2e tests for mobile and web. However, sometimes they break and you might need to retest manually to be sure if there is a bug.
Please write a test case according to this auto test written for iOS and Android platforms.
How would you improve the logic of this test? Give examples of which steps could be added or removed.

@Test(description = "Test favoriting item from item screen and unfavoriting it from favorites screen")
fun testItemFavoring() {
   deeplink
       .loginToNewUser()
   navigationRobot
       .clickOnSearchIcon()
   browseRobot
       .openFirstCategory()
   catalogRobot
       .clickOnFirstItem()
   itemRobot
       .assertHeartIconIsWhite()
       .clickFavoriteButton()
   navigationRobot
       .openProfileTab()
   profileTabRobot
       .openMyFavouriteItemsScreen()
   favoriteItemsRobot
       .assertHeartIconIsRed()
       .unfavoriteItemAndRefresh()
}
Answers
Test steps
Login with the new user from given credentials 
Click on the search icon 
Open the first category 
Click on first item 
Validate that the white heart icon is displayed
Click on heart icon 
Navigate to profile tab 
Click on ‘Favourite items’ from profile screen 
Validate that the heart icon is red 
Click on heart icon again 
Refresh the screen 
Improvements: 
Removing
In the 4th step If user click on first item then the user navigate to item detail screen and heart icon is missing in detail screen so I think this should not be present 
Adding
In the 4th step when the user click on first item then it would be good to make a note of the item 
Then after 8th step we should search back for same item from step 4 to validate favourite is working 
And Unfavourite the same item 
Then after refreshing the screen validate that the same item should disappear 
(assertion flow completes for both favourite and unfavourite) 


