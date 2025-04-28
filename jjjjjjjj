-- Pet Simulator X | Auto Farm Separate + STOP ALL Button
-- Executor: Delta X (hoặc các Executor khác tương thích)

-- Load OrionLib (Đảm bảo Delta X hỗ trợ thư viện này)
local OrionLib = loadstring(game:HttpGet(('https://raw.githubusercontent.com/shlexware/Orion/main/source')))()

local Window = OrionLib:MakeWindow({Name = "Pet Simulator X | Separate Auto + Stop All", HidePremium = false, SaveConfig = true, ConfigFolder = "PSXSeparateAutoStopAll"})

-- SERVICES
local Workspace = game:GetService("Workspace")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Network = ReplicatedStorage:WaitForChild("Network")
local Players = game:GetService("Players")

-- SETTINGS
local Settings = {
    AutoFarm = false,
    AutoUpgrade = false,
    AutoCollect = false,
    AutoEnchant = false
}

-- FUNCTIONS

function AutoFarmCoins()
    while Settings.AutoFarm do
        for _, coin in pairs(Workspace["__THINGS"].Coins:GetChildren()) do
            Network:FireServer("CollectCoin", coin.Name)
        end
        task.wait(1)
    end
end

function AutoBuyUpgrades()
    while Settings.AutoUpgrade do
        for _, upgrade in ipairs({"PetStrength", "PlayerSpeed", "PetSpeed"}) do
            Network:FireServer("BuyUpgrade", upgrade)
        end
        task.wait(5)
    end
end

function AutoCollectDrops()
    while Settings.AutoCollect do
        for _, orb in pairs(Workspace["__THINGS"].Orbs:GetChildren()) do
            Network:FireServer("CollectOrb", orb.Name)
        end
        task.wait(1)
    end
end

function AutoEnchantPets()
    while Settings.AutoEnchant do
        for _, pet in pairs(Workspace["__THINGS"].Pets:GetChildren()) do
            Network:InvokeServer("EnchantPet", pet.Name)
        end
        task.wait(5)
    end
end

-- STOP ALL FUNCTION
function StopAll()
    Settings.AutoFarm = false
    Settings.AutoUpgrade = false
    Settings.AutoCollect = false
    Settings.AutoEnchant = false
    OrionLib:MakeNotification({
        Name = "Stopped!",
        Content = "Đã tắt toàn bộ Auto!",
        Image = "rbxassetid://4483345998",
        Time = 3
    })
end

-- GUI Tabs
local Tab = Window:MakeTab({
    Name = "Auto Farm Separate",
    Icon = "rbxassetid://4483345998",
    PremiumOnly = false
})

-- Toggle từng chức năng

Tab:AddToggle({
    Name = "Auto Farm Coins",
    Default = false,
    Callback = function(Value)
        Settings.AutoFarm = Value
        if Value then
            AutoFarmCoins()
        end
    end
})

Tab:AddToggle({
    Name = "Auto Upgrade Stats",
    Default = false,
    Callback = function(Value)
        Settings.AutoUpgrade = Value
        if Value then
            AutoBuyUpgrades()
        end
    end
})

Tab:AddToggle({
    Name = "Auto Collect Drops",
    Default = false,
    Callback = function(Value)
        Settings.AutoCollect = Value
        if Value then
            AutoCollectDrops()
        end
    end
})

Tab:AddToggle({
    Name = "Auto Enchant Pets",
    Default = false,
    Callback = function(Value)
        Settings.AutoEnchant = Value
        if Value then
            AutoEnchantPets()
        end
    end
})

-- Nút STOP ALL
Tab:AddButton({
    Name = "🚫 STOP ALL AUTO",
    Callback = function()
        StopAll()
    end
})

OrionLib:Init()
