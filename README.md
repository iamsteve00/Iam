-- Emilli Hub - Estilo Chaos Hub com funções dos 4 hubs (Chaos, SanderX, Rael, Cartola) -- Tema: Preto, Branco e Vermelho | Layout: Abas Horizontais no Topo

local EmilliHub = Instance.new("ScreenGui") EmilliHub.Name = "EmilliHub" EmilliHub.ResetOnSpawn = false EmilliHub.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local MainFrame = Instance.new("Frame") MainFrame.Name = "MainFrame" MainFrame.Size = UDim2.new(0, 350, 0, 420) MainFrame.Position = UDim2.new(0.5, -175, 0.5, -210) MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20) MainFrame.BorderSizePixel = 0 MainFrame.Parent = EmilliHub

local UICorner = Instance.new("UICorner") UICorner.CornerRadius = UDim.new(0, 8) UICorner.Parent = MainFrame

local Title = Instance.new("TextLabel") Title.Size = UDim2.new(1, 0, 0, 40) Title.BackgroundTransparency = 1 Title.Text = "Emilli Hub" Title.TextColor3 = Color3.fromRGB(255, 0, 0) Title.Font = Enum.Font.GothamBold Title.TextSize = 24 Title.Parent = MainFrame

local TabsFrame = Instance.new("Frame") TabsFrame.Size = UDim2.new(1, 0, 0, 30) TabsFrame.Position = UDim2.new(0, 0, 0, 40) TabsFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30) TabsFrame.BorderSizePixel = 0 TabsFrame.Parent = MainFrame

local TabButtons = {} local Pages = {}

local function createTab(name) local tabButton = Instance.new("TextButton") tabButton.Size = UDim2.new(0, 70, 1, 0) tabButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40) tabButton.TextColor3 = Color3.fromRGB(255, 255, 255) tabButton.Font = Enum.Font.Gotham tabButton.TextSize = 14 tabButton.Text = name tabButton.Parent = TabsFrame

local page = Instance.new("Frame")
page.Size = UDim2.new(1, 0, 1, -70)
page.Position = UDim2.new(0, 0, 0, 70)
page.BackgroundTransparency = 1
page.Visible = false
page.Parent = MainFrame

TabButtons[#TabButtons + 1] = tabButton
Pages[#Pages + 1] = page

tabButton.MouseButton1Click:Connect(function()
    for i = 1, #Pages do
        Pages[i].Visible = false
        TabButtons[i].BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    end
    page.Visible = true
    tabButton.BackgroundColor3 = Color3.fromRGB(100, 0, 0)
end)

return page

end

local function createButton(parent, name, callback) local button = Instance.new("TextButton") button.Size = UDim2.new(1, -20, 0, 30) button.Position = UDim2.new(0, 10, 0, #parent:GetChildren() * 35) button.Text = name button.TextColor3 = Color3.fromRGB(255, 255, 255) button.BackgroundColor3 = Color3.fromRGB(45, 45, 45) button.BorderSizePixel = 0 button.Font = Enum.Font.Gotham button.TextSize = 14 button.Parent = parent button.MouseButton1Click:Connect(callback)

local corner = Instance.new("UICorner")
corner.CornerRadius = UDim.new(0, 4)
corner.Parent = button

end

-- Criando abas local tabNames = {"Movimento", "Jogadores", "Mapa", "Visual", "Diversão", "Extras"} local pagesByName = {}

for _, name in pairs(tabNames) do pagesByName[name] = createTab(name) end

-- MOVIMENTO createButton(pagesByName["Movimento"], "Fly", function() loadstring(game:HttpGet("https://pastebin.com/raw/5V9VwZ59"))() end)

createButton(pagesByName["Movimento"], "Speed", function() local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") if humanoid then humanoid.WalkSpeed = 100 end end)

createButton(pagesByName["Movimento"], "Super Jump", function() local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid") if humanoid then humanoid.JumpPower = 200 end end)

createButton(pagesByName["Movimento"], "No Clip", function() loadstring(game:HttpGet("https://pastebin.com/raw/FsJak1qR"))() end)

createButton(pagesByName["Movimento"], "Andar na Água", function() game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart").Anchored = false end)

-- JOGADORES local playerInput = Instance.new("TextBox") playerInput.Size = UDim2.new(1, -20, 0, 30) playerInput.Position = UDim2.new(0, 10, 0, 5) playerInput.PlaceholderText = "Nome do Jogador" playerInput.Text = "" playerInput.TextColor3 = Color3.fromRGB(255, 255, 255) playerInput.BackgroundColor3 = Color3.fromRGB(45, 45, 45) playerInput.Font = Enum.Font.Gotham playerInput.TextSize = 14 playerInput.Parent = pagesByName["Jogadores"]

createButton(pagesByName["Jogadores"], "Kill Player", function() local targetName = playerInput.Text local target = game.Workspace:FindFirstChild(targetName) if target and target:FindFirstChild("Humanoid") then target.Humanoid.Health = 0 end end)

createButton(pagesByName["Jogadores"], "Teleportar até Player", function() local targetName = playerInput.Text local target = game.Workspace:FindFirstChild(targetName) if target then game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = target:FindFirstChild("HumanoidRootPart").CFrame end end)

-- MAPA createButton(pagesByName["Mapa"], "Remover Portas", function() for _, obj in pairs(workspace:GetDescendants()) do if obj:IsA("Part") and obj.Name:lower():find("door") then obj:Destroy() end end end)

createButton(pagesByName["Mapa"], "Destravar Todas Casas", function() for _, house in pairs(workspace:GetChildren()) do if house:FindFirstChild("Lock") then house.Lock:Destroy() end end end)

createButton(pagesByName["Mapa"], "Iluminar o Mapa", function() game.Lighting.Brightness = 5 game.Lighting.ClockTime = 12 end)

createButton(pagesByName["Mapa"], "Teleporte para Spawn", function() game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(0, 10, 0)) end)

-- Mostrar primeira aba por padrão Pages[1].Visible = true TabButtons[1].BackgroundColor3 = Color3.fromRGB(100, 0, 0)

-- Botão de fechar local CloseButton = Instance.new("TextButton") CloseButton.Text = "X" CloseButton.Size = UDim2.new(0, 30, 0, 30) CloseButton.Position = UDim2.new(1, -35, 0, 5) CloseButton.BackgroundColor3 = Color3.fromRGB(150, 0, 0) CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255) CloseButton.Font = Enum.Font.GothamBold CloseButton.TextSize = 18 CloseButton.Parent = MainFrame CloseButton.MouseButton1Click:Connect(function() EmilliHub:Destroy() end)

print("Emilli Hub v2 carregado com visual Chaos + funções dos 4 hubs!")

