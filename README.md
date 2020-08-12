yarn global add react-static

react-static create
project name: create-react-static-electron-app

cd create-react-static-electron-app

yarn add --dev electron electron-builder wait-on concurrently

yarn add electron-serve

add conf to file: static.config.js
  paths: {
    dist: 'build', // The production output directory.
  },

touch main.js

favicon.png
