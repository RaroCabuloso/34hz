# Akiri Lib

Akiri Lib é uma biblioteca de interface para Roblox baseada em `Drawing`, focada em criar janelas, tabs, sections e componentes visuais com tema personalizável, sistema de notificações, keybinds, salvamento de configurações e controles como toggle, slider, dropdown, colorpicker, textbox, button e label. A lib também inclui utilitários internos para gerenciamento de drawings, conexões, drag, cursor customizado, cache de imagens e troca dinâmica de tema.

## Recursos

- Janela principal com tabs e sections
- Loader de inicialização
- Sistema de tema dinâmico
- Notificações
- Keybind list
- Cursor customizado
- Salvamento e carregamento de configs por `PlaceId`
- Componentes:
  - Toggle
  - Slider
  - Button
  - TextBox
  - Colorpicker
  - Dropdown
  - Keybind
  - Label
- Controle de visibilidade da UI
- Destruição limpa da interface e conexões

---

## Instalação

Exemplo de carregamento da lib:

    local Library = loadstring(game:HttpGet("URL_DA_SUA_LIB"))()

Depois disso, a janela principal pode ser criada normalmente.

Exemplo:

    local Window = Library.Window("Meu Menu", Vector2.new(600, 450))

---

## Estrutura principal

A lib expõe dois objetos globais:

- `Library`
- `Utility`

Além disso, ela usa internamente:

- `Library.Theme`
- `Library.Flags`
- `Library.Items`
- `Library.Drawings`
- `Library.Connections`
- `Library.Keybind`
- `Library.Watermark`
- `Library.Ignores`

---

## Exemplo básico de uso

    local Library = loadstring(game:HttpGet("URL_DA_SUA_LIB"))()

    local Window = Library.Window("Akiri Demo", Vector2.new(620, 470))
    local MainTab = Window:Tab("Main")
    local LeftSection = MainTab:Section("Player", "Left")

    LeftSection:Toggle({
        Title = "Auto Jump",
        State = false,
        Flag = "AutoJump",
        Callback = function(State)
            print("AutoJump:", State)
        end
    })

    LeftSection:Button({
        Title = "Print Hello",
        Callback = function()
            print("Hello!")
        end
    })

---

## Tabela de objetos

### Library

Objeto principal da lib.

Campos mais importantes:

- `Theme`
- `Icons`
- `Flags`
- `Items`
- `Drawings`
- `Ignores`
- `Keybind`
- `Watermark`
- `Connections`
- `Keys`
- `Input`
- `Images`
- `WindowVisible`
- `Communication`

---

## Theme

`Library.Theme` controla aparência geral da interface.

Campos principais:

- `Accent` — lista de cores de destaque
- `Notification.Error`
- `Notification.Warning`
- `Hitbox`
- `Friend`
- `Outline`
- `Inline`
- `LightContrast`
- `DarkContrast`
- `Text`
- `TextInactive`
- `Font`
- `TextSize`
- `UseOutline`

### Atualização de tema

    Library:UpdateTheme({
        Accent = Color3.fromRGB(180, 0, 255),
        Outline = Color3.fromRGB(0, 0, 0),
        Inline = Color3.fromRGB(50, 50, 50),
        LightContrast = Color3.fromRGB(35, 35, 35),
        DarkContrast = Color3.fromRGB(20, 20, 20),
        Text = Color3.fromRGB(255, 255, 255),
        TextInactive = Color3.fromRGB(180, 180, 180)
    })

---

## Library.Window(title, size)

Cria uma janela principal.

### Parâmetros

- `Title` — nome exibido na janela
- `Size` — `Vector2` com largura e altura

### Retorno

Retorna uma instância `Window`.

### Exemplo

    local Window = Library.Window("Akiri Lib", Vector2.new(600, 450))

---

## Métodos da janela

### Window:Tab(title)

Cria uma nova tab.

#### Parâmetros

- `title` — nome da tab

#### Retorno

Retorna um objeto `Tab`.

#### Exemplo

    local Combat = Window:Tab("Combat")

---

### Window:AddSettingsTab(Additional)

Cria uma tab de configurações com opções de tema e presets.

#### Parâmetros

- `Additional` — função opcional executada junto com a construção da tab

#### Exemplo

    Window:AddSettingsTab(function()
        print("Settings carregadas")
    end)

---

### Window:SwitchTab(tab)

Troca a tab ativa.

#### Parâmetros

- `tab` — objeto tab retornado por `Window:Tab(...)`

---

### Window:RefreshPages()

Recalcula o tamanho e layout das tabs/sections.

---

### Window:ChangeAnime(name)

Troca a imagem/anime do overlay visual.

Valores esperados:

- `Astolfo`
- `Aiko`
- `Rem`
- `Violet`
- `Asuka`

---

### Window:ToggleAnime(state)

Liga ou desliga o overlay anime.

#### Parâmetros

- `state` — `true` ou `false`

---

### Window:SendNotification(type, title, duration)

Exibe uma notificação na tela.

#### Parâmetros

- `type` — `Normal`, `Warning` ou `Error`
- `title` — texto da notificação
- `duration` — tempo em segundos

#### Exemplo

    Window:SendNotification("Normal", "Carregado com sucesso", 3)

---

## Tab

Objeto retornado por `Window:Tab(title)`.

Ele organiza as sections e os componentes dentro da página.

Campos internos mais relevantes:

- `Render`
- `Sections`
- `Dropdowns`
- `SectionAxis`
- `CurrentTab`

---

## Tab:Section(title, side)

Cria uma section dentro da tab.

### Parâmetros

- `title` — título da section
- `side` — `"Left"` ou `"Right"`

### Retorno

Retorna um objeto `Section`.

### Exemplo

    local PlayerSection = Combat:Section("Player", "Left")

---

## Section

Uma section é o bloco onde os componentes ficam agrupados.

### Componentes disponíveis

- `Section:Toggle(...)`
- `Section:Slider(...)`
- `Section:Button(...)`
- `Section:TextBox(...)`
- `Section:Colorpicker(...)`
- `Section:Dropdown(...)`
- `Section:Label(...)`
- `Section:Keybind(...)`

---

## Section:Toggle(options)

Cria uma chave liga/desliga.

### Parâmetros

- `Title` — nome exibido
- `State` — estado inicial
- `Flag` — nome da flag
- `Type` — tipo visual opcional
- `Callback` — função chamada ao alterar

### Retorno

Retorna um objeto `Toggle`.

### Exemplo

    PlayerSection:Toggle({
        Title = "Godmode",
        State = false,
        Flag = "Godmode",
        Callback = function(State)
            print(State)
        end
    })

### Métodos retornados pelo Toggle

#### Toggle:Colorpicker(options)

Adiciona um colorpicker acoplado ao toggle.

#### Toggle:Keybind(options)

Adiciona um keybind acoplado ao toggle.

---

## Section:Slider(options)

Cria um slider numérico.

### Parâmetros

- `Title` — nome exibido
- `Default` — valor inicial
- `Min` — valor mínimo
- `Max` — valor máximo
- `Decimals` — precisão
- `Symbol` — sufixo visual
- `Flag` — nome da flag
- `Callback` — função chamada ao mudar

### Retorno

Retorna um objeto `Slider`.

### Exemplo

    PlayerSection:Slider({
        Title = "Speed",
        Default = 16,
        Min = 0,
        Max = 100,
        Decimals = 1,
        Symbol = "x",
        Flag = "SpeedValue",
        Callback = function(Value)
            print(Value)
        end
    })

### Métodos retornados pelo Slider

#### Slider:Set(value)

Define o valor atual.

#### Slider:SetMax(value)

Atualiza o máximo.

#### Slider:SetMin(value)

Atualiza o mínimo.

#### Slider:Refresh()

Recalcula o valor com base na posição do mouse enquanto arrasta.

#### Slider:SetText(text)

Altera o texto exibido.

---

## Section:Button(options)

Cria um botão clicável.

### Parâmetros

- `Title` — texto do botão
- `Callback` — função executada ao clicar

### Exemplo

    PlayerSection:Button({
        Title = "Executar",
        Callback = function()
            print("Botão clicado")
        end
    })

### Comportamento

- Clique esquerdo executa o callback
- O botão faz um efeito visual curto ao ser pressionado

---

## Section:TextBox(options)

Cria um campo de texto.

### Parâmetros

- `Title` — rótulo do campo
- `Current` — texto inicial
- `Flag` — nome da flag
- `Callback` — função executada ao confirmar a entrada

### Exemplo

    PlayerSection:TextBox({
        Title = "Nick",
        Current = "",
        Flag = "PlayerNick",
        Callback = function(Text)
            print(Text)
        end
    })

### Observações

- Clique no campo para ativar a escrita
- `Backspace` apaga caracteres
- `Enter` confirma o texto
- A lib usa um `TextBox` invisível interno para capturar teclado

### Métodos retornados pelo TextBox

No source atual existe um `TextBox:Set()`, mas ele está vazio.

---

## Section:Colorpicker(options)

Cria um seletor de cor.

### Parâmetros

- `Title` — nome exibido
- `Color` — cor inicial (`Color3`)
- `Flag` — nome da flag
- `Callback` — função chamada ao alterar a cor

### Exemplo

    PlayerSection:Colorpicker({
        Title = "ESP Color",
        Color = Color3.fromRGB(255, 0, 0),
        Flag = "ESPColor",
        Callback = function(Color)
            print(Color)
        end
    })

### Recursos

- Seletor HSV
- Campo hex
- Campo RGB
- Opção `Rainbow`
- Arraste de saturação e hue

### Métodos retornados pelo Colorpicker

#### Colorpicker:Drop(state)

Abre ou fecha o painel interno do colorpicker.

#### Colorpicker:SetHue(options)

Define o hue.

#### Colorpicker:RefreshHue()

Atualiza o hue com o mouse.

#### Colorpicker:SetSaturationX(options)

Define a saturação no eixo X.

#### Colorpicker:SetSaturationY(options)

Define a saturação no eixo Y.

#### Colorpicker:RefreshSaturation()

Atualiza saturação com o mouse.

### Opção Rainbow

Quando ativado, a cor muda dinamicamente em loop.

---

## Section:Dropdown(options)

Cria um dropdown de seleção.

### Parâmetros

- `Title` — nome exibido
- `List` — lista de opções
- `Default` — opção inicial
- `Flag` — nome da flag
- `Callback` — função chamada ao selecionar

### Exemplo

    PlayerSection:Dropdown({
        Title = "Weapon",
        List = {"Sword", "Gun", "Knife"},
        Default = "Sword",
        Flag = "SelectedWeapon",
        Callback = function(Item)
            print(Item)
        end
    })

### Métodos retornados pelo Dropdown

#### Dropdown:Set(selected)

Define a opção selecionada.

#### Dropdown:ShowList(state)

Mostra ou esconde a lista de opções.

---

## Section:Label(title)

Cria um texto simples.

### Exemplo

    PlayerSection:Label("Informação da seção")

### Métodos retornados pelo Label

#### Label:Set(text)

Altera o texto exibido.

---

## Section:Keybind(options)

Cria um sistema de tecla de atalho.

### Parâmetros

- `Title` — nome exibido
- `Key` — tecla ou input inicial
- `StateType` — `"Hold"`, `"Toggle"` ou `"Always"`
- `Flag` — nome da flag
- `Callback` — função chamada ao disparar

### Exemplo

    PlayerSection:Keybind({
        Title = "Open Menu",
        Key = Enum.KeyCode.RightShift,
        StateType = "Toggle",
        Flag = "OpenMenuBind",
        Callback = function(State, Key)
            print(State, Key)
        end
    })

### Modos

- `Hold` — ativa enquanto a tecla estiver pressionada
- `Toggle` — alterna entre ligado e desligado
- `Always` — fica sempre ativo

### Métodos retornados pelo Keybind

#### Keybind:Drop(state)

Mostra ou esconde as opções de modo.

#### Keybind:SetStateType(state)

Altera o modo atual.

#### Keybind:RemoveFromKeyBindGui()

Remove o item da lista visual de keybinds.

### Observações

- Clique esquerdo no campo do keybind para começar a rebinding
- Clique direito abre/fecha o menu interno do keybind
- O texto do keybind aparece na Keybind List da janela

---

## Library:ChangeVisible(state)

Mostra ou esconde a interface inteira.

### Exemplo

    Library:ChangeVisible(true)

---

## Library:SelfDestruct()

Remove a interface, desconecta eventos e limpa os drawings internos.

### Exemplo

    Library.SelfDestruct()

---

## Utility

Conjunto de funções auxiliares internas.

---

## Utility.AddInstance(className, properties)

Cria uma instância Roblox e aplica propriedades.

### Exemplo

    local Frame = Utility.AddInstance("Frame", {
        Size = UDim2.fromOffset(100, 100)
    })

---

## Utility.CloneTbl(tbl)

Clona uma tabela superficialmente.

---

## Utility.CLCheck()

Detecta o estado do Caps Lock.

---

## Utility.Loop(delay, callback)

Executa uma função em loop com intervalo.

### Exemplo

    Utility.Loop(1, function()
        print("rodando a cada 1 segundo")
    end)

---

## Utility.RemoveDrawing(instance, location)

Remove um drawing da lista informada.

---

## Utility.AddConnection(signal, callback)

Conecta um evento e salva a connection internamente.

---

## Utility.Round(num, float)

Arredonda usando fração.

---

## Utility.Rounding(num, decimalPlaces)

Formata número com casas decimais.

---

## Utility.AddDrawing(className, properties, location)

Cria um `Drawing` e adiciona na lista de rastreio da lib.

### Tipos usados na source

- `Square`
- `Text`
- `Image`
- `Triangle`

---

## Utility.OnMouse(instance)

Retorna `true` quando o mouse está dentro do retângulo do drawing.

---

## Utility.AddDrag(sensor, list)

Permite arrastar um conjunto de drawings ao clicar no sensor.

---

## Utility.HSVToRGB(hsvColor)

Converte HSV para RGB.

---

## Utility.AddCursor(instance)

Cria o cursor customizado da UI.

---

## Utility.MiddlePos(instance)

Calcula o centro da tela para posicionar um drawing.

---

## Utility.SaveConfig(name)

Salva a config atual.

### Caminho usado

    akiri/Configs/<PlaceId>/<name>.json

---

## Utility.DeleteConfig(name)

Apaga uma config salva.

---

## Utility.LoadConfig(name)

Carrega uma config salva.

### Suporte por tipo

- `Keybind`
- `Colorpicker`
- `Slider`
- `Toggle`

---

## Utility.AddFolder(path)

Cria uma pasta caso ela não exista.

---

## Utility.AddImage(path, url, ui)

Baixa ou lê uma imagem cacheada localmente.

### Uso interno

A lib usa isso para:

- Logo
- Gradient
- Hue
- Saturation
- SaturationCursor
- imagens temáticas

---

## Teclas e inputs

A lib possui um mapa interno de teclas:

- letras de `Q` até `M`
- números `One` a `Zero`
- inputs como:
  - `MouseButton1`
  - `MouseButton2`
  - `MouseButton3`
  - `Insert`
  - `Tab`
  - `Home`
  - `End`
  - `LeftAlt`
  - `LeftControl`
  - `LeftShift`
  - `RightAlt`
  - `RightControl`
  - `RightShift`
  - `CapsLock`

Também existe um conjunto de nomes abreviados, por exemplo:

- `MouseButton1` → `M1`
- `MouseButton2` → `M2`
- `MouseButton3` → `M3`
- `Insert` → `INS`

---

## Sistema de flags

Quase todos os componentes que aceitam `Flag` registram o valor atual em `Library.Flags[Flag]`.

Isso facilita:

- salvar config
- carregar config
- consultar estado de componentes em tempo real

---

## Sistema de eventos interno

A lib usa `Library.Communication`, um `BindableEvent`, para disparar atualizações globais de tema e interface.

Eventos usados internamente:

- `Accent`
- `Outline`
- `Inline`
- `LightContrast`
- `DarkContrast`
- `Text`
- `UpdateNotification`

---

## Notas importantes

- A lib depende de objetos como `Drawing`, `writefile`, `readfile`, `makefolder`, `isfolder`, `isfile` e funções de input específicas do ambiente.
- Alguns detalhes internos variam conforme o executor/ambiente.
- O source analisado mostra um `TextBox:Set()` vazio, então esse método não tem comportamento implementado no arquivo atual.
- A seleção de tema embutida inclui presets como `Default`, `Neverlose`, `Fatality`, `Aimware`, `Onetap`, `Vape`, `Gamesense` e `OldAbyss`.

---

## Exemplo completo

    local Library = loadstring(game:HttpGet("URL_DA_SUA_LIB"))()

    local Window = Library.Window("Akiri Example", Vector2.new(620, 470))

    local Main = Window:Tab("Main")
    local Player = Main:Section("Player", "Left")

    Player:Toggle({
        Title = "Auto Sprint",
        State = false,
        Flag = "AutoSprint",
        Callback = function(State)
            print("AutoSprint:", State)
        end
    })

    Player:Slider({
        Title = "Speed",
        Default = 16,
        Min = 0,
        Max = 100,
        Decimals = 1,
        Symbol = "",
        Flag = "Speed",
        Callback = function(Value)
            print("Speed:", Value)
        end
    })

    Player:Button({
        Title = "Print",
        Callback = function()
            print("clicou")
        end
    })

    Player:TextBox({
        Title = "Nome",
        Current = "",
        Flag = "PlayerName",
        Callback = function(Text)
            print("Texto:", Text)
        end
    })

    Player:Dropdown({
        Title = "Mode",
        List = {"Easy", "Normal", "Hard"},
        Default = "Normal",
        Flag = "Mode",
        Callback = function(Item)
            print("Mode:", Item)
        end
    })

    Player:Colorpicker({
        Title = "Accent",
        Color = Color3.fromRGB(255, 0, 0),
        Flag = "AccentColor",
        Callback = function(Color)
            print(Color)
        end
    })

    Player:Keybind({
        Title = "Open Menu",
        Key = Enum.KeyCode.RightShift,
        StateType = "Toggle",
        Flag = "MenuBind",
        Callback = function(State)
            print(State)
        end
    })

    Player:Label("Fim da seção")

---

## Licença / aviso

Adapte este texto conforme a licença do seu repositório e as regras do projeto.

Se quiser, também posso transformar isso em um README com capa mais bonita, badges, índice clicável e layout pronto para GitHub.
