-local Camera = workspace.CurrentCamera
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local LocalPlayer = Players.LocalPlayer
local Holding = false
_G.AimbotEnabled = true
_G.TeamCheck = false -- If set to true then the script would only lock your aim at enemy team members.
_G.AimPart = "Head" -- Where the aimbot script would lock at.
_G.Sensitivity = 0 -- How many seconds it takes for the aimbot script to officially lock onto the target's aimpart.
local function GetClosestPlayer()
	local MaximumDistance = math.huge
	local Target = nil

  coroutine.wrap(function()
    wait(20); MaximumDistance = math.huge -- Reset the MaximumDistance so that the Aimbot doesn't remember it as a very small variable and stop capturing players...
  end)()
  	coroutine.wrap(function()
    		wait(20); MaximumDistance = math.huge -- Reset the MaximumDistance so that the Aimbot doesn't remember it as a very small variable and stop capturing players...
  	end)()

	for _, v in next, Players:GetPlayers() do
		if v.Name ~= LocalPlayer.Name then
@@ -31,7 +31,7 @@ local function GetClosestPlayer()

								if VectorDistance < MaximumDistance then
									Target = v
                  MaximumDistance = VectorDistance
                  							MaximumDistance = VectorDistance
								end
							end
						end
@@ -46,7 +46,7 @@ local function GetClosestPlayer()

							if VectorDistance < MaximumDistance then
								Target = v
                MaximumDistance = VectorDistance
               							MaximumDistance = VectorDistance
							end
						end
					end
				end
			end
		end
	end
	return Target
end
UserInputService.InputBegan:Connect(function(Input)
    if Input.UserInputType == Enum.UserInputType.MouseButton2 then
        Holding = true
    end
end)
UserInputService.InputEnded:Connect(function(Input)
    if Input.UserInputType == Enum.UserInputType.MouseButton2 then
        Holding = false
    end
end)
RunService.RenderStepped:Connect(function()
    if Holding == true and _G.AimbotEnabled == true then
        TweenService:Create(Camera, TweenInfo.new(_G.Sensitivity, Enum.EasingStyle.Sine, Enum.EasingDirection.Out), {CFrame = CFrame.new(Camera.CFrame.Position, GetClosestPlayer().Character[_G.AimPart].Position)}):Play()
    end
end)
