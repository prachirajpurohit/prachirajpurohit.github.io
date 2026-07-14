---
title: "Getting Started With React Native"
description: "Using the React Native CLI"
date: "June 1 2026"
---

After [Setting up our development environment](https://prachipurohit.hashnode.dev/setting-up-dev-environment-for-react-native-on-windows)\- we can start with our react native setup!

---

reference: [https://reactnative.dev/docs/getting-started-without-a-framework](https://reactnative.dev/docs/getting-started-without-a-framework)

---

First, create a new project directory and navigate into it:

`mkdir react-native-project`

`cd react-native-project`

Next, initialize a new React Native project by running:

`npx @react-native-community/cli@latest init AwesomeProject`

When prompted to install dependencies, select **Y**.

For me, the setup completed successfully without any issues using **React Native v0.85**.

Once the project has been created, start the Metro bundler:

`npm start`

Open a second terminal window and run:

`npm run android`

If you've already set up an Android emulator (as covered in the previous blog post), it should automatically connect and launch the application. The initial build may take a few minutes, but once it's finished you should see the default React Native app running in the emulator.
