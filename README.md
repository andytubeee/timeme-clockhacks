# Clockhacks GitHub 

## Frontend

```
import { sendMsg } from 'backend/twilioUtil.jsw';

$w.onReady(function () {

    // Write your Javascript code here using the Velo framework API

    // Print hello world:
    // console.log("Hello world!");

    // Call functions on page elements, e.g.:

    // Click "Run", or Preview your site, to execute your code
});


/**
*	Adds an event handler that runs when the element is clicked.
	[Read more](https://www.wix.com/corvid/reference/$w.ClickableMixin.html#onClick)
*	 @param {$w.MouseEvent} event
*/
export async function submit_click(event) {
    // This function was added from the Properties & Events panel. To learn more, visit http://wix.to/UcBnC-4
    // Add your code for this event here:

    const firstName = $w('#input45').value;
    const lastName = $w('#input44').value;
    const phoneNum = $w('#input46').value;

    if (phoneNum.length < 10) {
        console.log("Phone number length not good");
    }
    // console.log(firstName.length > 0 && lastName.length > 0 && phoneNum.length === 10);
    if (firstName.length > 0 && phoneNum.length === 10) {
        $w('#button2').label = "Done";
        await sendMsg(firstName+" "+lastName, phoneNum);
        console.log("End");
    } else {
        console.error("Something is wrong");
    }
}

```

## Backend

```
const accountSid = 'dQw4w9WgXcQ'; // Your Account SID from www.twilio.com/console
const authToken = 'o-YBDTqX_ZU'; // Your Auth Token from www.twilio.com/console

const client = require('twilio')(accountSid, authToken);
const moment = require('moment-timezone');

export async function sendMsg(name, phoneNum) {
    const currentdate = new Date();
    const format = 'YYYY/MM/DD HH:mm:ss';
    const currentTime = moment().tz("America/Toronto").format(format);
 

    await client.messages
        .create({
            body: `${name}, here is the time you lazy person: ${currentTime}`,
            to: `+1${phoneNum}`, // Text this number
            from: '+18088099557', // From a valid Twilio number
        })
        .then((message) => console.log(message.sid)).catch((err)=>console.error(err)); 
}
```
