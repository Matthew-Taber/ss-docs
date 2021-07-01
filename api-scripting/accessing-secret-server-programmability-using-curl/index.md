[title]: # (Accessing Secret Server Programmatically Using cURL)
[tags]: # (programmability,curl)
[priority]: # (1000)

# Accessing Secret Server Programmatically Using cURL

[cURL]( http://curl.haxx.se/) is a command-line tool for transferring data with URL syntax.

Click to access the [curl Download Wizard](http://curl.haxx.se/dlwiz/?type=bin).

>**Note**: When using curl with Secret Server's web services, it is important to use legacy methods whenever possible.
For example, use `GetSecretLegacy` instead of `GetSecret`.

## Using cURL with Method 1

Use the <http://your-secret-server-url/webservices/sswebservice.asmx> web service.
 >**Note**: A call to Authenticate must be made first. The token returned by this method is required by all the other methods.

### Step 1: Authenticate

`curl -v -H "Content-Type: application/x-www-form-urlencoded" -d "username={NAME}&password={PASSWORD}&organization=&domain=" --url "http://your-secret-server-url/webservices/sswebservice.asmx/Authenticate""`

The action returns the token in the form below:

```xml

<?xml version="1.0" encoding="utf-8"?>
<AuthenticateResult xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"" xmlns:
xsd="http://www.w3.org/2001/XMLSchema"" xmlns="urn:thesecretserver.com">
  <Errors />
  <Token>{TOKEN}</Token>
</AuthenticateResult>

```

### Step 2: Get Secret

`curl -v -H "Content-Type: application/x-www-form-urlencoded" -d "secretId={SECRET ID}&token={TOKEN}" --url "http://your-secret-server-url/webservices/sswebservice.asmx/GetSecretLegacy""`

The action returns the requested secret in XML form similar to the following:

```xml

<?xml version="1.0" encoding="utf-8"?>
<GetSecretResult xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"" xmlns:xsd
="http://www.w3.org/2001/XMLSchema"" xmlns="urn:thesecretserver.com">
  <Errors />
  <Secret>
    <Name>{SECRET NAME}</Name>
    <Items>
      <SecretItem>
        <Value>ABCDEF</Value>
        <Id>1</Id>
        <FieldId>1</FieldId>
        <FieldName>FullName</FieldName>
        <IsFile>false</IsFile>
        <IsNotes>false</IsNotes>
        <IsPassword>false</IsPassword>
        <FieldDisplayName>Full Name</FieldDisplayName>
      </SecretItem>
      {MORE SECRET ITEMS HERE...}
    </Items>
    <Id>1</Id>
    <SecretTypeId>1</SecretTypeId>
    <FolderId>1</FolderId>
    <IsWebLauncher>false</IsWebLauncher>
  </Secret>
</GetSecretResult>

```

## Using cURL with Method 2

Use the <http://your-secret-server-url/winauthwebservices/sswinauthwebservice.asmx> web service.
>**Note**: The user making the call must be NTLM authenticated and must already exist as a domain user who is enabled in Secret Server.

`curl --ntlm --url "<http://your-secret-server-url/winauthwebservices/sswinauthwebservice.asmx/GetSecretLegacy?secretId={SECRET> ID}" --user "{USER}:{PASSWORD}"`

The action returns the secret in the same XML format displayed above.
