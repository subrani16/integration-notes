---
title: Alnet SDK Integration Note v1.0.0
logo: images/alnet-logo.png
---

# Introduction

## Prerequisites

-   Net Professional service application version 3.4.5.34.
-   CMS 4 Professional Client application.

## Supported Features

-   Rules, zones, calibration and classification.

## Net Professional Configuration

### Adding a Network Camera

First, we configure an **ONVIF** device into the system. Run the Net Professional wizard.

1.  In **Network camera**, click **Add** and select the **Manufacturer** from the available options.

    ![](../assets/images/alnet-network-camera.png)

2.  Then, click **Next**.

3.  Click **Search** to discover the camera on the network. When the search is complete, select the IP camera you want
    to add and click **Next**.

    ![](../assets/images/alnet-camera-discovery.png)

4.  Confirm the camera model and click **Next**.

    ![](../assets/images/alnet-camera-model.png)

5.  Enter the **login** and **password** to access the camera and click **Next**.

    ![](../assets/images/alnet-camera-credentials.png)

6.  Make sure the camera properties have been detected correctly and click **Next**.

    ![](../assets/images/alnet-camera-properties.png)

7.  Configure the **Video stream** and **Audio** as required. Then, click **Next**.

    ![](../assets/images/images/alnet-stream-config.png)

8.  Enable the **Advance** settings as required and click **Next**.

    ![](../assets/images/alnet-advance-settings.png)

9.  Click **OK** to confirm the configuration and close the wizard.

    ![](../assets/images/alnet-finish-wizard.png)

## CMS 4 Professional Client Configuration

### Configuring VCA

Now, we configure VCA. In the CMS 4 Client application, click **Configuration** located top.

![](images/alnet-cms-configuration-tab.png)

1.  From the side menu, click **VCA - Video Content Analysis**.

    ![](../assets/images/alnet-sdk-vca-menu.png)

2.  In the **VCA Core Local Service** page, click **Open service configuration**.

    ![](../assets/images/alnet-sdk-open-configurator.png)

3.  The new screen represents the web interface for VCA. From the **View Channels** page, click the previously added
    source.

    ![](../assets/images/alnet-sdk-vca-channels-view.png)

4.  In the **Channel Settings** page, we can add zones, calibrate the video and choose the rules that will trigger the
    event.

    ![](../assets/images/alnet-sdk-vcs-settings.png)

5.  In the channel settings page, click **Calibration** in the right menu.

    ![](../assets/images/vca-calibration-button.png)

    -   **Enable** the option and use the mimics to match up with people or objects in the scene to help calibrate.
        They represent a height of 1.8 meters.

        ![](../assets/images/alnet-sdk-vca-calibration-config.png)

        _Calibration is required to allow the classification with the standard Object Tracker. If you are using DL_
        _Object/People Tracker then no calibration is required_.

6.  Return to the channel settings page and click **Zones** in the right menu.

    ![](../assets/images/vca-zones-button.png)

    -   Click **Create Zone +** located top right to create a detection zone.
    -   Position the zone and change the shape as required. You can add/remove nodes to create complex shapes.
    -   Enter a descriptive name for the zone and apply any colour to identify it.

        ![](../assets/images/alnet-sdk-vca-create-zone.png)

    -   Then, click the **Configure Rules** button below to go to the rules settings page.

        ![]images/vca-configure-rules.png)

7.  In the **Rules** page, click **Add Rule +** located top right.

    -   Select the rule that will trigger the events.
    -   Attached the zone to the rule.
    -   Modify its properties as required.

        ![](../assets/images/alnet-sdk-vca-create-rules.png)

### Verifying VCA Events

In the CMS 4 Client main screen, click **Select visible tabs** located top. Then, select **VCA** from the available
tabs and click the **green check** button located bottom to confirm.

![](../assets/images/alnet-cms-tabs-menu.png)

Every time an event is triggered by VCA, the notification will appear in the **VCA** tab showing the details of the
event such as object type, rule, zone, class, source and time.

![](images/alnet-sdk-events.png)
