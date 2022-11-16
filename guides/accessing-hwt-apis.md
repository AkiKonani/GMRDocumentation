# Accessing HWT APIs

The HWT APIs can be put on the global scope via `GMR.RunString('_G.HWT = ({...})[1]')`.

This also works without logging in to GMR in-game.

HWT APIs can be accessed from scripts which are run with `GMR.RunString` or `GMR.RunEncryptedScript` via `local HWT = ...`. I.e.

```lua
local HWT = ...

-- Rest of the script
```
