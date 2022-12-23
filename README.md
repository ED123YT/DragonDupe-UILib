local plrs = game:GetService("Players")
local coregui = game:GetService("CoreGui")
local uis = game:GetService("UserInputService")
local ts = game:GetService("TweenService")
local rs = game:GetService("RunService")
local tween = TweenInfo.new
local plr = plrs.LocalPlayer
local humroot = plr:FindFirstChild("HumanoidRootPart")
local hum = plr:FindFirstChild("Humanoid")
local mouse = plr:GetMouse()
local isClosed = false

if coregui:FindFirstChild("DragonDupe") then
    coregui.DragonDupe:Destroy()
end

local DragonDupe = Instance.new("ScreenGui",coregui)
DragonDupe.Name = "DragonDupe"

local cooldown = {
    ["Tabs"] = .3,
    ["Toggle"] = .3,
    ["DropDown"] = .3,
    ["Slider"] = .05
}

lib = {}

function Dragify(Frame) -- Not made by me
    dragToggle = nil
    dragSpeed = .25 -- You can edit this.
    dragInput = nil
    dragStart = nil
    dragPos = nil
    
    function updateInput(input)
    Delta = input.Position - dragStart
    Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + Delta.X, startPos.Y.Scale, startPos.Y.Offset + Delta.Y)
    game:GetService("TweenService"):Create(Frame, TweenInfo.new(.25), {Position = Position}):Play()
    end
    
    Frame.InputBegan:Connect(function(input)
    if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then
    dragToggle = true
    dragStart = input.Position
    startPos = Frame.Position
    input.Changed:Connect(function()
    if (input.UserInputState == Enum.UserInputState.End) then
    dragToggle = false
    end
    end)
    end
    end)
    
    Frame.InputChanged:Connect(function(input)
    if (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
    dragInput = input
    end
    end)
    
    game:GetService("UserInputService").InputChanged:Connect(function(input)
    if (input == dragInput and dragToggle) then
    updateInput(input)
    end
    end)
end

function DestroyUI(Frame,Frame2)
    uis.InputBegan:Connect(function(input, gameProcessedEvent)
        if input.KeyCode == Enum.KeyCode.Delete then
            Frame2.ClipsDescendants = true
            ts:Create(Frame2,tween(.3),{Size=UDim2.new(0,0,0,0)}):Play()
            wait(.2)
            Frame:Destroy()
        end
    end)
end

function ToggleUI(Frame)
    uis.InputBegan:Connect(function(input, gameProcessedEvent)
        if input.KeyCode == Enum.KeyCode.RightControl then
            isClosed = not isClosed
            if isClosed then
                ts:Create(Frame,tween(.3),{Size=UDim2.new(0,0,0,0)}):Play()
                wait(.3)
                Frame.Visible = false
            else
                Frame.Visible = true
                ts:Create(Frame,tween(.3),{Size=UDim2.new(0.5, 0, 0.8, 0)}):Play()
            end
        end
    end)
end

local themes = {
    SchemeColor = Color3.fromRGB(20, 20, 20),
    Background = Color3.fromRGB(20, 20, 20),
    Header = Color3.fromRGB(35, 35, 35),
    TextColor = Color3.fromRGB(255,255,255),
    ElementColor = Color3.fromRGB(35, 35, 35)
}
local themeStyle = {
    DarkMode = {
        SchemeColor = Color3.fromRGB(20, 20, 20),
        Background = Color3.fromRGB(20, 20, 20),
        Header = Color3.fromRGB(35, 35, 35),
        TextColor = Color3.fromRGB(255,255,255),
        ElementColor = Color3.fromRGB(35, 35, 35)
    },
    LightMode = {
        SchemeColor = Color3.fromRGB(120, 120, 120),
        Background = Color3.fromRGB(120, 120, 120),
        Header = Color3.fromRGB(135, 135, 135),
        TextColor = Color3.fromRGB(255,255,255),
        ElementColor = Color3.fromRGB(135, 135, 135)
    }
}

function lib(Options)
    if not Options.theme then
        Options.theme = themes
    end
    if Options.theme == "DarkMode" then
        Options.theme = themeStyle.DarkMode
    elseif Options.theme == "LightMode" then
        Options.theme = themeStyle.LightMode
    else
        if Options.theme.SchemeColor == nil then
            Options.theme.SchemeColor = Color3.fromRGB(20, 20, 20)
        elseif Options.theme.Background == nil then
            Options.theme.Background = Color3.fromRGB(20, 20, 20)
        elseif Options.theme.Header == nil then
            Options.theme.Header = Color3.fromRGB(35, 35, 35)
        elseif Options.theme.TextColor == nil then
            Options.theme.TextColor = Color3.fromRGB(255, 255, 255)
        elseif Options.theme.ElementColor == nil then
            Options.theme.ElementColor = Color3.fromRGB(35, 35, 35)
        end
    end
    tbss = {}
    local MainFrame = Instance.new("ImageLabel")
    local Title = Instance.new("ImageLabel")
    local UIName = Instance.new("TextLabel")
    local Side = Instance.new("ImageLabel")
    local Tabs = Instance.new("ScrollingFrame")
    local TabsLayout = Instance.new("UIListLayout")
    local UpperFrame = Instance.new("ImageLabel")
    local Exit = Instance.new("TextButton")
    local Containers = Instance.new("ImageLabel")
    DestroyUI(DragonDupe,MainFrame)
    Dragify(MainFrame)
    ToggleUI(MainFrame )

    MainFrame.Name = "MainFrame"
    MainFrame.Parent = DragonDupe
    MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
    MainFrame.BackgroundColor3 = Color3.fromRGB(255,255,255)
    MainFrame.BackgroundTransparency = 1.000
    MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
    MainFrame.Size = Options.Size or UDim2.new(0.5, 0, 0.800000012, 0)
    MainFrame.Image = "rbxassetid://3570695787"
    MainFrame.ImageColor3 = Options.theme.Background
    MainFrame.ScaleType = Enum.ScaleType.Slice
    MainFrame.SliceCenter = Rect.new(100, 100, 100, 100)
    MainFrame.SliceScale = 0.060
    
    Title.Name = "Title"
    Title.Parent = MainFrame
    Title.BackgroundColor3 = Color3.fromRGB(255,255,255)
    Title.BackgroundTransparency = 1.000
    Title.Position = UDim2.new(0.0104780616, 0, 0.0114829391, 0)
    Title.Size = UDim2.new(0.25, 0, 0.081, 0)
    Title.Image = "rbxassetid://3570695787"
    Title.ImageColor3 = Options.theme.Header
    Title.ScaleType = Enum.ScaleType.Slice
    Title.SliceCenter = Rect.new(100, 100, 100, 100)
    Title.SliceScale = 0.060
    
    UIName.Name = "UIName"
    UIName.Parent = Title
    UIName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    UIName.BackgroundTransparency = 1.000
    UIName.BorderSizePixel = 0
    UIName.Position = UDim2.new(0.0261951536, 0, 0.0799999982, 0)
    UIName.Size = UDim2.new(0.949999988, 0, 0.9, 0)
    UIName.Font = Enum.Font.SourceSansBold
    UIName.Text = Options.Name or "Dragon Dupe"
    UIName.TextColor3 = Color3.fromRGB(255, 255, 255)
    UIName.TextSize = 24.000
    
    Side.Name = "Side"
    Side.Parent = MainFrame
    Side.BackgroundColor3 = Color3.fromRGB(255,255,255)
    Side.BackgroundTransparency = 1.000
    Side.BorderSizePixel = 0
    Side.Position = UDim2.new(0.00999999978, 0, 0.104999997, 0)
    Side.Size = UDim2.new(0.25, 0, 0.88499999, 0)
    Side.Image = "rbxassetid://3570695787"
    Side.ImageColor3 = Options.theme.Header
    Side.ScaleType = Enum.ScaleType.Slice
    Side.SliceCenter = Rect.new(100, 100, 100, 100)
    Side.SliceScale = 0.060
    
    Tabs.Name = "Tabs"
    Tabs.Parent = Side
    Tabs.Active = true
    Tabs.BackgroundColor3 = Color3.fromRGB(255,255,255)
    Tabs.BackgroundTransparency = 1.000
    Tabs.BorderSizePixel = 0
    Tabs.Position = UDim2.new(0, 0, 0.0129750725, 0)
    Tabs.Size = UDim2.new(1, 0, 0.970000029, 0)
    Tabs.CanvasSize = UDim2.new(0, 0, 0, 0)
    Tabs.ScrollBarThickness = 6
    
    TabsLayout.Name = "TabsLayout"
    TabsLayout.Parent = Tabs
    TabsLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    TabsLayout.SortOrder = Enum.SortOrder.LayoutOrder
    TabsLayout.Padding = UDim.new(0, 6)

    UpperFrame.Name = "UpperFrame"
    UpperFrame.Parent = MainFrame
    UpperFrame.BackgroundColor3 = Color3.fromRGB(255,255,255)
    UpperFrame.BackgroundTransparency = 1.000
    UpperFrame.Position = UDim2.new(0.270000011, 0, 0.0109999999, 0)
    UpperFrame.Size = UDim2.new(0.720000029, 0, 0.081, 0)
    UpperFrame.Image = "rbxassetid://3570695787"
    UpperFrame.ImageColor3 = Options.theme.Header
    UpperFrame.ScaleType = Enum.ScaleType.Slice
    UpperFrame.SliceCenter = Rect.new(100, 100, 100, 100)
    UpperFrame.SliceScale = 0.060
    
    Exit.Name = "Exit"
    Exit.Parent = UpperFrame
    Exit.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    Exit.BackgroundTransparency = 1.000
    Exit.BorderColor3 = Color3.fromRGB(27, 42, 53)
    Exit.BorderSizePixel = 0
    Exit.Position = UDim2.new(0.899999976, 0, 0, 0)
    Exit.Size = UDim2.new(0.0920000002, 0, 1, 0)
    Exit.Font = Enum.Font.FredokaOne
    Exit.Text = "X"
    Exit.TextColor3 = Color3.fromRGB(255, 255, 255)
    Exit.TextSize = 24.000
    
    Containers.Name = "Containers"
    Containers.Parent = MainFrame
    Containers.AnchorPoint = Vector2.new(0.5, 0.5)
    Containers.BackgroundColor3 = Color3.fromRGB(255,255,255)
    Containers.BackgroundTransparency = 1.000
    Containers.BorderSizePixel = 0
    Containers.Position = UDim2.new(0.629999995, 0, 0.546999991, 0)
    Containers.Size = UDim2.new(0.721, 0, 0.88499999, 0)
    Containers.Image = "rbxassetid://3570695787"
    Containers.ImageColor3 = Options.theme.Header
    Containers.ScaleType = Enum.ScaleType.Slice
    Containers.SliceCenter = Rect.new(100, 100, 100, 100)
    Containers.SliceScale = 0.060

    Exit.MouseEnter:Connect(function()
        wait(.018)
        ts:Create(Exit,tween(.2),{
            TextColor3 = Color3.fromRGB(255,0,0)
        }):Play()
    end)
    Exit.MouseLeave:Connect(function()
        wait(.018)
        ts:Create(Exit,tween(.2),{
            TextColor3 = Color3.fromRGB(255,255,255)
        }):Play()
    end)
    Exit.MouseButton1Click:Connect(function()
        MainFrame.ClipsDescendants = true
        ts:Create(MainFrame,tween(.3),{Size=UDim2.new(0,0,0,0)}):Play()
        wait(.2)
        DragonDupe:Destroy()
    end)

    local firstPage = true
    function tbss:Tab(Name)
        secc = {}
        local TabButton = Instance.new("TextButton")
        local TabButtonC = Instance.new("UICorner")
        local Indicator = Instance.new("ImageLabel")
        local TabName = Instance.new("TextLabel")
        local Page = Instance.new("ScrollingFrame")
        local PageLayout = Instance.new("UIListLayout")

        TabButton.Name = Name
        TabButton.Parent = Tabs
        TabButton.BackgroundColor3 = Options.theme.SchemeColor
        TabButton.BorderSizePixel = 0
        TabButton.Size = UDim2.new(0.930000007, 0, 0, 40)
        TabButton.Font = Enum.Font.SourceSans
        TabButton.Text = ""
        TabButton.TextColor3 = Color3.fromRGB(0, 0, 0)
        TabButton.TextSize = 14.000
        
        TabButtonC.CornerRadius = UDim.new(0, 6)
        TabButtonC.Name = "TabButtonC"
        TabButtonC.Parent = TabButton
        
        Indicator.Name = "Indicator"
        Indicator.Parent = TabButton
        Indicator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Indicator.BackgroundTransparency = 1.000
        Indicator.Size = UDim2.new(0.0500000007, 0, 0, 40)
        Indicator.Image = "rbxassetid://3570695787"
        Indicator.ImageColor3 = Color3.fromRGB(0, 255, 0)
        Indicator.ScaleType = Enum.ScaleType.Slice
        Indicator.SliceCenter = Rect.new(100, 100, 100, 100)
        Indicator.SliceScale = 0.060
        
        TabName.Name = "TabName"
        TabName.Parent = TabButton
        TabName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        TabName.BackgroundTransparency = 1.000
        TabName.BorderColor3 = Color3.fromRGB(27, 42, 53)
        TabName.BorderSizePixel = 0
        TabName.Position = UDim2.new(0.100000001, 0, 0, 0)
        TabName.Size = UDim2.new(0.5, 0, 0, 40)
        TabName.Font = Enum.Font.SourceSansBold
        TabName.Text = Name or "Tab"
        TabName.TextColor3 = Color3.fromRGB(255, 255, 255)
        TabName.TextSize = 24.000
        TabName.TextXAlignment = Enum.TextXAlignment.Left
        
        Page.Name = Name
        Page.Parent = Containers
        Page.Active = true
        Page.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
        Page.BackgroundTransparency = 1.000
        Page.BorderSizePixel = 0
        Page.Position = UDim2.new(0, 0, 0.0129750725, 0)
        Page.Size = UDim2.new(1, 0, 0.970000029, 0)
        Page.CanvasSize = UDim2.new(0, 0, 0, 0)
        Page.ScrollBarThickness = 6
        
        PageLayout.Name = "PageLayout"
        PageLayout.Parent = Page
        PageLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
        PageLayout.SortOrder = Enum.SortOrder.LayoutOrder
        PageLayout.Padding = UDim.new(0, 8)

        if firstPage then
            firstPage = false
            Page.Visible = true
            Indicator.ImageColor3 = Color3.fromRGB(0,255,0)
        else
            Page.Visible = false
            Indicator.ImageColor3 = Color3.fromRGB(255,0,0)
        end
        TabButton.MouseButton1Click:Connect(function()
            for i,v in pairs(Tabs:GetChildren()) do
                if v:IsA("GuiButton") then
                    if v.Name == Page.Name then
                        ts:Create(v["Indicator"],tween(cooldown["Tabs"]),{
                            ImageColor3 = Color3.fromRGB(0,255,0)
                        }):Play()
                    else
                        ts:Create(v["Indicator"],tween(cooldown["Tabs"]),{
                            ImageColor3 = Color3.fromRGB(255,0,0)
                        }):Play()
                    end
                end
            end

            for i,v in pairs(Containers:GetChildren()) do
                if v:IsA("ScrollingFrame") then
                    if v.Name == TabButton.Name then
                        ts:Create(Containers,tween(cooldown["Tabs"]),{
                            Size=UDim2.new(0.721,0,0,0)
                        }):Play()
                        wait(cooldown["Tabs"] + .1)
                        v.Visible = true
                        ts:Create(Containers,tween(cooldown["Tabs"]),{
                            Size=UDim2.new(0.721,0,0.885,0)
                        }):Play()
                    else
                        v.Visible = false
                    end
                end
            end
        end)

        function secc:Section(Name)
            pgss = {}
            local Section = Instance.new("ImageLabel")
            local SectionLayout = Instance.new("UIListLayout")
            local SectionName = Instance.new("TextLabel")

            Section.Name = "Section"
            Section.Parent = Page
            Section.BackgroundColor3 = Color3.fromRGB(255,255,255)
            Section.BackgroundTransparency = 1.000
            Section.Position = UDim2.new(0.0150000192, 0, 0, 0)
            Section.Size = UDim2.new(0.970000088, 0, 0, 40)
            Section.Image = "rbxassetid://3570695787"
            Section.ImageColor3 = Options.theme.SchemeColor
            Section.ScaleType = Enum.ScaleType.Slice
            Section.SliceCenter = Rect.new(100, 100, 100, 100)
            Section.SliceScale = 0.060
            
            SectionLayout.Name = "SectionLayout"
            SectionLayout.Parent = Section
            SectionLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
            SectionLayout.SortOrder = Enum.SortOrder.LayoutOrder
            SectionLayout.Padding = UDim.new(0, 8)
            
            SectionName.Name = "SectionName"
            SectionName.Parent = Section
            SectionName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
            SectionName.BackgroundTransparency = 1.000
            SectionName.BorderSizePixel = 0
            SectionName.Position = UDim2.new(0.31272316, 0, 0, 0)
            SectionName.Size = UDim2.new(0.970000029, 0, 0, 40)
            SectionName.Font = Enum.Font.SourceSansBold
            SectionName.Text = Name
            SectionName.TextColor3 = Color3.fromRGB(255, 255, 255)
            SectionName.TextSize = 24.000
            SectionName.TextXAlignment = Enum.TextXAlignment.Left

            Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y)

            function pgss:Button(Name, callback, txtanimated)
                local BtnFunc = {}
                local Button = Instance.new("TextButton")
                local ButtonC = Instance.new("UICorner")
                
                Button.Name = Name .. " Button"
                Button.Parent = Section
                Button.BackgroundColor3 = Options.theme.ElementColor
                Button.BorderSizePixel = 0
                Button.Size = UDim2.new(0.959999979, 0, 0, 50)
                Button.Font = Enum.Font.SourceSansBold
                Button.Text = Name
                Button.TextColor3 = Color3.fromRGB(255, 255, 255)
                Button.TextSize = 24.000
                
                ButtonC.CornerRadius = UDim.new(0, 6)
                ButtonC.Name = "ButtonC"
                ButtonC.Parent = Button

                Section.Size = UDim2.new(0.97,0,0,SectionLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,13)
                Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,1)

                Button.MouseButton1Click:Connect(function()
                    callback()
                    if txtanimated == true or txtanimated ~= nil then
                        Button.TextSize = 18
                        task.wait(0.07)
                        Button.TextSize = 24
                    end
                end)

                function BtnFunc:UpdateText(Text)
                    Button.Text = Text
                end
                return BtnFunc
            end
            function pgss:Toggle(Name, callback, default)
                local enabled = false
                local togFunc = {}
                local Toggle = Instance.new("TextButton")
                local ToggleC = Instance.new("UICorner")
                local ToggleName = Instance.new("TextLabel")
                local Tog = Instance.new("TextButton")
                local TogC = Instance.new("UICorner")
                local Togg = Instance.new("ImageButton")
                
                Toggle.Name = "Toggle"
                Toggle.Parent = Section
                Toggle.BackgroundColor3 = Options.theme.ElementColor
                Toggle.BorderSizePixel = 0
                Toggle.Size = UDim2.new(0.959999979, 0, 0, 50)
                Toggle.Font = Enum.Font.SourceSansBold
                Toggle.Text = ""
                Toggle.TextColor3 = Color3.fromRGB(255, 255, 255)
                Toggle.TextSize = 24.000
                
                ToggleC.CornerRadius = UDim.new(0, 6)
                ToggleC.Name = "ToggleC"
                ToggleC.Parent = Toggle
                
                ToggleName.Name = "ToggleName"
                ToggleName.Parent = Toggle
                ToggleName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                ToggleName.BackgroundTransparency = 1.000
                ToggleName.BorderSizePixel = 0
                ToggleName.Position = UDim2.new(0.0149999997, 0, 0, 0)
                ToggleName.Size = UDim2.new(0.5, 0, 0, 50)
                ToggleName.Font = Enum.Font.SourceSansBold
                ToggleName.Text = Name or "Toggle"
                ToggleName.TextColor3 = Color3.fromRGB(255, 255, 255)
                ToggleName.TextSize = 24.000
                ToggleName.TextXAlignment = Enum.TextXAlignment.Left
                
                Tog.Name = "Tog"
                Tog.Parent = Toggle
                Tog.BackgroundColor3 = Options.theme.SchemeColor
                Tog.BorderSizePixel = 0
                Tog.Position = UDim2.new(0.907803178, 0, 0.100000001, 0)
                Tog.Size = UDim2.new(0.0790000036, 0, 0, 40)
                Tog.Font = Enum.Font.SourceSans
                Tog.Text = ""
                Tog.TextColor3 = Color3.fromRGB(0, 0, 0)
                Tog.TextSize = 14.000
                
                TogC.CornerRadius = UDim.new(0, 6)
                TogC.Name = "TogC"
                TogC.Parent = Tog
                
                Togg.Name = "Togg"
                Togg.Parent = Tog
                Togg.AnchorPoint = Vector2.new(0.5, 0.5)
                Togg.BackgroundTransparency = 1.000
                Togg.BorderSizePixel = 0
                Togg.Position = UDim2.new(0.5, 0, 0.5, 0)
                Togg.Size = UDim2.new(0, 0, 0, 0)
                Togg.Visible = true
                Togg.ZIndex = 2
                Togg.Image = "rbxassetid://3926305904"
                Togg.ImageRectOffset = Vector2.new(644, 204)
                Togg.ImageRectSize = Vector2.new(36, 36)

                Section.Size = UDim2.new(0.97,0,0,SectionLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,13)
                Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,1)

                if default then
                    enabled = true
                    Togg.Size = UDim2.new(0,25,0,25)
                    Tog.BackgroundColor3 = Color3.fromRGB(0,170,0)
                    callback(enabled)
                end

                local function Fire()
                    enabled = not enabled
                    if enabled then
                        ts:Create(Togg,tween(cooldown["Toggle"]),{
                            Size=UDim2.new(0,25,0,25)
                        }):Play()
                        ts:Create(Tog,tween(cooldown["Toggle"]),{
                            BackgroundColor3=Color3.fromRGB(0,170,0)
                        }):Play()
                    else
                        ts:Create(Togg,tween(cooldown["Toggle"]),{
                            Size=UDim2.new(0,0,0,0)
                        }):Play()
                        ts:Create(Tog,tween(cooldown["Toggle"]),{
                            BackgroundColor3=Options.theme.SchemeColor
                        }):Play()
                    end
                    if callback then
                        callback(enabled)
                    end
                end
                Toggle.MouseButton1Click:Connect(Fire)
                Togg.MouseButton1Click:Connect(Fire)
                Tog.MouseButton1Click:Connect(Fire)

                function togFunc:Toggle(set)
                    enabled = set
                    if set then
                        ts:Create(Togg,tween(cooldown["Toggle"]),{
                            Size=UDim2.new(0,25,0,25)
                        }):Play()
                        ts:Create(Tog,tween(cooldown["Toggle"]),{
                            BackgroundColor3=Color3.fromRGB(0,170,0)
                        }):Play()
                    else
                        ts:Create(Togg,tween(cooldown["Toggle"]),{
                            Size=UDim2.new(0,0,0,0)
                        }):Play()
                        ts:Create(Tog,tween(cooldown["Toggle"]),{
                            BackgroundColor3= Options.theme.SchemeColor
                        }):Play()
                    end
                    callback(enabled)
                end
                return togFunc
            end
            function pgss:Slider(Name, callback, min, max, default, precise)
                local moveconnection
                local Value;
                local Slider = Instance.new("ImageLabel")
                local SliderName = Instance.new("TextLabel")
                local SliderInner = Instance.new("TextButton")
                local SliderInnerC = Instance.new("UICorner")
                local SliderFrame = Instance.new("ImageLabel")
                local SliderCount = Instance.new("TextLabel")

                Slider.Name = "Slider"
                Slider.Parent = Section
                Slider.BackgroundColor3 = Color3.fromRGB(255,255,255)
                Slider.BackgroundTransparency = 1.000
                Slider.Size = UDim2.new(0.959999979, 0, 0, 70)
                Slider.Image = "rbxassetid://3570695787"
                Slider.ImageColor3 = Options.theme.ElementColor
                Slider.ScaleType = Enum.ScaleType.Slice
                Slider.SliceCenter = Rect.new(100, 100, 100, 100)
                Slider.SliceScale = 0.060

                SliderName.Name = "SliderName"
                SliderName.Parent = Slider
                SliderName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                SliderName.BackgroundTransparency = 1.000
                SliderName.BorderSizePixel = 0
                SliderName.Position = UDim2.new(0.0149999997, 0, 0, 0)
                SliderName.Size = UDim2.new(0, 200, 0, 40)
                SliderName.Font = Enum.Font.SourceSansBold
                SliderName.Text = Name or "Slider"
                SliderName.TextColor3 = Color3.fromRGB(255, 255, 255)
                SliderName.TextSize = 24.000
                SliderName.TextXAlignment = Enum.TextXAlignment.Left

                SliderInner.Name = "SliderInner"
                SliderInner.Parent = Slider
                SliderInner.BackgroundColor3 = Options.theme.SchemeColor
                SliderInner.BorderSizePixel = 0
                SliderInner.Position = UDim2.new(0.0149999876, 0, 0.680000067, 0)
                SliderInner.Size = UDim2.new(0.97, 0, 0, 15)
                SliderInner.Font = Enum.Font.SourceSans
                SliderInner.Text = ""
                SliderInner.TextColor3 = Color3.fromRGB(0, 0, 0)
                SliderInner.TextSize = 14.000

                SliderInnerC.CornerRadius = UDim.new(0, 6)
                SliderInnerC.Name = "SliderInnerC"
                SliderInnerC.Parent = SliderInner

                SliderFrame.Name = "SliderFrame"
                SliderFrame.Parent = SliderInner
                SliderFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                SliderFrame.BackgroundTransparency = 1.000
                SliderFrame.Size = UDim2.new(0, 100, 0, 15)
                SliderFrame.Image = "rbxassetid://3570695787"
                SliderFrame.ScaleType = Enum.ScaleType.Slice
                SliderFrame.SliceCenter = Rect.new(100, 100, 100, 100)
                SliderFrame.SliceScale = 0.060

                SliderCount.Name = "SliderCount"
                SliderCount.Parent = Slider
                SliderCount.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                SliderCount.BackgroundTransparency = 1.000
                SliderCount.BorderSizePixel = 0
                SliderCount.Position = UDim2.new(0.905852377, 0, 0, 0)
                SliderCount.Size = UDim2.new(0.0790000036, 0, 0, 40)
                SliderCount.Font = Enum.Font.SourceSansBold
                SliderCount.Text = min or "0"
                SliderCount.TextColor3 = Color3.fromRGB(255, 255, 255)
                SliderCount.TextSize = 24.000
                SliderCount.TextXAlignment = Enum.TextXAlignment.Right

                Section.Size = UDim2.new(0.97,0,0,SectionLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,13)
                Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,1)

                --This were used from Zypher ui library, huge thanks to xTheAlex14 who made an open source ui library
                if default then
                    SliderCount.Text = tostring(default)
                    local def = (default - min) / (max - min)
                    ts:Create(SliderFrame,tween(cooldown["Slider"]),{
                        Size=UDim2.new(def,0,0,15)
                    }):Play()
                    callback(default)
                end

                SliderInner.MouseButton1Down:Connect(function()
                    moveconnection = rs.Heartbeat:Connect(function()
                        local s = math.clamp(mouse.X - SliderInner.AbsolutePosition.X, 0, SliderInner.AbsoluteSize.X) / SliderInner.AbsoluteSize.X
                        if precise then
                            Value = string.format("%.1f", min + ((max - min) * s))
                        else
                            Value = math.floor(min + ((max - min) * s))
                        end
                        SliderCount.Text = tostring(Value)

                        if callback then
                            callback(Value)
                        end

                        ts:Create(SliderFrame, TweenInfo.new(0.05), {
                            Size = UDim2.new(s, 0, 0, 15)
                        }):Play()
                    end)

                    uis.InputEnded:Connect(function(Check)
                        if Check.UserInputType == Enum.UserInputType.MouseButton1 then
                            if moveconnection then
                                moveconnection:Disconnect()
                                moveconnection = nil
                            end
                        end
                    end)
                end)
                --Thanks alot for these script above, from zypher lib
            end
            function pgss:DropDown(Name, List, callback)
                local DropFunc = {}
                local isDropped = false
                local default = ''

                local DropDown = Instance.new("TextButton")
                local DropDownC = Instance.new("UICorner")
                local DropDownName = Instance.new("TextLabel")
                local Open = Instance.new("TextButton")
                local OpenC = Instance.new("UICorner")
                local DropContainers = Instance.new("ImageLabel")
                local DropFrame = Instance.new("ScrollingFrame")
                local DropFrameLayout = Instance.new("UIListLayout")

                DropDown.Name = "DropDown"
                DropDown.Parent = Section
                DropDown.BackgroundColor3 = Options.theme.ElementColor
                DropDown.BorderSizePixel = 0
                DropDown.Size = UDim2.new(0.959999979, 0, 0, 50)
                DropDown.Font = Enum.Font.SourceSansBold
                DropDown.Text = ""
                DropDown.TextColor3 = Color3.fromRGB(255, 255, 255)
                DropDown.TextSize = 24.000
                
                DropDownC.CornerRadius = UDim.new(0, 6)
                DropDownC.Name = "DropDownC"
                DropDownC.Parent = DropDown
                
                DropDownName.Name = "DropDownName"
                DropDownName.Parent = DropDown
                DropDownName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                DropDownName.BackgroundTransparency = 1.000
                DropDownName.BorderSizePixel = 0
                DropDownName.Position = UDim2.new(0.0149999997, 0, 0, 0)
                DropDownName.Size = UDim2.new(0.5, 0, 0, 50)
                DropDownName.Font = Enum.Font.SourceSansBold
                DropDownName.Text = Name or "DropDown"
                DropDownName.TextColor3 = Color3.fromRGB(255, 255, 255)
                DropDownName.TextSize = 24.000
                DropDownName.TextXAlignment = Enum.TextXAlignment.Left
                
                Open.Name = "Open"
                Open.Parent = DropDown
                Open.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
                Open.BorderSizePixel = 0
                Open.Position = UDim2.new(0.916344404, 0, 0.150000006, 0)
                Open.Size = UDim2.new(0.0700000003, 0, 0, 35)
                Open.Font = Enum.Font.SourceSans
                Open.Text = ""
                Open.TextColor3 = Color3.fromRGB(0, 0, 0)
                Open.TextSize = 14.000
                
                OpenC.CornerRadius = UDim.new(0, 6)
                OpenC.Name = "OpenC"
                OpenC.Parent = Open
                
                DropContainers.Name = "DropContainers"
                DropContainers.Parent = Section
                DropContainers.ClipsDescendants = true
                DropContainers.BackgroundColor3 = Color3.fromRGB(255,255,255)
                DropContainers.BackgroundTransparency = 1.000
                DropContainers.Position = UDim2.new(0.0199998878, 0, 0.580270767, 0)
                DropContainers.Size = UDim2.new(0.959999979, 0, 0, 0)
                DropContainers.Visible = false
                DropContainers.Image = "rbxassetid://3570695787"
                DropContainers.ImageColor3 = Options.theme.ElementColor
                DropContainers.ScaleType = Enum.ScaleType.Slice
                DropContainers.SliceCenter = Rect.new(100, 100, 100, 100)
                DropContainers.SliceScale = 0.060
                
                DropFrame.Name = "DropFrame"
                DropFrame.Parent = DropContainers
                DropFrame.Active = true
                DropFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                DropFrame.BackgroundTransparency = 1.000
                DropFrame.BorderSizePixel = 0
                DropFrame.Position = UDim2.new(0, 0, 0.0500000007, 0)
                DropFrame.Size = UDim2.new(1, 0, 0, 190)
                DropFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
                DropFrame.ScrollBarThickness = 6
                
                DropFrameLayout.Name = "DropFrameLayout"
                DropFrameLayout.Parent = DropFrame
                DropFrameLayout.HorizontalAlignment = Enum.HorizontalAlignment.Center
                DropFrameLayout.SortOrder = Enum.SortOrder.LayoutOrder
                DropFrameLayout.Padding = UDim.new(0, 8)

                Section.Size = UDim2.new(0.97,0,0,SectionLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,13)
                Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,1)

                local SectionDrop_Y = 217

                local function Fire()
                    isDropped = not isDropped
                    if isDropped then
                        DropContainers.Visible = true
                        ts:Create(Open,tween(cooldown["DropDown"]),{
                            BackgroundColor3 = Color3.fromRGB(0,255,0)
                        }):Play()
                        ts:Create(DropContainers,tween(cooldown["DropDown"]),{
                            Size=UDim2.new(0.96,0,0,210)
                        }):Play()
                        ts:Create(Page,tween(cooldown["DropDown"]),{
                            CanvasSize = Page.CanvasSize + UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        ts:Create(Section,tween(cooldown["DropDown"]),{
                            Size = Section.Size + UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        DropDownName.Text = Name
                    else
                        ts:Create(Open,tween(cooldown["DropDown"]),{
                            BackgroundColor3 = Color3.fromRGB(255,0,0)
                        }):Play()
                        ts:Create(DropContainers,tween(cooldown["DropDown"]),{
                            Size=UDim2.new(0.96,0,0,0)
                        }):Play()
                        ts:Create(Page,tween(cooldown["DropDown"]),{
                            CanvasSize = Page.CanvasSize - UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        ts:Create(Section,tween(cooldown["DropDown"]),{
                            Size = Section.Size - UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        task.wait(cooldown["DropDown"])
                        DropContainers.Visible = false
                        if default ~= '' then
                            DropDownName.Text = default
                        else
                            DropDownName.Text = Name
                        end
                    end
                end
                DropDown.MouseButton1Click:Connect(Fire)
                Open.MouseButton1Click:Connect(Fire)

                local DropAmount = 0
                for i,v in next, List do
                    DropAmount = DropAmount + 1
                    local Button = Instance.new("TextButton")
                    local ButtonC = Instance.new("UICorner")
                    
                    Button.Name = DropAmount
                    Button.Parent = DropFrame
                    Button.BackgroundColor3 = Options.theme.SchemeColor
                    Button.BorderSizePixel = 0
                    Button.Size = UDim2.new(0.970000029, 0, 0, 40)
                    Button.Font = Enum.Font.SourceSansBold
                    Button.Text = v
                    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
                    Button.TextSize = 24.000
                    
                    ButtonC.CornerRadius = UDim.new(0, 6)
                    ButtonC.Name = "ButtonC"
                    ButtonC.Parent = Button

                    Button.MouseButton1Click:Connect(function()
                        if callback then
                            callback(v)
                        end
                        isDropped = false
                        ts:Create(Open,tween(cooldown["DropDown"]),{
                            BackgroundColor3 = Color3.fromRGB(255,0,0)
                        }):Play()
                        ts:Create(DropContainers,tween(cooldown["DropDown"]),{
                            Size=UDim2.new(0.96,0,0,0)
                        }):Play()
                        ts:Create(Page,tween(cooldown["DropDown"]),{
                            CanvasSize = Page.CanvasSize - UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        ts:Create(Section,tween(cooldown["DropDown"]),{
                            Size = Section.Size - UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        task.wait(cooldown["DropDown"])
                        DropContainers.Visible = false
                        default = Button.Text
                        DropDownName.Text = Button.Text
                    end)

                end

                function DropFunc:Add(Text)
                    local Button = Instance.new("TextButton")
                    local ButtonC = Instance.new("UICorner")
                    
                    Button.Name = DropAmount
                    Button.Parent = DropFrame
                    Button.BackgroundColor3 = Options.theme.SchemeColor
                    Button.BorderSizePixel = 0
                    Button.Size = UDim2.new(0.970000029, 0, 0, 40)
                    Button.Font = Enum.Font.SourceSansBold
                    Button.Text = Text
                    Button.TextColor3 = Color3.fromRGB(255, 255, 255)
                    Button.TextSize = 24.000
                    
                    ButtonC.CornerRadius = UDim.new(0, 6)
                    ButtonC.Name = "ButtonC"
                    ButtonC.Parent = Button

                    Button.MouseButton1Click:Connect(function()
                        if callback then
                            callback(v)
                        end
                        isDropped = false
                        ts:Create(Open,tween(cooldown["DropDown"]),{
                            BackgroundColor3 = Color3.fromRGB(255,0,0)
                        }):Play()
                        ts:Create(DropContainers,tween(cooldown["DropDown"]),{
                            Size=UDim2.new(0.96,0,0,0)
                        }):Play()
                        ts:Create(Page,tween(cooldown["DropDown"]),{
                            CanvasSize = Page.CanvasSize - UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        ts:Create(Section,tween(cooldown["DropDown"]),{
                            Size = Section.Size - UDim2.new(0,0,0,SectionDrop_Y)
                        }):Play()
                        task.wait(cooldown["DropDown"])
                        DropContainers.Visible = false
                        default = Button.Text
                        DropDownName.Text = Button.Text
                    end)
                end

                function DropFunc:Remove(id)
                    if DropContainers[id] ~= nil then
                        for i,v in pairs(DropContainers:FindFirstChild(id)) do
                            v:Destroy()
                        end
                    end
                end

                function DropFunc:Clear(Text)
                    for i,v in pairs(DropContainers:GetChildren()) do
                        if v:IsA("GuiButton") then
                            DropContainers:Remove(i)
                        end
                    end
                end
                return DropFunc

            end
            function pgss:TextBox(Name, callback, text)
                local TextBox = Instance.new("TextButton")
                local TextBoxC = Instance.new("UICorner")
                local TextBoxName = Instance.new("TextLabel")
                local TypeBox = Instance.new("TextBox")
                local TypeBoxC = Instance.new("UICorner")
                
                TextBox.Name = "TextBox"
                TextBox.Parent = Section
                TextBox.BackgroundColor3 = Options.theme.ElementColor
                TextBox.BorderSizePixel = 0
                TextBox.Size = UDim2.new(0.959999979, 0, 0, 50)
                TextBox.Font = Enum.Font.SourceSansBold
                TextBox.Text = ""
                TextBox.TextColor3 = Color3.fromRGB(255, 255, 255)
                TextBox.TextSize = 24.000
                
                TextBoxC.CornerRadius = UDim.new(0, 6)
                TextBoxC.Name = "TextBoxC"
                TextBoxC.Parent = TextBox
                
                TextBoxName.Name = "TextBoxName"
                TextBoxName.Parent = TextBox
                TextBoxName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                TextBoxName.BackgroundTransparency = 1.000
                TextBoxName.BorderSizePixel = 0
                TextBoxName.Position = UDim2.new(0.0149999997, 0, 0, 0)
                TextBoxName.Size = UDim2.new(0.5, 0, 0, 50)
                TextBoxName.Font = Enum.Font.SourceSansBold
                TextBoxName.Text = Name or "TextBox"
                TextBoxName.TextColor3 = Color3.fromRGB(255, 255, 255)
                TextBoxName.TextSize = 24.000
                TextBoxName.TextXAlignment = Enum.TextXAlignment.Left
                
                TypeBox.Name = "TypeBox"
                TypeBox.Parent = TextBox
                TypeBox.BackgroundColor3 = Options.theme.SchemeColor
                TypeBox.BorderSizePixel = 0
                TypeBox.Position = UDim2.new(0.632532716, 0, 0.140000001, 0)
                TypeBox.Size = UDim2.new(0.349999994, 0, 0, 35)
                TypeBox.Font = Enum.Font.SourceSans
                TypeBox.PlaceholderText = text or "Type here"
                TypeBox.Text = ""
                TypeBox.TextColor3 = Color3.fromRGB(255, 255, 255)
                TypeBox.TextSize = 24.000
                TypeBox.TextXAlignment = Enum.TextXAlignment.Right
                
                TypeBoxC.CornerRadius = UDim.new(0, 6)
                TypeBoxC.Name = "TypeBoxC"
                TypeBoxC.Parent = TypeBox

                Section.Size = UDim2.new(0.97,0,0,SectionLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,13)
                Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,1)

                TypeBox.FocusLost:Connect(function(enterPressed, inputThatCausedFocusLoss)
                    if not enterPressed then
                        return
                    else
                        callback(TypeBox.Text)
                        task.wait(.018)
                        TypeBox.Text = ""
                    end
                end)
            end
            function pgss:Keybind(Name, callback, bind)
                local Keybind = Instance.new("TextButton")
                local KeybindC = Instance.new("UICorner")
                local KeybindName = Instance.new("TextLabel")
                local Bind = Instance.new("TextLabel")
                
                Keybind.Name = "Keybind"
                Keybind.Parent = Section
                Keybind.BackgroundColor3 = Options.theme.ElementColor
                Keybind.BorderSizePixel = 0
                Keybind.Size = UDim2.new(0.959999979, 0, 0, 50)
                Keybind.Font = Enum.Font.SourceSansBold
                Keybind.Text = ""
                Keybind.TextColor3 = Color3.fromRGB(255, 255, 255)
                Keybind.TextSize = 24.000
                
                KeybindC.CornerRadius = UDim.new(0, 6)
                KeybindC.Name = "KeybindC"
                KeybindC.Parent = Keybind
                
                KeybindName.Name = "KeybindName"
                KeybindName.Parent = Keybind
                KeybindName.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
                KeybindName.BackgroundTransparency = 1.000
                KeybindName.BorderSizePixel = 0
                KeybindName.Position = UDim2.new(0.0149999997, 0, 0, 0)
                KeybindName.Size = UDim2.new(0.5, 0, 0, 50)
                KeybindName.Font = Enum.Font.SourceSansBold
                KeybindName.Text = Name or "Keybind"
                KeybindName.TextColor3 = Color3.fromRGB(255, 255, 255)
                KeybindName.TextSize = 24.000
                KeybindName.TextXAlignment = Enum.TextXAlignment.Left
                
                Bind.Name = "Bind"
                Bind.Parent = Keybind
                Bind.BackgroundColor3 = Options.theme.SchemeColor
                Bind.BackgroundTransparency = 1.000
                Bind.BorderSizePixel = 0
                Bind.Position = UDim2.new(0.632532716, 0, 0.140000001, 0)
                Bind.Size = UDim2.new(0.335678488, 0, 0, 35)
                Bind.Font = Enum.Font.SourceSans
                Bind.Text = "[NONE]"
                Bind.TextColor3 = Color3.fromRGB(255, 255, 255)
                Bind.TextSize = 24.000
                Bind.TextXAlignment = Enum.TextXAlignment.Right

                Section.Size = UDim2.new(0.97,0,0,SectionLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,13)
                Page.CanvasSize = UDim2.new(0,0,0,PageLayout.AbsoluteContentSize.Y) + UDim2.new(0,0,0,1)

                local changing
                local oldKey

                Keybind.MouseButton1Click:Connect(function()
                    changing = true
                    Bind.Text = "..."
                    local a = uis.InputBegan:Wait()
                    if a.KeyCode.Name ~= "Unknown" then
                        Bind.Text = a.KeyCode.Name
                        oldKey = a.KeyCode.Name
                        wait(0.02)
                        changing = false
                    end
                end)

                uis.InputBegan:Connect(function(input, gameProcessedEvent)
                    if input.KeyCode.Name == oldKey then
                        if callback and not changing then
                            callback()
                        end
                    end
                end)
            end
            return pgss
        end
        return secc
    end
    return tbss
end
return lib
