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

<img src = "https://i.ibb.co/KKLBdg9/07.png" width = "700">

- Here we can see the services that we can use with this role, in this case this policy is just an example.
Note: If you doubt which policy to grab the role, choose the policy (AWSIoTFullAccess).

<img src = "https://i.ibb.co/T09tFjR/08.png" width = "700">

- We put the name we want to the new role.
<img src = "https://i.ibb.co/8XG3t5t/09.png" width = "700">

- We enter the AWS IoT console and go to the "Settings" section.

<img src = "https://i.ibb.co/hFcbkNT/10.png" width = "700">

- Once in the "Settings" section we will copy the "Endpoint", this will be used in the Soracom console tab.

<img src = "https://i.ibb.co/9V4QT8s/11.png" width = "700">

- The next step will be to create the connection between AWS IoT and the other AWS services such as Lambda, SNS and DynamoDB. So for that we will have to create a "Rule" which will serve to generate a bridge between this service and the aforementioned services.

<img src = "https://i.ibb.co/DgGFLZV/12.png" width = "700">

- Once we have our rule, we will configure it as shown in the image.

<img src = "https://i.ibb.co/8BkVC4K/13.png" width = "700">

- Already in this tab we will configure what lambda we want to be activated once a data arrives (not close until we finish configuring the other services)

<img src = "https://i.ibb.co/GfDnW68/14.png" width = "700">

## AWS Lambda Setup

- We create a Lambda as shown on the screen (it is quite intuitive, should not have problems).

<img src = "https://i.ibb.co/0jYH0Fz/15.png" width = "700">

- The lambda should be seen in this way, the reason for using a lambda would be because we need to process the data obtained from the module to give a response with a message and our web platform (do this process 2 times because we are going to configure 2 lambdas for connect to the services of SNS and DynamoDB)

<img src = "https://i.ibb.co/dptCCdH/16.png" width = "700">

### First Lambda SNS Service:

This is the code to send a notification to SNS, the TopicARN will be obtained later in the SNS configuration.

    console.log('Loading function');
    // Load the AWS SDK
    var AWS = require("aws-sdk");

    // Set up the code to call when the Lambda function is invoked
    exports.handler = (event, context, callback) => {
    // Load the message passed into the Lambda function into a JSON object 
    var eventText = JSON.parse(JSON.stringify(event, null, 2));


    // Log a message to the console; you can view this text in the Monitoring tab in the Lambda console or in the CloudWatch Logs console

    // Create a string, extracting the click type and serial number from the message sent by the AWS IoT button

    // Write the string to the console


    var temp=parseInt(eventText.temperature)
    var acc=parseInt(eventText.accelerometer)
    var moi=parseInt(eventText.moisture)
    var air=parseInt(eventText.air)
    var id=eventText.ID

    var myarray=[0,0,0,0]

    if(temp<15)
    {
    myarray[0]=4  
    }
    else if(temp >= 15 && temp < 18) 
    {
    myarray[0]=3  
    }
    else if(temp >= 18 && temp < 19) 
    {
    myarray[0]=2  
    }
    else if(temp >= 21 && temp < 24)  
    {
    myarray[0]=1  
    }
    else if(temp >= 24 && temp < 26) 
    {
    myarray[0]=2  
    }
    else if(temp >= 26 && temp < 28)  
    {
    myarray[0]=3  
    }
    else if(temp >= 28) 
    {
    myarray[0]=4  
    }

    temp=temp*1.8+32

    if(acc<3)
    {
    myarray[1]=1  
    }
    else if(acc >= 3 && acc < 6) 
    {
    myarray[1]=2  
    }
    else if(acc >= 6 && acc < 10) 
    {
    myarray[1]=3  
    }
    else if(acc >= 10)  
    {
    myarray[1]=4  
    }


    if(moi<20)
    {
    myarray[3]=4  
    }
    else if(moi >= 20 && moi < 30) 
    {
    myarray[3]=3  
    }
    else if(moi >= 30 && moi < 40) 
    {
    myarray[3]=2  
    }
    else if(moi >= 40 && moi < 50)  
    {
    myarray[3]=1  
    }
    else if(moi >= 50 && moi < 65) 
    {
    myarray[3]=2  
    }
    else if(moi >= 65 && moi < 80)  
    {
    myarray[3]=3  
    }
    else if(moi >= 80) 
    {
    myarray[3]=4  
    }

    air=0.5 * (temp + 61.0 + ((temp-68.0)*1.2) + (moi*0.094))        

    if(air<90)
    {
    myarray[2]=1  
    }
    else if(air >= 90 && air < 102) 
    {
    myarray[2]=2  
    }
    else if(air >= 102 && air < 122) 
    {
    myarray[2]=3  
    }
    else if(air >= 122)  
    {
    myarray[2]=4  
    }

    var mess="";

    if(myarray[3]==1 || myarray[2]==1 ||  myarray[1]==1 || myarray[0]==1)
    {
    mess="Your dog goes in perfect travel conditions"
    }
    if(myarray[3]==2 || myarray[2]==2 ||  myarray[1]==2 || myarray[0]==2)
    {
    mess="Your dog is in good condition"
    }
    if(myarray[3]==3 || myarray[2]==3 ||  myarray[1]==3 || myarray[0]==3)
    {
    mess="Your dog is fine but the travel conditions are not the best."
    }
    if(myarray[3]==4 || myarray[2]==4 ||  myarray[1]==4 || myarray[0]==4)
    {
    mess="Your dog is fine but travel conditions should improve"
    }

    // Create an SNS object
    var sns = new AWS.SNS();

    console.log("Received event:",JSON.stringify(myarray, null, 2),air);

    var params = {
    Message: mess,
    TopicArn: "YOURSNSENDPOINT"
    };
    sns.publish(params, context.done);

    };
    
### Second Lambda DynamoDB Service:

This is the code to send data to DynamoDB.

    console.log('Loading function');
    var AWS = require("aws-sdk");
    exports.handler = (event, context, callback) => {
    var eventText = JSON.parse(JSON.stringify(event, null, 2));
    var temp=parseInt(eventText.temperature)
    var acc=parseInt(eventText.accelerometer)
    var moi=parseInt(eventText.moisture)
    var air=0
    var id=eventText.ID

    var myarray=[0,0,0,0]


    if(temp<15)
    {
    myarray[0]=4  
    }
    else if(temp >= 15 && temp < 18) 
    {
    myarray[0]=3  
    }
    else if(temp >= 18 && temp < 19) 
    {
    myarray[0]=2  
    }
    else if(temp >= 21 && temp < 24)  
    {
    myarray[0]=1  
    }
    else if(temp >= 24 && temp < 26) 
    {
    myarray[0]=2  
    }
    else if(temp >= 26 && temp < 28)  
    {
    myarray[0]=3  
    }
    else if(temp >= 28) 
    {
    myarray[0]=4  
    }

    temp=temp*1.8+32

    if(acc<3)
    {
    myarray[1]=1  
    }
    else if(acc >= 3 && acc < 6) 
    {
    myarray[1]=2  
    }
    else if(acc >= 6 && acc < 10) 
    {
    myarray[1]=3  
    }
    else if(acc >= 10)  
    {
    myarray[1]=4  
    }


    if(moi<20)
    {
    myarray[3]=4  
    }
    else if(moi >= 20 && moi < 30) 
    {
    myarray[3]=3  
    }
    else if(moi >= 30 && moi < 40) 
    {
    myarray[3]=2  
    }
    else if(moi >= 40 && moi < 50)  
    {
    myarray[3]=1  
    }
    else if(moi >= 50 && moi < 65) 
    {
    myarray[3]=2  
    }
    else if(moi >= 65 && moi < 80)  
    {
    myarray[3]=3  
    }
    else if(moi >= 80) 
    {
    myarray[3]=4  
    }

    air=0.5 * (temp + 61.0 + ((temp-68.0)*1.2) + (moi*0.094))        

    if(air<90)
    {
    myarray[2]=1  
    }
    else if(air >= 90 && air < 102) 
    {
    myarray[2]=2  
    }
    else if(air >= 102 && air < 122) 
    {
    myarray[2]=3  
    }
    else if(air >= 122)  
    {
    myarray[2]=4  
    }


    // Set the region 
    AWS.config.update({region: 'ap-northeast-1'});

    // Create the DynamoDB service object
    var ddb = new AWS.DynamoDB({apiVersion: '2012-08-10'});

    var params = {
    TableName: 'FMPtemp',
    Item: {
    'ID' : {S: id},
    'Array' : {S: JSON.stringify(myarray, null, 2)}
    }
    };

    // Call DynamoDB to add the item to the table
    ddb.putItem(params, function(err, data) {if (err) {} else {}});
    };

## AWS SNS Setup:

- In the SNS service we created a topic

<img src = "https://i.ibb.co/2nZTHK0/17.png" width = "700">

- In the SNS service we created a topic.

<img src = "https://i.ibb.co/QCD3X5Z/18.png" width = "700">

- Since we create the topic we can create subscriptions where we want the notification to arrive.

<img src = "https://i.ibb.co/5hh3v6k/19.png" width = "700">

- This is an example of all sides that we can send notifications.

<img src = "https://i.ibb.co/F4WZ0xC/20.png" width = "700">

- Save this ARN for your First Lambda:

<img src = "https://i.ibb.co/xC8zm99/21.png" width = "700">

## AWS DynamoDB Setup:

For this project and for our web implementation, we will need 2 tables created in DynamoDB, since one we will use as data storage and another we will use it for temporary variables that we can use in the WEB platform.

- For this step, only two tables were created as shown in the image:

<img src = "https://i.ibb.co/MfmpWQN/22.png" width = "700">

## WEB Interface Setup:

The web platform may look simple, but it has a very interesting implementation in its way of interacting with AWS.

One of the biggest problems when working with a web page, is having temporary variables, because every time the page is updated, we will lose all the information stored by the variables, however in my implementation I extract data directly from DynamoDB, thanks to the javascript SDK that provides AWS, therefore I can store information in a database, as seen in the above image in the database called "FMP", and save temporary variables and quick access for the deployment and update of the web page "FMPtemp".

- At the time of displaying the web page, the FMPtemp database is called to obtain the status in real time of the pets and according to our algorithm determine the state of the pet in general, it will be notified by colors as shown in the image down.

<img src = "https://i.ibb.co/VvZP2wV/web.png" width = "700">

Each of the legs represents the following:

- Temp: Ambient Temperature
- Accel: Max Acceleration
- Air Q: Air Quality
- Moist: Air Moisture

Color Ranges:

| Paws                 | Temp                     | Accel      | Air Q                       | Moist          | 
|----------------------|--------------------------|------------|-----------------------------|----------------|
| Green Range Values   | 21<Temp<24               |Accel<3     |40<Air Q<50                  |  Moist<90      | 
| Yellow Range Values  | 18<Temp<21 or 24<Temp<26 |3<Accel<6   | 30<Air Q<40 or 50<Air Q<65  | 90<Moist<102   |
| Red Range Values     | 15<Temp<18 or 26<Temp<28 |6<Accel<10  | 20<Air Q<30 or 65<Air Q<80  | 102<Moist<122  |
| Black Range Values   | Temp<15 or 28<Temp       |10<Accel    | Air Q<20 or 80<Air Q        | 122<Moist      |

The air quality is calculated using the following formula using a reduced version to calculate the dew point of the air and according to the books it must be less than 90:

Air Q=0.5 * (temp + 61.0 + ((temp-68.0)*1.2) + (moist*0.094))   

## The Final Product:

- We assemble the temperature sensor in the case.
<img src = "https://i.ibb.co/68trBq1/IMG-20190425-212142-2.jpg" width = "700">
- We assembled the accelerometer in the case.
<img src = "https://i.ibb.co/0ZT4Lfp/IMG-20190425-212309-2.jpg" width = "700">
- Once we finish the assembly we will have something like that.
<img src = "https://i.ibb.co/Mp36spY/IMG-20190507-193102-2.jpg" width = "700">
- We keep the cables inside the case.
<img src = "https://i.ibb.co/QcDRcTn/IMG-20190507-193132-2.jpg" width = "700">
- We put the Battery for the module to start working.
<img src = "https://i.ibb.co/t2hvZXw/IMG-20190507-193143-2.jpg" width = "700">
- We close the case and admire our product.
<img src = "https://i.ibb.co/7R6tZpf/IMG-20190507-193152-2.jpg" width = "700">
- We admire more the final product and we notice that we have a hole where the temperature and humidity sensor can detect humidity and temperature.
<img src = "https://i.ibb.co/y8kfs5f/IMG-20190507-193204-2.jpg" width = "700">

Video: Click on the image. (Time of Our Epic Demo)
[![FMP - Demo](https://i.ibb.co/pwwW5qs/FMP.png)](https://www.youtube.com/watch?v=z4Z0MjegTp8)

Sorry github does not allow embed videos.
