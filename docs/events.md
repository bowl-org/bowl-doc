# Socket Events API
## **Event Handlers**
### **``onlineChats``**
Online chats of connected user.
```js title="RECEIVED PACKET"
{
    contacts: ["bowl@example.com", "bowl2@example.com"...],
    groups: [
        {
            groupId: "12 byte unique group id1",
            persons: ["bowl2@example.com", "bowl3@example.com"...]
        },
        {
            groupId: "12 byte unique group id2",
            persons: ["bowl@example.com", "bowl4@example.com"...]
        }
        ...
    ]
}
```
### **``contactChatMessage``**
Message packet that received from contact. Message has to be decrypted using private key of connected user.
```json title="RECEIVED PACKET"
{
    messageType: <Any>,
    message: "This received contact message is encrypted",
    date: "DD/MM/YY",
    time: "16:24",
    from: "bowl@example.com"
}
```
### **``groupChatMessage``**
Message packet that received from group. Message has to be decrypted using group key.
```json title="RECEIVED PACKET"
{
    groupId: "12 byte unique group id.",
    messageType: <Any>,
    message: "This received group message is encrypted",
    date: "DD/MM/YY",
    time: "16:24",
    from: "bowl@example.com"
}
```
### **``connect_error``**
Socker error handling.
```json title="RECEIVED PACKET"
Object(Error)
```
### **``online``**
Person become online.
```json title="RECEIVED PACKET"
{
    email: "bowl@example.com"
}
```
### **``offline``**
Person become offline.
```json title="RECEIVED PACKET"
{
    email: "bowl@example.com"
}
```
### **``contactRequestReceived``**
Received contact request packet.
```js title="RECEIVED PACKET"
{
    name: "Bowl",
    email: "bowl@example.com",
    publicKey: Base64(PublicKey(type: "spki", format: "der"))
}
```
### **``groupRequestReceived``**
Received group request packet. Encrypted group key has to be decrypted using private key of connected user. Decrypted group key format is AES256.
```js title="RECEIVED PACKET"
{
    name: "The Bowl Group",
    description: "This is description of group.",
    groupId: "12 byte unique group id.",
    encryptedGroupKey: "This is encrypted group key that encrypted with public key of connected user"
}
```
### **``newGroupMember``**
Received new group member packet.
```js title="RECEIVED PACKET"
{
    groupId: "12 byte unique group id.",
    name: "Member",
    email: "bowl@example.com",
    publicKey: Base64(PublicKey(type: "spki", format: "der"))
}
```
## **Event Emitters**
### **``contactChatMessage``**
Send encrypted chat message to contact. Message has to be encrypted using public key of contact.
=== "SEND"
    ``` js title="SEND"
    {
        date: "DD/MM/YYYY",
        time: "01:23",
        messageType: <Any>,
        message: "This sent contact message is encrypted",
        to: "bowl@example.com"
    }
    ```
=== "OK"
    ``` json title="RECEIVED PACKET"
    {
        status: "OK"
    }
    ```
=== "ERROR"

    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``groupChatMessage``**
Send encrypted chat message to group. Message has to be encrypted using group key.
=== "SEND"
    ``` js title="SEND"
    {
        groupId: "12 byte unique group id.",
        date: "DD/MM/YYYY",
        time: "01:23",
        messageType: <Any>,
        message: "This sent group message is encrypted",
    }
    ```
=== "OK"
    ``` json title="RECEIVED PACKET"
    {
        status: "OK"
    }
    ```
=== "ERROR"

    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``acceptContactRequest``**
Accept contact request that received.
=== "SEND"
    ``` json title="SEND"
    {
        email: "bowl@example.com"
    }
    ```
=== "OK"
    ``` json title="RECEIVED PACKET"
    {
        status: "OK"
    }
    ```
=== "ERROR"
    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``declineContactRequest``**
Decline contact request that received.
=== "SEND"
    ``` json title="SEND"
    {
        email: "bowl@example.com"
    }
    ```
=== "OK"
    ``` json title="RECEIVED PACKET"
    {
        status: "OK"
    }
    ```
=== "ERROR"
    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``sendContactRequest``**
Send contact request to person.
=== "SEND"
    ``` json title="SEND"
    {
        email:"bowl@example.com"
    }
    ```
=== "OK"
    ``` js title="RECEIVED PACKET"
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

    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``acceptGroupRequest``**
Accept group request that received.
=== "SEND"
    ``` json title="SEND"
    {
        groupId: "12 byte unique group id."
    }
    ```
=== "OK"
    ``` json title="RECEIVED PACKET"
    {
        status: "OK"
    }
    ```
=== "ERROR"
    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``declineGroupRequest``**
Decline group request that received.
=== "SEND"
    ``` json title="SEND"
    {
        groupId: "12 byte unique group id."
    }
    ```
=== "OK"
    ``` json title="RECEIVED PACKET"
    {
        status: "OK"
    }
    ```
=== "ERROR"
    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
### **``sendGroupRequest``**
Send group request to person. Group key has to be encrypted using public key of person. In order to encrypt key connected user needs to get public key of person.
=== "SEND"
    ``` json title="SEND"
    {
        groupId: "12 byte unique group id."
        encryptedGroupKey: "This is encrypted group key that encrypted with public key of target user",
        email:"bowl@example.com"
    }
    ```
=== "OK"
    ``` js title="RECEIVED PACKET"
    {
        status: "OK",
        personData: {
            name: "Member Name",
            email: "bowl@example.com",
            publicKey: Base64(PublicKey(type: "spki", format: "der"))
        }
    }
    ```
=== "ERROR"

    ```json title="RECEIVED PACKET"
    {
        status: "ERROR",
        error: "This is error message"
    }
    ```
