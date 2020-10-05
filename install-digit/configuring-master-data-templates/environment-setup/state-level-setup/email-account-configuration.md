# Email Account Configuration

## Introduction <a id="Introduction"></a>

An email account of the client/state team has to be set up in order to receive/send the email notifications.

In order to achieve the functionality, an email account has to be set up at there server since most of the states would defer from creating an account with the Gmail/public server. Further, this email account has to be integrated with the various DIGIT modules.

## Data Table <a id="Data-Table"></a>

In order to achieve the above functionality, we require the below-mentioned details

| Sr. No. | Email ID | Your Name | Account Type | Incoming Mail Server | Outgoing Mail Server \(SMTP\) | Password | Incoming Server POP3 Port | Outgoing server SMTP Port | Encrypted Connection Type | Days after which the email should be removed from the server |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | [bihar@gmail.com](mailto:bihar@gmail.com) | Bihar | POP3 | SMTP | SMTP | \*\*\*\* | 192.172.82.12 | 192.172.82.12 | Auto | 14 |

Note: The values mentioned here are sample data.

## Procedure <a id="Procedure"></a>

### Data Definition <a id="Data-Definition"></a>

| Sr. No. | Column Name | Data Type | Data Size | Is Mandatory? | Description |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Email ID | Alphanumeric |  N/A | Yes | Email id which is being configured. |
| 2 | Your Name | Text |  256 | Yes |  The name on behalf of which the email would be sent in order to receive the updates. |
| 3 | Account Type | Alphanumeric |  64 | Yes | The type of email account type protocol which will be used to download messages. |
| 4 | Incoming Mail Server | Numeric | \(12,2\) |  Yes |  The IP address of the email server through which messages would be received. |
| 5 | Outgoing Mail Server\(SMTP\) | Numeric |  \(12,2\) | Yes |  The IP address of the email server through which messages would be sent. |
| 6 | Password | Alphanumeric |  64 | Yes |  The password of the email server. |
| 7 | Incoming Server POP3 Port | Numeric |  \(12,2\) | Yes |  The port number through which the emails are received. |
| 8 | Outgoing server SMTP Port | Numeric |  \(12,2\) | Yes |  The port number through which the emails are to be sent. |
| 9 | Encrypted Connection Type | Alphanumeric |  64 | Yes |  The encryption type which is used for the connection. |
| 10 | Days after which the email should be removed from the server | Numeric |  \(12,2\) | Yes |  The number of days after which the email should be deleted from the server \(not from the local device\). |

### Steps to fill Data <a id="Steps-to-fill-Data"></a>

Below steps could be followed in order to fill the template:

1. Download the data template attached to this page.
2. Get a good understanding of all the headers in the template sheet, their data type, size, and definitions by referring to the ‘Data Definition’ section of this document.
3. In case of any doubt, please reach out to the person who has shared this template with you to discuss and clear your doubts.
4. Ask the state to gather all the data related to the technical configuration from the email server settings.
5. Get the attached template filled from the state and a sample data is provided in the data table section for reference.
6. The data would be available in the POP and IMAP account settings at the server level.
7. Verify the data once again by going through the checklist and taking care of each and every point mentioned in the checklist.

## Checklist <a id="Checklist"></a>

The checklist is a set of activities to be performed one the data is filled into a template to ensure data type, size, and format of data is as per the expectation. These activities have been divided into 2 groups as given below.

### Common Checklist <a id="Common-Checklist"></a>

This checklist covers all the activities which are common across the entities.

| Sr. No. | Checklist Parameter | Example |
| :--- | :--- | :--- |
| 1 | Make sure that each and every point in this reference list has been taken care of. | [Checklist](https://digit-discuss.atlassian.net/wiki/spaces/DO/pages/502203140/Checklist) |

### Entity Specific Checklist <a id="Entity-Specific-Checklist"></a>

Not Applicable

## Attachments <a id="Attachments"></a>

1. Following is the template for which is used for collecting the data:
2. Configurable Data Template - Email Account Configuration
3. Configurable Sample Data - Email Account Configuration
