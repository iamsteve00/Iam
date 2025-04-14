
local TweenService = game:GetService("TweenService")
local UserInputService = game:GetService("UserInputService")

-- Creating the main interface
local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local MinimizedFrame = Instance.new("Frame") -- Square when minimized

ScreenGui.Name = "CustomScript"
ScreenGui.Parent = game.CoreGui

Frame.Name = "MainFrame"
Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.Size = UDim2.new(0, 300, 0, 200)
Frame.BackgroundTransparency = 1 -- Start invisible

-- Fade-in animation when opening the interface
local FadeInTween = TweenService:Create(Frame, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {BackgroundTransparency = 0})
FadeInTween:Play()

-- Creating the welcome message
local WelcomeText = Instance.new("TextLabel")
WelcomeText.Parent = ScreenGui
WelcomeText.Text = "Welcome to Emilli Hub"
WelcomeText.Size = UDim2.new(0, 250, 0, 40)
WelcomeText.Position = UDim2.new(0.5, -125, 0.3, 0)
WelcomeText.BackgroundTransparency = 1
WelcomeText.TextScaled = true
WelcomeText.TextColor3 = Color3.fromRGB(255, 255, 255)
WelcomeText.Font = Enum.Font.SourceSansBold
WelcomeText.TextTransparency = 1 -- Start invisible

-- Fade-in and scale animation for the welcome message
local WelcomeTween = TweenService:Create(WelcomeText, TweenInfo.new(1.2, Enum.EasingStyle.Quint, Enum.EasingDirection.Out), {TextTransparency = 0, Size = UDim2.new(0, 320, 0, 55)})
FadeInTween.Completed:Connect(function()
    task.wait(0.5) -- Short delay before showing the message
    WelcomeTween:Play()
end)

-- Message disappears after a few seconds
task.wait(4)
local FadeOut = TweenService:Create(WelcomeText, TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {TextTransparency = 1})
FadeOut:Play()

FadeOut.Completed:Connect(function()
    WelcomeText:Destroy()
end)

-- Close button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Text = "X"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 1, -35)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)

CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- Creating the minimized square
MinimizedFrame.Name = "MinimizedFrame"
MinimizedFrame.Parent = ScreenGui
MinimizedFrame.BackgroundColor3 = Color3.fromRGB(255, 182, 193)
MinimizedFrame.Size = UDim2.new(0, 50, 0, 50)
MinimizedFrame.Position = UDim2.new(0.5, -25, 0.5, -25)
MinimizedFrame.Visible = false

-- Minimize button
local MinimizeButton = Instance.new("TextButton")
MinimizeButton.Parent = Frame
MinimizeButton.Text = "-"
MinimizeButton.Size = UDim2.new(0, 30, 0, 30)
MinimizeButton.Position = UDim2.new(1, -70, 1, -35)
MinimizeButton.BackgroundColor3 = Color3.fromRGB(255, 255, 0)

MinimizeButton.MouseButton1Click:Connect(function()
    Frame.Visible = false
    MinimizedFrame.Visible = true
end)

-- Restore button inside the minimized square
local RestoreButton = Instance.new("TextButton")
RestoreButton.Parent = MinimizedFrame
RestoreButton.Text = "🔄"
RestoreButton.Size = UDim2.new(1, 0, 1, 0)
RestoreButton.BackgroundTransparency = 1

RestoreButton.MouseButton1Click:Connect(function()
    MinimizedFrame.Visible = false
    Frame.Visible = true
    Frame.BackgroundTransparency = 1
    FadeInTween:Play()
end)

-- Making the minimized square draggable
local dragging = false
local dragInput, dragStart, startPos

MinimizedFrame.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = MinimizedFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

MinimizedFrame.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        local newX = math.clamp(startPos.X.Offset + delta.X, 0, game:GetService("Workspace").CurrentCamera.ViewportSize.X - MinimizedFrame.Size.X.Offset)
        local newY = math.clamp(startPos.Y.Offset + delta.Y, 0, game:GetService("Workspace").CurrentCamera.ViewportSize.Y - MinimizedFrame.Size.Y.Offset)
        
        MinimizedFrame.Position = UDim2.new(startPos.X.Scale, newX, startPos.Y.Scale, newY)
    end
end)

-- Adding a glowing effect to the minimized square
local GlowTween = TweenService:Create(MinimizedFrame, TweenInfo.new(1, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out), {BackgroundColor3 = Color3.fromRGB(255, 150, 150)})

MinimizeButton.MouseButton1Click:Connect(function()
    GlowTween:Play()
end)
