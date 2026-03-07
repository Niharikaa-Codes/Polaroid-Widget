Hey guys! This is a simple tutorial on how to make your first Electron App. 

**Step1**: Open terminal in your VS Code project folder where you just created your Polaroid Wall.  Write the following line of code to initialize a npm project.
```
npm init -y
```

**Step2**: Then to install electron, write:
```
npm install electron -D
```
This installs electron as a dev dependency.

**Step3**: Create an `index.js` file.\
**Step4**: Inside the `index.js` file, write:
```
console.log("Hello World!");
```

**Step5**: Inside your `package.json` file, under scripts write:
```
"start": "electron ."
```

**Step6**: In your Terminal, write:
```
npm run start
```
This should give you `Hello World!` in the console. This means your installation is succesfull.

**Step7**: In your `index.js` file, remove everything. The write:
```
const { app, BrowserWindow } = require('electron')

const path = require('node:path')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })
}

app.whenReady().then(() => {
  createWindow()
})
```
Then, in your Terminal: `npm run start`. This opens your app window.

**Step8**: Let's render our `index.html` file in the app now. Add `win.loadFile('index.html')` in your code.
```
const { app, BrowserWindow } = require('electron')

const path = require('node:path')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  win.loadFile('index.html')
}

app.whenReady().then(() => {
  createWindow()
})
```
Rerun `npm run start`. This should render your html file inside the app.

**Step9**: To remove the menu bar, write: `win.setMenuBarVisibility(false)`
```
 const { app, BrowserWindow } = require('electron')

const path = require('node:path')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  win.loadFile('index.html')
  win.setMenuBarVisibility(false)
}

app.whenReady().then(() => {
  createWindow()
})
```
The rerun your app. Your menu bar should be removed.

**Step10**: To remove the frame, write: `frame: false,`
```
const { app, BrowserWindow } = require('electron')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 320,
    height: 400,
    frame: false,
  })
  win.loadFile('index.html')
  win.setMenuBarVisibility(false)
}

app.whenReady().then(() => {
  createWindow()
})
```
Rerun your app, and your frame should be removed. To close your app, right click on the electron app in the task manager and click: **close window**.

To make your app background transparent, write: `transparent: true,`
```
const { app, BrowserWindow } = require('electron')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 320,
    height: 400,
    frame: false,
    transparent: true,
  })
  win.loadFile('index.html')
  win.setMenuBarVisibility(false)
}

app.whenReady().then(() => {
  createWindow()
})
```
Rerun your app, and your app background should be transparent.


That's it guys!\
If you have any further doubts: [Watch my YouTube Video]()\
Need help with index.html: [Decoding index.html](01_Decoding_index.html.md)\
Need help with style.css: [Decoding style.css](02_Decoding_style.css.md)
