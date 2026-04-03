--[[
    DAVI HUB - Night 3
    Com sistema de key, notificações e toggles On/Off (otimizado)
]]

-- ========== SISTEMA DE NOTIFICAÇÕES ==========
local function notificar(titulo, texto, cor, duracao)
    duracao = duracao or 3
    cor = cor or Color3.fromRGB(255, 140, 0)
    
    local gui = Instance.new("ScreenGui")
    gui.Name = "Notificacao"
    gui.Parent = game:GetService("CoreGui")
    gui.ResetOnSpawn = false
    
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0, 300, 0, 60)
    frame.Position = UDim2.new(1, -310, 0, 10)
    frame.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
    frame.BackgroundTransparency = 0.1
    frame.BorderSizePixel = 0
    frame.Parent = gui
    
    local titleLbl = Instance.new("TextLabel")
    titleLbl.Size = UDim2.new(1, -10, 0, 25)
    titleLbl.Position = UDim2.new(0, 5, 0, 5)
    titleLbl.Text = titulo
    titleLbl.TextColor3 = cor
    titleLbl.BackgroundTransparency = 1
    titleLbl.Font = Enum.Font.GothamBold
    titleLbl.TextSize = 14
    titleLbl.TextXAlignment = Enum.TextXAlignment.Left
    titleLbl.Parent = frame
    
    local msgLbl = Instance.new("TextLabel")
    msgLbl.Size = UDim2.new(1, -10, 0, 25)
    msgLbl.Position = UDim2.new(0, 5, 0, 30)
    msgLbl.Text = texto
    msgLbl.TextColor3 = Color3.fromRGB(200, 200, 200)
    msgLbl.BackgroundTransparency = 1
    msgLbl.Font = Enum.Font.Gotham
    msgLbl.TextSize = 12
    msgLbl.TextXAlignment = Enum.TextXAlignment.Left
    msgLbl.Parent = frame
    
    -- Animação de entrada
    frame:TweenPosition(UDim2.new(1, -10, 0, 10), Enum.TweenDirection.Out, Enum.TweenInfo.new(0.3), true)
    
    task.wait(duracao)
    
    -- Animação de saída
    frame:TweenPosition(UDim2.new(1, 10, 0, 10), Enum.TweenDirection.Out, Enum.TweenInfo.new(0.3), true)
    task.wait(0.3)
    gui:Destroy()
end

-- ========== SISTEMA DE KEY ==========
local key = "DAVI2024"

local keyGui = Instance.new("ScreenGui")
keyGui.Name = "KeySystem"
keyGui.Parent = game:GetService("CoreGui")

local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 150)
frame.Position = UDim2.new(0.5, -150, 0.5, -75)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 40)
frame.Parent = keyGui

local label = Instance.new("TextLabel")
label.Size = UDim2.new(1, 0, 0, 30)
label.Text = "Digite a key:"
label.TextColor3 = Color3.fromRGB(255, 255, 255)
label.BackgroundTransparency = 1
label.Parent = frame

local box = Instance.new("TextBox")
box.Size = UDim2.new(0.8, 0, 0, 40)
box.Position = UDim2.new(0.1, 0, 0.4, 0)
box.BackgroundColor3 = Color3.fromRGB(45, 45, 60)
box.TextColor3 = Color3.fromRGB(255, 255, 255)
box.Parent = frame

local btn = Instance.new("TextButton")
btn.Size = UDim2.new(0.4, 0, 0, 40)
btn.Position = UDim2.new(0.3, 0, 0.7, 0)
btn.Text = "Ativar"
btn.BackgroundColor3 = Color3.fromRGB(255, 140, 0)
btn.TextColor3 = Color3.fromRGB(255, 255, 255)
btn.Parent = frame

local errorLabel = Instance.new("TextLabel")
errorLabel.Size = UDim2.new(0.8, 0, 0, 25)
errorLabel.Position = UDim2.new(0.1, 0, 0.85, 0)
errorLabel.Text = ""
errorLabel.TextColor3 = Color3.fromRGB(255, 100, 100)
errorLabel.BackgroundTransparency = 1
errorLabel.TextSize = 11
errorLabel.Parent = frame

btn.MouseButton1Click:Connect(function()
    if box.Text == key then
        keyGui:Destroy()
        notificar("✅ KEY VÁLIDA", "Hub carregando...", Color3.fromRGB(100, 255, 100), 2)
        carregarHub()
    else
        box.Text = ""
        errorLabel.Text = "❌ Key inválida! Tente novamente."
        notificar("❌ KEY INVÁLIDA", "A key digitada está incorreta", Color3.fromRGB(255, 100, 100), 3)
    end
end)

-- ========== HUB PRINCIPAL (OTIMIZADO) ==========
function carregarHub()
    local player = game.Players.LocalPlayer
    local coreGui = game:GetService("CoreGui")
    local TweenService = game:GetService("TweenService")
    local RunService = game:GetService("RunService")
    local Lighting = game:GetService("Lighting")

    -- GUI
    local gui = Instance.new("ScreenGui")
    gui.Name = "DaviHubNight3"
    gui.Parent = coreGui

    local f = Instance.new("Frame")
    f.Size = UDim2.new(0, 400, 0, 500)
    f.Position = UDim2.new(0.5, -200, 0.3, 0)
    f.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
    f.Parent = gui

    -- Barra título
    local b = Instance.new("Frame")
    b.Size = UDim2.new(1, 0, 0, 35)
    b.BackgroundColor3 = Color3.fromRGB(255, 140, 0)
    b.Parent = f

    local t = Instance.new("TextLabel")
    t.Size = UDim2.new(1, -90, 1, 0)
    t.Position = UDim2.new(0, 10, 0, 0)
    t.Text = "DAVI HUB - Night 3"
    t.TextColor3 = Color3.fromRGB(255, 255, 255)
    t.BackgroundTransparency = 1
    t.Font = Enum.Font.GothamBold
    t.TextSize = 16
    t.Parent = b

    -- Minimizar
    local minBtn = Instance.new("TextButton")
    minBtn.Size = UDim2.new(0, 30, 0, 30)
    minBtn.Position = UDim2.new(1, -68, 0, 2.5)
    minBtn.Text = "−"
    minBtn.TextSize = 20
    minBtn.BackgroundColor3 = Color3.fromRGB(80, 80, 100)
    minBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    minBtn.Parent = b

    -- Fechar
    local closeBtn = Instance.new("TextButton")
    closeBtn.Size = UDim2.new(0, 30, 0, 30)
    closeBtn.Position = UDim2.new(1, -35, 0, 2.5)
    closeBtn.Text = "X"
    closeBtn.TextSize = 18
    closeBtn.BackgroundColor3 = Color3.fromRGB(200, 60, 60)
    closeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
    closeBtn.Parent = b
    closeBtn.MouseButton1Click:Connect(function() gui:Destroy() end)

    -- Arrastar
    local drag = false
    local dragStart, startPos
    b.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 then
            drag = true
            dragStart = i.Position
            startPos = f.Position
        end
    end)
    b.InputEnded:Connect(function() drag = false end)
    game:GetService("UserInputService").InputChanged:Connect(function(i)
        if drag and i.UserInputType == Enum.UserInputType.MouseMovement then
            local delta = i.Position - dragStart
            f.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        end
    end)

    -- Minimizar funcionalidade
    local minimized = false
    local scrollArea = nil
    local function getScrollArea()
        for _, child in pairs(f:GetChildren()) do
            if child:IsA("ScrollingFrame") then return child end
        end
        return nil
    end
    minBtn.MouseButton1Click:Connect(function()
        minimized = not minimized
        scrollArea = scrollArea or getScrollArea()
        if minimized then
            if scrollArea then scrollArea.Visible = false end
            TweenService:Create(f, TweenInfo.new(0.2), {Size = UDim2.new(0, 400, 0, 35)}):Play()
            minBtn.Text = "+"
        else
            TweenService:Create(f, TweenInfo.new(0.2), {Size = UDim2.new(0, 400, 0, 500)}):Play()
            task.wait(0.2)
            if scrollArea then scrollArea.Visible = true end
            minBtn.Text = "−"
        end
    end)

    -- Scroll
    local s = Instance.new("ScrollingFrame")
    s.Size = UDim2.new(1, 0, 1, -35)
    s.Position = UDim2.new(0, 0, 0, 35)
    s.BackgroundTransparency = 1
    s.ScrollBarThickness = 6
    s.Parent = f

    local layout = Instance.new("UIListLayout")
    layout.Padding = UDim.new(0, 8)
    layout.Parent = s

    -- Funções auxiliares
    function btn(txt, cb)
        local bt = Instance.new("TextButton")
        bt.Size = UDim2.new(0.9, 0, 0, 40)
        bt.Text = txt
        bt.BackgroundColor3 = Color3.fromRGB(45, 45, 60)
        bt.TextColor3 = Color3.fromRGB(255, 255, 255)
        bt.Parent = s
        bt.MouseButton1Click:Connect(function()
            cb()
            notificar("📌 TELEPORT", "Teleportado para " .. txt, Color3.fromRGB(255, 200, 100), 2)
        end)
        bt.MouseEnter:Connect(function() bt.BackgroundColor3 = Color3.fromRGB(255, 140, 0) end)
        bt.MouseLeave:Connect(function() bt.BackgroundColor3 = Color3.fromRGB(45, 45, 60) end)
    end

    function tog(txt, def, cb)
        local fr = Instance.new("Frame")
        fr.Size = UDim2.new(0.9, 0, 0, 40)
        fr.BackgroundTransparency = 1
        fr.Parent = s
        local lb = Instance.new("TextLabel")
        lb.Size = UDim2.new(0.65, 0, 1, 0)
        lb.Text = txt
        lb.TextColor3 = Color3.fromRGB(220, 220, 220)
        lb.BackgroundTransparency = 1
        lb.Parent = fr
        local bt = Instance.new("TextButton")
        bt.Size = UDim2.new(0.25, 0, 0.8, 0)
        bt.Position = UDim2.new(0.72, 0, 0.1, 0)
        bt.Text = def and "On" or "Off"
        bt.BackgroundColor3 = def and Color3.fromRGB(255, 140, 0) or Color3.fromRGB(80, 80, 100)
        bt.TextColor3 = def and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(255, 100, 100)
        bt.Parent = fr
        local st = def
        bt.MouseButton1Click:Connect(function()
            st = not st
            bt.Text = st and "On" or "Off"
            bt.BackgroundColor3 = st and Color3.fromRGB(255, 140, 0) or Color3.fromRGB(80, 80, 100)
            bt.TextColor3 = st and Color3.fromRGB(255, 255, 255) or Color3.fromRGB(255, 100, 100)
            cb(st)
            notificar("⚙️ CONFIG", txt .. " " .. (st and "ativado" or "desativado"), Color3.fromRGB(100, 200, 255), 2)
        end)
    end

    -- ========== FUNCIONALIDADES ==========
    local function teleport(pos)
        local char = player.Character
        if char and char:FindFirstChild("HumanoidRootPart") then
            char.HumanoidRootPart.CFrame = CFrame.new(pos)
        end
    end

    -- Auto Munição (otimizada)
    local function autoMunicao()
        local char = player.Character or player.CharacterAdded:Wait()
        local root = char:WaitForChild("HumanoidRootPart")
        local shotgun = char:FindFirstChild("Shotgun") or player.Backpack:FindFirstChild("Shotgun")
        if not shotgun then
            notificar("⚠️ ATENÇÃO", "Nenhuma shotgun encontrada. Tentando coletar mesmo assim...", Color3.fromRGB(255, 200, 100), 2)
        end
        local ammoPiles = workspace:FindFirstChild("AmmoPiles")
        if not ammoPiles then
            notificar("❌ ERRO", "Pasta 'AmmoPiles' não encontrada", Color3.fromRGB(255, 100, 100), 2)
            return
        end
        local ammoPile = nil
        for _, A in ipairs(ammoPiles:GetChildren()) do
            if A and A:FindFirstChild("Detector") and A.Detector:FindFirstChild("ClickDetector") then
                ammoPile = A
                break
            end
        end
        if not ammoPile then
            notificar("❌ ERRO", "Nenhuma pilha de munição disponível", Color3.fromRGB(255, 100, 100), 2)
            return
        end
        local detector = ammoPile.Detector
        local click = detector.ClickDetector
        local originalPos = root.Position
        root.CFrame = CFrame.new(detector.Position + Vector3.new(0, 2, 0))
        task.wait(0.1)
        for i = 1, 2 do
            fireclickdetector(click)
            task.wait(0.1)
        end
        notificar("🔫 MUNIÇÃO", "Coletada! Voltando em 1.5s...", Color3.fromRGB(100, 200, 255), 2)
        task.wait(1.5)
        root.CFrame = CFrame.new(originalPos)
        notificar("✅ RETORNO", "Voltou à posição original", Color3.fromRGB(100, 255, 100), 2)
    end

    -- Stamina
    local staminaLoop = nil
    local function setStamina(state)
        if staminaLoop then staminaLoop:Disconnect() end
        if state then
            staminaLoop = RunService.RenderStepped:Connect(function()
                local char = player.Character
                if char and char:FindFirstChild("Sprint") then
                    local sp = char.Sprint
                    if sp.Overdrive then sp.Overdrive.Value = 1e9 end
                    if sp.Stamina then sp.Stamina.Value = 100 end
                end
            end)
        end
    end

    -- ESP Players
    local espObjs = {}
    local function setESP(state)
        for _, h in pairs(espObjs) do if h then h:Destroy() end end
        espObjs = {}
        if state then
            for _, p in pairs(game.Players:GetPlayers()) do
                if p ~= player and p.Character then
                    local h = Instance.new("Highlight")
                    h.FillColor = Color3.fromRGB(255, 0, 0)
                    h.OutlineColor = Color3.fromRGB(200, 0, 0)
                    h.FillTransparency = 0.5
                    h.Adornee = p.Character
                    h.Parent = p.Character
                    espObjs[p] = h
                end
            end
        end
    end

    -- Fullbright
    local origLight = {}
    local function setFullbright(state)
        if state then
            origLight = {Ambient = Lighting.Ambient, OutdoorAmbient = Lighting.OutdoorAmbient, Brightness = Lighting.Brightness, GlobalShadows = Lighting.GlobalShadows}
            Lighting.Ambient = Color3.fromRGB(255, 255, 255)
            Lighting.OutdoorAmbient = Color3.fromRGB(255, 255, 255)
            Lighting.Brightness = 2
            Lighting.GlobalShadows = false
        else
            Lighting.Ambient = origLight.Ambient or Color3.fromRGB(128, 128, 128)
            Lighting.OutdoorAmbient = origLight.OutdoorAmbient or Color3.fromRGB(128, 128, 128)
            Lighting.Brightness = origLight.Brightness or 1
            Lighting.GlobalShadows = origLight.GlobalShadows or true
        end
    end

    -- ESP Worker e Aranha (persistente, otimizado)
    local function addNPCESP(npc, cor)
        if not npc or npc:FindFirstChild("ESP_NPC") then return end
        local h = Instance.new("Highlight")
        h.Name = "ESP_NPC"
        h.FillColor = cor or Color3.fromRGB(255, 50, 50)
        h.OutlineColor = Color3.fromRGB(255, 150, 0)
        h.FillTransparency = 0.3
        h.Adornee = npc
        h.Parent = npc
    end

    local lastRefresh = 0
    local function refreshNPCs()
        if tick() - lastRefresh < 3 then return end
        lastRefresh = tick()
        local worker = workspace:FindFirstChild("Mutant") or game.ReplicatedStorage:FindFirstChild("Mutant")
        if worker and not worker:FindFirstChild("ESP_NPC") then
            addNPCESP(worker, Color3.fromRGB(255, 0, 0))
        end
        local spider = workspace:FindFirstChild("WorkerHead") or game.ReplicatedStorage:FindFirstChild("WorkerHead")
        if spider and not spider:FindFirstChild("ESP_NPC") then
            addNPCESP(spider, Color3.fromRGB(255, 100, 0))
        end
    end

    RunService.Heartbeat:Connect(refreshNPCs)
    workspace.ChildAdded:Connect(function(child)
        if child.Name == "Mutant" or child.Name == "WorkerHead" then
            task.wait(0.5); refreshNPCs()
        end
    end)
    game.ReplicatedStorage.ChildAdded:Connect(function(child)
        if child.Name == "Mutant" or child.Name == "WorkerHead" then
            task.wait(0.5); refreshNPCs()
        end
    end)

    -- ========== TELEPORTS ==========
    btn("🏕️ Cabana 1", function() teleport(Vector3.new(99.8, 4.5, -247.2)) end)
    btn("🏕️ Cabana 2", function() teleport(Vector3.new(-36.9, 4.5, 68.7)) end)
    btn("🏕️ Cabana 3", function() teleport(Vector3.new(-31.7, 4.5, 268.8)) end)
    btn("🏕️ Cabana 4", function() teleport(Vector3.new(233.6, 4.5, 245.8)) end)
    btn("🎬 Cutscene Room", function() teleport(Vector3.new(-237.0, -22.5, 107.0)) end)
    btn("🛡️ Safe Spot", function() teleport(Vector3.new(194.0, 38.7, -217.4)) end)
    btn("🏠 Lodge", function() teleport(Vector3.new(-226.8, 17.4, 103.7)) end)
    btn("🌿 Jeffry Canna", function() teleport(Vector3.new(177.5, 4.3, 197.9)) end)

    -- ========== AUTO MUNIÇÃO ==========
    btn("🔫 Auto Coletar Munição (volta em 1.5s)", autoMunicao)

    -- ========== TOGGLES ==========
    tog("⚡ Infinite Stamina", false, setStamina)
    tog("👁️ ESP Players", false, setESP)
    tog("💡 Fullbright", false, setFullbright)

    -- Ajustar scroll
    task.wait(0.1)
    local totalH = 0
    for _, child in pairs(s:GetChildren()) do
        if child:IsA("TextButton") or child:IsA("Frame") then totalH = totalH + 48 end
    end
    s.CanvasSize = UDim2.new(0, 0, 0, totalH + 30)

    notificar("🎉 HUB CARREGADO", "DAVI HUB - Night 3 pronto para uso!", Color3.fromRGB(255, 140, 0), 3)
    print("✅ DAVI HUB - Night 3 carregado (otimizado, com notificações)")
end
