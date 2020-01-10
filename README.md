# Simple-Form-2-Sheet
Simple way of making a mobile friendly web app form connected to a googel sheet. good for things like budget tracking.

1. clone repo

2. enable github pages (with index.html file)

3. make a copy of this google sheet: https://docs.google.com/spreadsheets/d/1Kxcjg0L9PvboSuwXtbRm1QIWNZyaB9kahwOweF4qO6E/copy?usp=sharing

4. change sharing to "anyone with the link can edit"

5. click help, type "scripts," open script editor

6. in script editor, you should have "HTML Form to Google Sheet," replace ID-GOES-HERE with the long string of charecters in your document's URL, something like 1DQKTERuAw4QlWLxQkkAkRnk4mBSzHJHOZAfyGNnaHv8. it should now look like:

```
function doGet(e) {
  doPost(e);
}
function doPost(e) {
  // Sheet
  var ss = SpreadsheetApp.openById("1DQKTERuAw4QlWLxQkkAkRnk4mBSzHJHOZAfyGNnaHv8");
  var sheet = ss.getSheetByName("Data");
  // Timestamp
  var timeZone = ss.getSpreadsheetTimeZone();
  var timestamp = Utilities.formatDate(new Date(), timeZone, "dd/MM/yyyy HH:mm:ss");
  // Write
  sheet.appendRow([timestamp, e.parameter.hill, e.parameter.name, e.parameter.time, e.parameter.buggy, e.parameter.note]);
  return ContentService.createTextOutput('false');
}
```

7. Publish>Deploy as webapp>Who has access to the app> anyone, even anonymous>update>accept permissions.

8. Publish>Deploy as webapp> | now copy "Current web app URL:"

9. open index.html and paste the web app url into the form tag's action where it says "curren-web-app-url"

10. save, commit, and push index.html

11. test your form

12. now that it works, change the values of `name="your data name"` in the index.html form, and match those to the column names in the google sheet, and the parameter names in the google script.

13. if you edit the google script, repeat steps 7 and 8, and increase the project version in the deploy screen by 1.
