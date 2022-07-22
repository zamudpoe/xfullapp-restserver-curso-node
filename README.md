# 110 Subir El RESTServer A Heroku

Despleguemos nuestro RestServer a Heroku 

Vale la pena decir que podemos enlazar nuestro repositorio de ``Github`` a ``Heroku``, pero si lo hacemos va estar trabajando con la ultima version de nuestro repositorio y nosotros necesitamos que lo vayamos haciendo todo como esta viendose en este momento, podriamos hacer pruebas con ``Github`` , pero nosotros lo haremos con ``Heroku CLI`` 

Recordemos que  Heroku nos permite tener hasta 5 aplicaciones gratis , y en mi cuenta solo tengo una desplegada , asi que tengo 4 libres , ocuapre una de esas 4 libres para desplegar esta app.

## Creacion de nueva app en Heroku 

Craemos una nueva app en Heroku en esta url [Heroku-NewApp] con los siguientes datos: 

* **App name      :** xfullapp-restserver-curso-node  
* **Choose Region :** United States 

Una vez creada, ya podemos hacer el deploy, las instrucciones las encontramos en la pestaña de deploy -> [Heroku Deploy]

### Crea un nuevo repositorio Git

1. Crea un nuevo repositorio Git 

    Inicializamos un repositorio en Git en uno nuevo o directorio existente!. 

    ```unix
    $ cd my-project/ 
    $ git init 
    $ heroku git:remote -a xfullapp-restserver-curso-node 
    ```

1. Nosotros ya estamos en la carpeta del proyecto y ya realizamos el ``git init`` , ahora solo nos falta agregar el repositorio remoto, asi que realizamos ``heroku git:remote -a xfullapp-restserver-curso-node`` 

    **Respuesta :** 

    ```unix
    »   Warning: heroku update available from 7.53.0 to 7.60.2.
    set git remote heroku to https://git.heroku.com/xfullapp-restserver-curso-node.git 
    ```

1. **Despliega tu app** 

    Necesitamos hacer el commit de nuestro codigo y desplegarlo a Heroku usando Git asi : 

    ```unix
    $ git add .
    $ git commit -am "make it better"
    $ git push heroku master 
    ```

    Pero esto ``git push heroku master`` no nos dara un error, por la rama 
    
    ```javascript
    error: src refspec master does not match any
    error: failed to push some refs to 'https://git.heroku.com/xfullapp-restserver-curso-node.git'
    ```
    Si hacemos un ``git branch`` vamos a notar que aqui dice ``main`` 

    ```UNIX
    git branch
    * main    
    ```

    Como ya no tenemos el master y estaba intentando de subir el master que ya no existe por que yo lo renombre con el '-m' , entonces tenemos que hacer lo siguiente : 

    ``git push heroku main`` 

    Listo obtenemos este resultado, una vez que se hizo el deploy :  
    ```unix
        Enumerating objects: 19, done.
    Counting objects: 100% (19/19), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (14/14), done.
    Writing objects: 100% (19/19), 12.42 KiB | 1.13 MiB/s, done.
    Total 19 (delta 2), reused 0 (delta 0), pack-reused 0
    remote: Compressing source files... done.
    remote: Building source:
    remote:
    remote: -----> Building on the Heroku-20 stack
    remote: -----> Determining which buildpack to use for this app
    remote: -----> Node.js app detected
    remote:
    remote: -----> Creating runtime environment
    remote:
    remote:        NPM_CONFIG_LOGLEVEL=error
    remote:        NODE_VERBOSE=false
    remote:        NODE_ENV=production
    remote:        NODE_MODULES_CACHE=true
    remote:
    remote: -----> Installing binaries
    remote:        engines.node (package.json):  unspecified
    remote:        engines.npm (package.json):   unspecified (use default)
    remote:
    remote:        Resolving node version 16.x...
    remote:        Downloading and installing node 16.16.0...
    remote:        Using default npm version: 8.11.0
    remote:
    remote: -----> Installing dependencies
    remote:        Installing node modules
    remote:
    remote:        added 61 packages, and audited 62 packages in 1s
    remote:
    remote:        7 packages are looking for funding
    remote:          run `npm fund` for details
    remote:
    remote:        found 0 vulnerabilities
    remote:
    remote: -----> Build
    remote:
    remote: -----> Caching build
    remote:        - npm cache
    remote:
    remote: -----> Pruning devDependencies
    remote:
    remote:        up to date, audited 62 packages in 400ms
    remote:
    remote:        7 packages are looking for funding
    remote:          run `npm fund` for details
    remote:
    remote:        found 0 vulnerabilities
    remote:
    remote: -----> Build succeeded!
    remote:  !     This app may not specify any way to start a node process
    remote:        https://devcenter.heroku.com/articles/nodejs-support#default-web-process-type
    remote:
    remote: -----> Discovering process types
    remote:        Procfile declares types     -> (none)
    remote:        Default types for buildpack -> web
    remote:
    remote: -----> Compressing...
    remote:        Done: 32.2M
    remote: -----> Launching...
    remote:        Released v3
    remote:        https://xfullapp-restserver-curso-node.herokuapp.com/ deployed to Heroku
    remote:
    remote: This app is using the Heroku-20 stack, however a newer stack is available.
    remote: To upgrade to Heroku-22, see:
    remote: https://devcenter.heroku.com/articles/upgrading-to-the-latest-stack
    remote:
    remote: Verifying deploy... done.
    To https://git.heroku.com/xfullapp-restserver-curso-node.git
    * [new branch]      main -> main
    ```

    > **NOTA :** Si intentamos abrir la app de heroku nos mostrara error "``Application error``", ¿Por Que?, bueno esto es por que no modificamos nuestro archivo manifiesto ``package.json`` antes para agregarle la opcion del script "``start``" 


1.  Modificamos nuestro archivo manifiesto ``package.json`` para agregar el script para ``"start" : "node app.js",`` 

    ```json
    {
    "name": "07_restwerver",
    "version": "1.0.0",
    "description": "",
    "main": "app.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "dependencies": {
        "colors": "^1.4.0",
        "cors": "^2.8.5",
        "dotenv": "^16.0.1",
        "express": "^4.18.1"
    }
    }
    ```
    Lo modificamos y agregamos 


    ```json
    {
    "name": "07_restwerver",
    "version": "1.0.0",
    "description": "",
    "main": "app.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1",
        "start" : "node app.js" 
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "dependencies": {
        "colors": "^1.4.0",
        "cors": "^2.8.5",
        "dotenv": "^16.0.1",
        "express": "^4.18.1"
    }
    }
    ```

1. Ahora tenemos que desplegar a github 

    ```unix 
    git add . 
    git commit -m "package.json [Actualizado] - npm start agregado" 
    git push 
    ```
1. Lo subimos a heroku ``git push heroku main`` y consultamos ==> [Mi HerokuApp] y debemos de ver la pagina que nos dice ``Acceso Denegado``

1. Usamos **POSTMAN** para consultar la 


    **URL**: ``https://xfullapp-restserver-curso-node.herokuapp.com/api/usuarios?q=hola&empresa=Cydsa&apikey=980786&limit=10&page=666``  
    
    **Metodos :** GET . 

    **Body :** 

    ```json
    {
    "nombre": "Engelbert",
    "edad": 47
    }
    ```
    


    **URL :** ``https://xfullapp-restserver-curso-node.herokuapp.com/api/usuarios/15`` 
    
    **METODO :**: PUT 



    **URL     :**  ``https://xfullapp-restserver-curso-node.herokuapp.com/api/usuarios``

    **METODO  :** POST 

    **body    :** 
    ```json
    {
    "nombre": "Engelbert",
    "edad": 47
    }
    ```


    **URL :** ``https://xfullapp-restserver-curso-node.herokuapp.com/api/usuarios/`` .

    **METODO :** DELETE 


### Todas las rutas deben funcionar como hasta el momento qeu las probabamos en localhost:4500 , pero ahora ya estan en produccion 

Ahora cualquier cambio en nuestro proyecto , lo subimos a 

```unix
git add .
$ git commit -am "make it better"
$ git push heroku master
```

--- 
**URL's**
* [Heroku-git] 
* [Heroku-Apps] 
* [Heroku-NewApp] 
* [Heroku-cli] 


--- 
[Heroku-git]:(https://dashboard.heroku.com/apps/xapp-webserver-curso-node-fher/deploy/heroku-git) 
[Heroku-cli]:(https://devcenter.heroku.com/articles/heroku-cli)
[Heroku-Apps]:(https://dashboard.heroku.com/apps)
[Heroku-NewApp]:(https://dashboard.heroku.com/new-app)
[Heroku Deploy]:(https://dashboard.heroku.com/apps/xfullapp-restserver-curso-node/deploy/heroku-git) 
[Mi HerokuApp]:(https://xfullapp-restserver-curso-node.herokuapp.com/)


