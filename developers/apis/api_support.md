## API Support

### API Logging

#### Q. How to enable RPC Logging in BitShars

You can enable it by appending the below lins in `config.ini`

    # declare an appender named "rpc" that writes messages to rpc.log
    [log.file_appender.rpc]
    filename=logs/rpc/rpc.log
    # filename can be absolute or relative to this config file

    # route messages sent to the "rpc" logger to the rpc appender declared above
    [logger.rpc]
    level=debug
    appenders=rpc

About Log level: 

- level=error : logs errors
- level=warn : logs requests
- level=info : logs responses


***

