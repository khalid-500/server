# 1-3server

## require
```javascript
//required express js section
const express = require('express');
const app = express();
var http = require('http')


//require soket io section 
const {Server} =require("socket.io")
const server = http.createServer(app);
const io=new Server(server,{
  cors:{
      origin:"http://localhost:3000",
      methods:["GET","POST","PUT","DELETE"]
  }
})

//to mack safe connext between front and back
const cors=require("cors");
const corsOptions ={
   origin:'http://localhost:3000/', 
   credentials:true,            //access-control-allow-credentials:true
   optionSuccessStatus:200,
}

app.use(cors()) // Use this after the variable declaration


// support url encoded bodies{parser use to accept the encoded json come from front }
app.use(express.urlencoded({ extended: false }));
// support json encoded bodies
app.use(express.json());


//express middelware to handel cookies come from front 
const cookieParser = require('cookie-parser')
app.use(cookieParser())



```


## connection with the database and server

```javascript
//Connection With The Database
const @@@selectdatabase=require("../database/facebook_database")
async function start(PORT){// WHE MUST RUN DATABASE CONNECTION BEFORE LISTEN TO SERVER
  server.listen(PORT, async() => {
        try {
            await @@@selectdatabase.authenticate();
            //USE TO SYNC ANY CHANGE CAN HAPPEN  ON DATABASE 
            await @@@selectdatabase.sync();
            console.log('Connection has been established successfully.');
          } catch (error) {
            console.error('Unable to connect to the database:', error);
          }      
      console.log(`Example app listening on port ${PORT}`)
    })
    }
    
    
    
    module.exports ={
    app: app,
    start: start,
    server:server
}

```


