
class=class="string">"comment">-- Script has been decompiled successfully
class=class="string">"keyword">local Circle = Drawing.new(class="string">"Circle")
Circle.Radius = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Radius']
Circle.Filled = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Filled']
Circle.Visible = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Visible']
Circle.Transparency = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Transparency']
Circle.Color = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Color']
Circle.Thickness = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Thickness']

class=class="string">"keyword">local outline = Drawing.new(class="string">"Circle")
outline.Thickness = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'OutlineThickness'] class=class="string">"keyword">or 0.3 class=class="string">"comment">-- Default class=class="string">"keyword">if class=class="string">"keyword">not specified
outline.Radius = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Radius']
outline.Filled = false
outline.Visible = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'Outline'] class=class="string">"keyword">or false class=class="string">"comment">-- Default class=class="string">"keyword">if class=class="string">"keyword">not specified
outline.ZIndex = 999
outline.Transparency = 1
outline.Color = getgenv().Versal[class="string">'Silent'][class="string">'FOV'][class="string">'OutlineColor'] class=class="string">"keyword">or Color3.fromRGB(0, 0, 0) class=class="string">"comment">-- Default class=class="string">"keyword">if class=class="string">"keyword">not specified

class=class="string">"comment">-- Services class=class="string">"keyword">and variables
class=class="string">"keyword">local Players = game:GetService(class="string">"Players")
class=class="string">"keyword">local UserInputService = game:GetService(class="string">"UserInputService")
class=class="string">"keyword">local RunService = game:GetService(class="string">"RunService")
class=class="string">"keyword">local GuiService = game:GetService(class="string">"GuiService")
class=class="string">"keyword">local Client = Players.LocalPlayer
class=class="string">"keyword">local Character = Client.Character
class=class="string">"keyword">local Mouse = Client:GetMouse()
class=class="string">"keyword">local Camera = workspace.CurrentCamera

class=class="string">"keyword">local SilentTarget = nil
class=class="string">"keyword">local Highlight = nil
class=class="string">"keyword">local ClosestParts = {class="string">"Head", class="string">"UpperTorso", class="string">"HumanoidRootPart", class="string">"LowerTorso", class="string">"LeftHand", class="string">"RightHand", class="string">"LeftLowerArm", class="string">"RightLowerArm", class="string">"LeftUpperArm", class="string">"RightUpperArm", class="string">"LeftFoot", class="string">"LeftLowerLeg", class="string">"LeftUpperLeg", class="string">"RightLowerLeg", class="string">"RightFoot", class="string">"RightUpperLeg"}

class=class="string">"keyword">local class=class="string">"keyword">function GetClosestToMouse()
    class=class="string">"keyword">local Target, Closest = nil, math.huge

    class=class="string">"keyword">for _, v class=class="string">"keyword">in pairs(Players:GetPlayers()) class=class="string">"keyword">do
        class=class="string">"keyword">if v.Character class=class="string">"keyword">and v ~= Client class=class="string">"keyword">then
            class=class="string">"keyword">for _, partName class=class="string">"keyword">in ipairs(ClosestParts) class=class="string">"keyword">do
                class=class="string">"keyword">local part = v.Character:FindFirstChild(partName)
                class=class="string">"keyword">if part class=class="string">"keyword">then
                    class=class="string">"keyword">local Position, OnScreen = Camera:WorldToScreenPoint(part.Position)
                    class=class="string">"keyword">local Distance = (Vector2.new(Position.X, Position.Y) - Vector2.new(Mouse.X, Mouse.Y)).Magnitude

                    class=class="string">"keyword">if Circle.Radius > Distance class=class="string">"keyword">and Distance < Closest class=class="string">"keyword">and OnScreen class=class="string">"keyword">then
                        Closest = Distance
                        Target = v
                        class=class="string">"keyword">if getgenv().Versal[class="string">'Silent'][class="string">'ClosestPart'] class=class="string">"keyword">then
                            getgenv().Versal[class="string">'Silent'].HitPart = partName
                        class=class="string">"keyword">end
                    class=class="string">"keyword">end
                class=class="string">"keyword">end
            class=class="string">"keyword">end
        class=class="string">"keyword">end
    class=class="string">"keyword">end
    class=class="string">"keyword">return Target
class=class="string">"keyword">end

class=class="string">"keyword">local class=class="string">"keyword">function UpdateDrawings()
    Circle.Position = Vector2.new(Mouse.X, Mouse.Y + GuiService:GetGuiInset().Y)
    outline.Position = Vector2.new(Mouse.X, Mouse.Y + GuiService:GetGuiInset().Y)
class=class="string">"keyword">end

class=class="string">"keyword">local class=class="string">"keyword">function get_calculated_velocity(obj)
    class=class="string">"keyword">if obj class=class="string">"keyword">and obj.Character class=class="string">"keyword">and obj.Character:FindFirstChild(getgenv().Versal[class="string">'Silent'].HitPart) class=class="string">"keyword">then
        class=class="string">"keyword">local root = obj.Character.HumanoidRootPart
        class=class="string">"keyword">local currentPosition = root.Position
        class=class="string">"keyword">local currentTime = tick()

        wait(0.1)

        class=class="string">"keyword">local newPosition = root.Position
        class=class="string">"keyword">local newTime = tick()

        class=class="string">"keyword">local distanceTraveled = newPosition - currentPosition
        class=class="string">"keyword">local timeInterval = newTime - currentTime
        class=class="string">"keyword">local velocity = distanceTraveled / timeInterval
        class=class="string">"keyword">return velocity
    class=class="string">"keyword">end
    class=class="string">"keyword">return Vector3.new(0, 0, 0)
class=class="string">"keyword">end

class=class="string">"keyword">local class=class="string">"keyword">function calculatePosition(victim, velocity)
    class=class="string">"keyword">local prediction = getgenv().Versal[class="string">'Silent'][class="string">'Prediction Configuration'][class="string">'Prediction Amount']
    class=class="string">"keyword">local newYVelocity = velocity.Y + (prediction * 1)
    class=class="string">"keyword">local jumpOffset = Vector3.new(0, getgenv().Versal[class="string">'Silent'][class="string">'Offset'][class="string">'Jump'], 0)
    class=class="string">"keyword">local fallOffset = Vector3.new(0, getgenv().Versal[class="string">'Silent'][class="string">'Offset'][class="string">'Fall'], 0)
    class=class="string">"keyword">local pos

    pos = Vector3.new(
        victim.Position.X,
        victim.Position.Y,
        victim.Position.Z
    ) + Vector3.new(
        velocity.X,
        newYVelocity,
        velocity.Z
    ) * prediction

    class=class="string">"keyword">if newYVelocity > 0 class=class="string">"keyword">then
        pos = pos + jumpOffset
    class=class="string">"keyword">elseif newYVelocity < 0 class=class="string">"keyword">then
        pos = pos + fallOffset
    class=class="string">"keyword">end

    class=class="string">"keyword">return pos
class=class="string">"keyword">end

class=class="string">"keyword">local hue = 0
class=class="string">"keyword">local class=class="string">"keyword">function UpdateRainbowHighlight()
    class=class="string">"keyword">if getgenv().Versal[class="string">'Silent'][class="string">'RainbowHighlight'] class=class="string">"keyword">and SilentTarget class=class="string">"keyword">then
        hue = hue + 0.01
        class=class="string">"keyword">if hue > 1 class=class="string">"keyword">then hue = 0 class=class="string">"keyword">end
        class=class="string">"keyword">local color = Color3.fromHSV(hue, 1, 1)

        class=class="string">"keyword">if class=class="string">"keyword">not Highlight class=class="string">"keyword">then
            Highlight = Instance.new(class="string">"Highlight")
            Highlight.Parent = SilentTarget.Character
            Highlight.Adornee = SilentTarget.Character
        class=class="string">"keyword">end

        Highlight.FillColor = color
        Highlight.OutlineColor = color
    class=class="string">"keyword">elseif Highlight class=class="string">"keyword">then
        Highlight:Destroy()
        Highlight = nil
    class=class="string">"keyword">end
class=class="string">"keyword">end

RunService.RenderStepped:Connect(class=class="string">"keyword">function(deltaTime)
    UpdateDrawings()
    class=class="string">"keyword">local closestPlayer = GetClosestToMouse()

    class=class="string">"keyword">if SilentTarget ~= closestPlayer class=class="string">"keyword">then
        class=class="string">"keyword">if Highlight class=class="string">"keyword">then
            Highlight:Destroy()
            Highlight = nil
        class=class="string">"keyword">end
        SilentTarget = closestPlayer
    class=class="string">"keyword">end

    UpdateRainbowHighlight()

    class=class="string">"keyword">if SilentTarget class=class="string">"keyword">and getgenv().Versal[class="string">'Silent'][class="string">'Resolver'] class=class="string">"keyword">then
        class=class="string">"keyword">local character = SilentTarget.Character.HumanoidRootPart
        class=class="string">"keyword">local lastPosition = character.Position
        task.wait()
        class=class="string">"keyword">local currentPosition = character.Position
        class=class="string">"keyword">local velocity = calculateVelocity(lastPosition, currentPosition, deltaTime)
        character.AssemblyLinearVelocity = velocity
        character.Velocity = velocity
        lastPosition = currentPosition
    class=class="string">"keyword">end
class=class="string">"keyword">end)

class=class="string">"keyword">local Argument = class="string">""

class="keywordclass="string">">function getargument()
    class="keywordclass="string">">local bytecode = getscriptbytecode(game:GetService("Playersclass="string">").LocalPlayer.PlayerGui.Framework)
    class="keywordclass="string">">local convertreadable = tostring(bytecode)

    class="keywordclass="string">">for line class="keywordclass="string">">in convertreadable:gmatch("%w+class="string">") class="keywordclass="string">">do
        class="keywordclass="string">">if line:match("UpdateMousePosclass="string">") class="keywordclass="string">">then
            Argument = line
        class="keywordclass="string">">end
    class="keywordclass="string">">end
class="keywordclass="string">">end

class="keywordclass="string">">for i = 1, 5 class="keywordclass="string">">do
    getargument()
class="keywordclass="string">">end

warn(Argument)

class="keywordclass="string">">local class="keywordclass="string">">function CharAdded()
    Character.ChildAdded:Connect(class="keywordclass="string">">function(tool)
        class="keywordclass="string">">if tool:IsA("Toolclass="string">") class="keywordclass="string">">then
            tool.Activated:Connect(class="keywordclass="string">">function()
                class="keywordclass="string">">if SilentTarget class="keywordclass="string">">and getgenv().Versal['Silentclass="string">']['SilentEnabledclass="string">'] class="keywordclass="string">">then
                    class="keywordclass="string">">local predictedPos = calculatePosition(SilentTarget.Character[getgenv().Versal['Silentclass="string">'].HitPart], SilentTarget.Character[getgenv().Versal['Silentclass="string">'].HitPart].Velocity)
                    game:GetService("ReplicatedStorageclass="string">").MainEvent:FireServer(Argument, predictedPos)
                class="keywordclass="string">">end
            class="keywordclass="string">">end)
        class="keywordclass="string">">end
    class="keywordclass="string">">end)
class="keywordclass="string">">end

Client.CharacterAdded:Connect(CharAdded)

class="keywordclass="string">">if Character class="keywordclass="string">">then
    CharAdded()
class="keyword">end
