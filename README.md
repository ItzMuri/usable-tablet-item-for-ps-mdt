# usable-tablet-item-for-ps-mdt
create a tablet item for ps-mdt

• First go to qb-core/shared/items and add the following:
```
mdttablet                    = { name = 'mdttablet', label = 'MD Tablet', weight = 500, type = 'item', image = 'tablet.png', unique = false, useable = true, shouldClose = true, combinable = nil, description = 'Mobile Datenbank des Staates' },
```
• I assume you are using the pictures from qb-inventory, which has a tablet picture in it, otherwise you have to create one

• next go to ps-mdt/server/main.lua on line 230:
```
RegisterNetEvent('mdt:server:openMDT', function()
```
• Above that you copy the following:
```
QBCore.Functions.CreateUseableItem('mdttablet', function(source)
	TriggerClientEvent('mdt:client:Tablet', source)
end)
```

• then go to ps-mdt/client/main.lua to line 89:
```
RegisterKeyMapping('mdt', 'Open Police MDT', 'keyboard', 'k')
````
• and comment it out or delete like here
```
--RegisterKeyMapping('mdt', 'Open Police MDT', 'keyboard', 'k')
```
• go to line 91 to 106 and comment or delete the lines like here:
```
--[[RegisterCommand('mdt', function()
    local plyPed = PlayerPedId()
    PlayerData = QBCore.Functions.GetPlayerData()
    if not PlayerData.metadata["isdead"] and not PlayerData.metadata["inlaststand"] and not PlayerData.metadata["ishandcuffed"] and not IsPauseMenuActive() then
        if GetJobType(PlayerData.job.name) ~= nil then
            TriggerServerEvent('mdt:server:openMDT')
            TriggerServerEvent('mdt:requestOfficerData')
        end
    else
        QBCore.Functions.Notify("Can't do that!", "error")
    end
end, false)

Citizen.CreateThread(function()
    TriggerEvent('chat:addSuggestion', '/mdt', 'Open the emergency services MDT', {})
end)]]
```
• and just below you copy the following:
```
RegisterNetEvent('mdt:client:Tablet', function()
    local plyPed = PlayerPedId()
    PlayerData = QBCore.Functions.GetPlayerData()
    if not PlayerData.metadata["isdead"] and not PlayerData.metadata["inlaststand"] and not PlayerData.metadata["ishandcuffed"] and not IsPauseMenuActive() then
        if GetJobType(PlayerData.job.name) ~= nil then
            TriggerServerEvent('mdt:server:openMDT')
            TriggerServerEvent('mdt:requestOfficerData')
        end
    else
        QBCore.Functions.Notify("Can't do that!", "error")
    end
end, false)
```
In this way you can only open the mdt if you are using a tablet, the commands like /mdt or "K" are deactivated


