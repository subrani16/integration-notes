---
title: Ganz Cortrol VCAedge Integration Note v1.0.0
logo: assets/images/ganz-logo.png
---

# Introduction

## Prerequisites

-   IPM series camera.
-   VCAedge video analytics plug-in version 1.0.41 or greater.
-   Ganz Cortrol Premier VMS version 1.19 or greater.

## Supported features

-   All VCAedge event notification methods are available.

## Architecture

In this integration, the Ganz Cortrol VMS receives the annotated RTSP stream from the IPM camera and the Data
Source alarms are sent through the TCP notifications with VCA tokens containing details about the event.

![](assets/images/ipm-ganz-architecture.png)

# IPM Camera Configuration

## Video & Audio Settings

### Confirming the RTSP stream used for transmitting video footage

Check and change if required, the RTSP stream settings used by the IP camera for external connections to the channels.

1.  From the **Setup** menu, click on **VIDEO & AUDIO** and then, click on **VIDEO**.

    ![](assets/images/ipm-video-menu.png)

2.  Note the *Live Video Channel* settings as these will be needed when connecting to the RTSP stream from the Nx
    Witness server.

    ![](assets/images/ipm-video-configuration.png)

## Network Settings

### Confirming the RTSP port used for transmitting video footage

Check and change if required, the RTSP port used by the IP camera for external connections to the channels.

1.  From the **Setup** menu, click on **NETWORK** and then, click on **NETWORK SETTINGS**.

    ![](assets/images/ipm-network-settings-menu.png)

2.  Note the **IP Setup** and **Port Setup** as these will be needed when connecting to the RTSP stream from the Nx
    Witness server.

    ![](assets/images/ipm-vca-network-settings.png)

## Configuring The VCAedge Plug-in

The VCAedge plug-in is a set of analytical tools that can be loaded onto supported cameras. It provides the means to
perform advanced analytics and reduce false alerts when events occur. _Make sure you have a valid license that will_
_enable the VCAedge engine and all the features available._

Configure the VCAedge plug-in as required with the appropriate tracker, rules and a notification. A basic setup is
detailed below as an example.

### Enabling VCA

1.  From the **Setup** menu, click on **VCA** in the left side. Then, click on **ENABLE**.

    ![](assets/images/ipm-vca-enable-menu.png)

2.  Turn on the video analytics features and click **Apply** located at the bottom to save the configuration.

    ![](assets/images/ipm-vca-enable-config.png)

### Creating Rules

1.  From the **VCAedge** menu, click on **RULES** in the left side.

    ![](assets/images/ipm-vca-rules-menu.png)

2.  Click **Add** located at the bottom to display a list of available rules.

    ![](assets/images/ipm-vca-rules-list.png)

3.  Select a single rule to trigger an event and modify the **Rule property** as follows:

    -   Position the rule on the scene and change the shape as required. You can add/remove nodes to create complex
        shapes.
    -   In **Object Filter**, tick the box against the **Classes** that the rule should trigger events only.

        ![](assets/images/ipm-vca-rules-properties.png)

        _Note: The available classifiers are different depending on the hardware platform and the installed license._

4.  Then, define the action that will occur when the rule triggers an event in **Event Actions** as follows:

    -   In **Event Notification**, tick the box against the **TCP Event** to enable TCP notifications when a
        event occurs.
    -   In **Triggered By**, define when the notification will be sent. The available options are:
        -   **Object:** Send notification for each object triggering the rule.
        -   **Rule:** Send a notification every time the rule is triggered.
    -   In **Triggered At**, select one of the following options:
        -   **Object:** Choose between the **begin** of the object triggering the rule as it enters the zones or
             the **end** of the object triggering the rule as it leaves the zone. _A notification will be sent for each_
             _object triggering the rule._
        -   **Rule:** From the **begin** point of the first object to trigger the rule to the **end** point of the last
            object to trigger the rule. _A notification will be sent for each triggering of the rule._

        ![](assets/images/ipm-rules-tcp-event-actions.png)

5.  Click **Save** located at the bottom to save the configuration.

    ![](assets/images/ipm-rules-tcp-settings.png)

6.  Click **OK** to confirm the settings.

    ![](assets/images/ipm-vca-rules-added-ok.png)

### Configuring the Calibration

Camera calibration is required in order for object identification and classification to occur. _The calibration is only_
_required when using the motion Object Tracker, the IPM AI series will have the option to select the DL Object or_
_People Tracker and will not need any calibration for classification to occur._

1.  From the **VCAedge** menu, click on **CALIBRATION** in the left side.

    ![](assets/images/ipm-vca-calibration-menu.png)

2.  In **Enable Calibration**, turn on the calibration feature.

3.  Use the mimics to match up with people or objects in the scene to help calibrate. They represent a height of 1.8
    meters.

    ![](assets/images/ipm-vca-calibration-config.png)

4.  Click **Apply** located at the bottom to save the configuration.

### Creating TCP Notifications

The TCP notification sends data to a remote TCP server when triggered. The format is configurable with a mixture of
plain text and tokens. Tokens are used to represent the event metadata that will be included when a rule is triggered.

1.  From the **VCAedge** menu, click on **TCP NOTIFICATION** in the left side.

    ![](assets/images/ipm-vca-tcp-notification-menu.png)

2.  In **General Settings**, turn on the notification feature.

3.  In **TCP Settings**, configure the TCP request as follows:

    -   In **Host `url`**, enter the IP address of the Ganz Cortrol server.
    -   In **Port**, enter the TCP port configured for the Data Source of the Ganz Cortrol server.

        ![](assets/images/ipm-ganz-tcp-settings.png)

4.  In **Message**, select **Rule** and define the body of the notification that will be sent when the rule is
    triggered.

    ![](assets/images/ipm-ganz-tpc-message.png)

5.  Click **Apply** located at the bottom to save the configuration.

6.  Click **OK** to confirm configuring the notification.

    ![](assets/images/ipm-tcp-added-ok.png)

For this integration, the following tokens were used to send an information on the camera, zone, rule type and
classification that triggered the event:

-   `Event`: Represents the beginning of the message.
-   `{{name}}`: The name of the event.
-   `{{id}}`: The unique id of the event.
-   `{{type}}`: The type of the event. This is usually the type of rule that triggered the event.
-   `{{host}}`: The hostname of the device that generated the event.
-   `{{datetime}}`: The event time in the format `DD MM D HH:MM:SS YYYY Tue Jan 1 12:00:00 2019`.
-   `{{objclass}}`: The object class of the object triggering the rule.
-   `End`: Represents the end of the message.

_For more information on creating and configuring VCA in IPM cameras, please refer to the VCAedge IPM Plug-in Manual._

# Ganz Cortrol Management Console Configuration

## Configuring a New Device

1.  First we add a new device into the system. From the left menu, click on **Devices**. Then, click **New Device**
    located top.

    ![](assets/images/ganz-add-new-device.png)

2.  Click **Select Model** and select **RTSP Compatible** from the available devices.

    ![](assets/images/ganz-rtsp-compatible-menu.png)

3.  Enter a descriptive **name** for the device.

4.  Then, click **Network** in the left side and configure the new device as follows:

    -   **Host:** Enter the IP address of the IPM camera.
    -   **Port:** Enter the web port of the IPM camera.
    -   **Username:** Enter the username to access the IPM camera.
    -   **Password:** Enter the password to access the IPM camera.
    -   Click **Apply** to save the configuration.
    -   Click **OK** to finish creating the new device.

        ![](assets/images/ipm-ganz-add-device-settings.png)

## Configuring the Recording

1.  From the left menu, click on **Channels**. Then, click **Edit** located top to modify the newly created channel.

    ![](assets/images/ipm-ganz-channel-edit.png)

2.  In the **Details** page, configure the recording as follows:

    -   **Title:** Enter a descriptive name for the device.
    -   **Main stream recording configuration:** Click **Change** and select **continuous recording**.
        Then, click **OK** to confirm and close the window.

    -   **Sub stream recording configuration:** Click **Change** and select **continuous recording**.
        Then, click **OK** to confirm and close the window.

        ![](assets/images/ipm-ganz-recording.png)

3.  Click **Apply** and **OK** to save the settings.

### Configuring IPM Camera RTSP Stream

1.  In the *Channel* page, click on **Channel configuration**. Then, click **Open channel properties**.

    ![](assets/images/ipm-ganz-open-channel-properties.png)

2.  In the *Stream Properties* pop-up window, click the **RTSP** tab and configure the stream as follows:

    -   In **RTSP Transport Settings**, leave **Use Default Port 554** checked or untick the box against the default
        setting and enter the required RTSP port.

    -   Tick the box against the option **RTP over TCP (default settings is recommended)**.
    -   In **Path to Session Description Protocol File**, enter the path to connect to the channel for **High** and
        **Low**. Default URL: `/<description>`. Example: `/channel2`

        ![](assets/images/ipm-ganz-stream-properties.png)

3.  Click **Apply** to save the settings.

4.  Click **OK** to close all windows.

    _Note: To confirm the IPM channel is configured correctly you can show a live stream. From the Channels tab, select_
    _the newly created device, and click Show Video located top._

    ![](assets/images/ipm-ganz-live-video.png)

## Configuring Data Source

Next, we need to create a new Data Source to receive the TCP notifications from the VCAedge plug-in. Data is stored and
displayed embedded with the video stream from the channel(s) you choose to associate with it.

1.  In the left menu, click **Data Source**. Then, select **New data source** located top.

    ![](assets/images/ganz-new-ds.png)

2.  In the pop-up screen, configure the new Data Source as follows:

    -   **Data source title:** Enter a descriptive name for the Data Source.
    -   **Server:** Click **Change** and choose **Ganz Cortrol Server** from the available options.
    -   **Data source profile:** Leave none _(it will be created later)_.
    -   **Data source type:** Select **TCP** from the drop down list.
    -   **Mode:** Select **Server** _(the program will be listening to the specified port)_.
    -   **Port:** Enter the TCP port for the Data Source to listen for events (this port matches the port configured
        in the VCAedge TCP Notification).

    -   Click **OK** to close the window.

        ![](assets/images/ipm-ganz-ds-details.png)

        _Make sure any active firewalls are configured to allow traffic using the port detailed above._

### Configuring Data Source Profile

1.  Now, we configure the Data Source Profile. From the left menu, click **Data Sources**. Then, click
    **+ New data source profile** located top.

    ![](assets/images/ipm-ganz-add-ds-profile.png)

2.  In the **Details** page, enter a descriptive name for the Profile. Then, click **Configuration** in the left side.

    -   **Encoding:** Select **Western European Windows** from the available options.
    -   **Line Ending:** Select **CR + FL** from the drop down list.
    -   **Remove non-printable characters:** leave it checked.

        ![](assets/images/ipm-ganz-dsp-details-encoding.png)

#### Defining Data Source Profile Format

1.  In the *Details* page, click **load from data source...** located top right.

    -   Select the **Data Source** created previously and click **OK**.

    _Note: Make sure that the IPM camera is sending events to the Ganz Server so that it can be viewed._

    The events are displayed in the trace window. If no events are being received then review the device configuration
    and ensure that your VCAedge plug-in is producing events.

    ![](assets/images/ipm-ganz-load-from-device.png)

2.  Next, we need to define the _beginning_ of an event from the data being received.

    -   Locate the text that identifies the beginning of an event.
    -   In **Mappings**, click on the `BeginTransaction` entry that will show the settings for `BeginTransaction` on
        the left.

    -   In **Text**, enter the word for the beginning of the transaction.
    -   Click **Apply changes**.

        ![](assets/images/ipm-ganz-ds-beginning.png)

3.  Now, we need to define the _end_ of an event from the data being received.

    -   Locate the text that identifies the end of an event.
    -   In **Mappings**, click on the `EndTransaction` entry that will show the settings for `EndTransaction` on
        the left.

    -   In **Text**, enter the word for the end of the transaction.
    -   Click **Apply changes**.

        ![](assets/images/ipm-ganz-ds-end.png)

4.  Click **OK** to close the window and save the configuration.

##### Linking the Data Source Profile to the Data Source

1.  In the *Data Source configuration* page, select the data source created before and click **Edit** located top.

    ![](assets/images/ipm-ganz-ds-edit.png)

2.  Click **Change** next to the **Data Source profile**. Then, select the new Data Source Profile and click **OK** to
    confirm.

    ![](assets/images/ipm-ganz-dsp-add.png)

3.  Click **OK** to save the settings.

    ![](assets/images/ipm-ganz-linking-dsp.png)

    _To confirm the data source settings, select Test to start receiving events using the data source profile._

## Creating Events, Actions, and Rules

### Creating Events

Next, we configure the events, actions, and rules that will be sending the Data Sources notifications to the Ganz
Client. The first step is create an event as follows:

1.  Click **Events & Action** in the left menu.

2.  Then, lick **Events** and **New Event** located top.

    ![](assets/images/ganz-new-event.png))

3.  In **Variables and Counter (4)** and select **Data Source** from the available types.

    ![](assets/images/ganz-webui-ds-event.png)

4.  In the new screen, configure the new event as follows:

    -   **Title:** Enter a descriptive name for the event.
    -   **Source:** Click **Change** and select **Data Source**. Then, click **OK** to confirm and close the Event
        source window.

    -   **Text:** Enter the text that will be triggering events.
    -   Click **OK** to confirm and close the Event window.

        ![](assets/images/ipm-ganz-ds-event-setting.png)

### Creating Actions

1.  Next, we create a new action. From the left menu, click **Actions**  and **New action** located top.

    ![](assets/images/ganz-new-action.png)

2.  In **Notifications (4)**, select **Send event to client** from the available types.

    ![](assets/images/ganz-send-events.png)

3.  Then, configure the notification as follows:

    -   **Title:** Enter a descriptive name for the notification.
    -   **Message:** Click the **Insert field** button located top right to add the fields that will contain the details
        of the events in the notification.

        ![](assets/images/ganz-message-fields.png)

    -   **Enable** Display events in alert, Display a warning message box and Display event in notification panel.

        ![](assets/images/ipm-ganz-action-setting.png)

4.  Click **OK** to confirm and close the Actions window.

### Creating Rules

1.  The last step is to create a new rule. From the left menu, click **Rules** and **Open configuration** located top.

    ![](assets/images/ganz-rules-configurator.png)

2.  In the Event and Actions `configurator` page, you will see three boxes associated with Events, Rules, and Actions.

3.  In **Events**, select the **Data Source** created previously. Then, click the greater than **>** button to move the
    event into the Rules box.

4.  In **Actions**, select the **Notification** created previously. Then, click the less than **<** button to move the
    action into the Rules box.

5.  In **Rules**, configure the box as follows:

    -   Click **Target channel** located bottom. In the pop-up screen, select the IPM camera and click **OK** to
        confirm.

    -   Then, click **Schedule** located bottom. Configure the schedule for the events, and click **OK** to confirm.

        ![](assets/images/ipm-ganz-schedule.png)

6.  Click **OK** to save the rule configuration.

    ![](assets/images/ipm-ganz-rules-settings.png)

    _Optionally, you can test this Rule by clicking the Test button located top. The notification will appear on the_
    _Ganz Client._

## Verifying Events on the Ganz Cortrol Client

From the Ganz Cortrol Client, you can verify the Data Source events. Every time the VCAedge plug-in generates a new
events, a pop-up notification will appear on the **Live** screen as follows:

![](assets/images/ipm-ganz-client-ds-events.png)

![](assets/images/ipm-ganz-client-events.png)

You will see the notifications on the **Alerts** tab located top as follows:

![](assets/images/ipm-ganz-client-alerts.png)
