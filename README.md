# Node-RED with Watson IoT Platform Workshop HandsOn

_Program the Bluemix Innovation Platform without writing code!_

_Try some Watson / Bluemix / IoT Services_


## Overview
Skill Level: Beginner

With IBM Watson IoT Platform you can set up rules and actions that trigger from your IoT device data. The following recipe uses a simulated device to set cloud analytics rules and actions for three metrics: temperature, humidity and object temperature.

## Prerequisites:         

Bluemix Account, Browser (not Internet Explorer) 

Link to Bluemix console:   [console.ng.bluemix.net](https://console.ng.bluemix.net)

**We will use Bluemix in the "US South" region  for this workshop!**

Make sure that:

![bmx org](doc_img/bmx_org.png)

## Login to Bluemix & Create IoT Platform Starter incl. Node-RED runtime 

Go to the catalog and create the "Internet of Things Platform Starter" application ( Boilerplates Section )

![bmx starter](doc_img/bmx_iotp_starter.png)
 
you must give it a **unique name** ( this name is also your hostname and so needs to be unique across Bluemix.)

( I use:  [**red-iotp-workshop-m** - _mybluemix.net_](https://red-iotp-workshop-m.mybluemix.net) )

When the new app's dashboard appears, there is no reason to wait until the application is started. You can immediately open the section *Connections* from the menu on the left hand side and check, that there are two service instances bound to the app: an *Internet of Things Platform* service and a *Cloudant NoSQL DB* service.

## Registering the iotsensor with Watson IoT Platform

1. Before you can receive events and datapoints from a device, your must register it with the Watson IoT Platform. Open the **Internet of Things Platform** service and then **Launch** its IoT dashboard from the service's landing page.

1. In your Watson IoT Platform dashboard, select **Devices** from the menu pane, then click **Add Device** in the upper-right.
![bmx addDevice](doc_img/snap1.PNG)


1. Click **Create device type**. 

   Creating a device type will make it easier to find and identify the device after connecting it. Our device will identify itself as **device type** = *iotsensor_device* and **device ID** = *iotsensor*.

   Click **Create device type** again, then enter *iotsensor_device* as the **device type** name. On the next pages you may optionally define properties and metadata for the device type. Click **Next** on each page and finally finish the sequence by  clicking **Create**.
![bmx createDeviceType](doc_img/snap3.PNG)

1. Create a device definition

   You will return to the *Add Device* page, where your new device type is already pre-selected. Click **Next**, then enter *iotsensor* as the **Device ID**. Click **Next** twice.
   
   On the *Security* page either provide an authentication token, or accept an automatically generated token. Providing a memorable authentication token may be useful for recalling it later. Click **Next**.
   
   Verify that the summary information shown is correct and then click **Add**. From the device information page, copy and save the following device information
   
       Organization ID
       Device Type
       Device ID
       Authentication method
       Authentication token

![bmx deviceInformation](doc_img/snap7.PNG)


## Connect the iotsensor to the Watson IoT Platform

This step connects the "iotsensor" device to the registered device in your Watson IoT Platform organization. No device at hand? No problem! This time we use a simulated device. It's a web application, which can be called on any browser on your desktop or mobile phone or tablet.

1. In the Browser navigate to: http://watson-iot-sensor-simulator.mybluemix.net/

1. When prompted, enter the device information which you created in the Watson IoT Platform in the registration step before and saved it at the end.
![bmx configSensor](doc_img/snap8.PNG)

1. Verify that the connecting message changes to the name of your device, i.e. iotsensor. The device is now connected to the Watson IoT Platform.

1. In the Watson IoT Platform's *Device* dashboard, click your device and verify that data is being received.
![bmx deviceReceiveData](doc_img/snap9.PNG)


# Open the Node-RED editor 

You've seen the data coming in from the device to the Watson IoT Platform, what next? Now you will use your device in an application created with IBM Bluemix. This application is actually a node.js app, but you will not program the logic in JavaScript. Instead you will use the Node-RED framework (on top of node.js) to define a "flow of nodes" in the Node-RED editor.

So let's revisit the application you instantiated at the very beginning of this lab...

1. If not already visible in your browser, open the application dashboard. Check, that your app has successfully started in the meantime and is running now. Select the app URL or type it into the browser to open the **Node-RED flow editor**

    ```
    https://<appname>.mybluemix.net
    ```

1. You see a ready-made flow that can process temperature readings from a simulated device.

    ![](./images/nodered-defaultflow.png)

# Use Node-RED to read the sensor data

1. In the Node-RED workspace, double-click the **IBM IoT App In** node to open the configuration dialog.

    ![IOT App IN node](./images/iot-appnode.png)

1. In the Authentication type field, select **Quickstart** from the pull-down list. Enter the Device ID field and click OK.
<br />*Make sure that the device id is entered in lowercase, and that there are no leading or trailing space characters.*

1. Look for the **Deploy** button in the upper right hand corner of your Node-RED workspace. The deploy button is now red; click it to deploy your flow.

    ![Node-RED Deploy](./images/nodered-deploy.png)

1. Open the debug pane on the right. You will see that the flow is generating Temperature Status messages.

1. Increase the temperature value on the simulator to see the messages change in the debug pane.
<br /> *Note that a different message appears if the temperature exceeds 40 degrees.*

# Store the device data into a No SQL database

1. In Node-RED flow editor, add a **Cloudant out** node

    ![Cloudant out node](./images/nodered-cloudant.png)

1. In the Service type field, select the name of Cloudant service bound to Node.js runtime from the pull-down list.
<br />Enter a dabatase name in lowercase. Keep the default operation insert and finally give a name to the node.

  ![Cloudant configuration](./images/nodered-cloudantconfig.png)

1. Deploy the flow. Return to the Bluemix console, go to the Cloudant console and navigate into the records.

  ![Cloudant console](./images/cloudant-console.png)

# Translate messages with Watson.

The warning messages generated in Node-RED uses English by default. You may want to translate those messages into your oww language.

1. In Bluemix console, bind a new service **Language Translator** to your app.

1. In Node-RED flow editor, add a new **Language Translator** node to the flow.

1. Modify the flow accordingly to translate those messages.

    ![Watson Language Translator](./images/nodered-translationflow.png)

1. Deploy the updated flow.

1. Observe the translated output based on the selected language.


# Resources

For additional resources pay close attention to the following:

- [Real Time Data Analysis Using IoT Platform Analytics](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics)



## Optional step: create a board and some cards to visualize the data sent by your iotsensor device.

At this point, you can create a board and some cards from your Watson IoT Platform dashboard. Boards and cards can be used to keep track of device data, for example the temperature, humidity and object temperature data being sent by the iotsensor. To set up a new board follow these steps.
        In your Watson IoT Platform dashboard click Create New Board in the upper right.
        Give the board a name and description.
        Click Next then Create.
        Click on the board you have just created.
        Click Add New Card in the upper right. 
        Select the style of visualization, and select the iotsensor as the data source.


