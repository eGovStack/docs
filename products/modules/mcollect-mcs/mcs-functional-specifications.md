# MCS Functional Specifications

## Introduction

This page provides an overview of mCollect functions to all stakeholders. mCollect is an application in which ULB employees can collect any miscellaneous tax or fee from the citizens and citizens can search for the payment receipts to download. mCollect helps ULBs to eliminate the use of manual receipt (G8-receipt) to capture miscellaneous payments at the counter and on the field. It also streamlines the end-of-day collection process in the ULBs by digitising all payment streams.

## Functional Scope

The platform is available for use in both mediums as web and mobile app. mCollect features can be broadly classified as the following modules: Registration, Login and Creation of User Profile Capture Payment (ULB Employee) Search Receipt (ULB Employee) Search Receipt (Citizen) Dashboards and Reports (ULB Employee) General Features

### Registration, Login and Creation of User Profile

This module provides enables the following capabilities:

* OTP Based Login for Citizen via Web/Mobile App&#x20;
* Credentials (Username & Password) based Login for Employee via Web/Mobile App&#x20;
* Provision for language selection during first time registration for both Employee and citizens&#x20;
* Provision of creating a personalized Profile for Citizens and employees on Web App&#x20;
* Login Credentials for the various hierarchies of employees&#x20;
* Role-based access for performing different actions

### Capture Payment (ULB Employee)

When an employee wants to capture payments made to the ULB by the citizen. He will click on the “New Collection” button and will land on the payment capturing page. The Employee will fill out all the service details and click on “Next” to go to the Payment page. Employees can come back to the details page from the payment page and update all the details too.

On the Payment page, the employee selects the payment instrument, enters the payer details and clicks on the “Generate Receipt” to capture the payment and generate the receipt for the same.

![](https://lh6.googleusercontent.com/VQa6Z0MPcAxbxQHhGUfUSnJnZu89q5hHaNyKXj6J1VmuLwFskNrzJLVI2fWk029k491GiYd\_0v-BIcExpETzbX3DamEPkKUoCnFMPOiScCg3z4f8hGqi8LWWhovG3FgnLOrUBSB1laXj2KBTFA)

![](https://lh4.googleusercontent.com/NULcWyKjpJxWm4jRbVDgoGVhLxFHW8fqWxJWCzd3EZw\_iXF3k3rXE2lDjVJisdZaVtLoJTkjLPQ7YcK0Fmuhg\_MndPFCHWCyLMotnb77bMX4jSeaHU6CWM5Qq9OJMw1njowzPiwBtX8UPBzUxQ)

![](https://lh4.googleusercontent.com/LcRfDCUWQmniC6KDJ7p4z4OgUCt25L9znE9ab4f5FH3XOpLezSJNyX3K-g5TvfXD8JwEH3ES0f4HatCwJPs4stXnQ-wlAQxqCakoaf-sa-Sqcxi75l\_odU3XM-FVkrEzfBcq8cjvlY5pRWTvJQ)

![](https://lh4.googleusercontent.com/3HOEn1bnuQJTlejlxCQ-BHfDFQ4NRZBZOO-uyWynW4IFUIk0q7LqCuo7XlMK28brGjIWQ3wv2eIE3hnbBz2jHID4BGu1e\_zmNuK5N8Ws14rGR3m1qtTqrokRbyexnuds\_THe5-MoMbKOH7UEKw)

### Search Receipt (ULB Employee)

When an employee wants to search for a receipt from a previous payment. He will search based on the given parameters. Search results will give a receipt download link along with other details.

![](https://lh6.googleusercontent.com/IoJpRXVSVuxNEOGS\_wllPdfVclzcEU7cu2QwKxWOB24MOsuP2jIYUNDvd5IrrjtGa7tW7OXATo7qyW5EXjh1TXnAwu22amR\_ngQr-t4CnkMHSTIILe81COFCmLB-VS-AxEwd9Axut4OYT3TJyQ)

![](https://lh3.googleusercontent.com/zT8X481K4nQfRos8M8GWymwD8YV5eTbm9GW5J5STQXa36LvmpmTMPgfuq0Zx0V-bJS5Yr9sVGbRDBwGqW9DG6GZ4ksjgxA9fWDn0ShiDPtszcr-nP0Mu6kbGjQae8HRpJ1T0e2q186NcKvCGVA)

### Search Receipt (Citizen)

When a citizen wants to search for a receipt from a previous payment. He will search based on the given parameters. Search results will give a receipt download link along with other details.

![](https://lh3.googleusercontent.com/rnzp7Qddhh-dQR0JCNuyiN4mhnxk3Zb-4nUglda2rbJdEEraEYLu7zD5aDSDAs4UrKWKvPf7lT0fe72LdNMxvGeWtMnpnphkiBd6GW4QWKC0ll7XI\_lOczzg-p8MAYKQM723v2pFZLQDhpDwTA)

![](https://lh4.googleusercontent.com/BTBPdhRaw7ukG948SuuqPw3c2HPanB\_9u-qIcb0tWe-7yTryxizarRGImmJPIh4633\_G1hYytFkLAuu8-NfWUYSEMEtqQxojYyBBf4wHsMiQJzNK8aHmb4g1HrY9cwJAWmzjtXkQQXToohgLDQ)

### Dashboard and Reports

Administrators want to monitor the collection to drive and plan ULB revenue targets. mCollect offers a receipt register report and a Dashboard to view the data and make data driven decisions.

The Report has the following filters: Collection Channel, Collection Mode, Service Type, Date Range. The Dashboard provides a view like the following screenshot.

![](https://lh4.googleusercontent.com/U69AN3X-uPCk3yo5LLwcL-gZH7ytWemiWpAc8P6JcGl1qkElgNXezSW95ZMERmlGpYmNBMULyoHi7ZC9IDiPwC65Ix\_UpA91ZMpy0M8SMXxlbwOsdxmZfSCpq0aMzlb8hK6HkQ42hIb8SuM\_TA)

### General Features

**Notifications:** The system has the capability to send notifications to citizens. The notification is sent to the citizen when a payment is made. The citizen gets a receipt download link in the notification. These notifications can be sent in the language chosen by the ULB through all channels - SMS, WhatsApp, and Email.

**Configurable Masters**&#x20;

* **Business Service Master:** To configure the Service Categories and Service Types for which mCollect can capture payments&#x20;
* Tax Head Master: To define the tax heads for each Service Type&#x20;
* Tax Period Master: To define a tax period for each Service Type



[![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)](http://creativecommons.org/licenses/by/4.0/)All content on this page by [eGov Foundation ](https://egov.org.in/)is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).
