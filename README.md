# es-blackmarkets
EsScripts  - Simple script for black market with configurable item currency







=====================================================================

--> Installation Guide

=======================================================================


navigate to [qb]/qb-inventory/server/main.lua
and serch for the line: "elseif fromInventory == "crafting" then"
copy and past this "elseif" above "elseif fromInventory == "crafting" then"

==================================================================
from here from here from here from here from here from here
  
     elseif QBCore.Shared.SplitStr(fromInventory, "-")[1] == "dirtyshop" then
		local shopType = QBCore.Shared.SplitStr(fromInventory, "-")[2]
		local itemData = ShopItems[shopType].items[fromSlot]
		local itemInfo = QBCore.Shared.Items[itemData.name:lower()]
        local bankBalance = Player.PlayerData.money["bank"]
		local price = tonumber((itemData.price*fromAmount))
        local BlackMoneyItem = Config.BlackMoneyItem
        local hasItem = Player.Functions.HasItem(Config.BlackMoneyItem)
    if QBCore.Shared.SplitStr(shopType, "_")[1] == "dirtyshop" then
            if QBCore.Functions.HasItem(src, Config.BlackMoneyItem, price) then
             local dirtyBalance = Player.Functions.GetItemByName(Config.BlackMoneyItem).amount
                if dirtyBalance > price then
                Player.Functions.RemoveItem(Config.BlackMoneyItem, price)
                TriggerClientEvent('inventory:client:ItemBox', src, QBCore.Shared.Items[BlackMoneyItem], "remove")
              --  Player.Functions.RemoveMoney("bank", price, "itemshop-bought-item")
                local serial = itemData.info.serie
                local imageurl = ("https://cfx-nui-qb-inventory/html/images/%s.png"):format(itemData.name)
                local notes = "Purchased at Ammunation"
                local owner = Player.PlayerData.charinfo.firstname .. " " .. Player.PlayerData.charinfo.lastname
                local weapClass = 1
                local weapModel = QBCore.Shared.Items[itemData.name].label
                AddItem(src, itemData.name, fromAmount, toSlot, itemData.info)
                TriggerClientEvent('qb-shops:client:UpdateShop', src, QBCore.Shared.SplitStr(shopType, "_")[2], itemData, fromAmount)
                QBCore.Functions.Notify(src, itemInfo["label"] .. " bought!", "success")
                TriggerEvent("qb-log:server:CreateLog", "shops", "Shop item bought", "green", "**"..GetPlayerName(src) .. "** bought a " .. itemInfo["label"] .. " for $"..price)
      else
       QBCore.Functions.Notify(src, "i aint playin games kid..", "error")
      end
            else
                QBCore.Functions.Notify(src, "nothing comes for free fool!", "error")
            end
		else
			if Player.Functions.RemoveMoney("cash", price, "unkown-itemshop-bought-item") then
				AddItem(src, itemData.name, fromAmount, toSlot, itemData.info)
				QBCore.Functions.Notify(src, itemInfo["label"] .. " bought!", "success")
				TriggerEvent("qb-log:server:CreateLog", "shops", "Shop item bought", "green", "**"..GetPlayerName(src) .. "** bought a " .. itemInfo["label"] .. " for $"..price)
			elseif dirtyBalance >= price then
				Player.Functions.RemoveMoney("bank", price, "unkown-itemshop-bought-item")
				AddItem(src, itemData.name, fromAmount, toSlot, itemData.info)
				QBCore.Functions.Notify(src, itemInfo["label"] .. " bought!", "success")
				TriggerEvent("qb-log:server:CreateLog", "shops", "Shop item bought", "green", "**"..GetPlayerName(src) .. "** bought a " .. itemInfo["label"] .. " for $"..price)
			else
				TriggerClientEvent('QBCore:Notify', src, "You don\'t have enough cash..", "error")
			end
		end

up to here up to here up to here up to up to here up to here 

================================================================================
next step next step next step next step next step next step next step next step next step next step next step next step next
next step next step next step next step next step next step next step next step next step next step next step next step 

navigate to [qb]/qb-inventory/server/main.lua
and serch for the line: "elseif name == "traphouse" then"
copy and past this "elseif name == "traphouse" then"
======================================================================================
from here from here from here \/-\/-\/-\/ from here from here from here

    elseif name == "dirtyshop" then
				secondInv.name = "dirtyshop-"..id
				secondInv.label = other.label
				secondInv.maxweight = 9000000
				secondInv.inventory = SetupShopItems(other.items)
				ShopItems[id] = {}
				ShopItems[id].items = other.items
				secondInv.slots = #other.items

up to here up to here up to here  /\-/\-/\-/\ up to up to here up to here 

======================================================================================


next step next step next step next step next step next step next step next step

navigate to [qb]/qb-inventory/config.lua
copy and past this "Config.BlackMoneyItem = "dirtymoney"
anywhere you like !
======================================================================================
