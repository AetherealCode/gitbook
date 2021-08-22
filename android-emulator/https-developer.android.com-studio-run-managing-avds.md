# Create and manage virtual devices  \|  Android Developers

An Android Virtual Device \(AVD\) is a configuration that defines the characteristics of an Android phone, tablet, Wear OS, Android TV, or Automotive OS device that you want to simulate in the [Android Emulator](https://developer.android.com/studio/run/emulator). The AVD Manager is an interface you can launch from Android Studio that helps you create and manage AVDs.

To open the AVD Manager, do one of the following:

* Select **Tools &gt; AVD Manager**.
* Click **AVD**  **Manager** ![AVD Manager icon](https://developer.android.com/studio/images/buttons/toolbar-avd-manager.png)  in the toolbar.

![](../.gitbook/assets/image%20%2815%29.png)

## About AVDs <a id="about"></a>

An AVD contains a hardware profile, system image, storage area, skin, and other properties.

We recommend that you create an AVD for each system image that your app could potentially support based on  the [`<uses-sdk>`](https://developer.android.com/guide/topics/manifest/uses-sdk-element) setting in your manifest.

### Hardware profile <a id="hardware-profile"></a>

The hardware profile defines the characteristics of a device as shipped from the factory. The AVD Manager comes preloaded with certain hardware profiles, such as Pixel devices, and you can define or customize the hardware profiles as needed.

Notice that only some hardware profiles are indicated to include **Play Store**. This indicates that these profiles are fully [CTS](https://source.android.com/compatibility/cts/) compliant and may use system images that include the Play Store app.

### System images <a id="system-image"></a>

A system image labeled with **Google APIs** includes access to [Google Play services](https://developers.google.com/android/guides/overview). A system image labeled with the Google Play logo in the **Play Store** column includes the Google Play Store app _and_ access to Google Play services, including a **Google Play** tab in the **Extended controls** dialog that provides a convenient button for updating Google Play services on the device.

To ensure app security and a consistent experience with physical devices, system images with the Google Play Store included are signed with a release key, which means that you cannot get elevated privileges \(root\) with these images. If you require elevated privileges \(root\) to aid with your app troubleshooting, you can use the Android Open Source Project \(AOSP\) system images that do not include Google apps or services.

### Storage area <a id="storage"></a>

The AVD has a dedicated storage area on your development machine. It stores the device user data, such as installed apps and settings, as well as an emulated SD card. If needed, you can use the AVD Manager to wipe user data, so the device has the same data as if it were new.

### Skin <a id="emulator-skin"></a>

An emulator skin specifies the appearance of a device. The AVD Manager provides some predefined skins. You can also define your own, or use skins provided by third parties.

### AVD and app features <a id="app-features"></a>

Be sure your AVD definition includes the device features your app depends on. See [Hardware Profile Properties]() and [AVD Properties]() for lists of features you can define in your AVDs.

## Create an AVD <a id="createavd"></a>

{% hint style="info" %}
**Tip:** If you want to launch your app into an emulator, instead [run your app from Android Studio](https://developer.android.com/studio/run#RunningApp) and then in the **Select Deployment Target** dialog that appears, click **Create New Virtual Device**.
{% endhint %}

To create a new AVD:

* Open the AVD Manager by clicking **Tools &gt; AVD Manager**. 

![](../.gitbook/assets/image%20%284%29.png)

* Click **Create Virtual Device**, at the bottom of the AVD Manager dialog.

  The **Select Hardware** page appears. 

![](../.gitbook/assets/image%20%2820%29.png)

Notice that only some hardware profiles are indicated to include **Play Store**. This indicates that these profiles are fully [CTS](https://source.android.com/compatibility/cts/) compliant and may use system images that include the Play Store app.

* Select a hardware profile, and then click **Next**.

  If you don't see the hardware profile you want, you can [create]() or [import]() a hardware profile.

  The **System Image** page appears.

![](../.gitbook/assets/image%20%287%29.png)

* Select the system image for a particular API level, and then click **Next**.

The **Recommended** tab lists recommended system images. The other tabs include a more complete list. The right pane describes the selected system image. x86 images run the fastest in the emulator.

If you see **Download** next to the system image, you need to click it to download the system image. You must be connected to the internet to download it.

The API level of the target device is important, because your app won't be able to run on a system image with an API level that's less than that required by your app, as specified in the [`minSdkVersion`](https://developer.android.com/guide/topics/manifest/uses-sdk-element) attribute of the app manifest file. For more information about the relationship between system API level and `minSdkVersion`, see [Versioning Your Apps](https://developer.android.com/studio/publish/versioning).

If your app declares  a [`<uses-library>`](https://developer.android.com/guide/topics/manifest/uses-library-element) element  in the manifest file, the app requires a system image in which that external library is present. If you want to run your app on an emulator, create an AVD that includes the required library. To do so, you might need to use an add-on component for the AVD platform; for example, the Google APIs add-on contains the Google Maps library.

The **Verify Configuration** page appears.

![](../.gitbook/assets/image%20%281%29.png)

* Change [AVD properties]() as needed, and then click **Finish**.

  Click **Show Advanced Settings** to show more settings, such as the skin.

  The new AVD appears in the **Your Virtual Devices** page or the **Select Deployment Target** dialog.

To create an AVD starting with a copy:

1. From the [**Your Virtual Devices**]() page of the AVD Manager, right-click an AVD and select **Duplicate**.

   Or click  Menu ![](https://developer.android.com/images/tools/studio-advmgr-actions-dropdown-icon.png)   and select **Duplicate**.

   The [**Verify Configuration**]() page appears.

2. Click **Change** or **Previous** if you need to make changes on the [**System Image**]() and [**Select Hardware**]() pages.
3. Make your changes, and then click **Finish**.

   The AVD appears in the **Your Virtual Devices** page.

## Create a hardware profile <a id="createhp"></a>

The AVD Manager provides predefined hardware profiles for common devices so you can easily add them to your AVD definitions. If you need to define a different device, you can create a new hardware profile. You can define a new hardware profile from the beginning, or [copy a hardware profile]() as a start. The preloaded hardware profiles aren't editable.

To create a new hardware profile from the beginning:

1. In the [**Select Hardware**]() page, click **New Hardware Profile**.
2. In the **Configure Hardware Profile** page, change the [hardware profile properties]() as needed.
3. Click **Finish**.

   Your new hardware profile appears in the **Select Hardware** page. You can optionally [create an AVD]() that uses the hardware profile by clicking **Next**. Or, click **Cancel** to return to the **Your Virtual Devices** page or **Select Deployment Target** dialog.

To create a hardware profile starting with a copy:

1. In the [**Select Hardware**]() page, select a hardware profile and click **Clone Device**.

   Or right-click a hardware profile and select **Clone**.

2. In the **Configure Hardware Profile** page, change the [hardware profile properties]() as needed.
3. Click **Finish**.

   Your new hardware profile appears in the **Select Hardware** page. You can optionally [create an AVD]() that uses the hardware profile by clicking **Next**. Or, click **Cancel** to return to the **Your Virtual Devices** page or **Select Deployment Target** dialog.

## Edit existing AVDs <a id="workingavd"></a>

From the [**Your Virtual Devices**](https://developer.android.com/studio/run/managing-avds#viewing) page, you can perform the following operations on an existing AVD:

* To edit an AVD, click **Edit this AVD** ![](https://developer.android.com/studio/images/buttons/avd-edit.png) and [make your changes](https://developer.android.com/studio/run/managing-avds#copyavd).
* To delete an AVD, right-click an AVD and select **Delete**. Or click Menu ![](https://developer.android.com/images/tools/studio-advmgr-actions-dropdown-icon.png) and select **Delete**.
* To show the associated AVD `.ini` and `.img` files on disk, right-click an AVD and select **Show on Disk**. Or click Menu ![](https://developer.android.com/images/tools/studio-advmgr-actions-dropdown-icon.png) and select **Show on Disk**.
* To view AVD configuration details that you can include in any bug reports to the Android Studio team, right-click an AVD and select **View Details**. Or click Menu ![](https://developer.android.com/images/tools/studio-advmgr-actions-dropdown-icon.png) and select **View Details**.

## Edit existing hardware profiles <a id="workinghp"></a>

From the [**Select Hardware**]() page, you can perform the following operations on an existing hardware profile:

* To edit a hardware profile, select it and click **Edit Device**. Or right-click a hardware profile and select **Edit**. Next, [make your changes]().
* To delete a hardware profile, right-click it and select **Delete**.

You can't edit or delete the predefined hardware profiles.

## Run and stop an emulator, and clear data <a id="emulator"></a>

From the [**Your Virtual Devices**](https://developer.android.com/studio/run/managing-avds#viewing) page, you can perform the following operations on an emulator:

* To run an emulator that uses an AVD, double-click the AVD. Or click **Launch** ![](https://developer.android.com/images/tools/as-avd-start.png).
* To stop a running emulator, right-click an AVD and select **Stop**. Or click Menu ![](https://developer.android.com/images/tools/studio-advmgr-actions-dropdown-icon.png) and select **Stop**.
* To clear the data for an emulator, and return it to the same state as when it was first defined, right-click an AVD and select **Wipe Data**. Or click Menu ![](https://developer.android.com/images/tools/studio-advmgr-actions-dropdown-icon.png) and select **Wipe Data**.

## Import and export hardware profiles <a id="importexporthp"></a>

From the [**Select Hardware**]() page, you can import and export hardware profiles:

* To import a hardware profile, click **Import Hardware Profiles** and select the XML file containing the definition on your computer.
* To export a hardware profile, right-click it and select **Export**. Specify the location where you want to store the XML file containing the definition.

## Hardware profile properties <a id="hpproperties"></a>

You can specify the following properties of hardware profiles in the [**Configure Hardware Profile**]() page. AVD configuration properties override hardware profile properties, and emulator properties that you set while the emulator is running override them both.

The predefined hardware profiles included with the AVD Manager aren't editable. However, you can copy them and edit the copies.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Hardware Profile Property</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Device Name</td>
      <td style="text-align:left">Name of the hardware profile. The name can contain uppercase or lowercase
        letters, numbers from 0 to 9, periods (.), underscores (_), parentheses
        ( () ), and spaces. The name of the file storing the hardware profile is
        derived from the hardware profile name.</td>
    </tr>
    <tr>
      <td style="text-align:left">Device Type</td>
      <td style="text-align:left">
        <p>Select one of the following:</p>
        <ul>
          <li>Phone/Tablet</li>
          <li>Wear OS</li>
          <li>Android TV</li>
          <li>Chrome OS Device</li>
          <li>Android Automotive</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Screen Size</td>
      <td style="text-align:left">The physical size of the screen, in inches, measured at the diagonal.
        If the size is larger than your computer screen, it&#x2019;s reduced in
        size at launch.</td>
    </tr>
    <tr>
      <td style="text-align:left">Screen Resolution</td>
      <td style="text-align:left">Type a width and height in pixels to specify the total number of pixels
        on the simulated screen.</td>
    </tr>
    <tr>
      <td style="text-align:left">Round</td>
      <td style="text-align:left">Select this option if the device has a round screen, such as some Wear
        OS devices.</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory: RAM</td>
      <td style="text-align:left">Type a RAM size for the device and select the units, one of B (byte),
        KB (kilobyte), MB (megabyte), GB (gigabyte), or TB (terabyte).</td>
    </tr>
    <tr>
      <td style="text-align:left">Input: Has Hardware Buttons (Back/Home/Menu)</td>
      <td style="text-align:left">Select this option if your device has hardware navigation buttons. Deselect
        it if these buttons are implemented in software only. If you select this
        option, the buttons won&#x2019;t appear on the screen. You can use the
        emulator side panel to &quot;press&quot; the buttons, in either case.</td>
    </tr>
    <tr>
      <td style="text-align:left">Input: Has Hardware Keyboard</td>
      <td style="text-align:left">Select this option if your device has a hardware keyboard. Deselect it
        if it doesn&#x2019;t. If you select this option, a keyboard won&#x2019;t
        appear on the screen. You can use your computer keyboard to send keystrokes
        to the emulator, in either case.</td>
    </tr>
    <tr>
      <td style="text-align:left">Navigation Style</td>
      <td style="text-align:left">
        <p>Select one of the following:</p>
        <ul>
          <li>None - No hardware controls. Navigation is through the software.</li>
          <li>D-pad - Directional Pad support.</li>
          <li>Trackball</li>
          <li>Wheel</li>
        </ul>
        <p>These options are for actual hardware controls on the device itself. However,
          the events sent to the device by an external controller are the same.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Supported Device States</td>
      <td style="text-align:left">
        <p>Select one or both options:</p>
        <ul>
          <li>Portrait - Oriented taller than wide.</li>
          <li>Landscape - Oriented wider than tall.</li>
        </ul>
        <p>If you select both, you can switch between orientations in the emulator.
          You must select at least one option to continue.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Cameras</td>
      <td style="text-align:left">
        <p>To enable the camera, select one or both options:</p>
        <ul>
          <li>Back-Facing Camera - The lens faces away from the user.</li>
          <li>Front-Facing Camera - The lens faces toward the user.</li>
        </ul>
        <p>Later, you can use a webcam or a photo provided by the emulator to simulate
          taking a photo with the camera.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Sensors: Accelerometer</td>
      <td style="text-align:left">Select if the device has hardware that helps the device determine its
        orientation.</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensors: Gyroscope</td>
      <td style="text-align:left">Select if the device has hardware that detects rotation or twist. In combination
        with an accelerometer, it can provide smoother orientation detection and
        support a six-axis orientation system.</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensors: GPS</td>
      <td style="text-align:left">Select if the device has hardware that supports the Global Positioning
        System (GPS) satellite-based navigation system.</td>
    </tr>
    <tr>
      <td style="text-align:left">Sensors: Proximity Sensor</td>
      <td style="text-align:left">Select if the device has hardware that detects if the device is close
        to your face during a phone call to disable input from the screen.</td>
    </tr>
    <tr>
      <td style="text-align:left">Default Skin</td>
      <td style="text-align:left">Select a skin that controls what the device looks like when displayed
        in the emulator. Remember that specifying a screen size that&apos;s too
        big for the resolution can mean that the screen is cut off, so you can&apos;t
        see the whole screen. See <a href="https://developer.android.com/tools/devices/managing-avds#skins">Create an emulator skin</a> for
        more information.</td>
    </tr>
  </tbody>
</table>

## AVD properties <a id="avdproperties"></a>

You can specify the following properties for AVD configurations in the [**Verify Configuration**]() page. The AVD configuration specifies the interaction between the development computer and the emulator, as well as properties you want to override in the hardware profile.

AVD configuration properties override hardware profile properties. Emulator properties that you set while the emulator is running override them both.

<table>
  <thead>
    <tr>
      <th style="text-align:left">AVD Property</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">AVD Name</td>
      <td style="text-align:left">Name of the AVD. The name can contain uppercase or lowercase letters,
        numbers from 0 to 9, periods (.), underscores (_), parentheses ( () ),
        dashes (-), and spaces. The name of the file storing the AVD configuration
        is derived from the AVD name.</td>
    </tr>
    <tr>
      <td style="text-align:left">AVD ID (Advanced)</td>
      <td style="text-align:left">The AVD filename is derived from the ID, and you can use the ID to refer
        to the AVD from the command line.</td>
    </tr>
    <tr>
      <td style="text-align:left">Hardware Profile</td>
      <td style="text-align:left">Click <b>Change</b> to select a different hardware profile in the <a href><b>Select Hardware</b></a> page.</td>
    </tr>
    <tr>
      <td style="text-align:left">System Image</td>
      <td style="text-align:left">Click <b>Change</b> to select a different system image in the <a href><b>System Image</b></a> page.
        An active internet connection is required to download a new image.</td>
    </tr>
    <tr>
      <td style="text-align:left">Startup Orientation</td>
      <td style="text-align:left">
        <p>Select one option for the initial emulator orientation:</p>
        <ul>
          <li>Portrait - Oriented taller than wide.</li>
          <li>Landscape - Oriented wider than tall.</li>
        </ul>
        <p>An option is enabled only if it&#x2019;s selected in the hardware profile.
          When running the AVD in the emulator, you can change the orientation if
          both portrait and landscape are supported in the hardware profile.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Camera (Advanced)</td>
      <td style="text-align:left">
        <p>To enable a camera, select one or both options:</p>
        <ul>
          <li>Front - The lens faces away from the user.</li>
          <li>Back - The lens faces toward the user.</li>
        </ul>
        <p>The <b>Emulated</b> setting produces a software-generated image, while the <b>Webcam</b> setting
          uses your development computer webcam to take a picture.</p>
        <p>This option is available only if it&apos;s selected in the hardware profile;
          it&apos;s not available for Wear OS and Android TV.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Network: Speed (Advanced)</td>
      <td style="text-align:left">
        <p>Select a network protocol to determine the speed of data transfer:</p>
        <ul>
          <li>GSM - Global System for Mobile Communications</li>
          <li>HSCSD - High-Speed Circuit-Switched Data</li>
          <li>GPRS - Generic Packet Radio Service</li>
          <li>EDGE - Enhanced Data rates for GSM Evolution</li>
          <li>UMTS - Universal Mobile Telecommunications System</li>
          <li>HSDPA - High-Speed Downlink Packet Access</li>
          <li>LTE - Long-Term Evolution</li>
          <li>Full (default) - Transfer data as quickly as your computer allows.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Network: Latency (Advanced)</td>
      <td style="text-align:left">Select a network protocol to set how much time (delay) it takes for the
        protocol to transfer a data packet from one point to another point.</td>
    </tr>
    <tr>
      <td style="text-align:left">Emulated Performance: Graphics</td>
      <td style="text-align:left">
        <p>Select how graphics are rendered in the emulator:</p>
        <ul>
          <li>Hardware - Use your computer graphics card for faster rendering.</li>
          <li>Software - Emulate the graphics in software, which is useful if you&apos;re
            having a problem with rendering in your graphics card.</li>
          <li>Automatic - Let the emulator decide the best option based on your graphics
            card.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Emulated Performance: Boot option (Advanced)</td>
      <td style="text-align:left">
        <ul>
          <li>Cold boot - Start the device each time by powering up from the device-off
            state.</li>
          <li>Quick boot - Start the device by loading the device state from a saved
            snapshot. For details, see <a href="https://developer.android.com/studio/run/emulator#quickboot">Run the emulator with Quick Boot</a>.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Emulated Performance: Multi-Core CPU (Advanced)</td>
      <td style="text-align:left">Select the number of processor cores on your computer that you&#x2019;d
        like to use for the emulator. Using more processor cores speeds up the
        emulator.</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory and Storage: RAM</td>
      <td style="text-align:left">The amount of RAM on the device. This value is set by the hardware manufacturer,
        but you can override it, if needed, such as for faster emulator operation.
        Increasing the size uses more resources on your computer. Type a RAM size
        and select the units, one of B (byte), KB (kilobyte), MB (megabyte), GB
        (gigabyte), or TB (terabyte).</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory and Storage: VM Heap</td>
      <td style="text-align:left">The VM heap size. This value is set by the hardware manufacturer, but
        you can override it, if needed. Type a heap size and select the units,
        one of B (byte), KB (kilobyte), MB (megabyte), GB (gigabyte), or TB (terabyte).
        For more information on Android VMs, see <a href="https://developer.android.com/tools/help/am-memory#vm">Memory Management for Different Virtual Machines</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory and Storage: Internal Storage</td>
      <td style="text-align:left">The amount of nonremovable memory space available on the device. This
        value is set by the hardware manufacturer, but you can override it, if
        needed. Type a size and select the units, one of B (byte), KB (kilobyte),
        MB (megabyte), GB (gigabyte), or TB (terabyte).</td>
    </tr>
    <tr>
      <td style="text-align:left">Memory and Storage: SD Card</td>
      <td style="text-align:left">The amount of removable memory space available to store data on the device.
        To use a virtual SD card managed by Android Studio, select <b>Studio-managed</b>,
        type a size, and select the units, one of B (byte), KB (kilobyte), MB (megabyte),
        GB (gigabyte), or TB (terabyte). A minimum of 100 MB is recommended to
        use the camera. To manage the space in a file, select <b>External file</b> and
        click <b>...</b> to specify the file and location. For more information,
        see <a href="https://developer.android.com/tools/help/mksdcard">mksdcard</a> and
        <a
        href="https://developer.android.com/studio/run/emulator-commandline#data-filedir">AVD data directory</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Device Frame: Enable Device Frame</td>
      <td style="text-align:left">Select to enable a frame around the emulator window that mimics the look
        of a real device.</td>
    </tr>
    <tr>
      <td style="text-align:left">Custom Skin Definition (Advanced)</td>
      <td style="text-align:left">Select a skin that controls what the device looks like when displayed
        in the emulator. Remember that specifying a screen size that&apos;s too
        big for the skin can mean that the screen is cut off, so you can&apos;t
        see the whole screen. See <a href="https://developer.android.com/tools/devices/managing-avds#skins">Create an emulator skin</a> for
        more information.</td>
    </tr>
    <tr>
      <td style="text-align:left">Keyboard: Enable Keyboard Input (Advanced)</td>
      <td style="text-align:left">Select this option if you want to use your hardware keyboard to interact
        with the emulator. It&apos;s disabled for Wear OS and Android TV.</td>
    </tr>
  </tbody>
</table>

## Create an emulator skin <a id="skins"></a>

An Android emulator skin is a collection of files that define the visual and control elements of an emulator display. If the skin definitions available in the AVD settings don't meet your requirements, you can create your own custom skin definition, and then apply it to your AVD.

Each emulator skin contains:

* A `hardware.ini` file
* Layout files for supported orientations \(landscape, portrait\) and physical configuration
* Image files for display elements, such as background, keys and buttons

To create and use a custom skin:

1. Create a new directory where you will save your skin configuration files.
2. Define the visual appearance of the skin in a text file named `layout`. This file defines many characteristics of the skin, such as the size and image assets for specific buttons. For example:

   ```text
   parts {
       device {
           display {
               width   320
               height  480
               x       0
               y       0
           }
       }

       portrait {
           background {
               image background_port.png
           }

           buttons {
               power {
                   image  button_vertical.png
                   x 1229
                   y 616
               }
           }
       }
       ...
   }
   ```

3. Add the bitmap files of the device images in the same directory.
4. Specify additional hardware-specific device configurations in a `hardware.ini` file for the device settings, such as `hw.keyboard` and `hw.lcd.density`.
5. Archive the files in the skin folder and select the archive file as a custom skin.

For more detailed information about creating emulator skins, see the [Android Emulator Skin File Specification](https://android.googlesource.com/platform/external/qemu/+/emu-master-dev/android/docs/ANDROID-SKIN-FILES.TXT) in the tools source code.

