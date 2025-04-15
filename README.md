local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "EmilliHub"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 700, 0, 400)
MainFrame.Position = UDim2.new(0.5, -350, 0.5, -200)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
MainFrame.BorderSizePixel = 0
MainFrame.Parent = ScreenGui

local UICornerMain = Instance.new("UICorner", MainFrame)
UICornerMain.CornerRadius = UDim.new(0, 8)

local Sidebar = Instance.new("Frame")
Sidebar.Size = UDim2.new(0, 180, 1, 0)
Sidebar.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
Sidebar.BorderSizePixel = 0
Sidebar.Parent = MainFrame

local Tabs = {
    "Info",
    "Scripts Trolls",
    "Troll Player",
    "Avatar",
    "Casa",
    "Audio All",
    "Lag Server FE",
    "Nomes"
}

local tabButtons = {}

for i, tab in pairs(Tabs) do
    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(1, 0, 0, 35)
    Button.Position = UDim2.new(0, 0, 0, (i - 1) * 40)
    Button.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
    Button.Text = tab
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Font = Enum.Font.GothamBold
    Button.TextSize = 14
    Button.Parent = Sidebar
    tabButtons[tab] = Button
end

-- Aba Troll Player
local TrollPlayerTab = Instance.new("Frame")
TrollPlayerTab.Size = UDim2.new(1, -180, 1, 0)
TrollPlayerTab.Position = UDim2.new(0, 180, 0, 0)
TrollPlayerTab.BackgroundTransparency = 1
TrollPlayerTab.Visible = true
TrollPlayerTab.Parent = MainFrame

local function createButton(name, callback)
    local Button = Instance.new("TextButton")
    Button.Size = UDim2.new(1, -40, 0, 40)
    Button.Position = UDim2.new(0, 20, 0, (#TrollPlayerTab:GetChildren()) * 45)
    Button.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
    Button.Font = Enum.Font.GothamBold
    Button.TextSize = 14
    Button.Text = name
    Button.Parent = TrollPlayerTab

    local UICorner = Instance.new("UICorner", Button)
    UICorner.CornerRadius = UDim.new(0, 6)

    Button.MouseButton1Click:Connect(callback)
end

-- Funções Troll Player
createButton("Fling Boat", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/FlingBoat"))()
end)

createButton("Disable Fling Boat", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/DisableFling"))()
end)

createButton("Kill All Bus", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/KillAllBus"))()
end)

createButton("House Ban kill All", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/HouseBanKill"))()
end)

createButton("Fling Boat all", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/FlingAllBoat"))()
end)

createButton("Bring all [melhor]", function()
    loadstring(game:HttpGet("https://pastebin.com/raw/BringAll"))()
end)
