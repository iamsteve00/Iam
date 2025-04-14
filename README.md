
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

-- Criando a interface principal
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -300, 0.5, -200) -- Ajustado para 2x maior
Frame.Size = UDim2.new(0, 600, 0, 400) -- Interface maior
Frame.BackgroundTransparency = 1 -- Começa invisível

-- Animação de fade-in ao abrir a interface
local FadeInTween = TweenService:Create(Frame, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 0})
FadeInTween:Play()

-- Criando a área das abas
local Tabs = Instance.new("Frame")
Tabs.Parent = Frame
Tabs.Size = UDim2.new(1, 0, 0, 50)
Tabs.Position = UDim2.new(0, 0, 0, -50)
Tabs.BackgroundColor3 = Color3.fromRGB(255, 150, 150)

-- Criando as abas
local OthersTab = Instance.new("Frame")
OthersTab.Parent = Frame
OthersTab.Size = UDim2.new(1, 0, 1, -50)
OthersTab.Position = UDim2.new(0, 0, 0, 50)
OthersTab.BackgroundColor3 = Color3.fromRGB(100, 100, 255)

local TrollTab = Instance.new("Frame")
TrollTab.Parent = Frame
TrollTab.Size = UDim2.new(1, 0, 1, -50)
TrollTab.Position = UDim2.new(0, 0, 0, 50)
TrollTab.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
TrollTab.Visible = false

local PlayerTab = Instance.new("Frame")
PlayerTab.Parent = Frame
PlayerTab.Size = UDim2.new(1, 0, 1, -50)
PlayerTab.Position = UDim2.new(0, 0, 0, 50)
PlayerTab.BackgroundColor3 = Color3.fromRGB(100, 255, 100)
PlayerTab.Visible = false

-- Criando botões para alternar entre abas
local OthersButton = Instance.new("TextButton")
OthersButton.Parent = Tabs
OthersButton.Text = "Others"
OthersButton.Size = UDim2.new(0.3, 0, 1, 0)
OthersButton.BackgroundColor3 = Color3.fromRGB(100, 100, 255)
OthersButton.MouseButton1Click:Connect(function()
    OthersTab.Visible = true
    TrollTab.Visible = false
    PlayerTab.Visible = false
end)

local TrollButton = Instance.new("TextButton")
TrollButton.Parent = Tabs
TrollButton.Text = "Troll"
TrollButton.Size = UDim2.new(0.3, 0, 1, 0)
TrollButton.Position = UDim2.new(0.3, 0, 0, 0)
TrollButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
TrollButton.MouseButton1Click:Connect(function()
    OthersTab.Visible = false
    TrollTab.Visible = true
    PlayerTab.Visible = false
end)

local PlayerButton = Instance.new("TextButton")
PlayerButton.Parent = Tabs
PlayerButton.Text = "Player"
PlayerButton.Size = UDim2.new(0.3, 0, 1, 0)
PlayerButton.Position = UDim2.new(0.6, 0, 0, 0)
PlayerButton.BackgroundColor3 = Color3.fromRGB(100, 255, 100)
PlayerButton.MouseButton1Click:Connect(function()
    OthersTab.Visible = false
    TrollTab.Visible = false
    PlayerTab.Visible = true
end)

-- Adicionando funcionalidades dentro das abas
-- Aba "Others" - Fly GUI
local FlyButton = Instance.new("TextButton")
FlyButton.Parent = OthersTab
FlyButton.Text = "Activate Fly"
FlyButton.Size = UDim2.new(0.5, 0, 0.2, 0)
FlyButton.Position = UDim2.new(0.25, 0, 0.1, 0)
FlyButton.BackgroundColor3 = Color3.fromRGB(50, 150, 255)

local flying = false
FlyButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    if flying then
        character.HumanoidRootPart.Anchored = false
        FlyButton.Text = "Activate Fly"
    else
        character.HumanoidRootPart.Anchored = true
        FlyButton.Text = "Deactivate Fly"
    end

    flying = not flying
end)

-- Aba "Troll" - Void Player e View Player
local VoidButton = Instance.new("TextButton")
VoidButton.Parent = TrollTab
VoidButton.Text = "Void Player"
VoidButton.Size = UDim2.new(0.5, 0, 0.2, 0)
VoidButton.Position = UDim2.new(0.25, 0, 0.1, 0)
VoidButton.BackgroundColor3 = Color3.fromRGB(255, 50, 50)

VoidButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    character.HumanoidRootPart.CFrame = CFrame.new(0, -500, 0) -- Envia o jogador para o void
end)

local ViewButton = Instance.new("TextButton")
ViewButton.Parent = TrollTab
ViewButton.Text = "View Player"
ViewButton.Size = UDim2.new(0.5, 0, 0.2, 0)
ViewButton.Position = UDim2.new(0.25, 0, 0.35, 0)
ViewButton.BackgroundColor3 = Color3.fromRGB(50, 255, 50)

ViewButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local targetPlayer = game.Players:GetPlayers()[math.random(#game.Players:GetPlayers())] -- Escolhe um jogador aleatório

    if targetPlayer and targetPlayer.Character then
        game.Workspace.CurrentCamera.CameraSubject = targetPlayer.Character.Humanoid -- Alterna a câmera para o alvo
    end
end)

-- Aba "Player" - Boost Speed e Jump
local SpeedButton = Instance.new("TextButton")
SpeedButton.Parent = PlayerTab
SpeedButton.Text = "Boost Speed"
SpeedButton.Size = UDim2.new(0.5, 0, 0.2, 0)
SpeedButton.Position = UDim2.new(0.25, 0, 0.1, 0)
SpeedButton.BackgroundColor3 = Color3.fromRGB(50, 255, 50)

SpeedButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    character.Humanoid.WalkSpeed = 50 -- Aumenta a velocidade do jogador
end)

local JumpButton = Instance.new("TextButton")
JumpButton.Parent = PlayerTab
JumpButton.Text = "Boost Jump"
JumpButton.Size = UDim2.new(0.5, 0, 0.2, 0)
JumpButton.Position = UDim2.new(0.25, 0, 0.35, 0)
JumpButton.BackgroundColor3 = Color3.fromRGB(255, 255, 50)

JumpButton.MouseButton1Click:Connect(function()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    character.Humanoid.JumpPower = 100 -- Aumenta a altura do salto
end)
