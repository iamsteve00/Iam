
-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local MinimizedFrame = Instance.new("Frame") -- Small movable square when minimized

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)

-- Close button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 1, -35)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Minimized Square
MinimizedFrame.Name = "MinimizedFrame"
MinimizedFrame.Parent = ScreenGui
MinimizedFrame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
MinimizedFrame.Size = UDim2.new(0, 50, 0, 50)
MinimizedFrame.Position = UDim2.new(0.5, -25, 0.5, -25)
MinimizedFrame.Visible = false

-- Function to minimize and restore the interface
local minimized = false

MinimizedFrame.MouseButton1Click:Connect(function()
    minimized = false
    MinimizedFrame.Visible = false
    Frame.Visible = true
    TrollFrame.Visible = false
    PlayerFrame.Visible = false
    OthersFrame.Visible = false
end)

local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Frame
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 1, -35)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

MinimizeButton.MouseButton1Click:Connect(function()
    minimized = true
    Frame.Visible = false
    MinimizedFrame.Visible = true
end)

-- Creating tabs
local function createTabButton(name, text, position)
    local tabButton = Instance.new("TextButton")
    tabButton.Name = name
    tabButton.Parent = Frame
    tabButton.Text = text
    tabButton.Size = UDim2.new(0, 80, 0, 30)
    tabButton.Position = position
    return tabButton
end

local TrollTab = createTabButton("TrollTab", "Troll", UDim2.new(0, 10, 0, 10))
local PlayerTab = createTabButton("PlayerTab", "Player", UDim2.new(0, 100, 0, 10))
local OthersTab = createTabButton("OthersTab", "Others", UDim2.new(0, 190, 0, 10))

-- Ensuring only one tab is visible at a time
TrollTab.MouseButton1Click:Connect(function()
    Frame.Visible = false
    TrollFrame.Visible = true
    PlayerFrame.Visible = false
    OthersFrame.Visible = false
end)

PlayerTab.MouseButton1Click:Connect(function()
    Frame.Visible = false
    TrollFrame.Visible = false
    PlayerFrame.Visible = true
    OthersFrame.Visible = false
end)

OthersTab.MouseButton1Click:Connect(function()
    Frame.Visible = false
    TrollFrame.Visible = false
    PlayerFrame.Visible = false
    OthersFrame.Visible = true
    FlyGui.Enabled = true -- Activating Fly GUI when opening the Others tab
end)

-- Creating player selection box before Void and View Player
local PlayerNameBox = Instance.new("TextBox")
PlayerNameBox.Parent = TrollFrame
PlayerNameBox.PlaceholderText = "Enter Player Name"
PlayerNameBox.Size = UDim2.new(0, 150, 0, 30)
PlayerNameBox.Position = UDim2.new(0, 10, 0, 10)
PlayerNameBox.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
PlayerNameBox.TextScaled = true

-- Void Player functionality
local voidActive = false
local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollFrame
VoidButton.Text = "Void Player (ON/OFF)"
VoidButton.Size = UDim2.new(0, 150, 0, 30)
VoidButton.Position = UDim2.new(0, 10, 0, 50)

VoidButton.MouseButton1Click:Connect(function()
    local playerName = PlayerNameBox.Text
    if playerName == "" then return end

    local targetPlayer = game.Players:FindFirstChild(playerName)

    if targetPlayer and targetPlayer.Character and targetPlayer.Character:FindFirstChild("HumanoidRootPart") then
        voidActive = not voidActive
        VoidButton.Text = voidActive and "Void Player (ON)" or "Void Player (OFF)"

        if voidActive then
            targetPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0, -500, 0) -- Sends player to void
        end
    else
        print("Player not found.")
    end
end)

-- View Player functionality
local viewing = false
local ViewButton = Instance.new("TextButton")
ViewButton.Parent = TrollFrame
ViewButton.Text = "View Player (ON/OFF)"
ViewButton.Size = UDim2.new(0, 150, 0, 30)
ViewButton.Position = UDim2.new(0, 10, 0, 90)

ViewButton.MouseButton1Click:Connect(function()
    local playerName = PlayerNameBox.Text
    if playerName == "" then return end

    local targetPlayer = game.Players:FindFirstChild(playerName)

    if targetPlayer and targetPlayer.Character then
        viewing = not viewing
        ViewButton.Text = viewing and "View Player (ON)" or "View Player (OFF)"

        if viewing then
            game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character:FindFirstChild("Humanoid")
        else
            game.Workspace.CurrentCamera.CameraSubject = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        end
    else
        print("Player not found.")
    end
end)
