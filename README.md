local player = game.Players.LocalPlayer

local playerGui = player:WaitForChild("PlayerGui")

local outfitGui = Instance.new("ScreenGui")
outfitGui.Name = "OutfitGui"
outfitGui.Parent = playerGui

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 300, 0, 200)
mainFrame.Position = UDim2.new(0.5, -150, 0.5, -100)
mainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
mainFrame.BackgroundTransparency = 0.5
mainFrame.BackgroundColor3 = Color3.new(0, 0, 0)
mainFrame.Parent = outfitGui

local outfitFrame = Instance.new("Frame")
outfitFrame.Size = UDim2.new(0, 120, 1, 0)
outfitFrame.Position = UDim2.new(0, 0, 0, 0)
outfitFrame.BackgroundTransparency = 1
outfitFrame.Parent = mainFrame

local previewFrame = Instance.new("Frame")
previewFrame.Size = UDim2.new(1, -120, 1, 0)
previewFrame.Position = UDim2.new(1, 0, 0, 0)
previewFrame.AnchorPoint = Vector2.new(1, 0)
previewFrame.BackgroundTransparency = 0.8
previewFrame.BackgroundColor3 = Color3.new(0, 0, 0)
previewFrame.Parent = mainFrame

local outfits = {
    {Name = "OUTFITNAME", ImageId = "rbxassetid://IMAGEID"},
    {Name = "OUTFITNAME", ImageId = "rbxassetid://IMAGEID"},
}

local buttonTemplate = Instance.new("TextButton")
buttonTemplate.Size = UDim2.new(1, 0, 0, 30)
buttonTemplate.AutoButtonColor = false
buttonTemplate.BackgroundColor3 = Color3.new(1, 1, 1)
buttonTemplate.Parent = outfitFrame

for _, outfitInfo in ipairs(outfits) do
    local outfitButton = buttonTemplate:Clone()
    outfitButton.Text = outfitInfo.Name
    outfitButton.Parent = outfitFrame

    local outfitImage = Instance.new("ImageLabel")
    outfitImage.Size = UDim2.new(1, 0, 1, -30)
    outfitImage.Position = UDim2.new(0, 0, 0, 30)
    outfitImage.Image = outfitInfo.ImageId
    outfitImage.BackgroundTransparency = 0.5
    outfitImage.BackgroundColor3 = Color3.new(1, 1, 1)
    outfitImage.Parent = previewFrame

    outfitButton.MouseButton1Click:Connect(function()
        for _, child in ipairs(previewFrame:GetChildren()) do
            if child:IsA("ImageLabel") then
            child:Destroy()
            end
        end

        local previewImage = outfitImage:Clone()
        previewImage.Parent = previewFrame

        print("Changing outfit to", outfitInfo.Name)
    end)
end
