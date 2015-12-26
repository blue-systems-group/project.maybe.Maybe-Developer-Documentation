# Communicate with Maybe backend

## Register
Only apply when Maybe backend doesn't have a record for this device.
In other words, this device is a new device for Maybe.

It needs to prepare all metadata for this device. The metadata contains `deviceid`, `model`, `capability`, `version of Android`, `version of Maybe Library`, `Cloud Messaging registration_id`.

We'll discuss more detail for `Cloud Messaging registration_id` later.

TODO: add all metadata above in Android Library.

After prepare metadata, use `POST` to register device on Maybe Backend.

### Update Device Information
Every time Maybe Library starts and Internet is available, it will `GET` information from maybe backend,
then check whether all information is updated.

If any field is out of date, it uses `PUT` to update the information.

## Get Choices Update
There're two mechanism to update choices: **pull** and **push**.

**Pull** means we have a repeated timer which will run in certain interval.
The library will check whether there is an update when the timer fired.
If there is an update, it will retrieve them and update internal data (in memory and storage).

**Push** means the device will get notification when new choice(s) for this device is/are ready.
This depends on Google Cloud Messaging. When maybe backend generates new choice(s) for certain devices, it will send a request to Google; then the library will get a notification from Google.
Following process is same as **pull** mechanism.

In short, **push** mechanism replaces **repeated timer** in **pull** mechanism by Google Cloud Messaging.

## Communicate with Google [Cloud Messaging](https://developers.google.com/cloud-messaging/)
We use Google Cloud Messaging as **push** mechanism for now. It can only deliver `4k` data in one message.
So we use it as a signal to indicate there're new choice(s) for the library.

To use Cloud Messaging, we need to get `registration_id` of Cloud Messaging from device, and tell our Maybe Backend.

# Get machine learning algorithms
We'll discuss this in [Machine Learning Delivery](machine-learning.md) chapter.
