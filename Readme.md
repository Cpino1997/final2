# Método sencillo para implementar jwt en express js

En este método implementaremos jwt de una forma mucho más sencilla. 

Primero inicializaremos nuestro proyecto

```bash

#creamos la carpeta donde trabajaremos

mkdir app

#entramos en la carpeta

cd app

#inicializamos nuestro proyecto

npm init -y

#instalamos las dependencias que ussremos

npm install express jsonwebtoken express-jwt

```

Creamos el archivo app.js que contendrá toda la lógica de esta aplicación sencilla, en este archivo meteremos los siguentes codigos:

```js

//importamos nuestras dependencias

const express = require("express");

const jsonwebtoken = require("jsonwebtoken");

// la palabra secreta puede ser creada con un algoritmo.

const JWT_SECRET = "goK!pusp6ThEdURUtRenOwUhAsWUCLheBazl!uJLPlS8EbreWLdrupIwabRAsiBu";

//declaramos nuestra app expr3ss

const app = express();

app.use(express.json());

//get /

app.get("/", (req, res) => {

  res

    .status(401)

    .json({ message: "You need to be logged in to access this resource" });

});

//post /login

app.post("/login", (req, res) => {

  const { username, password } = req.body;

  console.log(`${username} is trying to login ..`);

// si el usuario y contraseña son validos enviaremos un token.

  if (username === "admin" && password === "admin") {

    return res.json({

      token: jsonwebtoken.sign({ user: "admin" }, JWT_SECRET),

    });

  }

//sino enviaremos error.

  return res

    .status(401)

    .json({ message: "The username and password your provided are invalid" });

});

//puerto escucha.

app.listen(3001, () => {

  console.log("API running on localhost:3001");

});

```

Probamos con postman o insomnia nuestra api, nos dirigimos a http://localhost:3001/login

Y con un método post enviaremos username y password, las cuales si son válidas devolverán un token de usuario. Sino enviara un error :(

Solicitud

![[Screenshot_20221004_125203.jpg]]

Respuesta

![[Screenshot_20221004-124934.jpg]]

Así de sencillo podemos tener un api trabajando con jwt, sencilla y fácil de implementar en otros proyectos.
