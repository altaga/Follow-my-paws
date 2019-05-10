# Follow my paws

<img src="https://i.ibb.co/pwwW5qs/FMP.png" width="500">

If you have a dog, cat or any pet that needs to go into a kennel when travelling and be left in the hands of parcel services, you know how stressfull and problematic it is for your precious friends. The main problem thus is: The horrid care pets get when they are transported in parcel services. Sometimes we need to send pets with parcel services. How can we be sure they're fine at all times? Take into consideration how baggage is treated.

Always use technology to improve the world, if you are a black hat or gray hat hacker please abstain at this point ......... or at least leave your star to make me feel less guilty XP.

# Table of contents
* [Introduction](#introduction)
* [Materials](#materials)
* [Hardware Hacking](#hardware-hacking)
* [Wio Setup](#wio-setup)
* [Wio Arduino Setup](#wio-arduino-setup)
* [Soracom Platform Setup](#soracom-platform-setup)
* [AWS IoT Setup](#aws-iot-setup)
* [AWS Lambda Setup](#aws-lambda-setup)
* [AWS SNS Setup](#aws-sns-setup)
* [AWS DynamoDB Setup](#aws-dynamodb-setup)
* [WEB Interface Setup](#web-interface-setup)
* [The Final Product](#the-final-product)
* [Future Rollout](#future-rollout)
* [References](#references)

## Introduction:

The horrid care pets get when they are transported in parcel services. Sometimes we need to send pets with parcel services. How can we be sure they're fine at all times? Take into consideration how baggage is treated.

<img src="https://i.ibb.co/rtkSBcX/177088359.jpg" width="500">

I will make an integral IoT solution to monitor the pet’s environment, in order to ensure their well-being throughout their journey, all this also integrated with a cloud platform which, in addition to showing me the status of the package in real time, also sends notifications at the frequency that is convenient. 

The current monitoring solutions are restricted to only lifeless packages, this making the continuous monitoring of pets a novelty. It is useful because thanks to this system pet owners can be 100% sure that their pets will be well and can monitor and follow them throughout their journey.

## Materials:

Hardware: 

- WIO Lte. 
- Soracom Air Global IoT SIM Card.
- DTH11 (Preferably the Grove version).
https://www.seeedstudio.com/Grove-Temperature-Humidity-Sensor-DHT11-p-745.html
- Grove - 3-Axis Digital Accelerometer.

Software: 

- Arduino IDE. 
- AWS Cloud Services.
- Soracom Platform.

## Hardware Hacking:

To connect the sensors to the WIO, it is necessary that the sensors have a Grove-type input, such as those shown in the following link.

https://www.seeedstudio.com/catalogsearch/result/index/?cat=890&q=Grove

For this project, I buy the "Grove Starter Kit Plus" package which is shown in the following images.

<img src = "https://i.ibb.co/rw19pcY/IMG-20190417-034237.jpg" width = "500">

The Content:

<img src = "https://www.mouser.mx/images/microsites/grovekitgalileo.jpg" width = "700">

The connections that were made were the following.

<img src = "https://i.ibb.co/5ryXPNm/Untitled-Sketch-bb.png" width = "700">

The accelerometer Grove had no problem connecting to the WIO because it already has its Grove entry, which had to hack was the DHT, as it did not have the Grove version DHT.

Accelerometer Grove Version:

<img src = "https://i.ibb.co/0ZT4Lfp/IMG-20190425-212309-2.jpg" width = "700">

DHT No-Grove Version:

<img src = "https://i.ibb.co/68trBq1/IMG-20190425-212142-2.jpg" width = "700">

This is how to connect the module to the grove cable:

<img src = "https://i.ibb.co/FDw8Q32/IMG-20190507-194743-2.jpg" width = "700">

## Wio Setup:

We will prepare the WIO LTE by connecting the SIM card in the appropriate slot.

<img src = "https://i.ibb.co/87hmB2L/Slot.png" width = "700">

Once we locate the Slot of the SIM card, insert the SIM card into the slot (yes, protect your IMEI and other data).

<img src = "https://i.ibb.co/98H4NN6/DSC07614.png" width = "700">

This will be seen once the card is inserted completely.

<img src = "https://i.ibb.co/pvcWMz6/DSC07615.png" width = "700">

Since we have the SIM card in the WIO LTE, we will connect the antennas to the slots shown in the image below.

<img src = "https://i.ibb.co/1K1v2wD/Antenna.png" width = "700">

Once we finish this, we will have ready our module to use it with Arduino IDE.

## Wio Arduino Setup:

This is the official guide to install WIO LTE on Arduino IDE. I recommend that they follow it 100%, it is very clear and concise.

https://github.com/Seeed-Studio/Wio_LTE_Arduino_Library

## Soracom Platform Setup:

It is very important to check that our SIM card is already attached to a group, in my case I call it Harvest Group.

<img src = "https://i.ibb.co/q0ZXn00/01.png" width = "700">

In the case that we do not have a group created, we will create one as shown in the image below, if we do not do this we will not be able to perform the AWS IoT configuration.

<img src = "https://i.ibb.co/N6NXMjh/02.png" width = "700">

Since the group was created, in my case we entered the group menu by pressing "Harvest Group" and once inside we will see the following.

<img src = "https://i.ibb.co/QKbcXjD/03.png" width = "700">

Within the group menu we will enter the option "SORACOM Funnel", this option will allow us the connectivity with the services of AWS, all the credentials will be obtained later in the AWS configuration, so do not close this tab (Please follow).

<img src = "https://i.ibb.co/tb2xk57/05.png" width = "700">

## AWS IoT Setup

To communicate with AWS IoT we need to create a role in the IAM console in order to authorize Soracom access to our console.

- The first step is to create a role that allows us to communicate with AWS.

<img src = "https://i.ibb.co/Yj0Gk39/06.png" width = "700">

- Within the role configuration we need to grant access to AWS IoT.

<img src = "https://i.ibb.co/6sms88y/07.png" width = "700">

- Here we can see the services that we can use with this role, in this case this policy is just an example.
Note: If you doubt which policy to grab the role, choose the policy (AWSIoTFullAccess).

<img src = "https://i.ibb.co/DKZR4v6/08.png" width = "700">

- We put the name we want to the new role.

<img src = "https://i.ibb.co/cvvMg63/09.png" width = "700">

- Entramos a la consola de AWS IoT y nos vamos a la seccion de "Settings".

<img src = "https://i.ibb.co/hFcbkNT/10.png" width = "700">

- Una vez en la seccion de "Settings" copiaremos el "Endpoint", este lo usaremos en la pestaña de la consola de Soracom.

<img src = "https://i.ibb.co/9V4QT8s/11.png" width = "700">















