local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer

local EmilliHub = Instance.new("ScreenGui", LocalPlayer:WaitForChild("PlayerGui"))
EmilliHub.Name = "EmilliHub"
EmilliHub.ResetOnSpawn = false

-- Main Frame
local MainFrame = Instance.new("Frame", EmilliHub)
MainFrame.Size = UDim2.new(0, 750, 0, 420)
MainFrame.Position = UDim2.new(0.5, -375, 0.5, -210)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BorderSizePixel = 0

Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 8)

-- Título
local Title = Instance.new("TextLabel", MainFrame)
Title.Size = UDim2.new(1, -40, 0, 40)
Title.Position = UDim2.new(0, 10, 0, 0)
Title.Text = "Brookhaven RP | Português"
Title.Font = Enum.Font.GothamBold
Title.TextSize = 18
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundTransparency = 1
Title.TextXAlignment = Enum.TextXAlignment.Left

-- Botões de fechar e minimizar
local CloseBtn = Instance.new("TextButton", MainFrame)
CloseBtn.Size = UDim2.new(0, 30, 0, 30)
CloseBtn.Position = UDim2.new(1, -35, 0, 5)
CloseBtn.Text = "X"
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 14
CloseBtn.BackgroundColor3 = Color3.fromRGB(40, 0, 0)
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.MouseButton1Click:Connect(function() EmilliHub:Destroy() end)

local MinimizeBtn = Instance.new("TextButton", MainFrame)
MinimizeBtn.Size = UDim2.new(0, 30, 0, 30)
MinimizeBtn.Position = UDim2.new(1, -70, 0, 5)
MinimizeBtn.Text = "-"
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.TextSize = 14
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
local minimized = false
MinimizeBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    MainFrame.Size = minimized and UDim2.new(0, 750, 0, 50) or UDim2.new(0, 750, 0, 420)
end)

-- Sidebar
local Sidebar = Instance.new("Frame", MainFrame)
Sidebar.Size = UDim2.new(0, 180, 1, -50)
Sidebar.Position = UDim2.new(0, 0, 0, 50)
Sidebar.BackgroundColor3 = Color3.fromRGB(15, 15, 15)

-- Tabs
local Tabs = {
    {"Info", "rbxassetid://7734093119"},
    {"Scripts Trolls", "rbxassetid://7734081304"},
    {"Troll Player", "rbxassetid://7733954764"},
    {"Avatar", "rbxassetid://7734083554"},
    {"Casa", "rbxassetid://7734089670"},
    {"Audio All", "rbxassetid://7734092889"},
    {"Lag Server FE", "rbxassetid://7734092291"},
    {"Nomes", "rbxassetid://7734091252"},
}

local tabFrames = {}

for i, tabData in ipairs(Tabs) do
    local name, icon = unpack(tabData)

    local Button = Instance.new("TextButton", Sidebar)
    Button.Size = UDim2.new(1, 0, 0, 40)
    Button.Position = UDim2.new(0, 0, 0, (i - 1) * 45)
    Button.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
    Button.Text = "     " .. name
    Button.Font = Enum.Font.Gotham
    Button.TextSize = 14
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.TextXAlignment = Enum.TextXAlignment.Left

    local Icon = Instance.new("ImageLabel", Button)
    Icon.Size = UDim2.new(0, 20, 0, 20)
    Icon.Position = UDim2.new(0, 10, 0.5, -10)
    Icon.BackgroundTransparency = 1
    Icon.Image = icon

    local tabFrame = Instance.new("ScrollingFrame", MainFrame)
    tabFrame.Position = UDim2.new(0, 190, 0, 50)
    tabFrame.Size = UDim2.new(1, -200, 1, -60)
    tabFrame.BackgroundTransparency = 1
    tabFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
    tabFrame.ScrollBarThickness = 4
    tabFrame.Visible = (name == "Troll Player")
    tabFrames[name] = tabFrame

    Button.MouseButton1Click:Connect(function()
        for tab, frame in pairs(tabFrames) do
            frame.Visible = (tab == name)
        end
    end)
end

-- Troll Player Buttons
local function createTrollBtn(parent, text, url)
    local Btn = Instance.new("TextButton", parent)
    Btn.Size = UDim2.new(1, -20, 0, 40)
    Btn.Position = UDim2.new(0, 10, 0, (#parent:GetChildren() - 1) * 45)
    Btn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    Btn.TextColor3 = Color3.fromRGB(255, 255, 255)
    Btn.Font = Enum.Font.GothamBold
    Btn.TextSize = 14
    Btn.Text = text

    local UIStroke = Instance.new("UIStroke", Btn)
    UIStroke.Color = Color3.fromRGB(255, 255, 255)
    UIStroke.Thickness = 1

    local Corner = Instance.new("UICorner", Btn)
    Corner.CornerRadius = UDim.new(0, 6)

    Btn.MouseButton1Click:Connect(function()
        loadstring(game:HttpGet(url))()
    end)

    parent.CanvasSize = UDim2.new(0, 0, 0, (#parent:GetChildren()) * 45)
end

local trollFrame = tabFrames["Troll Player"]

createTrollBtn(trollFrame, "Fling Boat", "https://pastebin.com/raw/FlingBoat")
createTrollBtn(trollFrame, "Disable Fling Boat", "https://pastebin.com/raw/DisableFling")
createTrollBtn(trollFrame, "Kill All Bus", "https://pastebin.com/raw/KillAllBus")
createTrollBtn(trollFrame, "House Ban kill All", "https://pastebin.com/raw/HouseBanKill")
createTrollBtn(trollFrame, "Fling Boat all", "https://pastebin.com/raw/FlingAllBoat")
createTrollBtn(trollFrame, "Bring all [melhor]", "https://pastebin.com/raw/BringAll")
