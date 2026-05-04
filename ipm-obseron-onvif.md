---
title: Obseron VCAedge Integration Note v1.0.0
logo: assets/images/obseron-logo.png
---

# Introduction

## Prerequisites

-   IPM series camera.
-   VCAedge video analytics plug-in version 1.0.41 or greater.
-   Obseron 2.19 VMS.

## Supported features

-   Motion detection, line detection, presence, loitering, tampering.

## Architecture

Obseron will connect to the IPM camera to consume the events provided. The integration does not require the
configuration of VCA notifications to send events to the VMS. The only requirement is that VCA rules are defined.

![](assets/images/ipm-obseron-architecture.png)

# IPM Camera Configuration

## Video & Audio Settings

### Confirming the RTSP stream used for transmitting video footage

Check and change if required, the RTSP stream settings used by the IP camera for external connections to the channels.

1.  From the **Setup** menu, click on **VIDEO & AUDIO** and then, click on **VIDEO**.

    ![](assets/images/ipm-video-menu.png)

2.  Note the *Live Video Channel* settings as these will be needed when connecting to the RTSP stream from the
    ExacqVision server.

    ![](assets/images/ipm-video-configuration.png)

## Network Settings

### Confirming the RTSP port used for transmitting video footage

Check and change if required, the RTSP port used by the IP camera for external connections to the channels.

1.  From the **Setup** menu, click on **NETWORK** and then, click on **NETWORK SETTINGS**.

    ![](assets/images/ipm-network-settings-menu.png)

2.  Note the **IP Setup** and **Port Setup** as these will be needed when connecting to the RTSP stream from the
    ExacqVision server.

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

        ![](assets/images/ipm-vca-obseron-rule-properties.png)

        _Note: The available classifiers are different depending on the hardware platform and the installed license._

4.  The VMS only supports Presence and Dwell events in ONVIF. For other rules, VCA must be converted to motion detection
    as follows:

    -   In **Event Actions**, tick the box against the **Convert VCA to MD** feature.

        ![](assets/images/ipm-vca-obseron-event-action.png)

5.  Click **Save** located at the bottom to save the configuration.

    ![](assets/images/ipm-vca-obseron-rules-config.png)

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

# Obseron Configuration

## Discovering an IP Camera

1.  From the Obseron GUI, click on **Main Menu** located top and select **Settings...** from the drop-down options.

    ![](assets/images/obseron-settings-menu.png)

2.  In the Settings pop-up window, click on **Cameras** in the left menu.

    ![](assets/images/obseron-camera-menu.png)

3.  In **Discovered cameras**, highlight the IPM camera and click **Add selected** located at the bottom.

    ![](assets/images/ipm-obseron-discovered-cameras.png)

4.  Then, click the **ONVIF camera 1** listed on the left side to access the settings.

5.  In the **General** tab, configure the **Connection** to the camera as follows:

    -   Enter the **username** and **password** to access the device.
    -   Click **Connect**.

        ![](assets/images/ipm-obseron-adding-stream.png)

    -   The **Status** will change to **OK** and the preview window will display a live camera image.

        ![](assets/images/ipm-obseron-live-view.png)

        _You can rename the camera by entering a name for the device on the Camera section below._

_Note: If the camera is not accessible, it will not be discovered automatically._ In this case, you will need to add it
manually as follows:

1.  From the *Cameras* menu, click the plus **+** button located at the bottom to add a new camera into the system.

    ![](assets/images/obseron-add-button.png)

2.  In the **Select camera type** pop-up window, select **ONVIF camera** from the available types.

    ![](assets/images/ipm-obseron-select-camera-type.png)

    -   Enter the number of cameras to add and click **OK** to confirm.

3.  In the **General** tab, configure the **Connection** to the IP device as follows:

    -   **IP address or hostname:** Enter the IP address or hostname of the IPM camera.
    -   **HTTP Port:** Enter the HTTP port configured in the camera.
    -   Enter the **username** and **password** to access the camera.
    -   Then, click **Connect**.

        ![](assets/images/ipm-obseron-add-camera-manually.png)

## Configuring the ONVIF Component

Obseron provides external sources called *components* which offer data such as video analytics or sensor readings that
allow to trigger rules.

1.  The next step is to connect to the camera to consume the events provided. click the **Components** tab from
    the top menu.

2.  Configure the `Component1` as follows:

    -   In **Component**, select **ONVIF events** from the drop-down list. Then, click on **Add** to add the new
        component.

        ![](assets/images/ipm-obseron-add-component-onvif.png)

    -   The VMS will automatically connect to the camera and the ONVIF events will be displayed on the **Received**
        **events** box in the **Info** section.

        ![](assets/images/ipm-obseron-onvif-events-view.png)

        _​If the connection fails, verify the configuration or tick the box against Manual connection settings to​_
        _connect to the camera manually.​_

## Configuring Camera Rules and Actions

### Configuring Rules

1.  Now, we configure the rule that will trigger a specific action when a condition is met. From the left menu, click on
    **Rules**.

    ![](assets/images/obseron-rules-menu.png)

2.  Then, click the plus **+** button located bottom to create a new rule.

    ![](assets/images/obseron-add-button.png)

3.  Enter a descriptive **Name** for the rule and click on **Add condition** below.

    ![](assets/images/ipm-obseron-add-condition-button.png)

4.  Then, configure the `Condition1` as follows:

    -   **Condition type:** Select **Camera event** from the drop-down list.
    -   **Camera:** Select the IPM camera.
    -   **Event type:** Select the detection rule configured in VCA from the drop-down list.
    -   **Hold for (sec):** ​Enter the time for the notification to remain on the screen.

        ![](assets/images/ipm-obseron-rules-config.png)

### Configuring Actions

Next, we decide how the system will react to the rules. ​Below is an example of how to configure the Obseron action to
create a Notification/Alarm for the events being received:

1.  Click on **Add action** located at the bottom.

    ![](assets/images/ipm-obseron-add-action-button.png)

2.  Then, configure the `Action1` as follows:

    -   `Action1:` Select **Notification/Alarm** from the drop-down list of actions.
    -   **Bind a camera to the notification:** Select the IPM camera.
    -   **Notification Colour:** Select a colour to identify the notification.
    -   **Text to show in the notification:** Enter a description for the notification to appear on the screen when the
        event occurs.

        ![](assets/images/ipm-obseron-action-notification-config.png)

    _Note: You can add the rules you need and configure different type of actions if required._

## Verifying The ONVIF Events

The **Live** screen of the Obseron Client will display a list of the events generated by the camera along with the
annotated video.

![](assets/images/ipm-obseron-onvif-events-gui.png)
