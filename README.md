-- **B Maxx's Prison Life Free Script**

-- Create GUI
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local ToggleButton = Instance.new("TextButton")
local CloseButton = Instance.new("TextButton")
local ShowButton = Instance.new("TextButton")

ScreenGui.Parent = game.CoreGui
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
Frame.Position = UDim2.new(0, 50, 0, 50)
Frame.Size = UDim2.new(0, 200, 0, 300)

ToggleButton.Parent = Frame
ToggleButton.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
ToggleButton.Position = UDim2.new(0, 25, 0, 25)
ToggleButton.Size = UDim2.new(0, 150, 0, 50)
ToggleButton.Text = "Toggle Features"

CloseButton.Parent = Frame
CloseButton.BackgroundColor3 = Color3.new(0.8, 0.2, 0.2)
CloseButton.Position = UDim2.new(0, 25, 0, 100)
CloseButton.Size = UDim2.new(0, 150, 0, 50)
CloseButton.Text = "Close Script"

ShowButton.Parent = ScreenGui
ShowButton.BackgroundColor3 = Color3.new(0.2, 0.8, 0.2)
ShowButton.Position = UDim2.new(0, 50, 0, 50)
ShowButton.Size = UDim2.new(0, 150, 0, 50)
ShowButton.Text = "Show Script"
ShowButton.Visible = false

local featuresEnabled = false

ToggleButton.MouseButton1Click:Connect(function()
    featuresEnabled = not featuresEnabled
    if featuresEnabled then
        ToggleButton.Text = "Disable Features"
        enableFeatures()
    else
        ToggleButton.Text = "Enable Features"
        disableFeatures()
    end
end)

CloseButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
    ShowButton.Visible = true
end)

ShowButton.MouseButton1Click:Connect(function()
    Frame.Visible = true
    ShowButton.Visible = false
end)

-- Functions to enable/disable features
local function enableFeatures()
    teleportTo(CFrame.new(0, 100, 0)) -- Teleport to a specific location
    giveWeapon("M9") -- Give yourself an M9 pistol
    setWalkSpeed(50) -- Set walk speed to 50
    setJumpPower(100) -- Set jump power to 100
    enableESP() -- Enable ESP
    enableMagicAim() -- Enable Magic Aim
    enableWallHack() -- Enable Wall Hack
    enableGodMode() -- Enable God Mode
end

local function disableFeatures()
    setWalkSpeed(16) -- Reset walk speed to default
    setJumpPower(50) -- Reset jump power to default
    disableESP() -- Disable ESP
    disableMagicAim() -- Disable Magic Aim
    disableWallHack() -- Disable Wall Hack
    disableGodMode() -- Disable God Mode
end

-- Teleport to different locations
local function teleportTo(location)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        player.Character.HumanoidRootPart.CFrame = location
    end
end

-- Give yourself a weapon
local function giveWeapon(weaponName)
    local player = game.Players.LocalPlayer
    local backpack = player:FindFirstChild("Backpack")
    if backpack then
        local weapon = game.ReplicatedStorage:FindFirstChild(weaponName)
        if weapon then
            weapon:Clone().Parent = backpack
        end
    end
end

-- Set walk speed
local function setWalkSpeed(speed)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.WalkSpeed = speed
    end
end

-- Set jump power
local function setJumpPower(power)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.JumpPower = power
    end
end

-- ESP function
local function enableESP()
    local players = game:GetService("Players")
    local localPlayer = players.LocalPlayer

    local function createESP(player)
        if player ~= localPlayer then
            local highlight = Instance.new("Highlight")
            highlight.Parent = player.Character
            highlight.Adornee = player.Character
            highlight.FillColor = Color3.new(1, 0, 0) -- Red color
            highlight.FillTransparency = 0.5
            highlight.OutlineTransparency = 0
        end
    end

    players.PlayerAdded:Connect(createESP)
    for _, player in pairs(players:GetPlayers()) do
        createESP(player)
    end
end

local function disableESP()
    for _, player in pairs(game:GetService("Players"):GetPlayers()) do
        if player.Character and player.Character:FindFirstChildOfClass("Highlight") then
            player.Character:FindFirstChildOfClass("Highlight"):Destroy()
        end
    end
end

-- Magic Aim function
local function enableMagicAim()
    -- Implement magic aim logic here
end

local function disableMagicAim()
    -- Implement logic to disable magic aim here
end

-- Wall Hack function
local function enableWallHack()
    -- Implement wall hack logic here
end

local function disableWallHack()
    -- Implement logic to disable wall hack here
end

-- God Mode function
local function enableGodMode()
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.MaxHealth = math.huge
        player.Character.Humanoid.Health = math.huge
    end
end

local function disableGodMode()
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("Humanoid") then
        player.Character.Humanoid.MaxHealth = 100
        player.Character.Humanoid.Health = 100
    end
end
