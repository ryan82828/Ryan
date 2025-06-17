local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

-- Botões
local flyButton = script.Parent:WaitForChild("FlyButton")
local speedButton = script.Parent:WaitForChild("SpeedButton")
local teleportButton = script.Parent:WaitForChild("TeleportButton")
local jumpButton = script.Parent:WaitForChild("JumpButton")

-- Voar
local flying = false
flyButton.MouseButton1Click:Connect(function()
	flying = not flying
	if flying then
		local bodyVelocity = Instance.new("BodyVelocity")
		bodyVelocity.Velocity = Vector3.new(0, 50, 0)
		bodyVelocity.MaxForce = Vector3.new(0, math.huge, 0)
		bodyVelocity.Name = "FlyForce"
		bodyVelocity.Parent = character.HumanoidRootPart
	else
		local fly = character.HumanoidRootPart:FindFirstChild("FlyForce")
		if fly then
			fly:Destroy()
		end
	end
end)

-- Velocidade
speedButton.MouseButton1Click:Connect(function()
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.WalkSpeed = 100
	end
end)

-- Teleporte (para posição fixa)
teleportButton.MouseButton1Click:Connect(function()
	character:MoveTo(Vector3.new(0, 10, 0)) -- Altere a posição como quiser
end)

-- Super pulo
jumpButton.MouseButton1Click:Connect(function()
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if humanoid then
		humanoid.JumpPower = 200
		humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
	end
end)
