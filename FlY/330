local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local CoreGui = game:GetService("CoreGui")
local UserInputService = game:GetService("UserInputService")

local player = Players.LocalPlayer
local camera = workspace.CurrentCamera

local controls = nil
pcall(function()
    local PlayerModule = require(player.PlayerScripts:WaitForChild("PlayerModule"))
    controls = PlayerModule:GetControls()
end)

local flying = false
local speed = 330
local bv = nil
local bg = nil
local holdingUp = false
local holdingDown = false
local heartbeatConn = nil

local screenGui = Instance.new("ScreenGui")
screenGui.Name = "mzher-hub"
screenGui.ResetOnSpawn = false
screenGui.Parent = CoreGui

local holder = Instance.new("Frame")
holder.Size = UDim2.new(0, 215, 0, 110)
holder.Position = UDim2.new(0.08, 0, 0.25, 0)
holder.BackgroundTransparency = 1
holder.Active = true
holder.Draggable = true
holder.Parent = screenGui

local btnClose = Instance.new("TextButton")
btnClose.Size = UDim2.new(0, 36, 0, 22)
btnClose.Position = UDim2.new(0, 0, 0, 0)
btnClose.BackgroundColor3 = Color3.fromRGB(180, 20, 20)
btnClose.BorderSizePixel = 0
btnClose.Text = "X"
btnClose.TextColor3 = Color3.fromRGB(255, 255, 255)
btnClose.TextSize = 16
btnClose.Font = Enum.Font.SourceSansBold
btnClose.Parent = holder

local closeCorner = Instance.new("UICorner")
closeCorner.CornerRadius = UDim.new(0, 6)
closeCorner.Parent = btnClose

local btnMin = Instance.new("TextButton")
btnMin.Size = UDim2.new(0, 36, 0, 22)
btnMin.Position = UDim2.new(0, 40, 0, 0)
btnMin.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
btnMin.BorderSizePixel = 0
btnMin.Text = "-"
btnMin.TextColor3 = Color3.fromRGB(255, 255, 255)
btnMin.TextSize = 18
btnMin.Font = Enum.Font.SourceSansBold
btnMin.Parent = holder

local minCorner = Instance.new("UICorner")
minCorner.CornerRadius = UDim.new(0, 6)
minCorner.Parent = btnMin

local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 215, 0, 75)
mainFrame.Position = UDim2.new(0, 0, 0, 26)
mainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
mainFrame.BorderSizePixel = 0
mainFrame.Parent = holder

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0, 8)
mainCorner.Parent = mainFrame

local rainbowStroke = Instance.new("UIStroke")
rainbowStroke.Thickness = 2
rainbowStroke.Parent = mainFrame

local rainbowGradient = Instance.new("UIGradient")
rainbowGradient.Color = ColorSequence.new({
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 0, 0)),
    ColorSequenceKeypoint.new(0.17, Color3.fromRGB(255, 127, 0)),
    ColorSequenceKeypoint.new(0.33, Color3.fromRGB(255, 255, 0)),
    ColorSequenceKeypoint.new(0.5, Color3.fromRGB(0, 255, 0)),
    ColorSequenceKeypoint.new(0.67, Color3.fromRGB(0, 150, 255)),
    ColorSequenceKeypoint.new(0.83, Color3.fromRGB(139, 0, 255)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 0, 0))
})
rainbowGradient.Parent = rainbowStroke

task.spawn(function()
    while task.wait(0.03) do
        if rainbowGradient and rainbowGradient.Parent then
            rainbowGradient.Rotation = (rainbowGradient.Rotation + 3) % 360
        end
    end
end)

local btnUp = Instance.new("TextButton")
btnUp.Size = UDim2.new(0, 44, 0, 26)
btnUp.Position = UDim2.new(0, 6, 0, 8)
btnUp.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
btnUp.BorderSizePixel = 0
btnUp.Text = "UP"
btnUp.TextColor3 = Color3.fromRGB(255, 255, 255)
btnUp.TextSize = 13
btnUp.Font = Enum.Font.SourceSans
btnUp.Parent = mainFrame

local upCorner = Instance.new("UICorner")
upCorner.CornerRadius = UDim.new(0, 6)
upCorner.Parent = btnUp

local btnSpeedPlus = Instance.new("TextButton")
btnSpeedPlus.Size = UDim2.new(0, 32, 0, 26)
btnSpeedPlus.Position = UDim2.new(0, 54, 0, 8)
btnSpeedPlus.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
btnSpeedPlus.BorderSizePixel = 0
btnSpeedPlus.Text = "+"
btnSpeedPlus.TextColor3 = Color3.fromRGB(255, 255, 255)
btnSpeedPlus.TextSize = 16
btnSpeedPlus.Font = Enum.Font.SourceSansBold
btnSpeedPlus.Parent = mainFrame

local spCorner = Instance.new("UICorner")
spCorner.CornerRadius = UDim.new(0, 6)
spCorner.Parent = btnSpeedPlus

local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(0, 120, 0, 26)
titleLabel.Position = UDim2.new(0, 90, 0, 8)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "mzher-hub"
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.TextSize = 15
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.TextXAlignment = Enum.TextXAlignment.Center
titleLabel.Parent = mainFrame

local btnDown = Instance.new("TextButton")
btnDown.Size = UDim2.new(0, 44, 0, 26)
btnDown.Position = UDim2.new(0, 6, 0, 40)
btnDown.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
btnDown.BorderSizePixel = 0
btnDown.Text = "DOWN"
btnDown.TextColor3 = Color3.fromRGB(255, 255, 255)
btnDown.TextSize = 13
btnDown.Font = Enum.Font.SourceSans
btnDown.Parent = mainFrame

local downCorner = Instance.new("UICorner")
downCorner.CornerRadius = UDim.new(0, 6)
downCorner.Parent = btnDown

local btnSpeedMinus = Instance.new("TextButton")
btnSpeedMinus.Size = UDim2.new(0, 32, 0, 26)
btnSpeedMinus.Position = UDim2.new(0, 54, 0, 40)
btnSpeedMinus.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
btnSpeedMinus.BorderSizePixel = 0
btnSpeedMinus.Text = "-"
btnSpeedMinus.TextColor3 = Color3.fromRGB(255, 255, 255)
btnSpeedMinus.TextSize = 16
btnSpeedMinus.Font = Enum.Font.SourceSansBold
btnSpeedMinus.Parent = mainFrame

local smCorner = Instance.new("UICorner")
smCorner.CornerRadius = UDim.new(0, 6)
smCorner.Parent = btnSpeedMinus

local speedBox = Instance.new("TextBox")
speedBox.Size = UDim2.new(0, 50, 0, 26)
speedBox.Position = UDim2.new(0, 90, 0, 40)
speedBox.BackgroundTransparency = 1
speedBox.Text = tostring(speed)
speedBox.TextColor3 = Color3.fromRGB(255, 255, 255)
speedBox.TextSize = 16
speedBox.Font = Enum.Font.SourceSansBold
speedBox.Parent = mainFrame

local btnFly = Instance.new("TextButton")
btnFly.Size = UDim2.new(0, 65, 0, 26)
btnFly.Position = UDim2.new(0, 144, 0, 40)
btnFly.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
btnFly.BorderSizePixel = 0
btnFly.Text = "fly"
btnFly.TextColor3 = Color3.fromRGB(255, 255, 255)
btnFly.TextSize = 14
btnFly.Font = Enum.Font.SourceSansBold
btnFly.Parent = mainFrame

local flyCorner = Instance.new("UICorner")
flyCorner.CornerRadius = UDim.new(0, 6)
flyCorner.Parent = btnFly

local function setupHold(button, callback)
    button.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            callback(true)
        end
    end)
    button.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            callback(false)
        end
    end)
end

setupHold(btnUp, function(val) holdingUp = val end)
setupHold(btnDown, function(val) holdingDown = val end)

btnSpeedPlus.MouseButton1Click:Connect(function()
    speed = speed + 10
    speedBox.Text = tostring(speed)
end)

btnSpeedMinus.MouseButton1Click:Connect(function()
    speed = math.max(1, speed - 10)
    speedBox.Text = tostring(speed)
end)

speedBox.FocusLost:Connect(function()
    local val = tonumber(speedBox.Text)
    if val then
        speed = val
    else
        speedBox.Text = tostring(speed)
    end
end)

btnMin.MouseButton1Click:Connect(function()
    mainFrame.Visible = not mainFrame.Visible
end)

local function stopFly()
    flying = false
    btnFly.TextColor3 = Color3.fromRGB(255, 255, 255)

    if heartbeatConn then
        heartbeatConn:Disconnect()
        heartbeatConn = nil
    end

    local char = player.Character
    if char then
        local hum = char:FindFirstChildOfClass("Humanoid")
        if hum then
            hum.PlatformStand = false
            hum:SetStateEnabled(Enum.HumanoidStateType.Running, true)
            hum:SetStateEnabled(Enum.HumanoidStateType.Landed, true)
            hum:SetStateEnabled(Enum.HumanoidStateType.GettingUp, true)
            hum:ChangeState(Enum.HumanoidStateType.GettingUp)
        end
        local anim = char:FindFirstChild("Animate")
        if anim then
            anim.Enabled = true
        end
        local root = char:FindFirstChild("HumanoidRootPart")
        if root then
            root.AssemblyLinearVelocity = Vector3.zero
            root.AssemblyAngularVelocity = Vector3.zero
        end
    end

    if bv then bv:Destroy() bv = nil end
    if bg then bg:Destroy() bg = nil end
end

local function startFly()
    local char = player.Character
    if not char then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not root or not hum then return end

    if bv then bv:Destroy() end
    if bg then bg:Destroy() end

    hum.PlatformStand = true

    local anim = char:FindFirstChild("Animate")
    if anim then
        anim.Enabled = false
    end
    for _, track in ipairs(hum:GetPlayingAnimationTracks()) do
        track:Stop(0)
    end

    bv = Instance.new("BodyVelocity")
    bv.Name = "mzher_bv"
    bv.MaxForce = Vector3.new(1e9, 1e9, 1e9)
    bv.Velocity = Vector3.zero
    bv.P = 1e5
    bv.Parent = root

    bg = Instance.new("BodyGyro")
    bg.Name = "mzher_bg"
    bg.MaxTorque = Vector3.new(1e9, 1e9, 1e9)
    bg.P = 1e5
    bg.D = 1000
    bg.CFrame = camera.CFrame
    bg.Parent = root

    flying = true
    btnFly.TextColor3 = Color3.fromRGB(0, 255, 120)

    heartbeatConn = RunService.Heartbeat:Connect(function()
        if not flying then return end
        local c = player.Character
        if not c then return end
        local r = c:FindFirstChild("HumanoidRootPart")
        local h = c:FindFirstChildOfClass("Humanoid")
        if not r or not h or not bv or not bg then return end

        h.PlatformStand = true

        for _, obj in ipairs(c:GetDescendants()) do
            if (obj:IsA("BodyVelocity") or obj:IsA("BodyPosition") or obj:IsA("LinearVelocity") or obj:IsA("VectorForce")) and obj ~= bv and obj ~= bg then
                pcall(function() obj:Destroy() end)
            end
        end

        local camCFrame = camera.CFrame
        local look = camCFrame.LookVector
        local right = camCFrame.RightVector
        local moveDir = Vector3.zero

        local rawMove = Vector3.zero
        if controls then
            pcall(function()
                rawMove = controls:GetMoveVector()
            end)
        end

        local forward = -rawMove.Z
        local strafe = rawMove.X

        if UserInputService:IsKeyDown(Enum.KeyCode.W) then forward = forward + 1 end
        if UserInputService:IsKeyDown(Enum.KeyCode.S) then forward = forward - 1 end
        if UserInputService:IsKeyDown(Enum.KeyCode.D) then strafe = strafe + 1 end
        if UserInputService:IsKeyDown(Enum.KeyCode.A) then strafe = strafe - 1 end

        if forward ~= 0 or strafe ~= 0 then
            moveDir = (look * forward) + (right * strafe)
        end

        local upVal = 0
        if holdingUp or UserInputService:IsKeyDown(Enum.KeyCode.Space) then upVal = upVal + 1 end
        if holdingDown or UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then upVal = upVal - 1 end

        moveDir = moveDir + Vector3.new(0, upVal, 0)

        if moveDir.Magnitude > 0 then
            bv.Velocity = moveDir.Unit * speed
            bg.CFrame = camCFrame
        else
            bv.Velocity = Vector3.zero
            r.AssemblyLinearVelocity = Vector3.zero
            r.AssemblyAngularVelocity = Vector3.zero
            bg.CFrame = camCFrame
        end
    end)
end

btnFly.MouseButton1Click:Connect(function()
    if flying then
        stopFly()
    else
        startFly()
    end
end)

btnClose.MouseButton1Click:Connect(function()
    stopFly()
    screenGui:Destroy()
end)

player.CharacterAdded:Connect(function()
    if flying then
        stopFly()
    end
end)
