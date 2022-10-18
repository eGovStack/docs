# Xstate-Chatbot Message Localisation

**Objective:** This document aims to facilitate communication between the software developers and whoever is localising the chatbot messages. The goal is to make it clear and unambiguous.

Click on the link to the google sheet below to access all the messages with the codes:

[<img src="https://developers.google.com/drive/images/drive_icon.png" alt="" data-size="line">https://docs.google.com/spreadsheets/d/1j5ldAHbwdR2jTCgUuxlrEdLKDZuHmkJg589v7OML-eA/edit?usp=sharing - Connect to preview](https://docs.google.com/spreadsheets/d/1j5ldAHbwdR2jTCgUuxlrEdLKDZuHmkJg589v7OML-eA/edit?usp=sharing)

## Message Localisation Details

### Project Structure

The project is organised such that all the messages are contained within the files present inside the /machine directory. /service directory, which is present inside it, also includes files that could contain localization messages.

Guidelines to be followed by developers:

_(According to the standard pattern followed in the project, all the localization messages will be present near the end of the file in a JavaScript object named “messages”.)_

Developers will be the ones first filling up the sheet with codes (and the English version of the messages). Below are the guidelines to be followed when writing the codes in the sheet:

1. The standard separator to be used is .(dot)
2. The first part is the filename—Eg: “pgr.”, when the filename is pgr.js.
3. Use “service.” as a prefix when the file is present inside the /service directory.
   * In the /service directory, filenames are like egov-pgr.js
   * For localization messages contained in those files, instead of writing “egov-pgr” just write “pgr”
   * So the prefix for such files would be “service.pgr.”
4. All the message bundles would be present in the “messages” object near the end of the file. They have been organized in a pattern in the JS object like fileComplaint.complaintType2Step.category.question
   * The corresponding localization code for such a message bundle in the sheet would be “pgr.fileComplaint.complaintType2Step.category.question”, where the first “pgr.” is added as the prefix for the file name.

### Message Writing Guidelines <a href="#guidelines-for-writing-messages" id="guidelines-for-writing-messages"></a>

Once the localization codes have been written correctly (and the English version of the messages) in the sheet, it is easy to add the new message in the corresponding new column.&#x20;

Some guidelines to follow when adding new messages:

1. The parameter names are written within \{{\}} _(double curly brackets)._
2. The content inside these curly brackets should be written in English even when writing messages for any new language.



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this website by_ [_eGov Foundation_ ](https://egov.org.in/)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
