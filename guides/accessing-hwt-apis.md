# Accessing HWT APIs

The HWT APIs can be put on the global scope via the following:

* Before log-in to GMR: `GMR.RunString('_G.HWT = ({...})[1]')`
* After log-in to GMR: `GMR.RunEncryptedScript(GMR.Encrypt('_G.HWT = ({...})[1]'))`

HWT APIs can be accessed from scripts which are run with `GMR.RunEncryptedScript` (before logging in to GMR also with `GMR.RunString`) via `local HWT = ...`. I.e.

```lua
local HWT = ...

-- Rest of the script
```
