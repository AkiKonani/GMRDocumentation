# Tips

* You can symlink your files into the folders that GMR provides. This way you can independently revision and publish them (i.e. with Git).
* Retrieving the quest id of the super tracked quest: `/dump C_SuperTrack.GetSuperTrackedQuestID()`
* Saving the player position into a file: `/script local playerPosition = GMR.GetPlayerPosition(); GMR.WriteFile('C:/position.txt', '{ x = ' .. playerPosition.x .. ', y = ' .. playerPosition.y .. ', z = ' .. playerPosition.z .. ' }')`
* Retrieving the item ID of the item in bag 0 in slot 1 (the first slot of the backpack): `/dump GetContainerItemID(0, 1)`
