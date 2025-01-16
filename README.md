local player = game.Players.LocalPlayer -- Identifica o jogador local
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

-- Criação da BillboardGui
local billboardGui = Instance.new("BillboardGui")
billboardGui.Adornee = humanoidRootPart
billboardGui.Size = UDim2.new(10, 0, 10, 0) -- Tamanho inicial
billboardGui.StudsOffset = Vector3.new(0, 5, 0) -- Posição acima do jogador
billboardGui.Parent = character

-- Adicionando uma imagem ao BillboardGui
local imageLabel = Instance.new("ImageLabel")
imageLabel.Image = "rbxassetid://ID_DA_IMAGEM" -- Substitua pelo ID da sua imagem
imageLabel.Size = UDim2.new(1, 0, 1, 0)
imageLabel.BackgroundTransparency = 1
imageLabel.Parent = billboardGui

-- Função para ajustar o tamanho da imagem com base na distância
local function adjustSize()
    local camera = workspace.CurrentCamera
    local distance = (camera.CFrame.Position - humanoidRootPart.Position).Magnitude
    local newSize = math.clamp(distance / 10, 5, 50) -- Ajusta o tamanho entre 5 e 50
    billboardGui.Size = UDim2.new(newSize, 0, newSize, 0)
end

-- Atualizar o tamanho continuamente
game:GetService("RunService").RenderStepped:Connect(adjustSize)
