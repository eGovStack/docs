# SMS Template Approval Process

According to TRAI’s regulation on unsolicited commercial communication, all telecoms must verify every SMS content before delivering it (Template scrubbing). For this, all the businesses using SMS need to register Entities, SenderIDs, SMS templates in a centralised DLT portal.\
\
Below are the steps to register the SMS template in a centralised DLT portal and to add the template in the SMS country portal (Service provider).

**Step 1:** Visit the **Airtel DLT portal**([![](https://dltconnect.airtel.in/static/img/fav.png)AIRTEL DLT](https://dltconnect.airtel.in/login/) ) and select your area of operation as **Enterprise** then click on next.

![](<../../../.gitbook/assets/Screenshot from 2021-09-27 18-49-15.png>)

**Step 2:** Login into the portal by entering the proper credentials and OTP.

{% hint style="info" %}
Please contact the HR manager for the credentials and the OTP.
{% endhint %}

![](<../../../.gitbook/assets/Screenshot from 2021-09-27 18-50-56.png>)

![](<../../../.gitbook/assets/Screenshot from 2021-09-27 17-17-10.png>)

**Step 3:** Now select the **Template** from option and then click on **content templates**.

![](../../../.gitbook/assets/imageedit\_2\_8566862511.jpg)

Now click on **Add** button to go to the next section.

![](../../../.gitbook/assets/imageedit\_6\_4107057795.jpg)

**Step 4:** Select the option mentioned in the image below.

![](../../../.gitbook/assets/imageedit\_18\_6753922375.jpg)

{% hint style="info" %}
Note:\
a) For placeholder text (dynamic text in message) mention **{#var#}** in the message. Each **{#var#}** can contains 0-30 character. If dynamic text is supposed to go more than 30 characters in length, then two **{#var#}** have to mention side by side. Now the dynamic text can be up to 60 characters.\
**Example**:- _Hi Citizen,_\
_Click on this link to pay the bill {#var#}{#var#}_\
\
_EGOVS_\
\
b) It is mandatory to mention _**EGOVS**_ at the end of every message.\
\
c) Select Template message Type as Regional if the message is in another language rather than English.
{% endhint %}

After clicking on the Save button, the template is added to the portal, Now wait for the approval of the template. Once the template gets approved save the template id and the message.

![](../../../.gitbook/assets/imageedit\_23\_9244125791.jpg)

**Step 5:** Repeat process from **Step 3** to **Step 4** to register template in DLT portal.

{% hint style="info" %}
Note: The below steps are to add approved templates in the SMS Country web portal. These steps might be different for other service providers but the data required for any service provider would be the same.
{% endhint %}

**Step 6:** Now, login into SMS Country portal ([![](https://www.smscountry.com/images/22.ico)Bulk SMS Software | Gateway and APIs | Bulk SMS Service |SMSCountry](https://www.smscountry.com/Index.aspx?msg=Logged%20out%20successfully) ) by entering proper credentials.

{% hint style="info" %}
Please contact the HR manager for the credentials.
{% endhint %}

![](<../../../.gitbook/assets/Screenshot from 2021-09-27 18-08-34.png>)

**Step 7:** Select option Features, then click on Manage button under Template section.

![](../../../.gitbook/assets/imageedit\_28\_8024855633.jpg)

Then click on **Add DLT Template** button.

![](../../../.gitbook/assets/imageedit\_31\_2340034251.jpg)

**Step 8:** Mention the template id and message of the approved template which we have saved earlier in step 4. And select sender id as **EGOVFS.**

![](<../../../.gitbook/assets/Screenshot from 2021-09-27 23-52-18.png>)

After adding all the above details click on **Add Template** button.\
Now the DLT approved template get added into SMS Country portal and it is ready to use.

{% hint style="info" %}
Select ISLanguage check box if the message is in any other language other than English.
{% endhint %}

**Step 9:** Repeat process from **Step 7** to **Step 8** to add approved template in SMS Country portal.



> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)_​_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_](https://egov.org.in/) _is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
