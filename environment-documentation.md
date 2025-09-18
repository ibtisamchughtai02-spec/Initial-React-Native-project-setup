Your system specifications
    Windows Edition: Windows 11 Home
    Processor: Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz (2.59 GHz)
    Installed RAM: 16.0 GB (15.8 GB usable)
    System Type: 64-bit operating system, x64-based processor

Software versions installed
    VS Code: 1.104.0
    Android Studio: Runtime version: 21.0.7+-13880790-b1038.58 amd64
    node --version: v22.19.0
    npm --version: 10.9.3

Setup steps you followed && Any deviations from the lab instructions && Time Taken for Each Step


1. Initial Attempt (Failed)(2 hours)
•	Started in EnvironmentTest
•	Tried to run npx react-native run-android
•	Failed: "Android project not found" - no React Native project structure existed

2. Project Structure Investigation(5mins)
•	Checked directory contents: only had package.json 

3. React Native Project Creation(5mins)
•	Ran: npx @react-native-community/cli init --skip-install
•	CLI prompted: "How would you like to name the app?"
•	Entered: "Test1"
•	CLI created new folder structure: EnvironmentTest/Test1/ with complete React Native setup

4. Java Environment Issues(10min)
•	First attempt failed: JAVA_HOME pointed to invalid C:\Program Files\Java\jdk-17
•	Fixed: Set JAVA_HOME to C:\Program Files\Java\jdk-24

5. Dependencies Installation(5mins)
•	Ran: npm install in Test1 directory to install React Native dependencies

6. Java 24 Compatibility Issues(1 hour)
•	First major failure: CMake configuration failed with "restricted method in java.lang.System"
•	React Native doctor showed Java 24 not supported (only 17-20)
•	Tried JVM arguments: --add-opens java.base/java.lang=ALL-UNNAMED
•	Command: $env:JAVA_OPTS = "--add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED"
•	Command: cd Test1; $env:JAVA_HOME = "C:\Program Files\Java\jdk-24"; $env:JAVA_OPTS = "--add-opens java.base/java.lang=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED"; npx react-native run-android
•	Combination of the 2 above. 

7. Architecture and Build Configuration Fixes(20 mins)
•	Key solution: Modified gradle.properties:
newArchEnabled=false  # Disabled new architecture (was true)
reactNativeArchitectures=x86_64  # Limited to single architecture
•	Modified build.gradle: Added ndk { abiFilters "x86_64" }

8. Successful Build(15mins)
•	Final working command: cd Test1; $env:JAVA_HOME = "C:\Program Files\Java\jdk-24"; npx react-native run-android
•	Result:  BUILD SUCCESSFUL - App installed on Pixel 4 emulator

9. GitHub Upload Process(10mins)
•	Added remote: git remote add origin https://github.com/ibtisamchughtai02-spec/Initial-React-Native-project-setup
•	Hit authentication issues - needed personal access token
•	Generated token with repo permissions
•	Encountered merge conflicts during git pull origin main --rebase
•	Resolved README.md conflicts manually
•	Successfully pushed with all 55 React Native files

10. Final Issues Identified(5mins)
•	Project ended up in nested structure: EnvironmentTest/Test1/
•	Wanted a cleaner directory structure

11. Professor’s way of running the app. (30mins)
•	Tried to make another test project using npx @react-native-community/cli@latest run-android
•	App launched but failed to sync with Android Sdk and same issue of JDK24 was encountered. 
•	Downloaded Android SDK Command-line Tools (latest) but no luck

12. Final Thoughts:
•	This process shouldnt have taken this long. I didnt have the right settings enabled. 
•   I tried so hard to troubleshoot but there was no luck. I'm gonna try again for the next Lab to save time. 


