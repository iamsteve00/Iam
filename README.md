local TweenService = game:GetService("TweenService")

-- Criando a interface principal
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Parent = game.CoreGui

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -200, 0.5, -120)
Frame.Size = UDim2.new(0, 400, 0, 240)

TweenService:Create(Frame, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 0}):Play()

-- Mensagem de boas-vindas
local WelcomeMessage = Instance.new("TextLabel")
WelcomeMessage.Parent = Frame
WelcomeMessage.Text = "Bem-vindo ao Emilli Hub!"
WelcomeMessage.Size = UDim2.new(1, 0, 0, 40)
WelcomeMessage.Position = UDim2.new(0, 0, -0.2, 0)
WelcomeMessage.BackgroundTransparency = 1
WelcomeMessage.TextColor3 = Color3.fromRGB(255, 255, 255)
WelcomeMessage.TextScaled = true

-- Criando a área das abas (empilhadas na esquerda)
local Tabs = Instance.new("Frame")
Tabs.Parent = Frame
Tabs.Size = UDim2.new(0, 100, 0, 200)
Tabs.Position = UDim2.new(0, -120, 0, 10)

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

-- Alternância das abas
local OthersVisible = false
local TrollVisible = false

local OthersButton = Instance.new("TextButton")
OthersButton.Parent = Tabs
OthersButton.Text = "Others"
OthersButton.Size = UDim2.new(1, 0, 0.33, 0)
OthersButton.MouseButton1Click:Connect(function()
    OthersVisible = not OthersVisible
    OthersTab.Visible = OthersVisible
end)

local TrollButton = Instance.new("TextButton")
TrollButton.Parent = Tabs
TrollButton.Text = "Troll"
TrollButton.Size = UDim2.new(1, 0, 0.33, 0)
TrollButton.MouseButton1Click:Connect(function()
    TrollVisible = not TrollVisible
    TrollTab.Visible = TrollVisible
end)

local PlayerButton = Instance.new("TextButton")
PlayerButton.Parent = Tabs
PlayerButton.Text = "Player"
PlayerButton.Size = UDim2.new(1, 0, 0.33, 0)
PlayerButton.MouseButton1Click:Connect(function()
    PlayerTab.Visible = not PlayerTab.Visible
end)

-- Aba Others - Fly GUI com barra de velocidade
local FlySpeedBox = Instance.new("TextBox")
FlySpeedBox.Parent = OthersTab
FlySpeedBox.PlaceholderText = "Velocidade do Fly"
FlySpeedBox.Size = UDim2.new(0.8, 0, 0.2, 0)
FlySpeedBox.Position = UDim2.new(0.1, 0, 0.05, 0)

local FlyButton = Instance.new("TextButton")
FlyButton.Parent = OthersTab
FlyButton.Text = "Ativar Fly"
FlyButton.Size = UDim2.new(0.5, 0, 0.2, 0)
FlyButton.Position = UDim2.new(0.25, 0, 0.3, 0)

local flying = false
FlyButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    local speed = tonumber(FlySpeedBox.Text) or 50

    if flying then
        character.HumanoidRootPart.Anchored = false
        FlyButton.Text = "Ativar Fly"
    else
        character.HumanoidRootPart.Anchored = true
        FlyButton.Text = "Desativar Fly"
    end

    character.HumanoidRootPart.Velocity = Vector3.new(0, speed, 0)
    flying = not flying
end)

-- Aba Troll - Void Player e View Player com barra de nome
local PlayerNameBox = Instance.new("TextBox")
PlayerNameBox.Parent = TrollTab
PlayerNameBox.PlaceholderText = "Nome do Player"
PlayerNameBox.Size = UDim2.new(0.8, 0, 0.2, 0)
PlayerNameBox.Position = UDim2.new(0.1, 0, 0.05, 0)

local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollTab
VoidButton.Text = "Void Player"
VoidButton.Size = UDim2.new(0.5, 0, 0.2, 0)
VoidButton.Position = UDim2.new(0.25, 0, 0.3, 0)

VoidButton.MouseButton1Click:Connect(function()
    local target = game.Players:FindFirstChild(PlayerNameBox.Text)
    if target and target.Character then
        target.Character.HumanoidRootPart.CFrame = CFrame.new(0, -500, 0)
    end
end)

local ViewButton = Instance.new("TextButton")
ViewButton.Parent = TrollTab
ViewButton.Text = "View Player"
ViewButton.Size = UDim2.new(0.5, 0, 0.2, 0)
ViewButton.Position = UDim2.new(0.25, 0, 0.55, 0)

ViewButton.MouseButton1Click:Connect(function()
    local target = game.Players:FindFirstChild(PlayerNameBox.Text)
    if target and target.Character then
        game.Workspace.CurrentCamera.CameraSubject = target.Character.Humanoid
    end
end)

-- Aba Player - Boost Speed e Boost Jump
local SpeedButton = Instance.new("TextButton")
SpeedButton.Parent = PlayerTab
SpeedButton.Text = "Boost Speed"
SpeedButton.Size = UDim2.new(0.5, 0, 0.2, 0)
SpeedButton.Position = UDim2.new(0.25, 0, 0.1, 0)

SpeedButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    character.Humanoid.WalkSpeed = 50
end)

local JumpButton = Instance.new("TextButton")
JumpButton.Parent = PlayerTab
JumpButton.Text = "Boost Jump"
JumpButton.Size = UDim2.new(0.5, 0, 0.2, 0)
JumpButton.Position = UDim2.new(0.25, 0, 0.35, 0)

JumpButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    character.Humanoid.JumpPower = 100
end)
