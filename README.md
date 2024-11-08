local tool = Instance.new("Tool")
tool.Name = "MagnetTool"
tool.RequiresHandle = false
tool.Parent = game.Players.LocalPlayer.Backpack

local function unanchorParts()
    for _, part in ipairs(workspace:GetDescendants()) do
        if part:IsA("BasePart") and part.Anchored then
            part.Anchored = false
        end
    end
end

local function attractPartsToPosition(position)
    for _, part in ipairs(workspace:GetDescendants()) do
        if part:IsA("BasePart") and (part.Position - position).magnitude < 50 then
            local bodyPosition = Instance.new("BodyPosition")
            bodyPosition.Position = position
            bodyPosition.MaxForce = Vector3.new(4000, 4000, 4000)
            bodyPosition.Parent = part
            game.Debris:AddItem(bodyPosition, 0.5)
        end
    end
end

tool.Activated:Connect(function()
    unanchorParts()
    local mouse = game.Players.LocalPlayer:GetMouse()
    attractPartsToPosition(mouse.Hit.p)
end)
