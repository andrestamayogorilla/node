## Comandos
    node => inicia la terminal interactiva de node (similar a la del navegador web)
    node nombreArchivo => ejecuta un archivo javascript

    npm init => permite crear el archivo de node packages
    npm start => ejecuta el comando start q tengamos instanciado en el package.json
    npm run dev => cualquiera otra palabra q no sea start, necesita la palabra run
                    con la configuracion actual ejecuta :nodemon

            para que el debugger funcione se debe ejecutar el programa desde el archivo package.json, y no mediante el comando

## Extensiones VS Code

    Live Server: servidor web
    ThunderClient : como un postman
    GitLens: Deja ver cosas de git
    JsonTool: Ctrl(Cmd)+Alt+M for JSON pretty.

    MaterialIcon Theme

## nvm

    Instalacion:
        curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

        También fue necesario actualizar el archivo: .zprofile (esta en la carpeta home) y agregar:
        
        export NVM_DIR="$HOME/.nvm"
        [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
        [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    
    comandos:
        nvm ls-remote = lista las versiones disponibles para instalar
        nvm install version = instala una version de node
        Nvm install 14 = instala la version 14

        Nvm use 14… hace q use la version 14
        Nvm ls = lista las version instaladas de node

## Typescript con node (explication): (https://gist.github.com/Klerith/47af527da090043f604b972b22dd4c01)
    Instalar TypeScript y tipos de Node, como dependencia de desarrollo
    npm i -D typescript

    npm install --save-dev nodemon
        nodemon src/app.js => comando para lanzar la aplicacion utilizando nodemon (con tsnode no es necesario)

   Inicializar el archivo de configuración de TypeScript 
   npx tsc --init --outDir dist/ --rootDir src 

   toca tener 2 archivos ejecutandose, haciendo click en el package.json script:
    * npx tsc --watch => detecta los cambios hechos en typescript y los compila a typescript //este toca lanzarlos desde el archivo package.json
    * nodemon dist/app =>esta pendiente de estos cambios en la carpeta de distribución

   para evitar lo anterior se utiliza ts-node
   npm install -D ts-node

   Ademas se crea el archivo: nodemon.json en la raiz de la aplicación el siguiente contenido:<br>
    ```
    {
        "watch": ["src"],
        "ext": ".ts, .js",
        "ignore": [],
        "exec": "ts-node ./src/app.ts"
    }
    ```
    <br>
    Ahora para ejecutarlo simplemente lo podemos hacer con nodemon:
    para ellos corremos del package.json: npm run-dev (ya lo configuré en dicho archivo)

    ### Scripts para production
    npm install -D rimraf

    "build": "rimfaf ./dist && tsc",   //Elimina la carperta de distribucion y crea una nueva
    "start": "npm run build && node dist/app.js" //ejecuta el build y luego corre la aplicacion
    
## UnitTest

    https://gist.github.com/Klerith/98d7b1bc0f1525e892f260813cad1007

    1. Instalaciones de desarrollo (super test es útil para probar Express):
    npm install -D jest @types/jest ts-jest supertest

    2. Crear archivo de configuración de Jest:
    npx jest --init

    3. En el archivo jest.config.js configurar
    preset: 'ts-jest',
    testEnvironment: "jest-environment-node",

    // Opcional - The paths to modules that run some code to configure or set up the testing environment before each test
    // setupFiles: ['dotenv/config'],


    4. Crear scripts en el package.json
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage"

    5. En el archivo tsConfig agregar las lineas:(indica q se va a generar en la carpeta dist)
        "include": ["src/**/*"],
        "exclude": ["node_modules", "**/*.spec.ts","**/*.test.ts"],

## Iniciación de proyecto resumen:
    0.Iniciar el archivo package.json
        npm init 

    1. Instalar TypeScript y demás dependencias
        npm i -D typescript @types/node ts-node nodemon rimraf

    2.Inicializar el archivo de configuración de TypeScript 
        npx tsc --init --outDir dist/ --rootDir src
    
    3.Crear archivo de configuración Nodemon - nodemon.json
        {
            "watch": ["src"],
            "ext": ".ts,.js",
            "ignore": [],
            "exec": "npx ts-node ./src/app.ts"
        }

    4. Crear scripts para dev, build y start en el package.json:
        "dev": "nodemon",
        "build": "rimraf ./dist && tsc",
        "start": "npm run build && node dist/app.js"
    
    nota: para correr scripts en la consola q sean de ts-node se antepone npx:
    npx ts-node src/app

## iniciacion de proyecto sin nodemon y con ts-node-dev

    0.Iniciar el archivo package.json
        npm init 

    1. Instalar TypeScript y demás dependencias
        npm i -D typescript @types/node ts-node-dev rimraf

    2.Inicializar el archivo de configuración de TypeScript 
        npx tsc --init --outDir dist/ --rootDir src

    4. Crear scripts para dev, build y start en el package.json:
        "dev": "tsnd --respawn src/app.ts",
        "build": "rimraf ./dist && tsc",
        "start": "npm run build && node dist/app.js"


## json-server
    es util para crear prototipos de aplicaciones rest 
    npm install json-server

    https://www.npmjs.com/package/json-server

    siemplemente se inicia el archivo package.json
        npm init 

    se crea un archivo db.json con data inicial
    
    y se ejecuta: npx json-server db.json


   