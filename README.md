-- Funções Comuns
local function getHumanoid(player)
    local character = player.Character
    if character then
        return character:FindFirstChild("Humanoid")
    end
    return nil
end

local function createButton(text, position, onClick)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 280, 0, 40)
    button.Position = position
    button.Text = text
    button.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.GothamBold
    button.TextSize = 18
    button.Parent = mainFrame
    button.MouseButton1Click:Connect(onClick)
end

-- Funções Admin Commands
local function killPlayer(targetPlayer)
    local humanoid = getHumanoid(targetPlayer)
    if humanoid then
        humanoid.Health = 0
        print(targetPlayer.Name .. " foi morto!")
    end
end

local function godMode()
    local humanoid = getHumanoid(player)
    if humanoid then
        humanoid.MaxHealth = math.huge
        humanoid.Health = humanoid.MaxHealth
        print("Modo Deus ativado!")
    end
end

-- Funções Teleportação
local function teleportToPlayer(targetPlayer)
    local targetCharacter = targetPlayer.Character
    if targetCharacter then
        player.Character.HumanoidRootPart.CFrame = targetCharacter.HumanoidRootPart.CFrame
        print("Teleportado para " .. targetPlayer.Name)
    end
end

local function teleportToPosition(position)
    player.Character.HumanoidRootPart.CFrame = CFrame.new(position)
    print("Teleportado para a posição " .. tostring(position))
end

-- Funções Avançadas
local function setSpeed(speed)
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = speed
            print("Velocidade ajustada para " .. speed)
        end
    end
end

local function noClip()
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.PlatformStand = true  -- Ativa NoClip
            print("NoClip ativado!")
        end
    end
end

local function disableNoClip()
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.PlatformStand = false  -- Desativa NoClip
            print("NoClip desativado!")
        end
    end
end

-- Função Anti-Ban (Esqueleto, necessita de implementação específica)
local function antiBan()
    -- Aqui seria implementado o anti-ban conforme as suas necessidades.
    print("Anti-Ban ativado!")
end

-- Função para organizar os botões por categorias
local function createCategoryButtons()
    -- Categoria de Admin Commands
    createButton("Kill Player", UDim2.new(0, 10, 0, 60), function() killPlayer(player) end)
    createButton("God Mode", UDim2.new(0, 10, 0, 110), godMode)
    
    -- Categoria de Teleportação
    createButton("Teleport to Player", UDim2.new(0, 10, 0, 160), function() teleportToPlayer(player) end)
    createButton("Teleport to Position", UDim2.new(0, 10, 0, 210), function() teleportToPosition(Vector3.new(0, 0, 0)) end)  -- Exemplo de posição

    -- Categoria de Funções Avançadas
    createButton("Set Speed", UDim2.new(0, 10, 0, 260), function() setSpeed(50) end)  -- Exemplo de speed
    createButton("NoClip", UDim2.new(0, 10, 0, 310), noClip)
    createButton("Disable NoClip", UDim2.new(0, 10, 0, 360), disableNoClip)

    -- Categoria Anti-Ban e Outras
    createButton("Anti-Ban", UDim2.new(0, 10, 0, 410), antiBan)
end

-- Criando o botão de fechar
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 280, 0, 40)
closeButton.Position = UDim2.new(0, 10, 0, 460)
closeButton.Text = "Fechar"
closeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 18
closeButton.Parent = mainFrame

closeButton.MouseButton1Click:Connect(function()
    mainFrame.Visible = false
    print("Hub fechado!")
end)

-- Criação da interface
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 400)  -- Ajuste do tamanho da interface
mainFrame.Position = UDim2.new(0, 0, 0, 0)  -- Posição da interface
mainFrame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)  -- Fundo preto
mainFrame.Visible = true
mainFrame.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

-- Chamar a função para criar os botões
createCategoryButtons()
