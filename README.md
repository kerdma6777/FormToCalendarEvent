# FormToCalendarEvent
These are custom functions that when added to the Google Script of a Google Spreadsheet can create calendar events from Google Form submissions.  This was originally created as a conference room reservation tool.  In that original usage, each calendar represented a different conference room and different forms correlated to different sheets.  To book a room, the user simply had to go to the url of the relevant Google Form and enter in the reservation information (start time, end time, company name, and contact information), and enter in the correct password.  Then, the user will receive an email either confirming the successful reservation or explaining why the reservation couldn't be created.  (The password entered is incorrect or the reservation conflicted with another existing reservation.)    

This code was written in [Google Apps Script](https://developers.google.com/apps-script/reference/calendar/), which is Javascript based.  

#Demo
To see the script in action, first submit a request through this [form](https://docs.google.com/forms/d/1C8IHwFUlC_TD1JiKnmwoEfZTFceqGsb7FJmaoJkRvUU/viewform).  The password is currently set to 1234.  You'll be able to see the calendar event being added to this [calendar](https://www.google.com/calendar/embed?src=v65s78cschonjk2rtj4s7jeeng%40group.calendar.google.com&ctz=America/New_York) in real-time.  Feel free to play around with it.  You'll notice that an attempt to create an event that overlaps another event will not be successful.  Requests that don't enter the correct password will not be successful.  Keep an eye on your email, as an email is sent after every request either confirming you're event or explaining why it wasn't added.


#TO USE THIS SCRIPT

#Create a Google Form
To utilize this script, first create a google form.  Follow this [model](https://docs.google.com/forms/d/1C8IHwFUlC_TD1JiKnmwoEfZTFceqGsb7FJmaoJkRvUU/viewform) for minimal edits.  

#Open the Google Spreadsheet
Once you've created your form, open it and click the "Responses(0)" button (next to "Insert" and "Tools") in the header of the webpage.  This should open the Google Spreadsheet associated with this form. 

If you don't want to require a password to create a calendar event, skip the next step.   

Once the spreadsheet is open, click the plus button in the lower left hand corner.  This will add another sheet to your Google Spreadsheet.  This sheet will store the password.  Type "Password" into cell A1.  Type "Active/Inactive" into cell B2.  Type your password into A2 and the word "Active" into B2.  If at any time you'd like to deactive this password, simply replace "Active" with "Inactive."  If at any time you'd like to add additional passwords, type the password into the first column of the next availabile row and the word "Active" into the next column of the same row.  Your spreadsheet should now look like [this](https://docs.google.com/spreadsheets/d/1PQUAgUwXmqNQHDScQqke3hunVtQdmBa1K2rrp-vgiP8/edit?usp=sharing).  

#Add the custom script
Open the spreadsheet.  Click "Tools" --> "Script editor..." from the header of the webpage.  Select "Custom Function in Sheets" from the pop-up menu.  Copy and paste the [script code](https://github.com/kerdma6777/FormToCalendarEvent/blob/master/Google%20Script%20with%20Password).  If you formatted the Google Form exactly like mine, then all you have to do is replace "MyCalendarName" with the name of the Google Calendar you'd like events added to when CalendarApp.getCalendarsByName("MyCalendarName")[0] is called.  Then, click "Run" --> "createEvent" and "Run" --> "createTrigger" to complete the necessary authorizations.  Then, you're good to go!

If you didn't require a password.  Complete the above steps, but instead copy and paste this [script code](https://github.com/kerdma6777/FormToCalendarEvent/blob/master/Google%20Script%20without%20Password).

If you didn't follow the format of my Google Form exactly, then you'll have to change how variables are assigned in the createEvent function.  Note that because the data is stored in an array the index begins at 0, so the data stored in column 1 would be stored in the row[0].

