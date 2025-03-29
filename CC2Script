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
uiFrame.Size = UDim2.new(0, 400, 0, 350)
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
frontCamberTextBox.PlaceholderText = "Ângulo Dianteiro"
frontCamberTextBox.Parent = uiFrame

-- Criar TextBox para modificar a inclinação das rodas traseiras
local rearCamberTextBox = Instance.new("TextBox")
rearCamberTextBox.Size = UDim2.new(0, 100, 0, 30)
rearCamberTextBox.Position = UDim2.new(0.6, 0, 0.15, 0)
rearCamberTextBox.BackgroundColor3 = Color3.fromRGB(100, 100, 100)
rearCamberTextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
rearCamberTextBox.PlaceholderText = "Ângulo Traseiro"
rearCamberTextBox.Parent = uiFrame

-- Criar TextBox para modificar o FreeLength dianteiro
local frontFreeLengthTextBox = Instance.new("TextBox")
frontFreeLengthTextBox.Size = UDim2.new(0, 100, 0, 30)
frontFreeLengthTextBox.Position = UDim2.new(0.1, 0, 0.25, 0)
frontFreeLengthTextBox.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
frontFreeLengthTextBox.Text = "Length Dianteiro"
frontFreeLengthTextBox.ClearTextOnFocus = false
frontFreeLengthTextBox.Parent = uiFrame

-- Criar TextBox para modificar o FreeLength traseiro
local rearFreeLengthTextBox = Instance.new("TextBox")
rearFreeLengthTextBox.Size = UDim2.new(0, 100, 0, 30)
rearFreeLengthTextBox.Position = UDim2.new(0.6, 0, 0.25, 0)
rearFreeLengthTextBox.BackgroundColor3 = Color3.fromRGB(200, 200, 200)
rearFreeLengthTextBox.Text = "Length Traseiro"
rearFreeLengthTextBox.ClearTextOnFocus = false
rearFreeLengthTextBox.Parent = uiFrame

-- Criar botão para aplicar mudanças (único botão para ambos Cambagem e FreeLength)
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

-- Função para alterar a cambagem e o FreeLength das rodas
local function applyChanges()
	-- Obter valores de Cambagem
	local frontCamber = tonumber(frontCamberTextBox.Text) or 0
	local rearCamber = tonumber(rearCamberTextBox.Text) or 0
	
	-- Obter valores de FreeLength
	local frontFreeLength = tonumber(frontFreeLengthTextBox.Text) or 0
	local rearFreeLength = tonumber(rearFreeLengthTextBox.Text) or 0
	
	-- Localizar a coleção de carros no workspace
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

					-- Alterar Cambagem
					for _, wheelName in pairs(frontWheels) do
						local wheel = wheels:FindFirstChild(wheelName)
						if wheel then
							local constraint = wheel:FindFirstChild("CylindricalConstraint")
							if constraint then
								constraint.InclinationAngle = frontCamber
							end
						end
					end
					for _, wheelName in pairs(rearWheels) do
						local wheel = wheels:FindFirstChild(wheelName)
						if wheel then
							local constraint = wheel:FindFirstChild("CylindricalConstraint")
							if constraint then
								constraint.InclinationAngle = rearCamber
							end
						end
					end

					-- Alterar FreeLength
					for _, wheelName in pairs(frontWheels) do
						local wheel = wheels:FindFirstChild(wheelName)
						if wheel then
							local spring = wheel:FindFirstChild("SpringConstraint")
							if spring then
								spring.FreeLength = frontFreeLength
							end
						end
					end
					for _, wheelName in pairs(rearWheels) do
						local wheel = wheels:FindFirstChild(wheelName)
						if wheel then
							local spring = wheel:FindFirstChild("SpringConstraint")
							if spring then
								spring.FreeLength = rearFreeLength
							end
						end
					end
				end
			end
		end
	end
end

-- Conectar o botão "Aplicar" à função
applyButton.MouseButton1Click:Connect(applyChanges)
