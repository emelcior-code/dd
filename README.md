local Players = game:GetService("Players")
local button = script.Parent

local speedBoostMultiplier = 3 -- Player moves 3x faster
local originalWalkSpeed = 16 -- Default walk speed

local isBoostActive = false

local function applySpeedBoost()
	local player = Players.LocalPlayer
	local character = player.Character
	if not character then return end
	
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if not humanoid then return end
	
	-- Store original walk speed
	originalWalkSpeed = humanoid.WalkSpeed
	
	-- Apply speed boost
	humanoid.WalkSpeed = originalWalkSpeed * speedBoostMultiplier
	isBoostActive = true
end

local function removeSpeedBoost()
	local player = Players.LocalPlayer
	local character = player.Character
	if not character then return end
	
	local humanoid = character:FindFirstChildOfClass("Humanoid")
	if not humanoid then return end
	
	-- Restore original speed
	humanoid.WalkSpeed = originalWalkSpeed
	isBoostActive = false
end

button.MouseButton1Click:Connect(function()
	if isBoostActive then
		-- If boost is active, remove it and restore original speed
		removeSpeedBoost()
	else
		-- If boost is not active, apply it
		applySpeedBoost()
	end
  end)
