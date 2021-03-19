## rn_ble_manager_v2
React Native app serving as a client to ESP32 (server), connecting via BLE. <br>
Data broadcasted from ESP32 is displayed real-time.<br>
This app does NOT work in Simulator -> **App must be run in an actual device.**<br>
<br>
Step-by-step tutorial provided here to successfully launch this app in an iPhone.<br>
(NOT tested under Android environment).

> This app is a modified version of the example app in https://github.com/innoveit/react-native-ble-manager. Changes are : <br>
> 1) Class components -> Function components with hooks <br>
> (Ref : https://nimblewebdeveloper.com/blog/convert-react-class-to-function-component)
> 2) Displaying data broadcasted from ESP32 in real-time
> 3) Using Context() as a global var to store States across various screens
> 4) Using Stack & Bottom-Tab navigators

> **Other References**
> Another example using react-native-ble-manager + code walkthrough
>  - Code : https://github.com/catarizea/bvm-ventilator-covid/blob/blog-post-ble-client/react-native/src/App.js
>  - Walkthough : https://catalin.works/blog/bluetooth-low-energy-client-on-react-native-application/

Arduino script (.ino) for ESP32 is here : https://github.com/onehwengineer/arduino_esp32_ble_v2 <br>
You need BOTH Arduino script and this app to run this project! <br>
Download Arduino script from above and flash on to your ESP32.


## App Screenshots
<p float="left">
  <img src="https://user-images.githubusercontent.com/60368973/103332121-bc625500-4a1d-11eb-94d8-7d32b53a88eb.png" width="200" />
  <img src="https://user-images.githubusercontent.com/60368973/103332136-c84e1700-4a1d-11eb-865a-07fc515cf54c.png" width="200" /> 
  <img src="https://user-images.githubusercontent.com/60368973/103709400-4dc64f80-4f67-11eb-97f4-bf8092f62ecd.png" width="200" />
</p>


## Install React Native
There are many prerequisites to be installed before we can actually install RN.<br>
Make sure ALL are installed.
- [0] Install **XCode** (from App Store)
  - Make sure to open the app in order to install all the components
  - **Xcode Command Line Tools** will be installed in step [1]
- [1] Install **Homebrew**
  - Homebrew is a package manager that let's you install stuff that Apple or Linux didn't need
  - Open Terminal, and paste :
  - ```/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"```
  - This will also install **Xcode Command Line Tools** (this step takes a while... 2.5GB)
    - Confirm installation by `xcode-select -p` -> Directory will show up
- [2] Install **Node JS**
  - ```brew install node```
- [3] Install **React Native Client**
  - `sudo npm i -g react-native-cli`
  - `# i for install, -g for global` <br>

To build ios projects under Xcode, we need the following as well (yarn is not a must, but a good to have). 
- [4] Install **CocoaPods**
  - CocoaPods is a dependency manager for Swift and Objective-C Cocoa projects.
  - `brew install cocoapods`
  - ~~`sudo gem install cocoapods`~~
- [5] Install **Watchman**
  - React Native uses watchman to detect when you've made code changes and then automatically build and push the update your device without you needing to manually refresh it (live reload).
  - `brew install watchman`
- [6] Install **Yarn**
  - Yarn is a new JavaScript package manager built by Facebook, Google, Exponent and Tilde.
  - `brew install yarn`
  
  
## Clone This Repository
>To do so, first check if Git is installed by `git --version`. <br>
>If nothing shows up, you need to install Xcode, which will also install Git.<br>
>Check if Xcode is installed by `xcode-select -p` <br>
>If directory exists, Xcode is installed. Otherwise, install Xcode from App Store.

From your local machine, open Terminal, and go to (`cd` into) a directory where you would like to copy (clone) this project. <br>
Do NOT create project directory, since `clone` will create a project directory with the name `rn_ble_manager_v2` (name of this repo).

- Paste following : <br>
- `git clone https://github.com/onehwengineer/rn_ble_manager_v2.git`

You will now notice that [your project dir]/rn_ble_manager_v2 is created. <br>


## (Repo Cloned Already) Getting Latest Changes from Remote Repo
If this repo was cloned before, and you'd like to "update" **LOCAL master** with latest **REMOTE master**, follow this step :
- In Terminal, `cd` into project directory, /rn_ble_manager_v2 -> `git pull origin master`

> (Optional) A few useful Git commands
> `git status` : Check for any commits that are staged of commited <br>
> `git remote -v` : Check what remote repository (Github) our local repository is connected to <br>


## (Repo Cloned Already) Create a Branch Locally, Make Some Changes, and Merge Branch with Master on Remote Repo 
(It's always a good practice to work with Branches)
- [1] Create a **local** branch : `git branch br` ("br" is the name of the branch)
  - Default branch of every repo is called "master" 
- [2] Switch branches locally : "master" -> "br"
  - `git branch` -> Use arrow key to select branch, "br"
  - `git checkout br`
- [3] Make some changes (or add new files), and commit & push your branch to **remote**
  - `git add -A`
  - `git commit -a -m "br 1st commit`
  - `git push origin br`
- [4] After pushing `br` to remote, switch to master branch **locally** : `git checkout master`
- [5] Update **local** master with **remote** master (if any changes in remote master) : `git pull origin master`
- [6] Merge `br` with **local** master : `git merge br`
  - (This may give you conflicts which need to be resolved and changes committed before moving further)
  - (https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line)
- [7] Commit merge of `br` with master : `git commit -a -m "master after merge"
- [8] Push **local** master to **remote** master : `git push origin master`


## Install All Node Libraries/Dependencies in Cloned Project (as specified under packages.json)
- From Terminal, `cd` into /rn_ble_manager_v2
- Type : `npm install`
- Next, `cd ios` (/ios is a sub-directory of rn_ble_manager_v2), and type `pod install`
- `cd ..` to go back to project directory

> Error during `pod install` :
```console
> xcrun: error: SDK "iphoneos" cannot be located
> ...
> xcrun: error: unable to lookup item 'Path' in SDK 'iphoneos'
```
> First, make sure XCode is installed (from step [0] above)
> Next, type `sudo xcode-select --switch /Applications/Xcode.app`
> Or, open Xcode, Xcode -> Preferences -> Locations -> Make sure Command Line Tools are selected
> Run `pod install` again!


## [IMPORTANT] MUST DO THIS STEP
For any apps with react-native-vector-icons library, below steps must be done after cloning. <br>
Otherwise, *failed to build ios project... error code 65* will show up when `react-native run-ios` is run.

- [1] Unlink react-native-vector-icons library
  - `react-native unlink react-native-vector-icons` 
  - `cd ios` -> `pod install` -> `cd ..`
- [2] Install again
  - `npm install --save react-native-vector-icons` **—save** is important here
  - `cd ios` -> `pod install` -> `cd ..`
- [3] Add fonts manuall for ios and android (use your text editor - I use VSCode)
  - [ios] Go to [project name]/ios/[project name]/**info.plist** 
  - Add the fonts BELOW UIAppFonts array 
  ```console
  <key>UIAppFonts</key>
    <array>
      <string>AntDesign.ttf</string>
      <string>Entypo.ttf</string>
      <string>EvilIcons.ttf</string>
      <string>Feather.ttf</string>
      <string>FontAwesome.ttf</string>
      <string>FontAwesome5_Brands.ttf</string>
      <string>FontAwesome5_Regular.ttf</string>
      <string>FontAwesome5_Solid.ttf</string>
      <string>Foundation.ttf</string>
      <string>Ionicons.ttf</string>
      <string>MaterialIcons.ttf</string>
      <string>MaterialCommunityIcons.ttf</string>
      <string>SimpleLineIcons.ttf</string>
      <string>Octicons.ttf</string>
      <string>Zocial.ttf</string>
    </array>
  ```
    - Save -> restart VSCode (or any other text editor) & metro bundler (Terminal)
    - [android] Add this line to android/app/**build.gradle**
      - `apply from: "../../node_modules/react-native-vector-icons/fonts.gradle"`
    
## Run App on Simulator (just to make sure no errors during build)
- Although the ultimate goal is to lauch this app in an ios device, we still need to test under Simulator to ensure that there are no build errors.
- In Terminal, make sure you are inside the project directory
- Type `react-native run-ios`
- Note that first build takes a while - be patient

## Run App on Actual Device (iPhone, our final goal!)
> For this step, **make sure to use your PERSONAL laptop/iphone**
- [0] Sign up for Apple Developer account (don't need to pay anything)
  - https://developer.apple.com/
  - Make sure to make this account separate from your personal
- **Connect your iPhone to a Mac via Lightening cable**
- **Double click : .../rn_ble_manager_v2/ios/rn_ble_manager_v2.xcworkspace to launch RN app in Xcode**
- [1] Sign in to Xcode with your developer's account
  - Xcode → Preferences → Accounts tab
![Image](https://user-images.githubusercontent.com/60368973/103330583-06940800-4a17-11eb-9d2c-927d5b22aabc.png)<br>
- [2] Assign team
  - Select the account name signed in from previous
![Image](https://user-images.githubusercontent.com/60368973/103330584-08f66200-4a17-11eb-89e6-f074e777dced.png)
- [3] Connect your iPhone to a Mac via Lightening cable
  - In Xcode, hit menu : Window → Devices and Simulators
  - A window will show up and indicate that this iPhone needs to be trusted
  - Unlock your (connected) iPhone, and hit Trust upon pop up
  - Xcode will then install debugger support on this iPhone (takes a few min)
  - Afterwards, make sure "Show as run destination" is checked  
  - Finally, select your iPhone as the target as shown below
![Image](https://user-images.githubusercontent.com/60368973/103330585-0a278f00-4a17-11eb-80f8-e23d58af33e8.png)
- [4] Verify Developer App certificate 
  - On your iPhone, click Settings → General → Device Management → Click Trust
- [5] Hit Run button in Xcode!
  - You will get a ton of warning messages, but just ignore them.
  - After a few min, your app will launch on your iPhone!
![Image](https://user-images.githubusercontent.com/60368973/107589828-b2567900-6bbb-11eb-8bbf-852e114dac96.png)  
  - During first build, you might see this pop up -> Enter your Mac login password, and hit Always Allow
