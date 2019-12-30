# apns

Library for Apple Push Notification.


# Installation

go get github.com/StarTeleLogic/apns

# Sending a notification

package main
```go
import (
  "fmt"
   apns "github.com/StarTeleLogic/apns"
) 
````

# Define a function calling
```go
func main() {
SendSinglePushNotification("This is single push notification","<Device TOKEN>")
}
```

# Define function definition
```go
func SendSinglePushNotification(pushText string,deviceToken string)  {
       payload := apns.NewPayload()
       payload.Alert = pushText
       payload.Badge = 11
       payload.Sound = ""// left blank  to use default sound
       pn := apns.NewPushNotification()
       pn.DeviceToken = deviceToken
       pn.AddPayload(payload)
       client := apns.NewClient("gateway.sandbox.push.apple.com:2195", "./config/Certificates.pem", "./config/Certificates.pem")
       resp := client.Send(pn)
       alert, _ := pn.PayloadString()
       fmt.Println("Alert:", alert)
       fmt.Println("Success:", resp.Success)
       fmt.Println("Error:", resp.Error)
}
````

#### Returns
```json
Alert: {"aps":{"alert":"This is single push notification!","badge":42,"sound":""}} 
Success: true 
Error: <nil>
```
