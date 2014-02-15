# sails-angular-seed

This code is based on [This Repository](https://github.com/levid/angular-sails-socketio-mongo-demo.git)


## Getting started
### Setup
    git clone git@github.com:NAzT/sails-angular-seed.git your_project
    cd your_project
    npm install
    bower install
    sails lift 
    
### Sails
    sails lift                       Run the Sails app in the current dir (if node_modules/sails exists, it will be used instead of the global install)
      [--dev]                        in development environment
      [--prod]                       in production environment
      [--port 9000]                  on port 9000
      [--verbose]                    with verbose logging enabled
    sails console                    Run this Sails app (in the current dir & in interactive mode.)
    sails new <appName>              Create a new Sails project in a folder called <appName>
    sails new <appName> --linker     Create a new Sails project in a folder called <appName>, using automatic asset linking
    sails generate <foo>             Generate api/models/Foo.js and api/controllers/FooController.js
    sails generate model <foo>       Generate api/models/Foo.js
    sails generate controller <foo>  Generate api/controllers/FooController.js
    sails version                    Get the current globally installed Sails version
    sails run <command>              Run a management command (exported by YOUR_APP/commands/index.js)

-----------------

## Configurations
### App-level socket
    
- config/sockets.js

        onConnect: function(session, socket) {
              console.log('onConnection')
              var numberOfSockets = Object.keys(socket.namespace.manager.sockets.sockets).length
              socket.emit('connectedUsers', { count: numberOfSockets });
              socket.broadcast.emit('connectedUsers', { count: numberOfSockets });
        }


### Controller-level socket

- api/controllers/your_controller.js

        method: function (req, res) {
            sails.io.sockets.emit('rfid', { card_id: req.params.id})
        }
