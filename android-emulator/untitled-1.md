# Start the emulator from the command line  \|  Android Developers

The Android SDK includes an Android device emulator — a virtual device that runs on your computer. The Android Emulator lets you develop and test Android apps without using a physical device.

This page describes command-line features that you can use with the Android Emulator. For information about using the Android Emulator UI, see [Run Apps on the Android Emulator](https://developer.android.com/studio/run/emulator).

## Starting the emulator <a id="starting"></a>

Use the `emulator` command to start the emulator, as an alternative to [running your project](https://developer.android.com/studio/run/emulator#runningapp) or [starting it through the AVD Manager](https://developer.android.com/studio/run/emulator#runningemulator).

 Here's the basic command-line syntax for starting a virtual device from a terminal prompt:

```text
emulator -avd avd_name [ {-option [value]} … ]
```

 Or

```text
emulator @avd_name [ {-option [value]} … ]
```

 For example, if you launch the emulator from within Android Studio running on a Mac, the default command line will be similar to the following:

```text
/Users/janedoe/Library/Android/sdk/emulator/emulator -avd Nexus_5X_API_23 -netdelay none -netspeed full
```

 You can specify startup options when you start the emulator, but not later on.

 For a list of AVD names, enter the following command:

```text
emulator -list-avds
```

 When you use this option, it displays a list of AVD names from your Android home directory. Note that you can override the default home directory by setting the `ANDROID_SDK_HOME` environment variable: the root of the user-specific directory where all configuration and AVD content is stored. You could set the environment variable in the terminal window before launching a virtual device, or you could set it through your user settings in the operating system; for example, in your `.bashrc` file on Linux.

 To stop the Android Emulator, just close the emulator window.

## Installing an app <a id="apps"></a>

 In addition to installing an app through [Android Studio](https://developer.android.com/studio/run/emulator#runningapp) or the [emulator UI](https://developer.android.com/studio/run/emulator#tasks), you can install your app on a virtual device by using the [adb](https://developer.android.com/tools/help/adb#move) utility.

 To install an app by using adb, and then run and test the app, follow these general steps:

1. Build and package your app into an APK as described in [Build and Run Your App](https://developer.android.com/studio/run).
2. Start the emulator from the command line as described in the previous section, using any startup options necessary.
3. Install your app using [adb](https://developer.android.com/tools/help/adb#move).
4. Run and test your app on the emulator.  While the emulator is running, you can also use the [Emulator Console](https://developer.android.com/studio/run/emulator-console) to issue commands as needed.
5. The virtual device preserves the app and its state data across restarts, in a user-data disk partition \(`userdata-qemu.img)`. To clear this data, start the emulator with the `-wipe-data` option or wipe the data in the AVD Manager, for example. For more information about the user-data partition and other storage, see the following section.  To uninstall an app, do so as you would on an Android device.

{% hint style="info" %}
**Note:** The `adb` utility sees the virtual device as an actual physical device. For this reason, you might have to use the `-d` flag with some common `adb` commands, such as `install`. The `-d` flag lets you specify which of several connected devices to use as the target of a command. If you don't specify `-d`, the emulator targets the first device in its list.
{% endhint %}

## Understanding the default directories and files <a id="filedir"></a>

 The emulator uses associated files, of which the AVD system and data directories are the most important. It helps to understand the emulator directory structure and files when specifying command-line options. Although, you normally don't need to modify the default directories or files.

 The Android Emulator uses the Quick Emulator \([QEMU](http://wiki.qemu.org/)\) hypervisor. Initial versions of the Android Emulator used QEMU 1 \(goldfish\), and later versions use QEMU 2 \(ranchu\).

### AVD system directory <a id="system-filedir"></a>

 The system directory contains the Android system images that the emulator uses to simulate the operating system. It has platform-specific, read-only files shared by all AVDs of the same type, including API level, CPU architecture, and Android variant. The default locations are the following:

* Mac OS X and Linux - `~/Library/Android/sdk/system-images/android-apiLevel/variant/arch/`
* Microsoft Windows XP - `C:\Documents and Settings\user\Library\Android\sdk\system-images\android-apiLevel\variant\arch\`
* Windows Vista - `C:\Users\user\Library\Android\sdk\system-images\android-apiLevel\variant\arch\`

 Where:

* `apiLevel` is a numeric API level, or a letter for preview releases. For example, `android-M` indicated the Android Marshmallow preview. On release, it became API level 23, designated by `android-23`.
* `variant` is a name corresponding to specific features implemented by the system image; for example, `google_apis` or `android-wear`.
* `arch` is the target CPU architecture; for example, `x86`.

 Use the `-sysdir` option to specify a different system directory for the AVD.

 The emulator reads the following files from the system directory.

| File | Description | Option to Specify a Different File |
| :--- | :--- | :--- |
| `kernel-qemu` or `kernel-ranchu` | The binary kernel image for the AVD. `kernel-ranchu` is the QEMU 2 emulator, the latest version. | `-kernel` |
| `system.img` | The read-only initial version of the system image; specifically, the partition containing the system libraries and data corresponding the API level and variant. | `-system` |
| `ramdisk.img` | The boot partition image. This is a subset of `system.img` that's loaded by the kernel initially before the system image is mounted. It typically contains just a few binaries and initialization scripts. | `-ramdisk` |
| `userdata.img` | The _initial_ version of the data partition, which appears as `data/` in the emulated system and contains all writable data for the AVD. The emulator uses this file when you create a new AVD or use the `‑wipe-data` option. For more information, see the `userdata-qemu.img` file description in the following section. | `-initdata`  `-init-data` |

### AVD data directory <a id="data-filedir"></a>

 The AVD data directory, also called the content directory, is specific to a single AVD instance and contains all modifiable data for the AVD.

 The default location is the following, where `name` is the AVD name:

* Mac OS X and Linux - `~/.android/avd/name.avd`/
* Microsoft Windows XP - `C:\Documents and Settings\user\.android\name.avd\`
* Windows Vista, and higher - `C:\Users\user\.android\name.avd\`

 Use the `-datadir` option to specify a different AVD data directory.

 The following table lists the most important files contained in this directory.

<table>
  <thead>
    <tr>
      <th style="text-align:left">File</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Option to Specify a Different File</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>userdata-qemu.img</code>
      </td>
      <td style="text-align:left">
        <p>The content of the data partition, which appears as <code>data/</code> in
          the emulated system. When you create a new AVD, or when you use the <code>-wipe-data</code> option
          to reset the AVD to the factory defaults, the emulator copies the <code>userdata.img</code> file
          in the system directory to create this file.</p>
        <p>Each virtual device instance uses a writable user-data image to store
          user- and session-specific data. For example, it uses the image to store
          a unique user&apos;s installed app data, settings, databases, and files.
          Each user has a different <code>ANDROID_SDK_HOME</code> directory that stores
          the data directories for the AVDs created by that user; each AVD has a
          single <code>userdata-qemu.img</code> file.</p>
      </td>
      <td style="text-align:left"><code>-data</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>cache.img</code>
      </td>
      <td style="text-align:left">The cache partition image, which appears as <code>cache/</code> in the emulated
        system. It&apos;s empty when you first create an AVD or use the <code>-wipe-data</code> option.
        It stores temporary download files and is populated by the download manager
        and sometimes the system; for example, the browser uses it to cache downloaded
        web pages and images while the emulator is running. When you power off
        the virtual device, the file is deleted. You can persist the file by using
        the <code>-cache</code> option.</td>
      <td style="text-align:left"><code>-cache</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>sdcard.img</code>
      </td>
      <td style="text-align:left">
        <p>(Optional) An SD card partition image that lets you simulate an SD card
          on a virtual device. You can create an SD card image file in the <a href="https://developer.android.com/studio/run/managing-avds">AVD Manager</a> or
          using the <a href="https://developer.android.com/studio/command-line/mksdcard"><code>mksdcard</code></a> tool.
          The file is stored on your development computer and must be loaded at startup.</p>
        <p>When defining an AVD in the AVD Manager, you have the choice to use an
          automatically managed SD card file, or a file that you created with the <code>mksdcard</code> tool.
          You can view the <code>sdcard.img</code> file associated with an AVD in the
          AVD Manager. The <code>-sdcard</code> option overrides the SD card file specified
          in the AVD.</p>
        <p>You can browse, send files to, and copy and remove files from a simulated
          SD card by using the emulator UI or the <a href="https://developer.android.com/studio/command-line/adb#copyfiles">adb</a> utility
          while the virtual device is running. You can&apos;t remove a simulated
          SD card from a running virtual device.</p>
        <p>To copy files to the SD card file before loading it, you can mount the
          image file as a loop device and then copy the files. Or use a utility such
          as the <code>mtools</code> package to copy the files directly to the image.</p>
        <p>The emulator treats the file as a pool of bytes so the SD card format
          doesn&apos;t matter.</p>
        <p>Note that the <code>-wipe-data</code> option doesn&apos;t affect this file.
          If you want to clear the file, you need to delete the file and then recreate
          it using the AVD Manager or the <code>mksdcard</code> tool. Changing the
          size of the file also deletes the file and creates a new file.</p>
      </td>
      <td style="text-align:left"><code>-sdcard</code>
      </td>
    </tr>
  </tbody>
</table>

### Listing directories and files used by the emulator <a id="listing-filedir"></a>

 You can discover where files are located in two ways:

* When you start the emulator from the command line, use the `-verbose` or `-debug init` option, and look at the output.
* Use the `emulator` `-help-option` command to list a default directory. For example:

  ```text
  emulator -help-datadir

    Use '-datadir ' to specify a directory where writable image files
    will be searched. On this system, the default directory is:

        /Users/me/.android

    See '-help-disk-images' for more information about disk image files.
  ```

## Command-line startup options <a id="startup-options"></a>

 This section lists options you can supply on the command line when you start the emulator.

{% hint style="info" %}
**Note:** The Android Emulator is continually under development to make it more reliable. For status on the issues reported against various command-line options, and to report bugs, see the [Android Issue Tracker](https://code.google.com/p/android/issues/list?can=2&q=%22emulator%22%20%20Subcomponent%3DTools-emulator%20opened-after%3A2016/1/1&colspec=ID%20Status%20Priority%20Owner%20Summary%20Stars%20Reporter%20Opened&sort=-id&num=100&start=100).
{% endhint %}

### Commonly used options <a id="common"></a>

 The following table lists command-line startup options that you might use more often.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Command-Line Option</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"> <em>Quick Boot</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>-no-snapshot-load</code>
      </td>
      <td style="text-align:left">Performs a cold boot, and saves the emulator state on exit.</td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>-no-snapshot-save</code>
      </td>
      <td style="text-align:left">Performs a quick boot if possible, but does not save the emulator state
        on exit.</td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>-no-snapshot</code>
      </td>
      <td style="text-align:left">Disables the <a href="https://developer.android.com/studio/run/emulator#quickboot">Quick Boot</a> feature
        completely&#x2014;it does not load or save the emulator state.</td>
    </tr>
    <tr>
      <td style="text-align:left"> <em>Device Hardware</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>-camera-back mode</code>
        <br /><code>-camera-front mode</code>
      </td>
      <td style="text-align:left">
        <p>Set the emulation mode for a camera facing back or front. It overrides
          any camera setting in the AVD.</p>
        <p><code>mode</code> can be any of the following values:</p>
        <ul>
          <li> <code>emulated</code> - The emulator simulates a camera in the software.</li>
          <li> <code>webcamn</code> - The emulator uses a webcam connected to your development
            computer, specified by number. For a list of webcams, use the <code>-webcam-list</code> option;
            for example, <code>webcam0</code>.</li>
          <li> <code>none</code> - Disable the camera in the virtual device.</li>
          <li><pre><code>emulator @Nexus_5X_API_23 -camera-back webcam0</code></pre>

          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>-webcam-list</code>
      </td>
      <td style="text-align:left">
        <p>List the web cameras on your development computer that are available for
          emulation.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -webcam-list
List of web cameras connected to the computer:   
Camera &apos;webcam0&apos; is connected to device &apos;webcam0&apos;
on channel 0 using pixel format &apos;UYVY&apos;</code></pre>

          </li>
        </ul>
        <p>In the example, the first <code>webcam0</code> is the name you use on the
          command line. The second <code>webcam0</code> is the name used by the OS
          on the development computer. The second name varies depending on the OS.</p>
        <p>As of SDK Tools 25.2.4, the AVD name is required, although it might not
          be in the future.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"> <em>Disk Images and Memory</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>-memory size</code>
      </td>
      <td style="text-align:left">
        <p>Specify the physical RAM size from 128 to 4096 MBs.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -memory 2048</code></pre>

          </li>
        </ul>
        <p>This value overrides the AVD setting.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-sdcard filepath</code>
      </td>
      <td style="text-align:left">
        <p>Specify the filename and path to an SD card partition image file.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -sdcard C:/sd/sdcard.img</code></pre>

          </li>
        </ul>
        <p>If the file isn&apos;t found, the emulator still launches, but without
          an SD card; the command returns a <b>No SD Card Image</b> warning.</p>
        <p>If you don&apos;t specify this option, the default is <code>sdcard.img</code> in
          the data directory (unless the AVD specifies something different). For
          details about emulated SD cards, see <a href>AVD data directory</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-wipe-data</code>
      </td>
      <td style="text-align:left">
        <p>Delete user data and copy data from the initial data file. This option
          clears the data for the virtual device and returns it to the same state
          as when it was first defined. All installed apps and settings are removed.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -wipe-data</code></pre>

          </li>
        </ul>
        <p>By default, the user data file is <code>userdata-qemu.img</code> and the
          initial data file is <code>userdata.img</code>, both residing in the data
          directory. The <code>-wipe-data</code> option doesn&apos;t affect the <code>sdcard.img</code> file.
          For more information about user data, see <a href>Understanding the default directories and files</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Debug</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-debug tags</code>
      </td>
      <td style="text-align:left">
        <p>Enable or disable the display of debug messages for one or more tags.
          Separate multiple tags by a space, comma, or column.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -debug init,metrics</code></pre>

          </li>
        </ul>
        <p>To disable a tag, place a dash (-) in front of it; for example, the following
          option displays all debug messages, except the ones related to network
          sockets and metrics:</p>
        <p> <code>-debug all,-socket,-metrics</code>
        </p>
        <p>For a list of tags and descriptions, use the <code>-help-debug-tags</code> option.</p>
        <ul>
          <li><pre><code>emulator -help-debug-tags</code></pre>

          </li>
        </ul>
        <p>You can define the default debug tags in the <a href="https://developer.android.com/studio/command-line/variables#android_verbose"><code>ANDROID_VERBOSE</code></a> environment
          variable. Define the tags you want to use in a comma-delimited list. Here&apos;s
          an example showing it defined with the <code>socket</code> and <code>gles</code> tags:</p>
        <ul>
          <li><pre><code class="lang-text">ANDROID_VERBOSE=socket,gles</code></pre>

          </li>
        </ul>
        <p>It&apos;s equivalent to using:</p>
        <p> <code>-debug-socket -debug-gles</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-debug-tag</code>
        <br /> <code>-debug-no-tag</code>
      </td>
      <td style="text-align:left">
        <p>Enable a specific debug message type. Use the <code>no</code> form to disable
          a debug message type.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -debug-all -debug-no-metrics</code></pre>

          </li>
        </ul>
        <p>For a list of tags, use the <code>emulator -help-debug-tags</code> command.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-logcat logtags</code>
      </td>
      <td style="text-align:left">
        <p>Enable the display of logcat messages for one or more tags, and write
          them to the terminal window. For example, the following command enables
          error messages from all components:</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -logcat *:e</code></pre>

          </li>
        </ul>
        <p> <code>logtags</code> uses the same format as the <code>adb logcat logtags</code> command
          (enter <code>adb logcat -help</code> for more information). It&apos;s a list
          of space- or comma-separated log filters of the format <code>componentName:logLevel</code>. <code>componentName</code> is
          either a wildcard asterisk (<code>*</code>) or a component name, such as
          ActivityManager, SystemServer, InputManager, WindowManager, and so on. <code>logLevel</code> is
          one of these values:</p>
        <ul>
          <li><code>v</code> - verbose</li>
          <li><code>d</code> - debug</li>
          <li><code>i</code> - informative</li>
          <li><code>w</code> - warning log level</li>
          <li><code>e</code> - error</li>
          <li><code>s</code> - silent</li>
        </ul>
        <p>The following example displays GSM component messages at the informative
          log level:</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -logcat &apos;*:s GSM:i&apos;</code></pre>

          </li>
        </ul>
        <p>If you don&apos;t supply the <code>-logcat</code> option on the command
          line, the emulator looks for the <a href="https://developer.android.com/studio/command-line/variables#android_log_tags"><code>ANDROID_LOG_TAGS</code></a> environment
          variable. If <code>ANDROID_LOG_TAGS</code> is defined with a valid <code>logtags</code> value
          and isn&apos;t empty, the emulator uses its value to enable logcat output
          to the terminal by default. You can also redirect the same, or other, log
          messages to the terminal through adb. For more information about logcat
          and adb, see <a href="https://developer.android.com/studio/command-line/logcat">logcat Command-Line Tool</a>,
          <a
          href="https://developer.android.com/studio/debug/am-logcat">Write and View Logs with Logcat</a>, <a href="https://developer.android.com/reference/android/util/Log">Log</a> class,
            and <a href="https://developer.android.com/studio/command-line/adb#issuingcommands">adb commands reference</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-show-kernel</code>
      </td>
      <td style="text-align:left">
        <p>Display kernel debug messages in the terminal window.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -show-kernel</code></pre>

          </li>
        </ul>
        <p>One use of this option is to check that the boot process works correctly.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-verbose</code>
      </td>
      <td style="text-align:left">
        <p>Print emulator initialization messages to the terminal window.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -verbose</code></pre>

          </li>
        </ul>
        <p>It displays which files and settings are actually selected when starting
          a virtual device defined in an AVD. This option is the same as specifying <code>-debug-init</code>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>Network</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-dns-server servers</code>
      </td>
      <td style="text-align:left">
        <p>Use the specified DNS servers. <code>servers</code> is a comma-separated
          list of up to four DNS server names or IP addresses.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -dns-server 192.0.2.0,
192.0.2.255</code></pre>

          </li>
        </ul>
        <p>By default, the emulator tries to detect the DNS servers you&apos;re using
          and sets up special aliases in the emulated firewall network to allow the
          Android system to connect directly to them. Use the <code>-dns-server</code> option
          to specify a different list of DNS servers.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-http-proxy proxy</code>
      </td>
      <td style="text-align:left">
        <p>Make all TCP connections through a specified HTTP/HTTPS proxy. If your
          emulator must access the internet through a proxy server, you can use this
          option or the <code>http_proxy</code> environment variable to set up the
          appropriate redirection.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -http-proxy myserver:1981</code></pre>

          </li>
        </ul>
        <p> <code>proxy</code> can be one of the following:
          <br /> <code>http://server:port</code>
          <br /> <code>http://username:password@server:port</code>
        </p>
        <p>The <code>http://</code> prefix can be omitted.</p>
        <p>If this option isn&apos;t supplied, the emulator looks up the <code>http_proxy</code> environment
          variable and automatically uses any value matching the <code>proxy</code> format.
          For more information, see <a href="https://developer.android.com/studio/run/emulator-networking#proxy">Using the emulator with a proxy</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-netdelay delay</code>
      </td>
      <td style="text-align:left">
        <p>Set network latency emulation to one of the following <code>delay</code> values
          in milliseconds:</p>
        <ul>
          <li><code>gsm</code> - GSM/CSD (min 150, max 550).</li>
          <li><code>hscsd</code> - HSCSD (min 80, max 400).</li>
          <li><code>gprs</code> - GPRS (min 35, max 200).</li>
          <li><code>edge</code> - EDGE/EGPRS (min 80, max 400).</li>
          <li><code>umts</code> - UMTS/3G (min 35, max 200).</li>
          <li><code>hsdpa</code> - HSDPA (min 0, max 0).</li>
          <li><code>lte</code> - LTE (min 0, max 0).</li>
          <li><code>evdo</code> - EVDO (min 0, max 0).</li>
          <li><code>none</code> - No latency, the default (min 0, max 0).</li>
          <li><code>num</code> - Specify exact latency.</li>
          <li><code>min:max</code> - Specify individual minimum and maximum latencies.</li>
        </ul>
        <p></p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -netdelay gsm</code></pre>

          </li>
        </ul>
        <p>The emulator supports network throttling (limiting the maximum network
          bandwidth, also called network shaping) as well as higher connection latencies.
          You can define it either through the skin configuration, or with the <code>&#x2011;netspeed</code> and <code>-netdelay</code> options.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-netfast</code>
      </td>
      <td style="text-align:left">
        <p>Disable network throttling.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -netfast</code></pre>

          </li>
        </ul>
        <p>This option is the same as specifying <code>-netspeed full -netdelay none</code>.
          These are the default values for these options.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-netspeed speed</code>
      </td>
      <td style="text-align:left">
        <p>Set the network speed emulation. Specify the maximum network upload and
          download speeds with one of the following <code>speed</code> values in kbps:</p>
        <ul>
          <li><code>gsm</code> - GSM/CSD (up: 14.4, down: 14.4).</li>
          <li><code>hscsd</code> - HSCSD (up: 14.4, down: 57.6).</li>
          <li><code>gprs</code> - GPRS (up: 28.8, down: 57.6).</li>
          <li><code>edge</code> - EDGE/EGPRS (up: 473.6, down: 473.6).</li>
          <li><code>umts</code> - UMTS/3G (up: 384.0, down: 384.0).</li>
          <li><code>hsdpa</code> - HSDPA (up: 5760.0, down: 13,980.0).</li>
          <li><code>lte</code> - LTE (up: 58,000, down: 173,000).</li>
          <li><code>evdo</code> - EVDO (up: 75,000, down: 280,000).</li>
          <li><code>full</code> - No limit, the default (up: 0.0, down: 0.0).</li>
          <li><code>num</code> - Specify both upload and download speed.</li>
          <li><code>up:down</code> - Specify individual up and down speeds.</li>
        </ul>
        <p></p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -netspeed edge</code></pre>

          </li>
        </ul>
        <p>The emulator supports network throttling (limiting the maximum network
          bandwidth, also called network shaping) as well as higher connection latencies.
          You can define it either through the skin configuration, or with the <code>&#x2011;netspeed</code> and <code>-netdelay</code> options.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-port port</code>
      </td>
      <td style="text-align:left">
        <p>Set the TCP port number that&apos;s used for the console and adb.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -port 5556</code></pre>

          </li>
        </ul>
        <p>The default value is 5554 for the first virtual device instance running
          on the your machine. A virtual device normally occupies a pair of adjacent
          ports: a console port and an adb port. The console of the first virtual
          device running on a particular machine uses console port 5554 and adb port
          5555. Subsequent instances use port numbers increasing by two &#x2014;
          for example, 5556/5557, 5558/5559, and so on. The range is 5554 to 5682,
          allowing for 64 concurrent virtual devices.</p>
        <p>The port assignments are often the same as specifying <code>-ports port,{port + 1}</code>. <code>{port + 1}</code> must
          be free and will be reserved for adb. If any of the console or adb ports
          is already in use, the emulator won&apos;t start. The <code>&#x2011;port</code> option
          reports which ports and serial number the virtual device is using, and
          warns if there are any issues with the values you provided. In the emulator
          UI, you can see the console port number in the window title, and you can
          view the adb port number by selecting <b>Help</b> &gt; <b>About</b>.</p>
        <p>Note that if the <code>port</code> value is not even and is in the range
          5554 to 5584, the virtual device will start but not be visible when you
          use the <code>adb devices</code> command if the adb server starts <em>after</em> the
          emulator. For this reason, we recommend using an even console port number.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-ports<br />console-port,adb-port</code>
      </td>
      <td style="text-align:left">
        <p>Set the TCP ports used for the console and adb.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -ports 5556,5559</code></pre>

          </li>
        </ul>
        <p>The valid ports range is 5554 to 5682, allowing for 64 concurrent virtual
          devices. The <code>-ports</code> option reports which ports and serial number
          the emulator instance is using, and warns if there are any issues with
          the values you provided.</p>
        <p>We recommend using the <code>-port</code> option instead, where possible.
          The <code>-ports</code> option is available for network configurations that
          require special settings.</p>
        <p>For more information about setting console and adb ports, see the <code>-port</code> option.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-tcpdump filepath</code>
      </td>
      <td style="text-align:left">
        <p>Capture network packets and store them in a file.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -tcpdump /path/dumpfile.cap</code></pre>

          </li>
        </ul>
        <p>Use the option to begin capturing all network packets that are sent through
          the virtual Ethernet LAN of the emulator. After, you can use a tool like
          Wireshark to analyze the traffic.</p>
        <p>Note that this option captures all Ethernet packets, and isn&apos;t limited
          to TCP connections.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>System</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-accel mode</code>
      </td>
      <td style="text-align:left">
        <p>Configure emulator VM acceleration.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -accel auto</code></pre>

          </li>
        </ul>
        <p>Accelerated emulation works for x86 and x86_64 system images only. On
          Linux, it relies on KVM. On Windows and Mac, it relies on an Intel CPU
          and Intel HAXM driver. This option is ignored if you&apos;re not emulating
          an x86 or x86_64 device.</p>
        <p>Valid values for <code>mode</code> are:</p>
        <ul>
          <li><code>auto</code> - Determine automatically if acceleration is supported
            and use it when possible (default).</li>
          <li><code>off</code> - Disables acceleration entirely, which is primarily useful
            for debugging.</li>
          <li><code>on</code> - Force acceleration. If KVM or HAXM isn&apos;t installed
            or usable, the emulator won&apos;t start and prints an error message.</li>
        </ul>
        <p>For more information, see <a href="https://developer.android.com/studio/run/emulator-acceleration">Configure Hardware Acceleration</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-accel-check</code>
      </td>
      <td style="text-align:left">
        <p>Check whether a required hypervisor for emulator VM acceleration is installed
          (HAXM or KVM).</p>
        <ul>
          <li><pre><code>emulator -accel-check</code></pre>

          </li>
        </ul>
        <p>For more information, see <a href="https://developer.android.com/studio/run/emulator-acceleration#accel-check">Determining whether HAXM or KVM is installed</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-engine engine</code>
      </td>
      <td style="text-align:left">
        <p>Specify the emulator engine:</p>
        <ul>
          <li><code>auto</code> - Automatically select an engine (default).</li>
          <li><code>classic</code> - Use the older QEMU 1 engine.</li>
          <li><code>qemu2</code> - Use the newer QEMU 2 engine.</li>
        </ul>
        <p></p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -engine auto</code></pre>

          </li>
        </ul>
        <p>Auto-detection should choose the value that provides the best performance
          when emulating a particular AVD. You should use the <code>-engine</code> option
          for debugging and comparison purposes only.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-gpu mode</code>
      </td>
      <td style="text-align:left">
        <p>Select the GPU emulation mode.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -gpu swiftshader_indirect</code></pre>

          </li>
        </ul>
        <p>For more information, see <a href="https://developer.android.com/studio/run/emulator-acceleration#accel-graphics">Configuring graphics acceleration on the command line</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-accel</code>
      </td>
      <td style="text-align:left">
        <p>Disable emulator VM acceleration when using an x86 or x86_64 system image.
          It&apos;s useful for debugging only and is the same as specifying <code>-accel off</code>.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -no-accel</code></pre>

          </li>
        </ul>
        <p>For more information, see <a href="https://developer.android.com/studio/run/emulator-acceleration">Configure Hardware Acceleration</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-nojni</code>
        <br /> <code>-no-jni</code>
      </td>
      <td style="text-align:left">
        <p>Disable extended Java Native Interface (JNI) checks in the Android Dalvik
          or ART runtime.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -nojni</code></pre>

          </li>
        </ul>
        <p>When you start a virtual device, extended JNI checks are enabled by default.
          For more information, see <a href="https://developer.android.com/training/articles/perf-jni">JNI Tips</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-selinux {disabled|permissive}</code>
      </td>
      <td style="text-align:left">
        <p>Set the Security-Enhanced Linux (<a href="https://en.wikipedia.org/wiki/Security-Enhanced_Linux">SELinux</a>)
          security module to either disabled or permissive mode on a Linux operating
          system.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">me-linux$ emulator @Nexus_5X_API_23 -selinux permissive</code></pre>

          </li>
        </ul>
        <p>By default, SELinux is in enforcing mode, meaning the security policy
          is enforced. <code>permissive</code> mode loads the SELinux policy, but doesn&apos;t
          enforce it; it just logs policy violations. <code>disabled</code> mode disables
          kernel support for SELinux.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-timezone timezone</code>
      </td>
      <td style="text-align:left">
        <p>Set the timezone for the virtual device to <code>timezone</code>, instead
          of the host timezone.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -timezone Europe/Paris</code></pre>

          </li>
        </ul>
        <p>By default, the emulator uses the timezone of your development computer.
          Use this option to specify a different timezone or if the automatic detection
          isn&apos;t working correctly. The <code>timezone</code> value must be in
          <a
          href="https://en.wikipedia.org/wiki/List_of_tz_database_time_zones">zoneinfo</a>format, which is <code>area/location</code> or <code>area/subarea/location</code>.
            For example:</p>
        <ul>
          <li><code>America/Los_Angeles</code>
          </li>
          <li><code>Europe/Paris</code>
          </li>
          <li><code>America/Argentina/Buenos_Aires</code>
          </li>
        </ul>
        <p>The specified timezone must be in the <a href="https://www.iana.org/time-zones">zoneinfo database</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-version</code>
      </td>
      <td style="text-align:left">
        <p>Display the emulator version number.</p>
        <ul>
          <li><pre><code>emulator @Nexus_5X_API_23 -version</code></pre>

<pre><code class="lang-text">or
emulator -version</code></pre>

          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><em>UI</em>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-boot-anim</code>
      </td>
      <td style="text-align:left">
        <p>Disable the boot animation during emulator startup for faster booting.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -no-boot-anim</code></pre>

          </li>
        </ul>
        <p>On slower computers, this option can significantly speed up the boot sequence.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-screen mode</code>
      </td>
      <td style="text-align:left">
        <p>Set emulated touch screen mode.</p>
        <ul>
          <li>
            <p>For example:</p><pre><code class="lang-text">emulator @Nexus_5X_API_23 -screen no-touch</code></pre>

          </li>
        </ul>
        <p> <code>mode</code> can be any of the following values:</p>
        <ul>
          <li><code>touch</code> - Emulate a touch screen (default).</li>
          <li><code>multi-touch</code> - Emulate a multi-touch screen.</li>
          <li><code>no-touch</code> - Disable touch and multi-touch screen emulation.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### Advanced options <a id="advanced"></a>

 The following command-line startup options are available, but not commonly used by the average app developer.

 In the descriptions, the _working directory_ is the current directory in the terminal where you're entering commands. For information about the AVD _system directory_ and _data directory_, and the files stored within them, see [Understanding the default directories and files]().

 Some of these options are appropriate for external app developers, and some of them are used primarily by platform developers. _App developers_ create Android apps and run them on specific AVDs. _Platform developers_ work on the Android system and run it inside the emulator with no pre-created AVD; they're internal Android team members, not external app developers.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Advanced Option</th>
      <th style="text-align:left">Brief Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>-bootchart timeout</code>
      </td>
      <td style="text-align:left">
        <p>Enable bootcharting, with a timeout in seconds. Some Android system images
          have a modified init system that integrates a <a href="http://www.bootchart.org/">bootcharting facility</a>.
          You can pass a bootcharting timeout period to the system with this option.
          If your init system doesn&apos;t have bootcharting activated, the option
          does nothing. This option is primarily useful to platform developers, not
          external app developers.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -bootchart 120</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-cache filepath</code>
      </td>
      <td style="text-align:left">
        <p>Specify a cache partition image file. Provide a filename, and an absolute
          path or a path relative to the data directory, to set up a persistent cache
          file. If the file doesn&apos;t exist, the emulator creates it as an empty
          file. If you don&apos;t use this option, the default is a temporary file
          named <code>cache.img</code>. For more information, see <a href>AVD data directory</a>.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -cache ~/.android/avd/Nexus_5X_API_23.avd/cache_persistent.img</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-cache-size size</code>
      </td>
      <td style="text-align:left">
        <p>Set the cache partition size in MBs. If you don&apos;t specify this option,
          the default is 66 MB. Normally, most app developers don&apos;t need this
          option, unless they need to download very large files that are larger than
          the default cache. For more information about the cache file, see <a href>AVD data directory</a>.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -cache-size 1000</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-data filepath</code>
      </td>
      <td style="text-align:left">
        <p>Set the user data partition image file. Provide a filename, and an absolute
          path or a path relative to the working directory, to set up a persistent
          user data file. If the file doesn&apos;t exist, the emulator creates an
          image from the default <code>userdata.img</code> file, stores it in the filename
          you specified, and persists user data to it at shutdown. If you don&apos;t
          use this option, the default is a file named <code>userdata-qemu.img</code>.
          For more information about the user data file, see <a href>AVD data directory</a>.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -data </code>
        </p>
        <p><code>~/.android/avd/Nexus_5X_API_23.avd/userdata-test.img</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-datadir dir</code>
      </td>
      <td style="text-align:left">
        <p>Specify a data directory using an absolute path. For more information,
          see <a href>AVD data directory</a>.</p>
        <p>For example:</p>
        <p><code>emulator  @Nexus_5X_API_23 -datadir </code>
        </p>
        <p><code>~/.android/avd/Nexus_5X_API_23.avd/mytest</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-force-32bit</code>
      </td>
      <td style="text-align:left">
        <p>Use the 32-bit emulator on 64-bit platforms. Occasionally, this option
          is useful for testing or debugging. For example, there was an issue where
          the emulator would sometimes not run on 64-bit Windows, but 32-bit did
          run; this option was helpful for performing comparisons to debug the issue.
          Here&apos;s an example:For example:</p>
        <p><code>emulator  @Nexus_5X_API_23 -force-32bit</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-help-disk-images</code>
      </td>
      <td style="text-align:left">
        <p>Get help about about disk images. It provides information relevant to
          both app and platform developers. For example:</p>
        <p><code>emulator -help-disk-images</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-help-char-devices</code>
      </td>
      <td style="text-align:left">
        <p>Get help about character <em><code>device</code></em> specifications. A <em><code>device</code></em> parameter
          is required by some emulator options.For example:</p>
        <p><code>emulator -help-char-devices</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-help-sdk-images</code>
      </td>
      <td style="text-align:left">
        <p>Get help about disk images relevant to app developers. It explains where
          the image files are located for an AVD created with the SDK tools. For
          example:</p>
        <p><code>emulator -help-sdk-images</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-help-build-images</code>
      </td>
      <td style="text-align:left">
        <p>Get help about disk images relevant to platform developers. For example:</p>
        <p><code>emulator -help-build-images</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-initdata filepath</code>
        <br /> <code>-init-data filepath</code>
      </td>
      <td style="text-align:left">
        <p>Specify the <em>initial</em> version of the data partition. After wiping
          user data, the emulator copies the contents of the specified file to user
          data (by default, the <code>userdata-qemu.img</code> file) instead of using
          the default <code>userdata.img</code> file as the initial version. Specify
          the filename, and an absolute path or a path relative to the working directory.
          If you don&apos;t specify a path, it places the file in the system directory.
          For more information, see <a href>AVD system directory</a>.</p>
        <p><code>emulator @Nexus_5X_API_23 -initdata ~/Library/Android/sdk/system-images/android-23/ google_apis/x86/userdata-test.img</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-kernel filepath</code>
      </td>
      <td style="text-align:left">
        <p>Use a specific emulated kernel. If you don&apos;t specify a path, the
          emulator looks in the system directory. If you don&apos;t specify this
          option, the default is <code>kernel-ranchu</code>. For more information,
          see <a href>AVD system directory</a>. Use the <code>&#x2011;show&#x2011;kernel</code> option
          to view kernel debug messages.</p>
        <p><code>emulator @Nexus_5X_API_23 -kernel ~/Library/Android/sdk/system-images/android-23/ google_apis/x86/kernel-test.img -show-kernel</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-noaudio</code>
        <br /> <code>-no-audio</code>
      </td>
      <td style="text-align:left">
        <p>Disable audio support for this virtual device. Some Linux and Windows
          computers have faulty audio drivers that cause different symptoms, such
          as preventing the emulator from starting. In this case, you can use this
          option to overcome the issue. Alternatively, you can use the <code>QEMU_AUDIO_DRV</code> environment
          variable to change the audio backend.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -noaudio</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-nocache</code>
        <br /> <code>-no-cache</code>
      </td>
      <td style="text-align:left">
        <p>Start the emulator without a cache partition. If you don&apos;t use this
          option, the default is a temporary file named <code>cache.img</code>. This
          option is for platform developers only. For more information, see <a href>AVD data directory</a>.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -nocache</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-snapshot</code>
      </td>
      <td style="text-align:left">
        <p>Inhibit both the automatic load and save operations, causing the emulator
          to execute a full boot sequence and to lose its state when closed. It overrides
          the <code>-snapshot</code> option.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -no-snapshot</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-snapshot-load</code>
      </td>
      <td style="text-align:left">
        <p>Prevent the emulator from loading the AVD state from snapshot storage.
          Perform a full boot.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -no-snapshot-load</code>:</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-snapshot-save</code>
      </td>
      <td style="text-align:left">
        <p>Prevent the emulator from saving the AVD state to snapshot storage on
          exit, meaning that all changes will be lost.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -no-snapshot-save</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-snapshot-update-time</code>
      </td>
      <td style="text-align:left">
        <p>Don&apos;t try to correct the AVD clock time immediately on snapshot restore.
          This option can be useful during testing as it avoids a sudden time jump.
          Time updates are still sent to the AVD about every 15 seconds, however.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23-no-snapshot-update-time </code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-snapstorage</code>
      </td>
      <td style="text-align:left">
        <p>Start the emulator without mounting a file to store or load state snapshots,
          forcing a full boot and disabling state snapshot functionality. This option
          overrides the <code>-snapstorage</code> and <code>-snapshot</code> options.</p>
        <p>For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -no-snapstorage</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-no-window</code>
      </td>
      <td style="text-align:left">
        <p>Disable graphical window display on the emulator. This option is useful
          when running the emulator on servers that have no display. You&apos;ll
          still be able to access the emulator through adb or the console. For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -no-window</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-partition-size size</code>
      </td>
      <td style="text-align:left">
        <p>Specify the system data partition size in MBs. For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -partition-size 1024</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-prop name=value</code>
      </td>
      <td style="text-align:left">
        <p>Set an Android system property in the emulator when it boots. <code>name</code> must
          be a property name labeled as <code>qemu_prop</code> (for an example, see
          the <a href="https://android.googlesource.com/device/generic/goldfish/+/refs/heads/master/sepolicy/common/property_contexts">property_contexts file</a>)
          of at most 32 characters, without any spaces in it, and <code>value</code> must
          be a string of at most 92 characters. You can specify several <code>&#x2011;prop</code> options
          on one command line. This option can be useful for debugging. For example:</p>
        <p><code>emulator @Nexus_5X_API_23 -prop qemu.name=value -prop qemu.abc=xyz</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-qemu args</code>
      </td>
      <td style="text-align:left">Pass arguments to the QEMU emulator software. Note that QEMU 1 and QEMU
        2 can use different arguments. When using this option, make sure it&apos;s
        the last option specified, as all options after it are interpreted as QEMU-specific
        options. This option is quite advanced and should be used only by developers
        who are <em>very</em> familiar with QEMU <em>and</em> Android emulation.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-qemu -h</code>
      </td>
      <td style="text-align:left">
        <p>Display <code>-qemu</code> help. For example:</p>
        <p><code>emulator -qemu -h</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-ramdisk filepath</code>
      </td>
      <td style="text-align:left">
        <p>Specify a ramdisk boot image. Specify the filename, and an absolute path
          or a path relative to the working directory. If you don&apos;t use this
          option, the default is the <code>ramdisk.img</code> file in the system directory.
          For more information, see <a href>AVD system directory</a>.</p>
        <p><code>emulator @Nexus_5X_API_23 -ramdisk ~/Library/Android/sdk/system-images/android-23/ google_apis/x86/ramdisk-test.img</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-report-console socket</code>
      </td>
      <td style="text-align:left">
        <p>Report the console port to a remote third party before starting emulation.
          It can be useful for an automated testing script. <code>socket</code> must
          use one of these formats:</p>
        <ul>
          <li><code>tcp:port[,server][,max=seconds][,ipv6]</code>
          </li>
          <li><code>unix:port[,server][,max=seconds][,ipv6]</code>
          </li>
        </ul>
        <p>For more information, use the <code>-help-report-console</code> option as
          described in <a href>Getting detailed help for a specific option</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-shell</code>
      </td>
      <td style="text-align:left">
        <p>Create a root shell console on the current terminal. It differs from the
          <a
          href="https://developer.android.com/studio/command-line/adb#shellcommands"><code>adb shell</code>
            </a>command in the following ways:</p>
        <ul>
          <li>It creates a <em>root</em> shell that allows you to modify many parts of
            the system.</li>
          <li>It works even if the adb daemon in the emulated system is broken.</li>
          <li>Pressing Ctrl+C (&#x2318;C) stops the emulator, instead of the shell.</li>
        </ul>
        <p><code>emulator @Nexus_5X_API_23 -shell</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-snapshot name</code>
      </td>
      <td style="text-align:left">
        <p>Specify the name of a snapshot within a snapshot storage file for automatic
          start and save operations. Rather than executing a full boot sequence,
          the emulator can resume execution from an earlier state snapshot, which
          is usually significantly faster. When you supply this option, the emulator
          loads the snapshot of that name from the snapshot image and saves it back
          under the same name on exit. If you don&#x2019;t use this option, the default
          is a full boot sequence. If the specified snapshot doesn&#x2019;t exist,
          the emulator performs a full boot sequence instead, and performs a save
          operation.</p>
        <p>See the <code>-snapstorage</code> option for information on specifying a
          snapshot storage file and the default file</p>
        <p><code>emulator @Nexus_5X_API_23 -snapshot snapshot2</code>
        </p>
        <p>It&#x2019;s important to remember that in the process of loading a snapshot,
          all contents of the system, user data, and SD card images are overwritten
          with the contents they held when the snapshot was made. Unless you save
          this information in a different snapshot, any changes since then are lost.</p>
        <p>You can also create a snapshot from the Emulator Console by using the <code>avd snapshot save name</code> command.
          For more information, see <a href="https://developer.android.com/studio/run/emulator-console">Send Emulator Console Commands to a Virtual Device</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-snapshot-list</code>
      </td>
      <td style="text-align:left">
        <p>Display a list of available snapshots. It prints a table of snapshots
          that are stored in the snapshot storage file that the emulator was started
          with, then exits. If you specify <code>-snapstorage file</code> as well,
          this command prints a table of the snapshots stored in file.</p>
        <p><code>emulator @Nexus_5X_API_23 -snapshot-list -snapstorage ~/.android/avd/Nexus_5X_API_23.avd/snapshots-test.img</code>
        </p>
        <p>You can use the ID and TAG column values in the output as arguments for
          the <code>-snapshot</code> option.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-snapstorage filepath</code>
      </td>
      <td style="text-align:left">
        <p>Specify a repository file that contains all state snapshots. All snapshots
          made during execution will be saved in this file, and only snapshots in
          this file can be restored during the emulator run. If you don&#x2019;t
          specify this option, the default is <code>snapshots.img</code> in the data
          directory. If the specified file doesn&#x2019;t exist, the emulator will
          start, but without support for saving or loading state snapshots.</p>
        <p>For example</p>
        <p><code>emulator @Nexus_5X_API_23 -snapstorage ~/.android/avd/Nexus_5X_API_23.avd/snapshots-test.img</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-sysdir dir</code>
      </td>
      <td style="text-align:left">
        <p>Specify a system directory using an absolute path. For more information,
          see <a href>AVD system directory</a>. For example</p>
        <p><code>emulator @Nexus_5X_API_23 -sysdir ~/Library/Android/sdk/system-images/android-23/ google_apis/x86/test</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-system filepath</code>
      </td>
      <td style="text-align:left">
        <p>Specify an initial system file. Provide the filename, and an absolute
          path or a path relative to the working directory. If you don&apos;t use
          this option, the default is the <code>system.img</code> file in the system
          directory. For more information, see <a href>AVD system directory</a>. For
          example:</p>
        <p><code>emulator @Nexus_5X_API_23 -system ~/Library/Android/sdk/system-images/android-23/ google_apis/x86/system-test.img</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-use-system-libs</code>
      </td>
      <td style="text-align:left">
        <p>On Linux, use the system <code>libstdc++</code> instead of the version bundled
          with the emulator system. Use this option only if the emulator won&#x2019;t
          start normally, although it doesn&#x2019;t always work. Alternatively,
          set the <a href="https://developer.android.com/studio/command-line/variables#android_emulator_use_system_libs"><code>ANDROID_EMULATOR_USE_SYSTEM_LIBS</code></a> environment
          variable to 1.</p>
        <p><code>me-linux$ emulator @Nexus_5X_API_23 -use-system-libs</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>-writable-system</code>
      </td>
      <td style="text-align:left">
        <p>Use this option to have a writable system image during your emulation
          session. To do so:</p>
        <ol>
          <li>Start a virtual device with the <code>-writable-system</code> option.</li>
          <li>Enter the <code>adb remount</code> command from a command terminal to tell
            the emulator to remount <code>system/</code> as read/write (it&#x2019;s mounted
            as read-only by default).</li>
        </ol>
        <p>Note that using this flag will create a temporary copy of the system image
          that can be very large (several hundred MBs), but will be destroyed when
          the emulator exits.</p>
      </td>
    </tr>
  </tbody>
</table>

### Deprecated options <a id="deprecated"></a>

 The following command-line options are deprecated:

* `-audio-in`
* `-audio-out`
* `-charmap`
* `-code-profile`
* `-cpu-delay`
* `-dpi-device`
* `-dynamic_skin`
* `-enable-kvm`
* `-gps`
* `-image`
* `-keyset`
* `-help-keys`
* `-help-keyset-file`
* `-nand-limits`
* `-noskin`
* `-no-skin`
* `-onion`
* `-onion-alpha`
* `-onion-rotation`
* `-radio`
* `-ranchu`
* `-raw-keys`
* `-scale`
* `-shared-net-id`
* `-shell-serial`
* `-skin`
* `-skindir`
* `-trace`
* `-useaudio`

## Getting help about command-line options <a id="help"></a>

 This section describes how to get help about the command-line options. The following section provides more in-depth information about the commonly used emulator command-line options that are available when you start the emulator.

### Listing all emulator options <a id="help-all"></a>

 To print a list of all emulator options, including a short description, enter this command:

```text
emulator -help
```

### Getting detailed help for a specific option <a id="help-detailed"></a>

 To print help for a specific startup option, enter this command:

```text
emulator -help-option
```

 For example:

```text
emulator -help-netspeed
```

 This help is more detailed than the description provided by the `-help` option.

### Getting detailed help for all options <a id="help-detailed-all"></a>

 To get detailed help for all emulator options, enter this command:

```text
emulator -help-all
```

### Listing emulator environment variables <a id="help-envvar"></a>

 To get a list of emulator environment variables, enter this command:

```text
emulator -help-environment
```

 You can set environment variables in the terminal window before launching a virtual device, or you could set it through your user settings in the operating system; for example, in your `.bashrc` file on Linux.

### Listing debug tags <a id="help-debug"></a>

 To print a list of tags for the `-debug` options, enter this command:

```text
emulator -help-debug-tags
```

 The `-debug` options let you enable or disable debug messages from specific emulator components, as specified by the tags.

