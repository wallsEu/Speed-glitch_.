# Speed-glitch_.
Speed glitch only r15
-- // GUI
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "SpeedGlitchMobileGUI"
ScreenGui.ResetOnSpawn = false

local Frame = Instance.new("Frame", ScreenGui)
Frame.Size = UDim2.new(0, 260, 0, 170)
Frame.Position = UDim2.new(0.05, 0, 0.2, 0)
Frame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
Frame.BorderSizePixel = 0
Frame.Active = true
Frame.Draggable = true

local UIStroke = Instance.new("UIStroke", Frame)
UIStroke.Color = Color3.fromRGB(80, 80, 80)
UIStroke.Thickness = 1.2

local Title = Instance.new("TextLabel", Frame)
Title.Size = UDim2.new(1, 0, 0, 30)
Title.BackgroundTransparency = 1
Title.Text = "Speed Glitch R15 - Mobile"
Title.Font = Enum.Font.GothamBold
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 18

-- Toggle Button
local Toggle = Instance.new("TextButton", Frame)
Toggle.Size = UDim2.new(0.9, 0, 0, 35)
Toggle.Position = UDim2.new(0.05, 0, 0.25, 0)
Toggle.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
Toggle.Text = "🔘 Ativar Speed Glitch"
Toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
Toggle.Font = Enum.Font.GothamBold
Toggle.TextSize = 16

-- Intensidade Label
local SliderLabel = Instance.new("TextLabel", Frame)
SliderLabel.Size = UDim2.new(1, 0, 0, 20)
SliderLabel.Position = UDim2.new(0, 0, 0.55, 0)
SliderLabel.BackgroundTransparency = 1
SliderLabel.Text = "Intensidade: 50"
SliderLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
SliderLabel.Font = Enum.Font.Gotham
SliderLabel.TextSize = 14

-- Intensidade Input
local Slider = Instance.new("TextBox", Frame)
Slider.Size = UDim2.new(0.9, 0, 0, 30)
Slider.Position = UDim2.new(0.05, 0, 0.7, 0)
Slider.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
Slider.Text = "50"
Slider.TextColor3 = Color3.fromRGB(255, 255, 255)
Slider.Font = Enum.Font.Gotham
Slider.TextSize = 16
Slider.ClearTextOnFocus = false

-- // Variáveis
local running = false
local intensity = 50

-- Toggle Lógico
Toggle.MouseButton1Click:Connect(function()
    running = not running
    Toggle.Text = running and "✅ Desativar Speed Glitch" or "🔘 Ativar Speed Glitch"
    Toggle.BackgroundColor3 = running and Color3.fromRGB(70, 150, 70) or Color3.fromRGB(50, 50, 50)
end)

-- Intensidade Ajustável
Slider:GetPropertyChangedSignal("Text"):Connect(function()
    local val = tonumber(Slider.Text)
    if val and val >= 10 and val <= 300 then
        intensity = val
        SliderLabel.Text = "Intensidade: " .. tostring(val)
    end
end)

-- Loop do Glitch
task.spawn(function()
    while true do
        task.wait()
        if running then
            local plr = game.Players.LocalPlayer
            local char = plr.Character
            if char and char:FindFirstChild("Humanoid") and char:FindFirstChild("HumanoidRootPart") then
                local humanoid = char:FindFirstChild("Humanoid")
                local hrp = char:FindFirstChild("HumanoidRootPart")
                humanoid:ChangeState(Enum.HumanoidStateType.Physics)
                hrp.Velocity = hrp.CFrame.LookVector * (intensity / 5)
            end
        end
    end
end)
