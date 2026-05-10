
# Interface




## Config Manager

```lua
local ConfigManager = Arcane:ConfigManager({
	Directory = "Arcane-UI",
	Config = "Example-Configs",
});
```

```
Directory: Folder in workspace
Config: Config Folder for your script
```

## Loading Animation

```lua
Arcane:Loader("rbxassetid://120245531583106", 2.5).yield();
```

## Creating Window

```lua
local Window = Arcane.new({
	Name = "Arcane",
	Keybind = "LeftAlt",
	Logo = "rbxassetid://120245531583106",
	Scale = Arcane.Scale.Window, -- Leave blank if you want automatic scale for PC and Mobile.
	TextSize = 15,
});
```

## Creating Watermark

```lua
local Watermark = Window:Watermark();
```

```lua
local Time = Watermark:AddText({
	Icon = "timer",
	Text = "TIME",
});

task.spawn(function()
	while true do task.wait()
		Time:SetText(Arcane:GetTimeNow());
	end
end)
```

## Creating Tab Category

```lua
Window:DrawCategory({
	Name = "Category"
});
```

## Creating Tab (Normal)

```lua
local NormalTab = Window:DrawTab({
	Name = "Example Tab",
	Icon = "apple",
});
```

## Creating Tab (Single)

```lua
local NormalTab = Window:DrawTab({
	Name = "Example Tab",
	Icon = "apple",
	Type = "Single",
});
```

## Creating Container Tab

<figure><img src="/files/2XekL9G6CArtzBk3QOCA" alt=""><figcaption><p>Container Tab Preview</p></figcaption></figure>

```lua
local ContainerTab = Window:DrawContainerTab({
	Name = "Extract Tabs",
	Icon = "contact",
});

-- Creating Tab (Normal) --
local ExtractTab = ContainerTab:DrawTab({
	Name = "Tab 1",
	Type = "Double"
});

-- Creating Tab (Single) --
local SingleExtractTab = ContainerTab:DrawTab({
	Name = "Tab 2",
	Type = "Single",
	EnableScrolling = true, -- this will make tab can scrolling (recommend)
});
```

## Creating Section

```lua
local NormalSection = NormalTab:DrawSection({
	Name = "Section",
	Position = 'left'	
});
```

## Creating Toggle

```lua
local Toggle = NormalSection:AddToggle({
	Name = "Toggle",
	Flag = "Toggle_Example", -- Leave it blank will not save to config (ALL ELEMENTS)
	Default = false,
	Callback = print,
});
```

### Element Link

<figure><img src="/files/KBR3Z8EO9C3tBwDntOmg" alt=""><figcaption><p>Example</p></figcaption></figure>

Link is available for **Toggle Slider Keybind Color Picker**

#### Link Keybind

```lua
Element.Link:AddKeybind({
	Default = "E",
	Flag = "Option_Keybind",
	Callback = print
});
```

#### Link Helper

```lua
Element.Link:AddHelper({
	Text = "Helper Text"
})
```

#### Link Color Picker

```lua
Element.Link:AddColorPicker({
	Default = Color3.fromRGB(255,255,255),
	Callback = print
})
```

#### Link Option

<figure><img src="/files/7DuuZoVyl26F2fiyjBbq" alt=""><figcaption><p>Link Option Preview</p></figcaption></figure>

"Option" it's "Section" but in "element"

```lua
local Option = Toggle.Link:AddOption()

Option:AddToggle({
	Name = "Toggle in option!",
	Callback = print
})
```

## Creating Keybind

```lua
NormalSection:AddKeybind({
	Name = "Keybind",
	Default = "LeftAlt",
	Flag = "Keybind_Example",
	Callback = print,
});
```

## Creating Slider

```lua
NormalSection:AddSlider({
	Name = "Slider",
	Min = 0,
	Max = 100,
	Default = 50,
	Round = 0,
	Flag = "Slider_Example",
	Callback = print
});
```

## Creating ColorPicker

```lua
NormalSection:AddColorPicker({
	Name = "ColorPicker",
	Default = Color3.fromRGB(0, 255, 140),
	Flag = "Color_Picker_Example",
	Callback = print
})
```

## Creating Dropdown

```lua
NormalSection:AddDropdown({
	Name = "Single Dropdown",
	Default = "Head",
	Flag = "Single_Dropdown",
	Values = {"Head","Body","Arms","Legs"},
	Callback = print
})
```

### Multi Dropdown

```lua
NormalSection:AddDropdown({
	Name = "Multi Dropdown",
	Default = {"Head"},
	Multi = true,
	Flag = "Multi_Dropdown",
	Values = {"Head","Body","Arms","Legs"},
	Callback = print
})
```

## Creating Button

```lua
NormalSection:AddButton({
	Name = "Button",
	Callback = function()
		print('PRINT!')
	end,
})
```

## Creating Paragraph

<pre class="language-lua"><code class="lang-lua"><strong>NormalSection:AddParagraph({
</strong>	Title = "Paragraph",
	Content = "Very cool paragraph"
})
</code></pre>

## Creating Config Tab

```lua
local ConfigUI = Window:DrawConfig({
	Name = "Config",
	Icon = "folder",
	Config = ConfigManager, -- Config Manager (required)
});

ConfigUI:Init();
```

<figure><img src="/files/4JamuHMlEfW8RCJgZpLn" alt=""><figcaption><p>Config Tab Preview</p></figcaption></figure>

## Config Manager

### Write Config

write current value to config

```lua
ConfigManager:WriteConfig({
	Name = "Config Name",
	Author = "Creator Name"
})
```

### Read Info

read config info. Ex: Author and Created date

```lua
ConfigManager:ReadInfo("<Config Name>")
```

### Load Config

Load the config in directory

```lua
ConfigManager:LoadConfig("<Config Name>")
```

### Delete Config

Delete the config in directory

```lua
ConfigManager:DeleteConfig("<Config Name>")
```

### Get Configs

get all configs in directory

```lua
ConfigManager:GetConfigs()
```

### Directory Path

config directory path

```lua
ConfigManager.Directory
```


---

