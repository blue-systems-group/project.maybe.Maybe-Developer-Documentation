# Communicate with Maybe backend

## Register
Only apply when Maybe backend don't have record for this device.
In other words, this device is a new device for Maybe.

It need prepare all metadata for this device, include `deviceid`, `model`, `capability`, `version of Android`,
`version of Maybe Library`, `Cloud Messaging registration_id`.

We'll discuss more detail for `Cloud Messaging registration_id` later.

TODO: add all metadata above in Android Library.

After prepare metadata, use `POST` to register device on Maybe Backend.

### Update Device Information
Every time Maybe Library start and Internet is available. It'll `GET` information from maybe backend,
then check whether all information is updated.

If any field is out of date. It use `PUT` to update the information.

## Get Choices Update
There're two mechanism to update choices: **pull** and **push**.

**Pull** means we have a repeated timer will run in certain interval.
The library will check whether there're update when the timer fired.
If there're update, it'll retrieve them and update internal data (in memory and storage).

**Push** means the device will get notification when new choice(s) for this device is ready.
This depends on Google Cloud Messaging. When maybe backend generate new choice(s) for certain device.
It will send a request to Google, then the library will get a notification from Google.
Following process is same as **pull** mechanism.

In short, **push** mechanism replace **repeated timer** in **pull** mechanism by Google Cloud Messaging.

## Communicate with Google [Cloud Messaging](https://developers.google.com/cloud-messaging/)
We use Google Cloud Messaging as **push** mechanism for now. It can only deliver `4k` data in one message.
So we just it as an signal to indicate there're new choice(s) for library.

To use Cloud Messaging, we need to get `registration_id` of Cloud Messaging from device, and tell our Maybe Backend.

# Get machine learning algorithms
We'll discuss this in [Machine Learning Delivery](machine-learning.md) chapter.
