
---

-- 🦗 RAYFIELD HUB - CHAPOLIN COLORADO
-- TOOLS | VISUAL | BROOKHAVEN

local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

local Window = Rayfield:CreateWindow({
Name = "🦗 Chapolin Colorado Hub",
LoadingTitle = "Carregando Astúcia...",
LoadingSubtitle = "Não contavam com minha astúcia!",
ConfigurationSaving = {
Enabled = true,
FolderName = "ChapolinHub",
FileName = "ChapolinColorado"
}
})


---

-- SERVICES

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local char = player.Character or player.CharacterAdded:Wait()
local hum = char:WaitForChild("Humanoid")
local hrp = char:WaitForChild("HumanoidRootPart")


---

-- VARIÁVEIS

local aura
local hammerTool


---

-- 🔧 FUNÇÃO DE ESCALA (R15 FIX)

local function setScale(scale)
local desc = hum:GetAppliedDescription()
desc.HeightScale = scale
desc.WidthScale  = scale
desc.DepthScale  = scale
desc.HeadScale   = scale
hum:ApplyDescription(desc)
end


---

-- 🟥 PASTILHA ENCOLHEDORA (TOOL)

local PastilhaTab = Window:CreateTab("🟥 Pastilha", 4483362458)

local function createPastilhaTool()
if player.Backpack:FindFirstChild("🟥 Pastilha Encolhedora") then return end

local tool = Instance.new("Tool")  
tool.Name = "🟥 Pastilha Encolhedora"  
tool.RequiresHandle = true  
tool.CanBeDropped = false  

local handle = Instance.new("Part")  
handle.Name = "Handle"  
handle.Size = Vector3.new(1,1,1)  
handle.Shape = Enum.PartType.Ball  
handle.Material = Enum.Material.Neon  
handle.Color = Color3.fromRGB(255,0,0)  
handle.Parent = tool  

local small = false  

tool.Activated:Connect(function()  
	small = not small  

	if small then  
		setScale(0.5)  
		hum.WalkSpeed = 22  
		hum.JumpPower = 70  
	else  
		setScale(1)  
		hum.WalkSpeed = 16  
		hum.JumpPower = 50  
	end  
end)  

tool.Parent = player.Backpack

end

PastilhaTab:CreateButton({
Name = "Pegar Pastilha Encolhedora (TOOL)",
Callback = createPastilhaTool
})


---

-- 🔨 MARTELO BIÔNICO (TOOL)

local HammerTab = Window:CreateTab("🔨 Martelo", 4483362458)

local function createHammerTool()
if hammerTool then hammerTool:Destroy() end

local tool = Instance.new("Tool")  
tool.Name = "🔨 Martelo Biônico"  
tool.RequiresHandle = true  
tool.CanBeDropped = false  

local handle = Instance.new("Part")  
handle.Name = "Handle"  
handle.Size = Vector3.new(1,4,1)  
handle.Color = Color3.fromRGB(255,221,0)  
handle.Parent = tool  

local head = Instance.new("Part")  
head.Size = Vector3.new(4,2,2)  
head.Color = Color3.fromRGB(255,0,0)  
head.Parent = tool  

local weld = Instance.new("WeldConstraint")  
weld.Part0 = handle  
weld.Part1 = head  
weld.Parent = handle  
head.CFrame = handle.CFrame * CFrame.new(0,2.5,0)  

tool.Activated:Connect(function()  
	local exp = Instance.new("Explosion")  
	exp.Position = hrp.Position  
	exp.BlastRadius = 18  
	exp.BlastPressure = 0  
	exp.Parent = workspace  
end)  

tool.Parent = player.Backpack  
hammerTool = tool

end

HammerTab:CreateButton({
Name = "Pegar Martelo Biônico (TOOL)",
Callback = createHammerTool
})


---

-- 📣 BUZINA PARALISADORA (TOOL)

local BuzinaTab = Window:CreateTab("📣 Buzina", 4483362458)

local function createBuzinaTool()
if player.Backpack:FindFirstChild("📣 Buzina Paralisadora") then return end

local tool = Instance.new("Tool")  
tool.Name = "📣 Buzina Paralisadora"  
tool.RequiresHandle = true  
tool.CanBeDropped = false  

local handle = Instance.new("Part")  
handle.Name = "Handle"  
handle.Size = Vector3.new(1,2,1)  
handle.Material = Enum.Material.Metal  
handle.Color = Color3.fromRGB(255,255,0)  
handle.Parent = tool  

tool.Activated:Connect(function()  
	for _,plr in pairs(Players:GetPlayers()) do  
		if plr ~= player and plr.Character then  
			local h = plr.Character:FindFirstChild("Humanoid")  
			local r = plr.Character:FindFirstChild("HumanoidRootPart")  

			if h and r and (r.Position - hrp.Position).Magnitude <= 25 then  
				local oldSpeed = h.WalkSpeed  
				h.WalkSpeed = 0  

				task.delay(3, function()  
					if h then h.WalkSpeed = oldSpeed end  
				end)  
			end  
		end  
	end  
end)  

tool.Parent = player.Backpack

end

BuzinaTab:CreateButton({
Name = "Pegar Buzina Paralisadora (TOOL)",
Callback = createBuzinaTool
})


---

-- ✨ AURA

local AuraTab = Window:CreateTab("✨ Astúcia", 4483362458)

AuraTab:CreateToggle({
Name = "Aura do Chapolin",
CurrentValue = false,
Callback = function(v)
if v then
aura = Instance.new("ParticleEmitter")
aura.Texture = "rbxassetid://296874871"
aura.Rate = 60
aura.Lifetime = NumberRange.new(0.6)
aura.Size = NumberSequence.new(1.5)
aura.Color = ColorSequence.new(Color3.fromRGB(255,0,0))
aura.Parent = hrp
else
if aura then aura:Destroy() end
end
end
})


---

-- 🏃 MOVIMENTO

local MoveTab = Window:CreateTab("🏃 Movimento", 4483362458)

MoveTab:CreateButton({
Name = "Salto do Chapolin",
Callback = function()
hrp.Velocity = Vector3.new(0,80,0)
end
})

MoveTab:CreateButton({
Name = "Dash Heroico",
Callback = function()
hrp.CFrame = hrp.CFrame * CFrame.new(0,0,-20)
end
})


---

-- FINAL

Rayfield:Notify({
Title = "🦗 Chapolin Colorado",
Content = "Pastilha, Martelo e Buzina prontos!",
Duration = 5
}) e o script tem que funcional
