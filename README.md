<div align="center">
<img alt="Electron React-Static Crossover Banner" src="https://raw.githubusercontent.com/soulehshaikh99/assets/master/create-electron-framework-app/readme/svg/Electron_React_Static.svg" width="580" />
</div>
<br />
The boilerplate code to get started creating Cross-platform Desktop Apps with Electron and React-Static as front-end technology.
<br />
<br />
<div align="center">

[![forthebadge](http://forthebadge.com/images/badges/built-by-developers.svg)](http://forthebadge.com)&nbsp;&nbsp;&nbsp;&nbsp;[![forthebadge](http://forthebadge.com/images/badges/makes-people-smile.svg)](http://forthebadge.com)<br />

[![forthebadge](http://forthebadge.com/images/badges/uses-html.svg)](http://forthebadge.com)&nbsp;&nbsp;&nbsp;[![forthebadge](http://forthebadge.com/images/badges/uses-css.svg)](http://forthebadge.com)&nbsp;&nbsp;&nbsp;[![forthebadge](http://forthebadge.com/images/badges/uses-js.svg)](http://forthebadge.com)

[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)

</div>

## ✒️ Overview

The aim of this project is to provide Web Developers using `react-static` the power to create cross-platform desktop apps using `electron`.

#### 🧐 What packages does the project use?

**`electron`** enables you to create desktop applications with pure JavaScript by providing a runtime with rich native (operating system) APIs. You could see it as a variant of the Node.js runtime that is focused on desktop applications instead of web servers.

**`electron-builder`** is used as a complete solution to package and build a ready for distribution (supports Numerous target formats) Electron app with "auto update" support out of the box.

**`electron-serve`** is used for Static file serving for Electron apps.

**`react-static`** is a fast, lightweight, and powerful progressive static site generator based on React and its ecosystem. It resembles the simplicity and developer experience you're used to in tools like Create React App and has been carefully designed for performance, flexibility, and user/developer experience.

**`concurrently`** is used to run multiple commands concurrently.

**`wait-on`** is used as it can wait for sockets, and http(s) resources to become available.
<br />

## 🚀 Getting Started

**Note:** If you wish to use npm over yarn then modify package.json by replacing `yarn` with `npm` in `electron-dev` and `preelectron-pack` scripts.
But I strongly recommend using <em>yarn</em> as it is a better choice when compared to <em>npm</em>.

### 🤓 Use this boilerplate

```bash
# Clone the Project
# GitHub CLI Users
$ gh repo clone https://github.com/soulehshaikh99/create-react-static-electron-app.git
# or Normal Git Users
$ git clone https://github.com/soulehshaikh99/create-react-static-electron-app.git

# Switch location to the cloned directory
$ cd create-react-static-electron-app

# Install dependencies
$ yarn # or npm install

# Run your app
$ yarn electron-dev # or npm run electron-dev

# Package Your App
$ yarn electron-pack # or npm run electron-pack
```

### 💫 Create this boilerplate from scratch (Manual Setup)

#### 1) Start by installing `react-static` globally
```bash
$ yarn global add react-static
# npm i -g react-static
``` 

#### 2) Create project using react-static static-site generator tool.
```bash
# project name: create-react-static-electron-app
# template: basic
$ react-static create
```

#### 3) Switch to project directory.
```bash
$ cd create-react-static-electron-app
```

#### 4) Initailize project with your favourite package manager

```bash
# set entry point to main.js
$ yarn init # or npm init
```

#### 5) Download the app icon

[favicon.png](https://raw.githubusercontent.com/soulehshaikh99/assets/master/framework-icons/react-static/favicon.png) and place it in the public directory.

#### 6) Install Development Dependencies

```bash
$ yarn add --dev electron electron-builder wait-on concurrently
# npm i -D electron electron-builder wait-on concurrently
```

#### 7) Install Production Dependency

```bash
$ yarn add electron-serve # or npm i electron-serve
```

#### 8) Your dependencies should look something like this

```json
"dependencies": {
  "@reach/router": "^1.2.1",
  "axios": "^0.19.0",
  "electron-serve": "^1.0.0",
  "react": "^16.9.0",
  "react-dom": "^16.9.0",
  "react-static": "^7.2.0",
  "react-static-plugin-reach-router": "^7.2.0",
  "react-static-plugin-sitemap": "^7.2.0",
  "react-static-plugin-source-filesystem": "^7.2.0"
},
"devDependencies": {
  "babel-eslint": "^10.0.2",
  "concurrently": "^5.3.0",
  "electron": "^9.2.0",
  "electron-builder": "^22.8.0",
  "eslint": "^6.1.0",
  "eslint-config-react-app": "^5.0.1",
  "eslint-config-react-tools": "^1.1.7",
  "eslint-plugin-flowtype": "^4.2.0",
  "eslint-plugin-import": "^2.18.2",
  "eslint-plugin-jsx-a11y": "^6.2.3",
  "eslint-plugin-react": "^7.14.3",
  "eslint-plugin-react-hooks": "^4.0.2",
  "serve": "^11.1.0",
  "wait-on": "^5.2.0"
}
```

#### 9) Paste react-static configuration in static.config.js file

```bash
# Add this configuration directly inside default exported object, this makes sure that the production code is generated in 'build' directory and not in the 'dist' directory as it is reserved for electron-builder output.
export default {
...
  paths: {
      dist: 'build', // The production output directory.
  }
}
```

#### 10) Create main.js file (serves as entry point for Electron App's Main Process)

```bash
# Windows Users
$ fsutil file createnew main.js 0
# notepad main.js 

# Linux and macOS Users
$ touch main.js
```

#### 11) Paste the below code in main.js file

```js
// Modules to control application life and create native browser window
const { app, BrowserWindow } = require('electron');
const path = require('path');
const serve = require('electron-serve');
const loadURL = serve({ directory: 'build' });

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
let mainWindow;

function isDev() {
    return !app.isPackaged;
}

function createWindow() {
    // Create the browser window.
    mainWindow = new BrowserWindow({
        width: 800,
        height: 600,
        webPreferences: {
            nodeIntegration: true
        },
        // Use this in development mode.
        icon: isDev() ? path.join(process.cwd(), 'public/favicon.png') : path.join(__dirname, 'build/favicon.png'),
        // Use this in production mode.
        // icon: path.join(__dirname, 'build/favicon.png'),
        show: false
    });

    // This block of code is intended for development purpose only.
    // Delete this entire block of code when you are ready to package the application.
    if (isDev()) {
        mainWindow.loadURL('http://localhost:3000/');
    } else {
        //Do not delete this statement, Use this piece of code when packaging app for production environment
        loadURL(mainWindow);
    }
    
    // Uncomment the following line of code when app is ready to be packaged.
    // loadURL(mainWindow);

    // Open the DevTools and also disable Electron Security Warning.
    // process.env['ELECTRON_DISABLE_SECURITY_WARNINGS'] = true;
    // mainWindow.webContents.openDevTools();

    // Emitted when the window is closed.
    mainWindow.on('closed', function () {
        // Dereference the window object, usually you would store windows
        // in an array if your app supports multi windows, this is the time
        // when you should delete the corresponding element.
        mainWindow = null
    });

    // Emitted when the window is ready to be shown
    // This helps in showing the window gracefully.
    mainWindow.once('ready-to-show', () => {
        mainWindow.show()
    });
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.on('ready', createWindow);

// Quit when all windows are closed.
app.on('window-all-closed', function () {
    // On macOS it is common for applications and their menu bar
    // to stay active until the user quits explicitly with Cmd + Q
    if (process.platform !== 'darwin') app.quit()
});

app.on('activate', function () {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (mainWindow === null) createWindow()
});

// In this file you can include the rest of your app's specific main process
// code. You can also put them in separate files and require them here.
```

#### 12) Add scripts in package.json

```bash
"electron": "wait-on http://localhost:3000 && electron .",
"electron-dev": "concurrently \"yarn start\" \"yarn electron\"",
"preelectron-pack": "yarn build",
"electron-pack": "electron-builder"
```

#### 13) Add the following Electron Configuration in package.json

**Note:** build configuration is used by electron-builder, modify it if you wish to add more packaging and native distribution options for different OS Platforms.

```bash
"main": "main.js", # please verify entry point is set to main.js 
"build": {
  "icon": "public/favicon.png",
  "productName": "React Static and Electron App",
  "files": [
    "build/**/*",
    "main.js"
  ]
}
```

#### 14) Test drive your app

```bash
# Run your app
$ yarn electron-dev # or npm run electron-dev

# Package Your App
$ yarn electron-pack # or npm run electron-pack
```

### 💯 Result

<div align="center">
<img alt="Electron React-Static Window Screeenshot" src="https://raw.githubusercontent.com/soulehshaikh99/assets/master/create-electron-framework-app/readme/png/create-react-static-electron-app.png" />
</div>

<h3>😍 Made with ❤️ from Souleh</h3>

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)
<br/>

<h3>📋 License: </h3>
Licensed under the <a href="https://github.com/soulehshaikh99/create-react-static-electron-app/blob/master/LICENSE">MIT License</a>.