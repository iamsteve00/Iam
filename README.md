local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- Black background
Frame.BackgroundTransparency = 0.5 -- Semi-transparent
Frame.Position = UDim2.new(0.5, -200, 0.5, -120)
Frame.Size = UDim2.new(0, 400, 0, 240)
Frame.Visible = false

TweenService:Create(Frame, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 0}):Play()

-- Welcome message
local WelcomeMessage = Instance.new("TextLabel")
WelcomeMessage.Parent = ScreenGui
WelcomeMessage.Text = "Welcome to Emilli Hub!"
WelcomeMessage.Size = UDim2.new(0, 300, 0, 50)
WelcomeMessage.Position = UDim2.new(0.5, -150, 0.5, -25)
WelcomeMessage.BackgroundTransparency = 1
WelcomeMessage.TextColor3 = Color3.fromRGB(255, 255, 255)
WelcomeMessage.TextScaled = true

task.spawn(function()
    wait(5) -- The message stays for exactly 5 seconds
    TweenService:Create(WelcomeMessage, TweenInfo.new(1), {TextTransparency = 1}):Play()
    wait(1)
    WelcomeMessage:Destroy()
    Frame.Visible = true
end)

-- Creating tab area
local Tabs = Instance.new("Frame")
Tabs.Parent = Frame
Tabs.Size = UDim2.new(0, 100, 0, 200)
Tabs.Position = UDim2.new(0, -120, 0, 10)

local InitialMessage = Instance.new("TextLabel")
InitialMessage.Parent = Frame
InitialMessage.Text = "v1 Emilli Hub"
InitialMessage.Size = UDim2.new(1, 0, 1, -50)
InitialMessage.Position = UDim2.new(0, 0, 0, 50)
InitialMessage.BackgroundTransparency = 1
InitialMessage.TextColor3 = Color3.fromRGB(255, 255, 255)
InitialMessage.TextScaled = true

-- Creating tabs
local OthersTab = Instance.new("Frame")
OthersTab.Parent = Frame
OthersTab.Size = UDim2.new(1, 0, 1, -50)
OthersTab.Position = UDim2.new(0, 0, 0, 50)
OthersTab.Visible = false

local TrollTab = Instance.new("Frame")
TrollTab.Parent = Frame
TrollTab.Size = UDim2.new(1, 0, 1, -50)
TrollTab.Position = UDim2.new(0, 0, 0, 50)
TrollTab.Visible = false

local PlayerTab = Instance.new("Frame")
PlayerTab.Parent = Frame
PlayerTab.Size = UDim2.new(1, 0, 1, -50)
PlayerTab.Position = UDim2.new(0, 0, 0, 50)
PlayerTab.Visible = false

local OthersVisible, TrollVisible, PlayerVisible = false, false, false

local function ToggleTab(tab, visibilityFlag)
    visibilityFlag = not visibilityFlag
    tab.Visible = visibilityFlag
    InitialMessage.Visible = not (OthersVisible or TrollVisible or PlayerVisible)
    return visibilityFlag
end

local OthersButton = Instance.new("TextButton")
OthersButton.Parent = Tabs
OthersButton.Text = "Others"
OthersButton.Size = UDim2.new(1, 0, 0.2, 0)
OthersButton.MouseButton1Click:Connect(function()
    OthersVisible = ToggleTab(OthersTab, OthersVisible)
    TrollTab.Visible, PlayerTab.Visible = false, false
end)

local TrollButton = Instance.new("TextButton")
TrollButton.Parent = Tabs
TrollButton.Text = "Troll"
TrollButton.Size = UDim2.new(1, 0, 0.2, 0)
TrollButton.MouseButton1Click:Connect(function()
    TrollVisible = ToggleTab(TrollTab, TrollVisible)
    OthersTab.Visible, PlayerTab.Visible = false, false
end)

local PlayerButton = Instance.new("TextButton")
PlayerButton.Parent = Tabs
PlayerButton.Text = "Player"
PlayerButton.Size = UDim2.new(1, 0, 0.2, 0)
PlayerButton.MouseButton1Click:Connect(function()
    PlayerVisible = ToggleTab(PlayerTab, PlayerVisible)
    OthersTab.Visible, TrollTab.Visible = false, false
end)

-- Adding input bars
local PlayerNameBox = Instance.new("TextBox")
PlayerNameBox.Parent = TrollTab
PlayerNameBox.PlaceholderText = "Enter player name"
PlayerNameBox.Size = UDim2.new(0.8, 0, 0.2, 0)
PlayerNameBox.Position = UDim2.new(0.1, 0, 0.05, 0)

local FlySpeedBox = Instance.new("TextBox")
FlySpeedBox.Parent = OthersTab
FlySpeedBox.PlaceholderText = "Fly speed"
FlySpeedBox.Size = UDim2.new(0.8, 0, 0.2, 0)
FlySpeedBox.Position = UDim2.new(0.1, 0, 0.05, 0)

-- Minimized mode system
local MinimizedFrame = Instance.new("TextButton")
MinimizedFrame.Parent = ScreenGui
MinimizedFrame.Text = "Open"
MinimizedFrame.Size = UDim2.new(0, 50, 0, 50)
MinimizedFrame.Position = UDim2.new(0.5, -25, 0.5, -25)
MinimizedFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 0)
MinimizedFrame.Visible = false

MinimizedFrame.MouseButton1Click:Connect(function()
    Frame.Visible = true
    MinimizedFrame.Visible = false
end)

local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Tabs
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(1, 0, 0.2, 0)
MinimizeButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
    MinimizedFrame.Visible = true
end)

local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Tabs
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(1, 0, 0.2, 0)
CloseButton.MouseButton1Click:Connect(function()
    Frame:Destroy()
end)
