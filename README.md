-- Espera o jogo carregar
if not game:IsLoaded() then game.Loaded:Wait() end

local CoreGui = game:GetService("CoreGui")
if CoreGui:FindFirstChild("EmilliHub") then CoreGui.EmilliHub:Destroy() end

local gui = Instance.new("ScreenGui")
gui.Name = "EmilliHub"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = CoreGui

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 400)
frame.Position = UDim2.new(0.5, -150, 0.5, -200)
frame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
frame.BorderSizePixel = 0
frame.Parent = gui

local frameCorner = Instance.new("UICorner", frame)
frameCorner.CornerRadius = UDim.new(0, 6)

-- Título
local titleBar = Instance.new("Frame")
titleBar.Size = UDim2.new(1, 0, 0, 40)
titleBar.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
titleBar.BorderSizePixel = 0
titleBar.Parent = frame

local titleCorner = Instance.new("UICorner", titleBar)
titleCorner.CornerRadius = UDim.new(0, 6)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -40, 1, 0)
title.Position = UDim2.new(0, 10, 0, 0)
title.BackgroundTransparency = 1
title.Text = "Emilli Hub"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.GothamBold
title.TextSize = 18
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = titleBar

-- Botão de fechar
local close = Instance.new("TextButton")
close.Size = UDim2.new(0, 30, 0, 30)
close.Position = UDim2.new(1, -35, 0, 5)
close.BackgroundColor3 = Color3.fromRGB(255, 70, 70)
close.Text = "X"
close.TextColor3 = Color3.new(1, 1, 1)
close.Font = Enum.Font.GothamBold
close.TextSize = 14
close.Parent = titleBar

local closeCorner = Instance.new("UICorner", close)
closeCorner.CornerRadius = UDim.new(1, 0)

close.MouseButton1Click:Connect(function()
	gui:Destroy()
end)

-- Menu lateral de categorias
local categoryMenu = Instance.new("Frame")
categoryMenu.Size = UDim2.new(0, 80, 1, -40)
categoryMenu.Position = UDim2.new(0, 0, 0, 40)
categoryMenu.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
categoryMenu.BorderSizePixel = 0
categoryMenu.Parent = frame

local menuCorner = Instance.new("UICorner", categoryMenu)
menuCorner.CornerRadius = UDim.new(0, 6)

-- Área de conteúdo
local content = Instance.new("Frame")
content.Size = UDim2.new(1, -80, 1, -40)
content.Position = UDim2.new(0, 80, 0, 40)
content.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
content.BorderSizePixel = 0
content.Parent = frame

local contentCorner = Instance.new("UICorner", content)
contentCorner.CornerRadius = UDim.new(0, 6)

local pages = {}

local function createPage(name)
	local page = Instance.new("ScrollingFrame")
	page.Size = UDim2.new(1, 0, 1, 0)
	page.CanvasSize = UDim2.new(0, 0, 0, 0)
	page.BackgroundTransparency = 1
	page.ScrollBarThickness = 5
	page.Visible = false
	page.Parent = content
	pages[name] = page
	return page
end

local function switchPage(name)
	for i, page in pairs(pages) do
		page.Visible = (i == name)
	end
end

local function createCategory(name)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(1, 0, 0, 30)
	btn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
	btn.Text = name
	btn.TextColor3 = Color3.new(1, 1, 1)
	btn.Font = Enum.Font.Gotham
	btn.TextSize = 14
	btn.Parent = categoryMenu

	local btnCorner = Instance.new("UICorner", btn)
	btnCorner.CornerRadius = UDim.new(0, 6)

	local page = createPage(name)

	btn.MouseButton1Click:Connect(function()
		switchPage(name)
	end)

	return page
end

-- Categorias
local flyPage = createCategory("Fly")
local playerPage = createCategory("Player")
local visualPage = createCategory("Visual")
local teleportPage = createCategory("TP")
local miscPage = createCategory("Outros")

-- Exibir primeira categoria
switchPage("Fly")

-- Exemplo de botão em uma página
local function createOption(page, name, callback)
	local btn = Instance.new("TextButton")
	btn.Size = UDim2.new(1, -10, 0, 30)
	btn.Position = UDim2.new(0, 5, 0, #page:GetChildren() * 35)
	btn.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
	btn.Text = name
	btn.TextColor3 = Color3.new(1, 1, 1)
	btn.Font = Enum.Font.Gotham
	btn.TextSize = 14
	btn.Parent = page
	page.CanvasSize = UDim2.new(0, 0, 0, #page:GetChildren() * 35)

	local btnCorner = Instance.new("UICorner", btn)
	btnCorner.CornerRadius = UDim.new(0, 6)

	btn.MouseButton1Click:Connect(callback)
end

-- Adiciona opções de exemplo
createOption(flyPage, "Ativar Fly", function()
	print("Fly ligado")
end)

createOption(playerPage, "Kill Player", function()
	print("Kill ativado")
end)

createOption(visualPage, "ESP Players", function()
	print("ESP ligado")
end)

createOption(teleportPage, "Ir para Hospital", function()
	print("Teleport para Hospital")
end)

createOption(miscPage, "Speed x2", function()
	print("Speed 2x")
end)
