# REACT NATIVE APK BUILDIING GUIDE

### Fixed: React Native App Compilation Speed Is Too Slow

I achieved a clean 'release' build time of 1m 42s on a PC with an 8GB RAM and a SATA SSD.

Thanks to everyone for the suggestions on the ReactNative Reddit community!

---

#### Key Points:
- **Avoid using Expo**: Instead, use react-native-cli. [Source](https://reactnative.dev/docs/getting-started-without-a-framework)
- **Install Watchman**: This really boosted the speed and solved many issues.
- **Switch to Linux**: Switching to Linux (Kali in my case) really helped a lot.


---

### Complete Guide on How to Build React Native Apps Faster

#### A. Installing Brew (on Linux) and Watchman

  1. Run this in your terminal:
     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```
  2. After the script completes, copy and paste the two commands printed at the end, and press Enter.
  3. Install Watchman:
     ```bash
     brew install watchman
     ```
<br/>

#### B. Installing react-native-cli and Creating a Project

1. Uninstall the global react-native-cli and @react-native-community/cli:
   ```bash
   npm uninstall -g react-native-cli @react-native-community/cli
   ```
2. Initialize a new project:
   ```bash
   npx @react-native-community/cli@latest init AwesomeProject
   ```
<br/>


#### C. Setting Up the Environment and Dependencies

1. Open the project folder in Android Studio and let it install dependencies. Ignore any errors at the end.
2. In the same project folder, open the `android` folder in Android Studio and let it install dependencies (it will automatically create `local.properties`, etc.).


<br/>

#### D. Working on Your Project and Creating a Debug Variant

*Disable all VS Code extensions related to Java and Gradle.*

1. Open the project in VS Code.
2. Open the terminal and run:
   ```bash
   npm run start
   ```
   (If port 8081 is occupied, kill it using the command `sudo kill -9 $(sudo lsof -t -i:8081)`).
3. Connect your device in USB debugging mode or use a virtual device and type 'a'. It will build and run the debug version of the app on your connected device.
   *The AAB file can be found in `android/app/build/outputs/bundle/debug/`.

<br/>

#### E. Creating a Release Build

1. **Building AAB file**:
   ```bash
   npx react-native build-android --mode=release
   ```
   *The AAB file can be found in `android/app/build/outputs/bundle/release/`.
2. **Building APK file**:
   ```bash
   npm run android -- --mode="release"
   ```
   *The APK file can be found in `android/app/build/outputs/apk/release/`.

Release builds should take around 2 minutes with 8GB RAM and a SATA SSD. 
