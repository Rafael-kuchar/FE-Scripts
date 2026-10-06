--// CATALOG AVATAR CREATOR
--// INSTANT LAST OUTFIT - LITE
--// FE
--// Made By Sgreemble!

local Players = game:GetService("Players")
local RS = game:GetService("ReplicatedStorage")

local Player = Players.LocalPlayer
local PlayerGui = Player:WaitForChild("PlayerGui")
local Events = RS:WaitForChild("Events")

local LoadPrompt = Events:WaitForChild("LoadLastOutfitPrompt")
local CatalogRemote = Events:WaitForChild("CatalogGuiRemote")
local ToggleUI = Events:WaitForChild("ClientToggleUIVisible")

local Properties
local RigType

local function ShowUI()
    pcall(function()
        ToggleUI:Fire(true)
    end)
end

local function HidePrompt()
    local gui = PlayerGui:FindFirstChild("LoadLastOutfitPromptGui")
    if gui then
        gui.Enabled = false
    end
end

-- Guardar outfit enviado por CAC
LoadPrompt.OnClientEvent:Connect(function(props, rig)
    Properties = props
    RigType = rig

    -- Evitar que CAC deje las demás GUIs ocultas
    ShowUI()

    -- Ocultar solo el prompt
    HidePrompt()
end)

-- Si el prompt se crea otra vez, eliminarlo sin bucle
PlayerGui.ChildAdded:Connect(function(child)
    if child.Name == "LoadLastOutfitPromptGui" then
        child.Enabled = false
        ShowUI()
    end
end)

-- Restaurar inmediatamente al respawn
Player.CharacterAdded:Connect(function()
    if Properties then
        pcall(function()
            CatalogRemote:InvokeServer({
                Action = "CreateAndWearHumanoidDescription",
                Properties = Properties,
                RigType = RigType
            })
        end)
    end

    ShowUI()
    HidePrompt()
end)

HidePrompt()

print("✅ CAC LAST OUTFIT LITE")
