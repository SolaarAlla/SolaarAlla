Admin Command script by me:
-- Admin Command GUI Script for Roblox Executor
local player = game.Players.LocalPlayer
local screenGui = Instance.new("ScreenGui", player.PlayerGui)
screenGui.ResetOnSpawn = false

-- Create the main frame
local frame = Instance.new("Frame", screenGui)
frame.Size = UDim2.new(0.3, 0, 0.4, 0)
frame.Position = UDim2.new(0.35, 0, 0.3, 0)
frame.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
frame.BorderSizePixel = 0

-- Create the command input box
local commandBox = Instance.new("TextBox", frame)
commandBox.Size = UDim2.new(1, 0, 0.6, 0)
commandBox.Position = UDim2.new(0, 0, 0, 0)
commandBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
commandBox.TextColor3 = Color3.fromRGB(255, 255, 255)
commandBox.PlaceholderText = "Enter command here..."
commandBox.TextScaled = true
commandBox.TextWrapped = true

-- Create the execute button
local executeButton = Instance.new("TextButton", frame)
executeButton.Size = UDim2.new(0.5, 0, 0.2, 0)
executeButton.Position = UDim2.new(0, 0, 0.6, 0)
executeButton.BackgroundColor3 = Color3.fromRGB(0, 170, 0)
executeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
executeButton.Text = "Execute"
executeButton.TextScaled = true

-- Create the close button
local closeButton = Instance.new("TextButton", frame)
closeButton.Size = UDim2.new(0.5, 0, 0.2, 0)
closeButton.Position = UDim2.new(0.5, 0, 0.6, 0)
closeButton.BackgroundColor3 = Color3.fromRGB(170, 0, 0)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Text = "Close"
closeButton.TextScaled = true

-- Function to execute commands
local function executeCommand()
    local command = commandBox.Text
    if command and command ~= "" then
        local success, errorMessage = pcall(function()
            loadstring(command)()  -- Executes the command entered in the command box
        end)
        if not success then
            warn("Error executing command: " .. errorMessage)
        end
        commandBox.Text = ""  -- Clear the command box after execution
    end
end

-- Function to close the GUI
local function closeGui()
    screenGui:Destroy()  -- Closes the GUI
end

-- Event connections
executeButton.MouseButton1Click:Connect(executeCommand)
closeButton.MouseButton1Click:Connect(closeGui)
