-- Garantir que estamos dentro do jogo
if not game:IsLoaded() then
    game.Loaded:Wait()
end

-- Variáveis
local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
gui.Name = "EmilliHub"

-- Frame principal
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 400)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -200)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = gui

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 40)
title.Position = UDim2.new(0, 0, 0, 0)
title.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
title.Text = "Emilli Hub"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 20
title.Parent = mainFrame

-- Exemplo de botão
local function createButton(text, yPos, callback)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(1, -20, 0, 40)
    btn.Position = UDim2.new(0, 10, 0, yPos)
    btn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 16
    btn.Text = text
    btn.Parent = mainFrame
    btn.MouseButton1Click:Connect(callback)
end

-- Botões de exemplo
createButton("Fly GUI", 60, function()
    print("Fly GUI ativado")
end)

createButton("Kill Player", 110, function()
    print("Kill Player ativado")
end)

createButton("Speed", 160, function()
    print("Speed ativado")
end)

createButton("Admin Commands", 210, function()
    print("Admin Commands ativado")
end)

createButton("Teleport", 260, function()
    print("Teleport ativado")
end)

-- Botão de fechar
createButton("Fechar Hub", 310, function()
    gui:Destroy()
end)
