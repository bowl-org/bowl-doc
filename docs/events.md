# Socket Events API
## **Event Handlers**
### **``onlineChats``**
Online chats of current user
```json title="RESPONSE"
{
    contacts: ["bowl@example.com", "bowl2@example.com"],
    groups: [//TODO]
}
```
### **``chatMessage``**
Message packet that received from contact
```json title="RESPONSE"
{
    messageType: <Any>,
    message: "This is received message. It might be encrypted message too",
    date: "DD/MM/YY",
    time: "16:24",
    from: "bowl@example.com"
}
```
### **``connect_error``**
Socker error handling
```json title="RESPONSE"
Object(Error)
```
### **``online``**
 User become online
```json title="RESPONSE"
{
    email: "bowl@example.com"
}
```
### **``offline``**
 User become offline
```json title="RESPONSE"
{
    email: "bowl@example.com"
}
```
### **``contactRequestReceived``**
Contact request packet that received from contact
```js title="RESPONSE"
{
    name: "Bowl",
    email: "bowl@example.com",
    publicKey: Base64(PublicKey(type: "spki", format: "der"))
}
```
## **Event Emitters**
### **``acceptContactRequest``**
=== "SEND"
    ``` json title="SEND"
    {
        email: "bowl@example.com"
    }
    ```
=== "OK"
    ``` json title="RESPONSE"
    {
        status: "OK"
    }
    ```
=== "ERROR"
    ```json title="RESPONSE"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``declineContactRequest``**
=== "SEND"
    ``` json title="SEND"
    {
        email: "bowl@example.com"
    }
    ```
=== "OK"
    ``` json title="RESPONSE"
    {
        status: "OK"
    }
    ```
=== "ERROR"
    ```json title="RESPONSE"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``sendContactRequest``**
=== "SEND"
    ``` json title="SEND"
    {
        email:"bowl@example.com"
    }
    ```
=== "OK"
    ``` js title="RESPONSE"
    {
        status: "OK",
        contactData: {
            name: "Contact Name",
            email: "bowl@example.com",
            publicKey: Base64(PublicKey(type: "spki", format: "der"))
        }
    }
    ```
=== "ERROR"

    ```json title="RESPONSE"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``chatMessage``**
=== "SEND"
    ``` js title="SEND"
    {
        date: "DD/MM/YYYY",
        time: "01:23",
        messageType: <Any>,
        message: "This is message to send. It might be encrypted message too",
        to: "bowl@example.com"
    }
    ```
=== "OK"
    ``` json title="RESPONSE"
    {
        status: "OK"
    }
    ```
=== "ERROR"

    ```json title="RESPONSE"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
