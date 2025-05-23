### How to start and quit GDB
type ‘gdb’ to start GDB.  
type quit, exit or Ctrl-d to exit.

### Shell Commands
`shell command-string`  
`!command-string`

### Logging Output (先把logging设置好，最后set logging enabled on)
`set logging enabled [on|off]`  
Enable or disable logging.

`set logging file file`  
Change the name of the current logfile. The default logfile is gdb.txt.

`set logging overwrite [on|off]`  
By default, GDB will append to the logfile. Set overwrite if you want set logging enabled on to overwrite the logfile instead.

`set logging redirect [on|off]`  
By default, GDB output will go to both the terminal and the logfile. Set redirect if you want output to go only to the log file.

`set logging debugredirect [on|off]`  
By default, GDB debug output will go to both the terminal and the logfile. Set debugredirect if you want debug output to go only to the log file.

`show logging`  
Show the current values of the logging settings.

