# Test Electro con Angular 7
Este es un ejemplo más de uso de electronjs con angular 7, aquí se describe el proceso de configuración inicial como uno de tantos tutoriales disponibles en la web.

# Entorno
- Angular CLI: 7.0.6
- Node: 10.14.1
- OS: linux x64
- electron: 3.0.10

# Configuración
Web oficial de electronjs : https://electronjs.org/docs
## Generar un nuevo proyecto con angular CLI 
ng new nombreProyecto
## instalar la última versión de electron
Se recomienda instalar como un dependencia de desarrollo
 npm install electron@latest -save-dev

## Crear el archivo main.js
Se debe agregar el contenido que se describe en la pagina oficial de electron que es similar al siguiente
```javascript
//main script for electron
const { app, BrowserWindow } = require('electron')
  
  // Keep a global reference of the window object, if you don't, the window will
  // be closed automatically when the JavaScript object is garbage collected.
  let win
  
  function createWindow () {
    // Create the browser window.
    win = new BrowserWindow({ width: 400, height: 400 })
  
    // and load the index.html of the app.
    win.loadFile('./dist/TestElectron/index.html')
  
    // Open the DevTools.
    //win.webContents.openDevTools()
  
    // Emitted when the window is closed.
    win.on('closed', () => {
      // Dereference the window object, usually you would store windows
      // in an array if your app supports multi windows, this is the time
      // when you should delete the corresponding element.
      win = null
    })
  }
  
  // This method will be called when Electron has finished
  // initialization and is ready to create browser windows.
  // Some APIs can only be used after this event occurs.
  app.on('ready', createWindow)
  
  // Quit when all windows are closed.
  app.on('window-all-closed', () => {
    // On macOS it is common for applications and their menu bar
    // to stay active until the user quits explicitly with Cmd + Q
    if (process.platform !== 'darwin') {
      app.quit()
    }
  })
  
  app.on('activate', () => {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (win === null) {
      createWindow()
    }
  })
  
  // In this file you can include the rest of your app's specific main process
  // code. You can also put them in separate files and require them here.

```

* notesé que en la linea win.loadFile('./dist/TestElectron/index.html') se apunta al directorio dist el cual se debe crear en la compilación.
## Configurar el archivo package.json
Se debe configurar el archivo para que angular sepa que se debe ejecutar electron

relaizar los siguientes cambios:

Luego de "version": "0.0.0" agregar la linea "main": "main.js",
Debe quedar similar a lo siguiente:
```json
 "version": "0.0.0",
  "main": "main.js",
```
En la sección scripts agregar. "electron-build": "ng build --prod" y "electron": "electron ."
Debe quedar similar a lo siguiente:
```json
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test",
    "lint": "ng lint",
    "e2e": "ng e2e",
    "electron-build": "ng build --prod",
    "electron": "electron ."
  },
```
## Cambiar el archivo index.html

En la linea ```html <base href="/"> ``` sustituir por ```html <base href="./"> ```

## probar la configuración
ejecutar la compilación mediante 
ng run electron-build

ejecutar electron mediante 
ng electron
