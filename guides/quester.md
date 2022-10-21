# How to write a quester

A quester is an object that defines quests.
Each quest definition includes information for how the quest can be done.

## Basic structure

* Create a LUA file `<questerName>.lua` (i.e. `Quester.lua`) for the quester in the `Plugins` folder.
* Create a LUA file `<profileName>.lua` (i.e. `Questing.lua`) for the profile in the `Profiles/02. Questing` folder.

### Plugins/Quester.lua

```lua
local Quester = {}

function Quester.defineQuestA()
    local questID = 123
    GMR.DefineQuest(
        { 'Alliance', 'Horde' },
        nil,
        questID,
        '<quest name>',
        'Custom',
        nil,
        nil,
        nil,
        nil,
        nil,
        nil,
        nil,
        nil,
        {
            function()
                print('custom quest logic')
                if not GMR.Questing.IsObjectiveCompleted(questID, 1) then
                    
                elseif not GMR.Questing.IsObjectiveCompleted(questID, 2) then
                    
                end
            end
        },
        function()
            print('setting profile settings')
            
        end
    )
end

GMR.DefineQuester('Quester', function()
    Quester.defineQuestA()
end)
```

### Profiles/02. Questing/Questing.lua

```
GMR.LoadQuester('Quester')
```

## The APIs in more depth

### GMR.DefineQuester

With this API one can add a quester to GMR.
The first argument is the quester name.
The second argument is a function which can register quest definitions.

### GMR.DefineQuest

With this API one can add a quest to GMR.
It is usually called in the function that has been passed as second argument to `GMR.DefineQuester`.

The first argument tells GMR, for what faction the quest is. Can be either `{ 'Alliance', 'Horde' }`, `{ 'Alliance' }` or `{ 'Horde' }`.

The second argument tells GMR, if the quest is for a specific class. `nil` can be passed if it's a class independent quest.

The third argument is the quest id.

The fourth argument is the quest name.

The fifth argument is the GMR quest type. With the value `Custom` one can define custom quest fulfillment logic.
Another possible value is `Grinding`.

The sixth argument is the quest pick up X coordinate. Can also be set to `nil` if no pick up is required.

The seventh argument is the quest pick up Y coordinate. Can also be set to `nil` if no pick up is required.

The eighth argument is the quest pick up Z coordinate. Can also be set to `nil` if no pick up is required.

The ninth argument is the quest pick up ID. It seems to be the ID of the NPC that gives the quest.
Can also be set to `nil` if no pick up is required.

The tenth argument is the quest turn in X coordinate. Can also be set to `nil` if no turn in is required.

The eleventh argument is the quest turn in Y coordinate. Can also be set to `nil` if no turn in is required.

The twelfth argument is the quest turn in Z coordinate. Can also be set to `nil` if no turn in is required.

The thirteenth argument can be used to define the custom quest logic when the GMR quest type is 'Custom'.
It is called regularly with GMR. It seems required to pass a table with a function as argument (see code example above).

The fourteenth argument can be used to set profile settings for the quest.

#### Custom questing logic

When as fifth argument `Custom` is passed to `GMR.DefineQuest` then one can define custom quest logic.
The function for the custom quest logic is passed, wrapped inside a table, as thirteenth argument to `GMR.DefineQuest`.

In this function one can check if certain quest objectives are still open and in the case that a quest objective is open,
tell GMR what to do, to fulfill it.

This is done via the functions that can be found in the `GMR.Questing` namespace.

They can be listed with `/dump GMR.Questing`.

### GMR.LoadQuester

This function loads the quester as "active" quester. The first argument is the quest name, as passed to `GMR.DefineQuester` as first argument.