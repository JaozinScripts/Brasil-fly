local UserInputService = game:GetService("UserInputService")

-- Função para ativar/desativar o voo
local function toggleFly()
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoid = character:FindFirstChildOfClass("Humanoid")
    
    if humanoid then
        humanoid.PlatformStand = not humanoid.PlatformStand
    end
end

-- Criar o botão na tela
local screenGui = Instance.new("ScreenGui")
local flyButton = Instance.new("TextButton")

screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
flyButton.Parent = screenGui

flyButton.Size = UDim2.new(0, 200, 0, 50)
flyButton.Position = UDim2.new(0.5, -100, 0.5, -25)
flyButton.Text = "e pra voar auqi rs"
flyButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0) -- Cor de fundo preta
flyButton.TextColor3 = Color3.fromRGB(255, 255, 255) -- Cor do texto branca
flyButton.Font = Enum.Font.SourceSans
flyButton.TextSize = 24

-- Adicionar uma borda branca ao botão
flyButton.BorderSizePixel = 2
flyButton.BorderColor3 = Color3.fromRGB(255, 255, 255) -- Cor da borda branca

-- Conectar a função ao evento de clique do botão
flyButton.MouseButton1Click:Connect(toggleFly)

-- Detectar toques na tela para dispositivos móveis
UserInputService.TouchTap:Connect(function(touchPositions)
    for _, touch in ipairs(touchPositions) do
        if flyButton.AbsolutePosition.X <= touch.X and touch.X <= flyButton.AbsolutePosition.X + flyButton.AbsoluteSize.X and
           flyButton.AbsolutePosition.Y <= touch.Y and touch.Y <= flyButton.AbsolutePosition.Y + flyButton.AbsoluteSize.Y then
            toggleFly()
        end
    end
end)
