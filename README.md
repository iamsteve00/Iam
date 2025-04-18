 Estrutura inicial, message e setup de interface
-- Criar a tela principal local ScreenGui = Instance.new("ScreenGui") ScreenGui.Name = "EmilliHub" ScreenGui.ResetOnSpawn = false ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Global ScreenGui.Parent = game:GetService("Players").LocalPlayer:WaitForChild("PlayerGui")

-- Função de fade local function tweenFade(guiObject, goal, time) game:GetService("TweenService"):Create(guiObject, TweenInfo.new(time), goal):Play() end

-- Mensagem de boas-vindas com fade in/out local welcome = Instance.new("TextLabel") welcome.Name = "WelcomeMessage" welcome.Size = UDim2.new(1, 0, 1, 0) welcome.Position = UDim2.new(0, 0, 0, 0) welcome.BackgroundTransparency = 1 welcome.Text = "Bem-vindo ao Emilli Hub" welcome.TextColor3 = Color3.new(1, 1, 1) welcome.TextStrokeTransparency = 0.5 welcome.Font = Enum.Font.GothamBold welcome.TextScaled = true welcome.Parent = ScreenGui

welcome.TextTransparency = 1 wait(0.2) tweenFade(welcome, {TextTransparency = 0}, 1.5) wait(2) tweenFade(welcome, {TextTransparency = 1}, 1.5) wait(1) welcome:Destroy()

-- Container principal da interface local MainUI = Instance.new("Frame") MainUI.Name = "MainUI" MainUI.Size = UDim2.new(0, 600, 0, 400) MainUI.Position = UDim2.new(0.5, -300, 0.5, -200) MainUI.BackgroundColor3 = Color3.fromRGB(25, 25, 25) MainUI.BackgroundTransparency = 0.1 MainUI.BorderSizePixel = 0 MainUI.Visible = false MainUI.Parent = ScreenGui

-- Fade in da interface MainUI.BackgroundTransparency = 1 MainUI.Visible = true tweenFade(MainUI, {BackgroundTransparency = 0.1}, 1)

BARRA LATERAL COM ÍCONES DAS ABAS

-- Ícones para as abas (pode usar ID de imagens do Roblox)
local icons = {
    Troll = "rbxassetid://7734053495",
    Movimentacao = "rbxassetid://7734068323",
    Visual = "rbxassetid://7734070183",
    Admin = "rbxassetid://7734072953",
    Musica = "rbxassetid://7734074736",
    Config = "rbxassetid://7734076287"
}

-- Criação da Sidebar (barra lateral)
local Sidebar = Instance.new("Frame")
Sidebar.Name = "Sidebar"
Sidebar.Size = UDim2.new(0, 60, 1, 0)
Sidebar.Position = UDim2.new(0, 0, 0, 0)
Sidebar.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Sidebar.BorderSizePixel = 0
Sidebar.Parent = MainFrame

-- Criação dos botões de abas com ícones
local Abas = {"Troll", "Movimentacao", "Visual", "Admin", "Musica", "Config"}
local AbaButtons = {}

for i, nome in ipairs(Abas) do
    local botao = Instance.new("ImageButton")
    botao.Name = nome .. "Button"
    botao.Image = icons[nome]
    botao.Size = UDim2.new(0, 40, 0, 40)
    botao.Position = UDim2.new(0, 10, 0, (i - 1) * 50 + 10)
    botao.BackgroundTransparency = 1
    botao.Parent = Sidebar

    -- Hover effect
    botao.MouseEnter:Connect(function()
        botao.ImageColor3 = Color3.fromRGB(255, 0, 0)
    end)
    botao.MouseLeave:Connect(function()
        botao.ImageColor3 = Color3.fromRGB(255, 255, 255)
    end)

    AbaButtons[nome] = botao
end

-- Função para criar cada aba
local function CriarAba(nome)
    local aba = Instance.new("Frame")
    aba.Name = nome .. "Aba"
    aba.Size = UDim2.new(1, -60, 1, -40)
    aba.Position = UDim2.new(0, 60, 0, 40)
    aba.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    aba.Visible = false
    aba.Parent = MainFrame
    return aba
end

-- Criar as abas principais
local AbasFrames = {}
for _, nome in ipairs(Abas) do
    AbasFrames[nome] = CriarAba(nome)
end

-- Sistema de troca de abas
for nome, botao in pairs(AbaButtons) do
    botao.MouseButton1Click:Connect(function()
        for _, frame in pairs(AbasFrames) do
            frame.Visible = false
        end
        AbasFrames[nome].Visible = true
    end)
end

-- Tornar a aba Troll visível por padrão
AbasFrames["Troll"].Visible = true

FUNÇÕES DA ABA TROLL

local TrollAba = AbasFrames["Troll"]

-- Título da aba
local TituloTroll = Instance.new("TextLabel")
TituloTroll.Text = "Aba Troll"
TituloTroll.Font = Enum.Font.GothamBold
TituloTroll.TextSize = 20
TituloTroll.TextColor3 = Color3.fromRGB(255, 255, 255)
TituloTroll.BackgroundTransparency = 1
TituloTroll.Position = UDim2.new(0, 10, 0, 10)
TituloTroll.Size = UDim2.new(1, -20, 0, 30)
TituloTroll.TextXAlignment = Enum.TextXAlignment.Left
TituloTroll.Parent = TrollAba

-- Função de utilidade para criar botões
local function CriarBotao(nome, ordemY, callback)
	local botao = Instance.new("TextButton")
	botao.Text = nome
	botao.Size = UDim2.new(0, 180, 0, 30)
	botao.Position = UDim2.new(0, 10, 0, 50 + (ordemY * 40))
	botao.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	botao.TextColor3 = Color3.fromRGB(255, 255, 255)
	botao.Font = Enum.Font.Gotham
	botao.TextSize = 14
	botao.BorderSizePixel = 0
	botao.AutoButtonColor = true
	botao.Parent = TrollAba
	botao.MouseButton1Click:Connect(callback)
	return botao
end

-- Funções reais da aba Troll:

-- "Flingar todo mundo"
CriarBotao("Fling All", 0, function()
	for _, player in ipairs(game.Players:GetPlayers()) do
		if player ~= game.Players.LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
			local hrp = game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
			if hrp then
				hrp.CFrame = player.Character.HumanoidRootPart.CFrame + Vector3.new(0,5,0)
				wait(0.1)
				hrp.Velocity = Vector3.new(9999,9999,9999)
			end
		end
	end
end)

-- "Crashar o servidor (lag)"
CriarBotao("Crash Server", 1, function()
	for i = 1, 100 do
		local part = Instance.new("Part", workspace)
		part.Anchored = true
		part.Size = Vector3.new(999,1,999)
		part.Position = Vector3.new(0,i*2,0)
	end
end)

-- "Spamar mensagens"
CriarBotao("Spam Chat", 2, function()
	while true do
		game.ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer("Emilli Hub dominando!", "All")
		wait(0.5)
	end
end)

-- "Buggar personagens"
CriarBotao("Bug Player", 3, function()
	local target = game.Players:FindFirstChild(InputName.Text)
	if target and target.Character and target.Character:FindFirstChild("HumanoidRootPart") then
		local bug = Instance.new("Part", target.Character)
		bug.Anchored = true
		bug.Size = Vector3.new(20,20,20)
		bug.Position = target.Character.HumanoidRootPart.Position
	end
end)

-- Caixa de input para nome de player (usado por algumas funções)
InputName = Instance.new("TextBox")
InputName.Size = UDim2.new(0, 180, 0, 25)
InputName.Position = UDim2.new(0, 10, 0, 250)
InputName.PlaceholderText = "Nome do jogador"
InputName.Text = ""
InputName.Font = Enum.Font.Gotham
InputName.TextSize = 14
InputName.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
InputName.TextColor3 = Color3.fromRGB(255, 255, 255)
InputName.BorderSizePixel = 0
InputName.Parent = TrollAba-- PARTE 4: FUNÇÕES DA ABA MOVIMENTAÇÃO

local MovAba = AbasFrames["Movimentação"]

-- Título da aba
local TituloMov = Instance.new("TextLabel")
TituloMov.Text = "Aba Movimentação"
TituloMov.Font = Enum.Font.GothamBold
TituloMov.TextSize = 20
TituloMov.TextColor3 = Color3.fromRGB(255, 255, 255)
TituloMov.BackgroundTransparency = 1
TituloMov.Position = UDim2.new(0, 10, 0, 10)
TituloMov.Size = UDim2.new(1, -20, 0, 30)
TituloMov.TextXAlignment = Enum.TextXAlignment.Left
TituloMov.Parent = MovAba

-- Utilitário para criar botões
local function CriarBotaoMov(nome, ordemY, callback)
	local botao = Instance.new("TextButton")
	botao.Text = nome
	botao.Size = UDim2.new(0, 180, 0, 30)
	botao.Position = UDim2.new(0, 10, 0, 50 + (ordemY * 40))
	botao.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	botao.TextColor3 = Color3.fromRGB(255, 255, 255)
	botao.Font = Enum.Font.Gotham
	botao.TextSize = 14
	botao.BorderSizePixel = 0
	botao.AutoButtonColor = true
	botao.Parent = MovAba
	botao.MouseButton1Click:Connect(callback)
	return botao
end

-- Funções reais da aba Movimentação:

-- Ativar Fly
CriarBotaoMov("Ativar Fly", 0, function()
	local plr = game.Players.LocalPlayer
	local mouse = plr:GetMouse()
	local flying = true
	local torso = plr.Character:WaitForChild("HumanoidRootPart")
	local speed = 5
	local bodyGyro = Instance.new("BodyGyro",-- PARTE 5: ABA VISUAL

local VisualAba = AbasFrames["Visual"]

-- Título da aba
local TituloVisual = Instance.new("TextLabel")
TituloVisual.Text = "Aba Visual"
TituloVisual.Font = Enum.Font.GothamBold
TituloVisual.TextSize = 20
TituloVisual.TextColor3 = Color3.fromRGB(255, 255, 255)
TituloVisual.BackgroundTransparency = 1
TituloVisual.Position = UDim2.new(0, 10, 0, 10)
TituloVisual.Size = UDim2.new(1, -20, 0, 30)
TituloVisual.TextXAlignment = Enum.TextXAlignment.Left
TituloVisual.Parent = VisualAba

-- Função para criar botões da aba Visual
local function CriarBotaoVisual(nome, ordemY, callback)
	local botao = Instance.new("TextButton")
	botao.Text = nome
	botao.Size = UDim2.new(0, 180, 0, 30)
	botao.Position = UDim2.new(0, 10, 0, 50 + (ordemY * 40))
	botao.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	botao.TextColor3 = Color3.fromRGB(255, 255, 255)
	botao.Font = Enum.Font.Gotham
	botao.TextSize = 14
	botao.BorderSizePixel = 0
	botao.AutoButtonColor = true
	botao.Parent = VisualAba
	botao.MouseButton1Click:Connect(callback)
	return botao
end

-- Funções reais da aba Visual:

-- ESP (ver jogadores através das paredes)
CriarBotaoVisual("Ativar ESP", 0, function()
	for _, player in pairs(game.Players:GetPlayers()) do
		if player ~= game.Players.LocalPlayer then
			local espBox = Instance.new("BoxHandleAdornment")
			espBox.Size = Vector3.new(4, 5, 2)
			espBox.Color3 = Color3.new(1, 0, 0)
			espBox.Transparency = 0.5
			espBox.Adornee = player.Character and player.Character:FindFirstChild("HumanoidRootPart")
			espBox.AlwaysOnTop = true
			espBox.ZIndex = 5
			espBox.Parent = player.Character:FindFirstChild("HumanoidRootPart")
		end
	end
end)

-- Remover ESP
CriarBotaoVisual("Remover ESP", 1, function()
	for _, player in pairs(game.Players:GetPlayers()) do
		if player ~= game.Players.LocalPlayer and player.Character then
			local hrp = player.Character:FindFirstChild("HumanoidRootPart")
			if hrp then
				for _, adornment in pairs(hrp:GetChildren()) do
					if adornment:IsA("BoxHandleAdornment") then
						adornment:Destroy()
					end
				end
			end
		end
	end
end)

-- Altera o FOV (campo de visão)
CriarBotaoVisual("FOV 120", 2, function()
	game.Workspace.CurrentCamera.FieldOfView = 120
end)

CriarBotaoVisual("FOV 70 (Padrão)", 3, function()
	game.Workspace.CurrentCamera.FieldOfView = 70
end)

-- Modo noturno (estilo visual escuro)
CriarBotaoVisual("Modo Noturno", 4, function()
	game.Lighting.Brightness = 0
	game.Lighting.ClockTime = 0
	game.Lighting.FogEnd = 100
	game.Lighting.Ambient = Color3.fromRGB(0, 0, 0)
end)

-- Restaurar visual padrão
CriarBotaoVisual("Modo Padrão", 5, function()
	game.Lighting.Brightness = 2
	game.Lighting.ClockTime = 14
	game.Lighting.FogEnd = 100000
	game.Lighting.Ambient = Color3.fromRGB(128, 128, 128)
end) torso)
	local bodyVelocity = Instance.new("BodyVelocity", torso)
	bodyGyro.P = 9e4
	bodyGyro.maxTorque = Vector3.new(9e9, 9e9, 9e9)
	bodyGyro.cframe = torso.CFrame
	bodyVelocity.velocity = Vector3.new(0, 0, 0)
	bodyVelocity.maxForce = Vector3.new(9e9, 9e9, 9e9)

	mouse.KeyDown:Connect(function(key)
		if key == "w" then
			bodyVelocity.velocity = workspace.CurrentCamera.CFrame.lookVector * speed
		elseif key == "s" then
			bodyVelocity.velocity = -workspace.CurrentCamera.CFrame.lookVector * speed
		elseif key == "a" then
			bodyVelocity.velocity = -workspace.CurrentCamera.CFrame.rightVector * speed
		elseif key == "d" then
			bodyVelocity.velocity = workspace.CurrentCamera.CFrame.rightVector * speed
		elseif key == "q" then
			flying = false
			bodyGyro:Destroy()
			bodyVelocity:Destroy()
		end
	end)
end)

-- Aumentar velocidade
CriarBotaoMov("Speed x3", 1, function()
	local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.WalkSpeed = 48
	end
end)

-- Resetar velocidade
CriarBotaoMov("Reset Speed", 2, function()
	local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.WalkSpeed = 16
	end
end)

-- Super pulo
CriarBotaoMov("Super Jump", 3, function()
	local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.JumpPower = 150
	end
end)

-- Resetar pulo
CriarBotaoMov("Reset Jump", 4, function()
	local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.JumpPower = 50
	end
end)

 ABA ADMIN

local AdminAba = AbasFrames["Admin"]

-- Título
local TituloAdmin = Instance.new("TextLabel")
TituloAdmin.Text = "Comandos de Admin"
TituloAdmin.Font = Enum.Font.GothamBold
TituloAdmin.TextSize = 20
TituloAdmin.TextColor3 = Color3.fromRGB(255, 255, 255)
TituloAdmin.BackgroundTransparency = 1
TituloAdmin.Position = UDim2.new(0, 10, 0, 10)
TituloAdmin.Size = UDim2.new(1, -20, 0, 30)
TituloAdmin.TextXAlignment = Enum.TextXAlignment.Left
TituloAdmin.Parent = AdminAba

-- Input de nome
local InputNome = Instance.new("TextBox")
InputNome.PlaceholderText = "Nome do jogador"
InputNome.Size = UDim2.new(0, 180, 0, 30)
InputNome.Position = UDim2.new(0, 10, 0, 50)
InputNome.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
InputNome.TextColor3 = Color3.fromRGB(255, 255, 255)
InputNome.Font = Enum.Font.Gotham
InputNome.TextSize = 14
InputNome.ClearTextOnFocus = false
InputNome.Parent = AdminAba

local ordemY = 1

local function CriarBotaoAdmin(nome, callback)
	local botao = Instance.new("TextButton")
	botao.Text = nome
	botao.Size = UDim2.new(0, 180, 0, 30)
	botao.Position = UDim2.new(0, 10, 0, 50 + (ordemY * 40))
	botao.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	botao.TextColor3 = Color3.fromRGB(255, 255, 255)
	botao.Font = Enum.Font.Gotham
	botao.TextSize = 14
	botao.BorderSizePixel = 0
	botao.Parent = AdminAba
	botao.MouseButton1Click:Connect(callback)
	ordemY += 1
end

-- Kick
CriarBotaoAdmin("Kick Jogador", function()
	local nome = InputNome.Text
	for _, p in pairs(game.Players:GetPlayers()) do
		if string.lower(p.Name) == string.lower(nome) then
			p:Kick("Você foi expulso pelo Emilli Hub.")
		end
	end
end)

-- Respawn
CriarBotaoAdmin("Respawn Jogador", function()
	local nome = InputNome.Text
	for _, p in pairs(game.Players:GetPlayers()) do
		if string.lower(p.Name) == string.lower(nome) and p.Character then
			p.Character:BreakJoints()
		end
	end
end)

-- Trazer (Teleportar até você)
CriarBotaoAdmin("Trazer Jogador", function()
	local nome = InputNome.Text
	for _, p in pairs(game.Players:GetPlayers()) do
		if string.lower(p.Name) == string.lower(nome) and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
			p.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame + Vector3.new(3, 0, 0)
		end
	end
end)

-- Congelar
CriarBotaoAdmin("Congelar Jogador", function()
	local nome = InputNome.Text
	for _, p in pairs(game.Players:GetPlayers()) do
		if string.lower(p.Name) == string.lower(nome) and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
			p.Character.HumanoidRootPart.Anchored = true
		end
	end
end)

-- Descongelar
CriarBotaoAdmin("Descongelar Jogador", function()
	local nome = InputNome.Text
	for _, p in pairs(game.Players:GetPlayers()) do
		if string.lower(p.Name) == string.lower(nome) and p.Character and p.Character:FindFirstChild("HumanoidRootPart") then
			p.Character.HumanoidRootPart.Anchored = false
		end
	end
end)

-- Tornar invisível
CriarBotaoAdmin("Invisível", function()
	local char = game.Players.LocalPlayer.Character
	for _, p in pairs(char:GetDescendants()) do
		if p:IsA("BasePart") and p.Name ~= "HumanoidRootPart" then
			p.Transparency = 1
		end
	end
end)

-- Tornar visível
CriarBotaoAdmin("Visível", function()
	local char = game.Players.LocalPlayer.Character
	for _, p in pairs(char:GetDescendants()) do
		if p:IsA("BasePart") then
			p.Transparency = 0
		end
	end
end)

 ABA MÚSICA

local MusicaAba = AbasFrames["Música"]

-- Título
local TituloMusica = Instance.new("TextLabel")
TituloMusica.Text = "Reprodutor de Música"
TituloMusica.Font = Enum.Font.GothamBold
TituloMusica.TextSize = 20
TituloMusica.TextColor3 = Color3.fromRGB(255, 255, 255)
TituloMusica.BackgroundTransparency = 1
TituloMusica.Position = UDim2.new(0, 10, 0, 10)
TituloMusica.Size = UDim2.new(1, -20, 0, 30)
TituloMusica.TextXAlignment = Enum.TextXAlignment.Left
TituloMusica.Parent = MusicaAba

-- Input de ID da música
local InputID = Instance.new("TextBox")
InputID.PlaceholderText = "ID da Música"
InputID.Size = UDim2.new(0, 180, 0, 30)
InputID.Position = UDim2.new(0, 10, 0, 50)
InputID.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
InputID.TextColor3 = Color3.fromRGB(255, 255, 255)
InputID.Font = Enum.Font.Gotham
InputID.TextSize = 14
InputID.ClearTextOnFocus = false
InputID.Parent = MusicaAba

-- Som
local som = Instance.new("Sound")
som.Volume = 2
som.Name = "SomDoHub"
som.Looped = true
som.Parent = game:GetService("SoundService")

-- Botão de Tocar Música
local Tocar = Instance.new("TextButton")
Tocar.Text = "Tocar Música"
Tocar.Size = UDim2.new(0, 180, 0, 30)
Tocar.Position = UDim2.new(0, 10, 0, 90)
Tocar.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
Tocar.TextColor3 = Color3.fromRGB(255, 255, 255)
Tocar.Font = Enum.Font.Gotham
Tocar.TextSize = 14
Tocar.BorderSizePixel = 0
Tocar.Parent = MusicaAba

Tocar.MouseButton1Click:Connect(function()
	local id = InputID.Text
	if id and id ~= "" then
		pcall(function()
			som:Stop()
			som.SoundId = "rbxassetid://" .. id
			som:Play()
		end)
	end
end)

-- Botão de Parar Música
local Parar = Instance.new("TextButton")
Parar.Text = "Parar Música"
Parar.Size = UDim2.new(0, 180, 0, 30)
Parar.Position = UDim2.new(0, 10, 0, 130)
Parar.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
Parar.TextColor3 = Color3.fromRGB(255, 255, 255)
Parar.Font = Enum.Font.Gotham
Parar.TextSize = 14
Parar.BorderSizePixel = 0
Parar.Parent = MusicaAba

Parar.MouseButton1Click:Connect(function()
	som:Stop()
end)
