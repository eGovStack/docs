# Security Guidelines Handbook

## Best Practices

**POJO**

* Size validations on strings
* Regex validations wherever applicable
* @SafeHtml or custom annotation to block any html code in string fields

**File Upload**

* Rename files before storing
* The file should not be stored in the application folder
* Only required file extensions should be whitelisted
* Magic number should be checked for the file using a library like Apache Tika

**API**

* \_create API should have some sort of rate throttling on it
* \_search API should return results in a paginated manner
* Before whitelisting any API all use cases must be properly thought through(check if it can lead to any security loophole)
* Some sort of IP based throttling should be applied on whitelisted API to prevent DDoS attack
* Role action mapping should be thoroughly checked especially in the case of the CITIZEN role, only API required from Citizen UI should be mapped to the CITIZEN role
* Sensitive information should not be sent in URL (as a query param) instead should be sent in request body or in headers

**Coding Practises**

* Error handling should be proper. Custom Exception should be thrown instead of returning the complete stack trace
* For generating hash use a strong hashing algorithm like SHA-2
* Avoid capturing Java.Lang Security Exception
* Don’t throw exceptions in finally block
* Always close Input and Output resources in finally block
* Avoid using external input directly to create pathname that is intended to identify file or directory
* Scan for potential infinite loops. Avoid executing loops using user input directly
* Check for SQL injection. Always use prepared statements instead of directly creating query as string from input parameters
* Instead of standard pseudo-random generators use cryptographic PRNG
* Sensitive and Environment dependent properties like DB host and password should not be hardcoded and should be overwritten during deployment
* Avoid logging sensitive information or its exposure through error messages
* Do not compare class objects with getName() or getSimpleName() methods
* The setter method for an identifier property (id or composite-id) should be private
* Do not allow external input to control resource identifiers

## Detailed Guidelines

#### Privilege Escalation <a href="#privilege-escalation" id="privilege-escalation"></a>

Role Action mapping should be in accordance with the business requirements. No role should have access to resources that are not required by that role on UI. In the case of a CITIZEN role, extra precaution should be taken. If there is a business requirement for user-based access to entities instead of role-based access, validations should be added at the module level to verify the user id.

There is a possibility of horizontal/vertical escalation in the case of workflows. We have fixed this issue by validating the logged in user and the workflow item's owner. Allowing access if the logged-in user and the workflow owner are the same.

#### Failure to restrict URL Access <a href="#failure-to-restrict-url-access" id="failure-to-restrict-url-access"></a>

We use pre-signed URLs, so we cannot restrict access to the file if someone gets the URL. As a security measure, we should restrict the value of the URL validity to as minimum as possible. The value is configurable and can be overwritten in helm charts using the following property:

```
filestore-url-validity
```

#### Insecure direct object references (IDOR) <a href="#insecure-direct-object-references-idor" id="insecure-direct-object-references-idor"></a>

API’s like /user/\_search which exposes the personal data of users shouldn’t be directly exposed. We have removed access to the API from UI, the user information of logged in user can be instead fetched from /user/oauth/token which is now enhanced to return the required info.

#### Malicious file upload leads to Cross-Site scripting <a href="#malicious-file-upload-leads-to-cross-site-scripting" id="malicious-file-upload-leads-to-cross-site-scripting"></a>

Unrestricted file upload is a serious security risk. To tackle this problem we have a bunch of security validations. The file extension, content and content type in the header are all validated. We define the allowed extensions and their corresponding content type as a map and is configurable using the following property:

```
  allowed-file-formats-map: "{jpg:{'image/jpg','image/jpeg'},jpeg:{'image/jpeg','image/jpg'},png:{'image/png'},pdf:{'application/pdf'},odt:{'application/vnd.oasis.opendocument.text'},ods:{'application/vnd.oasis.opendocument.spreadsheet'},docx:{'application/x-tika-msoffice','application/x-tika-ooxml','application/vnd.oasis.opendocument.text'},doc:{'application/x-tika-msoffice','application/x-tika-ooxml','application/vnd.oasis.opendocument.text'},dxf:{'text/plain','application/dxf','application/octet-stream','image/vnd.dxf','image/vnd.dxf; format=ascii','image/vnd.dxf; format=binary','image/vnd.dxb'},csv:{'text/plain'},txt:{'text/plain'},xlsx:{'application/x-tika-ooxml','application/x-tika-msoffice','application/vnd.ms-excel'},xls:{'application/x-tika-ooxml','application/x-tika-msoffice','application/vnd.ms-excel'}}"
```

#### Improper Authentication <a href="#improper-authentication" id="improper-authentication"></a>

Before adding endpoints in the whitelist or mixed endpoints list all security implications should be thought through, as there will be no authentication or authorisation of the request. It’s a good practice to add origin-based rate limiting to avoid DDoS attack.

#### Missing Account Lockout <a href="#missing-account-lockout" id="missing-account-lockout"></a>

The account locking mechanism is provided in the DIGIT platform and should never be disabled. It helps in mitigating brute force attacks.

#### Request Throttling Attack <a href="#request-throttling-attack" id="request-throttling-attack"></a>

All \_create API’s should have some sort of rate throttling to avoid DDoS attack that can overwhelm the system. The rate-limiting can be achieved by configuring the endpoint in limiter.properties of zuul. Following is a sample configuration:

```
zuul.ratelimit.policy-list.tl-services[0].limit=5
zuul.ratelimit.policy-list.tl-services[0].quota=10000
zuul.ratelimit.policy-list.tl-services[0].refresh-interval=60
zuul.ratelimit.policy-list.tl-services[0].type[0]=url=/tl-services/v1/_create
zuul.ratelimit.policy-list.tl-services[0].type[1]=user
```

#### Weak Encoding Mechanism <a href="#weak-encoding-mechanism" id="weak-encoding-mechanism"></a>

Client secrets shouldn’t be sent in Base64 encoded format from UI, only for the server to server call the secret can be sent in Authorization header in Base64 format. We have removed client secret from the Authorization header in Digit Platform

#### Sensitive Information in URL <a href="#sensitive-information-in-url" id="sensitive-information-in-url"></a>

Avoid sending sensitive information in URL as a query param. Instead, it can be sent either in the request body or in headers. For example in the previous Digit version in \_logout API, authToken was sent in query param as below:

```
https://uat.digit.org/user/logout?access_token=04f03b3b-3db1-4127-ab3a-dedce685a428&tenantId=pg.citya
```

The API is now enhanced to accept the authToken in Request Body as below :

```
{
    "RequestInfo": {
        "apiId": "Rainmaker",
        "ver": ".01",
        "ts": "",
        "action": "_logout",
        "did": "1",
        "key": "",
        "msgId": "20170310130900|en_IN",
        "authToken": "04f03b3b-3db1-4127-ab3a-dedce685a4281"
    },
    "access_token": "04f03b3b-3db1-4127-ab3a-dedce685a428"
}
```

#### Lack of Automatic Session Expiration <a href="#lack-of-automatic-session-expiration" id="lack-of-automatic-session-expiration"></a>

Proper expiry time should be set for authToken validity. In case the authToken get’s stolen, it can be exploited only till the time the token is valid. The validity can be configured from the following two property in helm charts:

```
  access-token-validity: 15
  refresh-token-validity: 15
```

#### Concurrent Session <a href="#concurrent-session" id="concurrent-session"></a>

Multiple logins using the same user name and password should be avoided. Due to business requirement, we currently have not implemented the feature in Digit

#### Improper Error Handling <a href="#improper-error-handling" id="improper-error-handling"></a>

Errors should not expose any sensitive data or detailed error message to the end-user. Hackers can use this information to attack the system. Use of e.printStackTrace() should be avoided instead the error should be logged using logger. Always return a custom error message to the end-user.

```
// INCORRECT
try{
  // Some code
}
catch(Exception e){
  e.printStackTrace()
}

// OK
try{
  // Some code
}
catch(Exception e){
  log.error("ERROR_CODE", e)
}
```

#### Improper Input Validation <a href="#improper-input-validation" id="improper-input-validation"></a>

All user inputs should be validated before storing in DB. If not done attacker could use malicious input to\
modify data or possibly alter control flow in unexpected ways, including arbitrary command execution. In Digit we use annotations to validate user data Following is a sample validation using annotations:

```
@NotNull
@SafeHtml
@Size(max=64)
@JsonProperty("tenantId")
private String tenantId
```

#### Mail Command Injection <a href="#mail-command-injection" id="mail-command-injection"></a>

Validate any user input that is used to create an email subject line from user input. And encode special characters after proper canonicalization, and in particular, any line break (CR / LF) characters\
in the input, that attackers may use to inject unexpected headers in the mail message sent to the server.

#### Use of hardcoded credentials <a href="#use-of-hardcoded-credentials" id="use-of-hardcoded-credentials"></a>

Always overwrite sensitive values in application.properties during deployment. Never use hardcoded credentials. Generally, the sensitive values in application.properties will be like the DB user name and password, secrets etc. In Digit all the sensitive values are overwritten using kubernetes ConfigMaps. Following is examples of properties that we overwrite:

```
spring.datasource.url=jdbc:postgresql://localhost:5432/rainmaker_tl
spring.datasource.username=postgres
spring.datasource.password=postgres
```

#### Use of sensitive information into the configuration file <a href="#use-of-sensitive-information-into-configuration-file" id="use-of-sensitive-information-into-configuration-file"></a>

Make sure any sensitive information like authToken or secrets are not exposed in any configuration file.

#### Exclude unsanitized user input from format strings <a href="#exclude-unsanitized-user-input-from-format-strings" id="exclude-unsanitized-user-input-from-format-strings"></a>

If the format string is constructed with untrusted input, an attacker may produce unexpected application behaviour. It may cause an exception such as java.util.MissingFormatArgumentException to be thrown (which, if not cached, may lead to a denial-of-service condition), or information leak. Do not compose format strings from untrusted input. The arguments, except format string, to the formatting methods, are data and could contain format specifiers without any unexpected behaviour.

#### HTTP Parameter Pollution <a href="#http-parameter-pollution" id="http-parameter-pollution"></a>

Sanitize user input before using it in HTTP parameters. Concatenating unvalidated user input into a URL can allow an attacker to override the value of a request parameter

#### Standard pseudo-random number generators cannot withstand cryptographic attacks <a href="#standard-pseudo-random-number-generators-cannot-withstand-cryptographic-attacks" id="standard-pseudo-random-number-generators-cannot-withstand-cryptographic-attacks"></a>

There are two types of PRNGs: statistical and cryptographic. Statistical PRNGs provide useful statistical\
properties, but their output is highly predictable and form an easy to reproduce numeric stream that is unsuitable for use in cases where security depends on generated values being unpredictable. Cryptographic PRNGs address this problem by generating output that is more difficult to predict. In the latest release of Digit we have taken care of it by the following replacement:

```
Random random = new Random();
```

replaced with

```
SecureRandom random = new SecureRandom();
```

#### Weak cryptographic hash <a href="#weak-cryptographic-hash" id="weak-cryptographic-hash"></a>

The use of a weak hashing algorithm could compromise the original value. For example, if an authentication system takes an incoming password and generates a hash, then compares the hash to another hash stored in the authentication database, then the ability to create a collision could allow an attacker to provide an alternate password that produces the same target hash, bypassing authentication. It is recommended to use SHA-2 instead of SHA-1.

```
MessageDigest messageDigest1 = MessageDigest.getInstance(SHA_1); // INCORRECT

MessageDigest messageDigest2 = MessageDigest.getInstance(SHA_256); // OK

MessageDigest messageDigest3 = MessageDigest.getInstance("SHA-384"); // OK
```

#### Insecure SSL configuration <a href="#insecure-ssl-configuration" id="insecure-ssl-configuration"></a>

The problem with a flawed SSL configuration is that it may allow man-in-the-middle attacks and other issues. Following is a reference implementation:

```
SSLContext ctx = SSLContext.getInstance("SSL");
// FIXED, null here means to use the default (with proper validations) implementation
ctx.init(null, null, SecureRandom.getInstance("SHA1PRNG"));
HttpsURLConnection.setDefaultSSLSocketFactory(ctx.getSocketFactory());
URL url = new URL("https://spoofable.mybank.com/online-banking");
return url.openConnection().getInputStream();
```

#### Improper Neutralization of CRLF Sequences in HTTP Header <a href="#improper-neutralization-of-crlf-sequences-in-http-header" id="improper-neutralization-of-crlf-sequences-in-http-header"></a>

An attacker could inject line separators (CR/LF sequences) that could split the response message generated by the software into two messages. The second response is completely under the control of the attacker (intermediate web proxies may cache it), with could produce multiple conditions (web defacement, cache poisoning, cross-site scripting, or page hijacking). It is recommended to strip out any input which contains the %0d%0a URL encoded characters in HTTP request headers.

#### Avoid Capturing Java.Lang Security Exception <a href="#avoid-capturing-java.lang-security-exception" id="avoid-capturing-java.lang-security-exception"></a>

Security exceptions are related to security breaches such as denied permissions and improper use of the API. The code should not catch security exceptions except in specific cases where it may be necessary to mask some of these exceptions, for example, in the case of a log-on failure.

```
  // INCORRECT 
  catch (IllegalArgumentException e) {
                e.printStackTrace();
            } catch (SecurityException e) {
                e.printStackTrace();
            }
            
  //OK   
  catch (IllegalArgumentException e) {
                log.error("ERROR_CODE",e);
      }       
```

#### Always normalize system inputs <a href="#always-normalize-system-inputs" id="always-normalize-system-inputs"></a>

Not validating and normalizing the user input can lead to the execution of arbitrary code. An application’s strategy for avoiding cross-site scripting (XSS) vulnerabilities may include forbidding \<script> tags in inputs. Such blacklisting mechanisms are a useful part of a security strategy, even though they are insufficient for complete input validation and sanitization. When implemented, this form of\
validation must be performed only after normalizing the input. We handle this by annotating all string user input field with @SafetHtml annotation

```
	@SafeHtml
	@JsonProperty("ownershipCategory")
	private String ownershipCategory;
```

#### Avoid the Command Throws within Finally <a href="#avoid-the-command-throws-within-finally" id="avoid-the-command-throws-within-finally"></a>

Throwing an exception from within a finally block will mask any exception which was previously thrown in\
the try or catch block, and the masked's exception message and stack trace will be lost.

```
```

#### Close Input and Output resources in finally block <a href="#close-input-and-output-resources-in-finally-block" id="close-input-and-output-resources-in-finally-block"></a>

Failure to properly close resources will result in a resource leak which could bring first the application on to their knees. Always closes any input stream in finally block.

```
// INCORRECT
public void readMdmsConfigFiles(String masterConfigUrl) {
        log.info("Loading master configs from: " + masterConfigUrl);
        Resource resource = resourceLoader.getResource(masterConfigUrl);
        try {
            masterConfigMap = objectMapper.readValue(resource.getInputStream(), new TypeReference<Map<String, Map<String, Object>>>() {
            });
        } catch (IOException e) {
            log.error("Exception while fetching service map for: ", e);
        }
    }

// OK
public void readMdmsConfigFiles(String masterConfigUrl) {
        log.info("Loading master configs from: " + masterConfigUrl);
        Resource resource = resourceLoader.getResource(masterConfigUrl);
        InputStream inputStream = null;
        try {
            inputStream = resource.getInputStream();
            masterConfigMap = objectMapper.readValue(inputStream, new TypeReference<Map<String, Map<String, Object>>>() {
            });
        } catch (IOException e) {
            log.error("Exception while fetching service map for: ", e);
        } finally {
            IOUtils.closeQuietly(inputStream);
        }
    }
```

#### Cross Site Request Forgery <a href="#cross-site-request-forgery" id="cross-site-request-forgery"></a>

CSRF attack forces a logged-on victim’s browser to send a request to a vulnerable web application, which then performs the chosen action on behalf of the victim. A successful CSRF exploit can compromise end user data and operation in the case of a normal user. If the targeted end user is the administrator account, this can compromise the entire web application. For this attack to be successful, the user must be logged into the application.

We have fixed these CSRF issues by adding a CSRF Filter in the security filter chain. All requests mapped pass through the csrf filter and the csrf token validation happens in the filter. All the requests except GET required to pass a csrf token.

**applicationContext-security.xml**

```
<bean id="csrfFilter" class="org.egov.infra.web.filter.CsrfFilter">
       <constructor-arg name="csrfTokenRepository">
            <bean class="org.springframework.security.web.csrf.HttpSessionCsrfTokenRepository"/>
        </constructor-arg>
        <property name="accessDeniedHandler" ref="accessDeniedHandler"/>
</bean>
```

**applicationSecurityContext-\<modulename>.xml**

ex: applicationSecurityContext-egi.xml

```
<security:filter-chain pattern="/**"  filters="concurrentSessionFilter,securityContextPersistenceFilter,logoutFilter,authenticationProcessingFilter,headerWriterFilter,csrfFilter,securityContextHolderAwareRequestFilter,rememberMeAuthenticationFilter,anonymousAuthenticationFilter,exceptionTranslationFilter,filterSecurityInterceptor" />
```

#### Cross Site Scripting - Stored <a href="#cross-site-scripting-stored" id="cross-site-scripting-stored"></a>

Cross-site scripting is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application. It allows an attacker to circumvent the same origin policy, which is designed to segregate different websites from each other.

1. We have added a Validation Interceptor to validate the user input for all struts requests. Used OWASP AntiSamy policy to validate the user input.
2. Added entity level validation annotations to validate the entities used in spring requests.

**struts.xml**

```
<interceptor name="egov-validator" class="org.egov.infra.web.struts.interceptors.ValidationInterceptor" />
```

**XSSValidator.java**

```
public static String validate(String field, String input) {
        try {
            if (isBlank(input)) {
                return input;
            }
            CleanResults cr = getAntiSamy().scan(input, policy);
            if (!cr.getErrorMessages().isEmpty()) {
                if (LOG.isWarnEnabled())
                    LOG.warn(cr.getErrorMessages().toString());
                throw new ValidationException(field, "Invalid, contains unsafe value");
            }
            return input;
        } catch (PolicyException | ScanException exp) {
            throw new ApplicationRuntimeException("Error occurred while validating inputs", exp);
        }

    }
```

#### Insufficient Cookie Attributes <a href="#insufficient-cookie-attributes" id="insufficient-cookie-attributes"></a>

The application was missing the “Secure” cookie attribute which was carrying the session information (SessionID). The Secure attribute makes sure that the cookie will only be sent with requests made over an encrypted connection and an attacker will not be able to steal cookies by sniffing.

Added the missing secure cookie attribute

```
@Value("${secure.cookie}")
private boolean secureCookie;
	
@Bean
public CookieSerializer cookieSerializer() {
    DefaultCookieSerializer serializer = new DefaultCookieSerializer();
    serializer.setCookieName(SESSION_COOKIE_NAME);
    serializer.setCookiePath(SESSION_COOKIE_PATH);
    serializer.setUseSecureCookie(secureCookie);
    return serializer;
}
```

#### Code Injection <a href="#code-injection" id="code-injection"></a>

Application accepts the unvalidated user input. Interpreting user-controlled instructions at run-time can allow attackers to execute malicious code.

Fixed this issue by sanitizing the user input and removed eval().

```
function preventBack(){
	var sanitizedUrl = sanitizeHTML(document.URL);
	history.pushState(null, null, sanitizedUrl);
    window.addEventListener('popstate', function () {
        history.pushState(null, null, sanitizedUrl);
    });
}
function sanitizeHTML(text) {
	return jQuery('<div>').text(text).html();
}
```

#### Exclude unsanitized user input from format strings <a href="#exclude-unsanitized-user-input-from-format-strings.1" id="exclude-unsanitized-user-input-from-format-strings.1"></a>

Used format specifiers (%s, %d, %c etc) while constructing format strings instead of adding using the additional operator.

```
String validationMessage = String.format("Glcode: %1$s which  is mapped with Istrument type cheque in mdms is not exist in database",  accountCode.getGlcode());

cgvnNumber = String.format("%s/%s/%s%010d", vh.getFundId().getIdentifier(), getCgnType(vh.getType()), "CGVN",
				nextSequence);
```

#### Avoid data submissions to non-editable fields <a href="#avoid-data-submissions-to-non-editable-fields" id="avoid-data-submissions-to-non-editable-fields"></a>

Fixed this issue by using WebDataBinder.setDisallowedFields() to disallow id in request binding.

```
@InitBinder
public void initBinder(WebDataBinder binder) {
		binder.setDisallowedFields("id");
}
```

#### Potential Infinite Loops <a href="#potential-infinite-loops" id="potential-infinite-loops"></a>

Most of the loops present in the third party (YUI) libraries. So we have not changed this.

#### Avoid dangerous J2EE API, use replacements from security-focused libraries (like OWASP ESAPI) <a href="#avoid-dangerous-j2ee-api-use-replacements-from-security-focused-libraries-like-owasp-esapi" id="avoid-dangerous-j2ee-api-use-replacements-from-security-focused-libraries-like-owasp-esapi"></a>

Replaced the dangerous J2EE API with OWASP Enterprise Security API (ESAPI) equivalent APIs

**pom.xml**

```
<dependency>
            <groupId>org.owasp.esapi</groupId>
            <artifactId>esapi</artifactId>
            <version>2.2.3.1</version>
</dependency>
```

```
HTTPUtilities httpUtilities = ESAPI.httpUtilities();
httpUtilities.setCurrentHTTP(request, response);
httpUtilities.setHeader("Content-Type", mimeType);

referenceDocument = ESAPI.encoder().encodeForURL(referenceDocument);

ESAPI.httpUtilities().sendRedirect(request.getContextPath() + errorPage);

HTTPUtilities httpUtilities = ESAPI.httpUtilities();
httpUtilities.addHeader(response, "Cache-control", "no-cache, no-store, must-revalidate");
httpUtilities.addHeader(response, "Pragma", "no-cache");
httpUtilities.addHeader(response, "Expires", "-1");
httpUtilities.addHeader(response, "Vary", "*");
```

#### Do not allow external input to control resource identifiers <a href="#do-not-allow-external-input-to-control-resource-identifiers" id="do-not-allow-external-input-to-control-resource-identifiers"></a>

Sanitized the user input to fix this issue.

```
function sanitizeHTML(text) {
	return jQuery('<div>').text(text).html();
}

url: "/services/EGF/voucher/common-ajaxYearCode.action?departmentId="+sanitizeHTML(departmentid.value)
			+"&bankaccount="+sanitizeHTML(document.getElementById('bankaccount').value)
```

#### The setter method for an identifier property (id or composite-id) should be private <a href="#the-setter-method-for-an-identifier-property-id-or-composite-id-should-be-private" id="the-setter-method-for-an-identifier-property-id-or-composite-id-should-be-private"></a>

Changed the identifiers setter to private/protected

```
@Override
protected void setId(final Long id) {
  this.id = id;
}

private void setId(final Integer id) {
  this.id = id;
}
```

## **Frontend - Android APK**

**URL Redirection to Untrusted Site ('Open Redirect')**\
It was observed that the application redirects the user’s browser to a URL provided in a user request, without proper validation of the user input.\
_So it is recommended not to allow external input to modify the target URL. Perform a strict validation on the external input to ensure that the final URL is valid, appropriate for the application, and authorized_

```
window.open(validateAndReturn(strDest), "myresults");
validateAndReturn(url){
Validation Logic to prevent only Allowed URL to Redirect to External Website
}
```

**Exported activity must require permissions**

Activity can be exported by setting its attribute exported=true, or adding an intent-filter not setting attribute exported=false. To receive or bind them permission must be required, otherwise, any apps can access the activity

_It is recommended to set attribute exported=false or remove the intent-filter as default value without the intent is considered as false._

```
	<activity
			android:name="org.egovernment.mseva.MainActivity"
			android:launchMode="singleInstance"
			android:permission="dangerous"  // Set Permissions
			android:screenOrientation="portrait"> <!-- remove or alter as your apps requirement -->
			<intent-filter
				android:label="@string/app_name"
				android:exported="false">
				<action android:name="android.intent.action.VIEW" />
				<category android:name="android.intent.category.DEFAULT" />
				<category android:name="android.intent.category.BROWSABLE" />
				<data android:scheme="https"
					android:host="staging.digit.org"
					android:pathPattern=".*"
					android:pathPrefix="/" /> <!-- if you want only a specific directory from your website to be opened in the app through external links -->
			</intent-filter>
		</activity>
```

**Potential code injection via WebView.addJavaScriptInterface()**

Exposing Java objects to JavaScript could have negative security implications, such as code injection (allowing access to native phone functionality like sending SMS to premium numbers, accessing account information and sensitive data, etc.) Such code injection may, for example, do something like this (to launch a system command): exposedObj.getClass().forName('java.lang.Runtime').getMethod('getRuntime', null).invoke(null, null).exec(cmd)\
_To avoid this security issue, you may remove addJavaScriptInterface() when possible_

_Either_

_(1) remove the JavaScript/Java bridge (addJavascriptInterface) or_

_(2) make sure that the content loaded by WebView is really trusted (and place a suppression for violations when needed), or_

_(3) upgrade to API level 17 or higher and place a @JavascriptInterface annotation on allowed public methods, as in the following code_

```
	@JavascriptInterface    // Added Anotation to overcome this issue.
	public boolean isMsewaApp() {
		return true;
	}
```

**Intent Manipulation**

The application allows the user input to control Intent parameters that could enable an attacker to control the behaviour of the subsequent activity\
If untrusted input is inserted into certain parts of an Android Intent, without proper sanitization, a malicious user or app could force, via the tainted Intent, the execution of unintended code or inject malicious data in the vulnerable app. Certain Intent properties could change the expected semantics of the Intent, like setAction(), setClass(), setClassName(), or setComponent(). If the Intent is used to start an Activity or Service, for example, the attacker may change the expected element launched, with potential nefarious consequences\
_It is recommended to validate untrusted input that does not proceed from app-controlled resources, and in particular user interface fields and other Intents coming from other apps._

```
	void loadView(String url, Boolean tab) {
		Intent request = getIntent(); // possibly coming from a malicious app
		ComponentName component = request.getComponent();
		if(  isValidComponent(component) ) {  // Validating Intent
		if (tab) {
			Intent intent = new Intent(Intent.ACTION_VIEW);
			intent.setData(Uri.parse(url));
			startActivity(intent);
		} else {
			webView.loadUrl(url);
		}}
	}

	private boolean isValidComponent(ComponentName component) {  // Validation Logic
		String activityName = component.getClassName();
		if(activityName.contains("MainActivity")){ 
			return true;
		}
		return false;
	}
```

**Do not release debuggable apps**

It was observed that android:debuggable is set to true. Android allows the attribute android:debuggable to be set to true in the manifest so that the app can be debugged. By default this attribute is disabled, i.e., it is set to false, but it may be set to true to help with debugging during the development of the app. However, an app should never be released with this attribute set to true as it enables users to gain access to details of the app that should be kept secure.\
_The best practice is to set android:debuggable="false">_

**Enabling JavaScript is not recommended**\
WebView consumes web content that can include HTML and JavaScript from an external URL, improper use can introduce common web security issues such as cross-site-scripting (XSS, or JavaScript injection).

Android includes several mechanisms to reduce the scope of these potential issues by limiting the capability of WebView to the minimum functionality required by your application.

```
WebView webView = (WebView)findViewById(R.id.webView);
 webView.getSettings().setJavaScriptEnabled(false); // FIXED, is the default value
```

## **Frontend- Web Application**

**Do not use eval() function, for security and performance reasons**\
It was observed that the application uses eval(code)

If the end-user has control over evaluated code (because the code is concatenated with user data), this leads to 'script injection' vulnerabilities, which could end in well-known security attacks like cross-site scripting.

_It is recommended to avoid the use of eval(code)._

```
 <--  Wrong way using Eval -->

 if (wfSlaConfig) {
      if ((MAX_SLA - (MAX_SLA * eval(wfSlaConfig[0].slotPercentage)) <= sla) && sla <= MAX_SLA) {
        return wfSlaConfig[0].positiveSlabColor;
      } else if (0 < sla && sla < MAX_SLA - (MAX_SLA * eval(wfSlaConfig[0].slotPercentage))) {
        return wfSlaConfig[0].middleSlabColor;
      } else {
        return wfSlaConfig[0].negativeSlabColor;
      }
    }


<--  Correct way without Eval -->
if (wfSlaConfig) {
      if ((MAX_SLA - (MAX_SLA * wfSlaConfig[0].slotPercentage / 100) <= sla) && sla <= MAX_SLA) {
        return wfSlaConfig[0].positiveSlabColor;
      } else if (0 < sla && sla < MAX_SLA - (MAX_SLA * wfSlaConfig[0].slotPercentage / 100)) {
        return wfSlaConfig[0].middleSlabColor;
      } else {
        return wfSlaConfig[0].negativeSlabColor;
      }
    }
```

**Do not use dangerouslySetInnerHTML property in React components.**

dangerouslySetInnerHTML is React’s replacement for using innerHTML in the browser DOM. In general, setting HTML from code is risky because it’s easy to inadvertently expose your users to a cross-site scripting (XSS) attack.

_Avoid dangerouslySetInnerHTML, equivalent to the risky innerHTML in DOM, when possible. Try using HTML directly from React, but use dangerouslySetInnerHTML and pass an object with a \_\_html key._

**Avoid post cross-document messages with an overly permissive target origin**\
It was observed that the cross-document messaging feature has been used. The feature allows scripts to post messages to other windows. The corresponding API allows the user to specify the origin of the target window. However, caution should be taken when specifying the target origin because an overly permissive target origin will allow malicious script to communicate with the victim window in an inappropriate way.

_Always specify an exact target origin, not \*, when you use postMessage to send data to other windows. A malicious site can change the location of the window without your knowledge, and therefore it can intercept the data sent using postMessage._

We have Removed the instance as it was not required.

**Potential infinite loops**\
The application executing infinite loops using user inputs. would lead to denial of service.

_It Is recommended to a proper termination condition for every lo0ps_

```
All the user inputs included in the loop should have proper validation along with length check. 
while(true) {if(cond()) break;}
do { if(cond) break; } while(true);
function f() {
 while(true) {if(cond()) return;}
}
for(var i=0;i<P; i++) { ejecuta(); }
for(var i=Q;i<P; i+=3) { ejecuta(); }
for(var i=0,j=0;i<=N && j<=M; i++, ++j) { ejecuta(); }
for(var i=Q,j=E;i>=P && j>P2; i--, --j) { ejecuta(); }
for(var i=0;i<P; i--) { if(comprueba(i)) break; }
for(i=0;!(i<P); i--) { ejecuta(); }
```

**Never use JavaScript 'history' object or navigation-based positioning functions**\
Using 'history' (window.history, self.history) or navigation-based positioning functions (window.back(), window.forward()) is a bad practice for different reasons: \* POST: If a visited page was generated with POST, _the_ browser will emit a warning if the submitted data is not encoded in the URL. \* PRIVACY: No application should know which pages a user visited (browsers will emit a security alert and block access). \* POOR NAVIGATION LOGIC: The exact page sequence taken by users may not match programmer expectations

_It is recommended not to use the navigation history._

```
 window.location.replace(targetUrl); // OK, not using navigation history
```

> [![Creative Commons License](https://i.creativecommons.org/l/by/4.0/80x15.png)\_\_](http://creativecommons.org/licenses/by/4.0/)_All content on this page by_ [_eGov Foundation_ ](https://egov.org.in)_is licensed under a_ [_Creative Commons Attribution 4.0 International License_](http://creativecommons.org/licenses/by/4.0/)_._
