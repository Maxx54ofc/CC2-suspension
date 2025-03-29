local Players = game:GetService("Players")
local player = Players.LocalPlayer
local playerGui = player:FindFirstChildOfClass("PlayerGui")
local workspace = game:GetService("Workspace")

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = playerGui

-- Criar Botão Principal
local mainButton = Instance.new("TextButton")
mainButton.Size = UDim2.new(0, 45, 0, 45)
mainButton.Position = UDim2.new(0.1, 0, 0.1, 0)
mainButton.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
mainButton.Text = "+"
mainButton.TextScaled = true
mainButton.Parent = screenGui
mainButton.Draggable = true
mainButton.Active = true
mainButton.Selectable = true

-- Criar Frame da Interface
local uiFrame = Instance.new("Frame")
uiFrame.Size = UDim2.new(0, 400, 0, 300)
uiFrame.Position = UDim2.new(0.1, 50, 0.1, 0)
uiFrame.BackgroundColor3 = Color3.fromRGB(70, 70, 70)
uiFrame.Visible = false
uiFrame.Active = true
uiFrame.Draggable = true
uiFrame.Parent = screenGui

-- Criar título para a seção dianteira
local frontLabel = Instance.new("TextLabel")
frontLabel.Size = UDim2.new(0, 100, 0, 30)
frontLabel.Position = UDim2.new(0.1, 0, 0.05, 0)
frontLabel.BackgroundTransparency = 1
frontLabel.Text = "Dianteira"
frontLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
frontLabel.TextScaled = true
frontLabel.Parent = uiFrame

-- Criar título para a seção traseira
local rearLabel = Instance.new("TextLabel")
rearLabel.Size = UDim2.new(0, 100, 0, 30)
rearLabel.Position = UDim2.new(0.6, 0, 0.05, 0)
rearLabel.BackgroundTransparency = 1
rearLabel.Text = "Traseira"
rearLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
rearLabel.TextScaled = true
rearLabel.Parent = uiFrame

-- Criar TextBox para modificar a inclinação das rodas dianteiras
local frontCamberTextBox = Instance.new("TextBox")
frontCamberTextBox.Size = UDim2.new(0, 100, 0, 30)
frontCamberTextBox.Position = UDim2.new(0.1, 0, 0.15, 0)
frontCamberTextBox.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
frontCamberTextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
frontCamberTextBox.PlaceholderText = "Ângulo"
frontCamberTextBox.Parent = uiFrame

-- Criar TextBox para modificar a inclinação das rodas traseiras
local rearCamberTextBox = Instance.new("TextBox")
rearCamberTextBox.Size = UDim2.new(0, 100, 0, 30)
rearCamberTextBox.Position = UDim2.new(0.6, 0, 0.15, 0)
rearCamberTextBox.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
rearCamberTextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
rearCamberTextBox.PlaceholderText = "Ângulo"
rearCamberTextBox.Parent = uiFrame

-- Criar botão para aplicar mudanças
local applyButton = Instance.new("TextButton")
applyButton.Size = UDim2.new(0, 150, 0, 40)
applyButton.Position = UDim2.new(0.5, -75, 0.7, 0)
applyButton.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
applyButton.Text = "Aplicar"
applyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
applyButton.TextScaled = true
applyButton.Parent = uiFrame

-- Alternar visibilidade ao clicar no botão
mainButton.MouseButton1Click:Connect(function()
    uiFrame.Visible = not uiFrame.Visible
    if uiFrame.Visible then
        mainButton.Text = "-"
    else
        mainButton.Text = "+"
    end
end)

-- Função para alterar a cambagem das rodas
local function changeCamber()
    local frontAngle = tonumber(frontCamberTextBox.Text) or 0
    local rearAngle = tonumber(rearCamberTextBox.Text) or 0
    local carCollection = workspace:FindFirstChild("CarCollection")
    if carCollection then
        local playerCar = carCollection:FindFirstChild(player.Name)
        if playerCar then
            local car = playerCar:FindFirstChild("Car")
            if car then
                local wheels = car:FindFirstChild("Wheels")
                if wheels then
                    local frontWheels = {"FR", "FL"}
                    local rearWheels = {"RL", "RR"}
                    for _, wheelName in pairs(frontWheels) do
                        local wheel = wheels:FindFirstChild(wheelName)
                        if wheel then
                            local constraint = wheel:FindFirstChild("CylindricalConstraint")
                            if constraint then
                                constraint.InclinationAngle = frontAngle
                            end
                        end
                    end
                    for _, wheelName in pairs(rearWheels) do
                        local wheel = wheels:FindFirstChild(wheelName)
                        if wheel then
                            local constraint = wheel:FindFirstChild("CylindricalConstraint")
                            if constraint then
                                constraint.InclinationAngle = rearAngle
                            end
                        end
                    end
                end
            end
        end
    end
end

-- Aplicar mudanças ao clicar no botão
applyButton.MouseButton1Click:Connect(changeCamber)
