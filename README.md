
-- c00lgui, EQUIPE C00LKIDD!
screenGui local = Instância.new("ScreenGui")
screenGui.Nome = "C00lgui"
screenGui.Parent = jogo.Jogadores.LocalPlayer:WaitForChild("PlayerGui")

ícone local = Instance.new("ImageLabel")
ícone.Tamanho = UDim2.novo(0, 50, 0, 50)
ícone.Posição = UDim2.novo(0, 5, 0, 5)
ícone.TransparênciaDeFundo = 1
ícone.Imagem = "rbxassetid://130381521049312"
ícone.Parent = screenGui

quadro local = Instance.new("Quadro")
frame.Size = UDim2.new(0, 350, 0, 450)
frame.Posição = UDim2.novo(0,5, -175, 0,5, -225)
frame.BackgroundColor3 = Cor3.fromRGB(255, 0, 0)
frame.Active = verdadeiro
frame.Draggable = verdadeiro
frame.Parent = screenGui

local uiCorner = Instância.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 40)
uiCorner.Parent = quadro

título localLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 40)
titleLabel.BackgroundColor3 = Cor3.fromRGB(0, 0, 0)
titleLabel.Text = "GUI C00lkid v2"
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.TextSize = 20
titleLabel.Parent = quadro

páginas locais = {"Combate", "Movimento", "Caos do Servidor", "Utilitário", "Segredo"}
página atual local = 1
botões locais = {}

pageLabel local = Instance.new("TextLabel")
pageLabel.Size = UDim2.new(1, 0, 0, 30)
pageLabel.Position = UDim2.new(0, 0, 0, 40)
pageLabel.BackgroundColor3 = Cor3.fromRGB(0, 0, 0)
pageLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
pageLabel.TextSize = 18
pageLabel.Parent = quadro

nextPageBtn local = Instância.new("TextButton")
nextPageBtn.Size = UDim2.new(0, 50, 0, 30)
nextPageBtn.Position = UDim2.new(1, -55, 1, -35)
nextPageBtn.Text = ">"
nextPageBtn.TextColor3 = Color3.fromRGB(255, 0, 0)
nextPageBtn.BackgroundColor3 = Cor3.fromRGB(0, 0, 0)
nextPageBtn.Parent = quadro

prevPageBtn local = Instance.new("TextButton")
prevPageBtn.Size = UDim2.new(0, 50, 0, 30)
prevPageBtn.Position = UDim2.new(0, 5, 1, -35)
prevPageBtn.Text = "<"
prevPageBtn.TextColor3 = Color3.fromRGB(255, 0, 0)
prevPageBtn.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
prevPageBtn.Parent = quadro

-- Funções
função local clearButtons()
	para _, btn em pares (botões) faça
		btn:Destruir()
	fim
	tabela.clear(botões)
fim

todos os scripts locais = {
	Combate = {
		{"Matar todos", função()
			para _, jogador em pares(game.Players:GetPlayers()) faça
				se player.Character e player.Character:FindFirstChild("Humanoid") então
					jogador.Personagem.Humanoide.Saúde = 0
				fim
			fim
		fim},
		{"Arremessar tudo", função()
			para _, p em pares(game.Players:GetPlayers()) faça
				se p.Character e p.Character:FindFirstChild("HumanoidRootPart") então
					p.Character.HumanoidRootPart.Velocity = Vetor3.novo(9999,9999,9999)
				fim
			fim
		fim},
		{"KO instantâneo", função()
			alvo local = jogo.Jogadores:ObterJogadores()[2]
			se alvo e alvo.Caractere então
				alvo.Caractere:BreakJoints()
			fim
		fim},
		{"Soco de Fogo", função()
			-- Animação divertida
		fim},
		{"Ban Hammer", função()
			-- Efeito imaginário de proibição do martelo
		fim},
		{"Slam Ground", função()
			-- Golpe falso em área de efeito
		fim},
		{"Olhos de Laser", function()
			-- Lasers oculares pew pew
		fim},
		{"Jogar Jogador", function()
			-- Animação de arremesso falso
		fim},
		{"Explodir Soco", function()
			-- Estrondoso soco
		fim},
		{"Punho Nuclear", função()
			-- Animação combinada com efeito falso
		fim},
	},
	Movimento = {
		{"Salto Infinito", function()
			jogo:GetService("UserInputService").JumpRequest:Connect(função()
				game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid"):ChangeState("Pulando")
			fim)
		fim},
		{"Freecam", função()
			-- Mesmo código freecam aqui
		fim},
		{"Modo de voo", função()
			-- Animação de voo ou BodyVelocity
		fim},
		{"Aumento de velocidade", função()
			jogo.Jogadores.JogadorLocal.Personagem.Humanoide.VelocidadeDeCaminhada = 100
		fim},
		{"Super Salto", função()
			jogo.Jogadores.JogadorLocal.Personagem.Humanoide.JumpPower = 150
		fim},
		{"Teleportar para frente", function()
			char local = jogo.Jogadores.JogadorLocal.Personagem
			char:SetPrimaryPartCFrame(char.PrimaryPart.CFrame * CFrame.new(0, 0, -50))
		fim},
		{"Teletransporte para o lobby", function()
			jogo.Jogadores.JogadorLocal.Personagem:MoveTo(Vector3.novo(0, 50, 0))
		fim},
		{"Invisível", função()
			para _, p em pares(game.Players.LocalPlayer.Character:GetDescendants()) faça
				se p:IsA("BasePart") e p.Name ~= "HumanoidRootPart" então p.Transparency = 1 fim
			fim
		fim},
		{"Teletransporte para o jogador", function()
			-- Opcional
		fim},
		{"Câmera Lenta", função()
			-- Efeito de caminhada lenta
		fim},
	},
	Servidor_Caos = {
		{"Destruir Servidor", function()
			-- Chute todos
		fim},
		{"Servidor Lag", função()
			enquanto verdadeiro faça game.Workspace:Clone() fim
		fim},
		{"Mapa Nuclear", função()
			-- Efeito boom
		fim},
		{"Explodir Tudo", function()
			-- Explosões
		fim},
		{"Âncora do Caos", função()
			-- Desancorar tudo
		fim},
		{"Excluir todas as partes", function()
			para _, obj em pares(workspace:GetChildren()) faça se obj:IsA("BasePart") então obj:Destroy() fim fim
		fim},
		{"Quebrar a gravidade", function()
			espaço de trabalho.Gravidade = 0
		fim},
		{"Peças de chuva", function()
			-- Geração de parte do loop
		fim},
		{"Rebater tudo", function()
			-- Parte elástica em loop
		fim},
		{"Spin World", função()
			-- Gire todas as peças
		fim},
	},
	Utilidade = {
		{"Modo Deus", função()
			local h = jogo.Jogadores.JogadorLocal.Personagem:FindFirstChild("Humanoide")
			h.MaxHealth = matemática.enorme
			h.Saúde = matemática.enorme
		fim},
		{"ESP", função()
			-- Adicionar contornos ESP
		fim},
		{"Ferramenta TP", função()
			-- Ferramenta para clicar em teletransporte
		fim},
		{"Bate-papo do administrador", função()
			-- Imitação de bate-papo global
		fim},
		{"Clone Player", função()
			-- Clone fictício
		fim},
		{"Ver outros", function()
			-- Definir câmera para outras pessoas
		fim},
		{"Doador de ferramentas", função()
			-- Dê todas as ferramentas
		fim},
		{"Gerador de Partes", function()
			-- Gera peças
		fim},
		{"Clique em Destruir", function()
			-- Clique para excluir parte
		fim},
		{"Alterador de Nome", função()
			-- Nome falso
		fim},
	},
	Segredo = {
		{"C00lkid sobe", function()
			-- Animação legal de geração de C00lkid
		fim},
		{"Modo de falha", função()
			-- Efeitos de partes malucas
		fim},
		{"Gerar Exército de Clones", function()
			-- Gerar vários bonecos
		fim},
		{"Caos do Arco-Íris", function()
			-- Laços de cor
		fim},
		{"Jumpscare LOL", função()
			-- Jumpscare falso
		fim},
		{"Inundação de erro de script", função()
			-- Spam de GUI
		fim},
		{"Música Estranha", function()
			-- Começa uma música estranha
		fim},
		{"Efeito Tontura", função()
			-- Girar a câmera do jogador
		fim},
		{"Mundo Invertido", função()
			-- Inverter tudo
		fim},
		{"Clone você mesmo x100", function()
			-- Diversão lenta
		fim},
	}
}

função local createButton(nome, posição, ação)
	botão local = Instance.new("TextButton")
	botão.Tamanho = UDim2.novo(1, -10, 0, 30)
	button.Position = posição
	botão.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
	button.Text = nome
	botão.TextColor3 = Color3.fromRGB(255, 0, 0)
	botão.TextSize = 18
	botão.Parent = quadro
	tabela.insert(botões, botão)
	botão.MouseButton1Click:Conectar(ação)
fim

função local updatePage()
	botões de limpeza()
	nome local = páginas[currentPage]
	scriptList local = allScripts[nome:gsub(" ", "_")]
	pageLabel.Text = "[" .. nome .. "] - Página " .. currentPage
	para i, v em ipairs(scriptList) faça
		createButton(v[1], UDim2.new(0, 5, 0, 80 + (i-1) * 35), v[2])
	fim
fim

nextPageBtn.MouseButton1Click:Conectar(função()
	se currentPage < #pages então
		página atual += 1
		atualizarPágina()
	fim
fim)

prevPageBtn.MouseButton1Click:Connect(função()
	se currentPage > 1 então
		página atual -= 1
		atualizarPágina()
	fim
fim)

atualizarPágina()

-- equipe c00lkidd junte-se hoje!







-- não é o fim do roteiro

















-- Segredo

jogador local = jogo.Jogadores.JogadorLocal
screenGui local = Instância.new("ScreenGui")
screenGui.Nome = "C00lguiV2"
screenGui.Parent = jogador:WaitForChild("PlayerGui")

-- Crie o botão de canto
caixa local = Instance.new("TextButton")
caixa.Tamanho = UDim2.novo(0, 100, 0, 50)
caixa.Posição = UDim2.novo(1, -120, 0, 20)
caixa.BackgroundColor3 = Cor3.fromRGB(0, 0, 0)
caixa.BorderColor3 = Cor3.fromRGB(255, 0, 0)
caixa.BorderSizePixel = 3
box.Text = "Não toque"
caixa.TextColor3 = Cor3.fromRGB(255, 0, 0)
caixa.Parent = screenGui

-- Adicionar canto à caixa
boxCorner local = Instance.new("UICorner")
boxCorner.CornerRadius = UDim.new(0, 12)
boxCorner.Parent = caixa

-- GUI principal
local c00lgui = Instância.new("Quadro")
c00lgui.Tamanho = UDim2.novo(0, 400, 0, 600)
c00lgui.Posição = UDim2.novo(0,5, -200, 0,5, -300)
c00lgui.BackgroundColor3 = Cor3.fromRGB(0, 0, 0)
c00lgui.BorderColor3 = Cor3.fromRGB(255, 0, 0)
c00lgui.BorderSizePixel = 5
c00lgui.Visível = falso
c00lgui.Parent = screenGui

-- Adicionar canto à interface gráfica principal
guiCorner local = Instance.new("UICorner")
guiCorner.CornerRadius = UDim.new(0, 16)
guiCorner.Parent = c00lgui

-- Botão de Destruição do Servidor
destruição localButton = Instance.new("TextButton")
destroyButton.Size = UDim2.new(0, 200, 0, 50)
destroyButton.Position = UDim2.new(0,5, -100, 0,8, -25)
destroyButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
destroyButton.BorderColor3 = Color3.fromRGB(255, 0, 0)
destroyButton.BorderSizePixel = 3
destructionButton.Text = "Destruir Servidor"
destruiçãoButton.TextColor3 = Color3.fromRGB(255, 0, 0)
destroyButton.Parent = c00lgui

-- Adicionar canto ao botão
local destroyCorner = Instance.new("UICorner")
destroyCorner.CornerRadius = UDim.new(0, 10)
destroyCorner.Parent = botãoDestruição

-- Área de mensagem de rolagem
messageHolder local = Instance.new("ScrollingFrame")
messageHolder.Size = UDim2.new(1, -20, 0,6, 0)
messageHolder.Position = UDim2.new(0, 10, 0, 10)
messageHolder.BackgroundTransparency = 1
messageHolder.CanvasSize = UDim2.new(0, 0, 5, 0)
messageHolder.BorderSizePixel = 0
messageHolder.ScrollBarImageColor3 = Cor3.fromRGB(255, 0, 0)
messageHolder.Parent = c00lgui

-- Adicionar canto à área de mensagens
messageCorner local = Instance.new("UICorner")
messageCorner.CornerRadius = UDim.new(0, 10)
messageCorner.Parent = messageHolder

-- Efeito sonoro
grampeador localSom = Instance.new("Som")
staplerSound.Name = "StaplerGodSound"
staplerSound.SoundId = "rbxassetid://9118823106" -- Você pode alterar isso
grampeadorSom.Volume = 1
staplerSound.Looped = verdadeiro
staplerSound.Parent = screenGui

-- Função para criar rótulos de mensagens
função local addMessage(texto)
	rótulo local = Instance.new("TextLabel")
	rótulo.Tamanho = UDim2.novo(1, 0, 0, 30)
	rótulo.BackgroundTransparency = 1
	label.Text = texto
	label.TextColor3 = Color3.fromRGB(255, 0, 0)
	rótulo.TextScaled = verdadeiro
	rótulo.Fonte = Enum.Fonte.GothamBlack
	rótulo.Parent = messageHolder
	messageHolder.CanvasSize = UDim2.new(0, 0, 0, #messageHolder:GetChildren() * 30)
fim

-- Mostrar GUI, reproduzir som, mensagens de spam
box.MouseButton1Click:Conectar(função()
	c00lgui.Visible = verdadeiro
	grampeadorSom:Reproduzir()

	coroutine.wrap(função()
		enquanto c00lgui.Visible faz
			addMessage("DEUS ESTÁ AQUI")
			espere(0,5)
		fim
	fim)()
fim)

-- Lógica de destruição do servidor
destroyButton.MouseButton1Click:Connect(função()
	para _, parte em pares(workspace:GetDescendants()) faça
		se parte:IsA("BasePart") então
			parte:Destruir()
		fim
	fim
fim)



-- equipe c00lkidd junte-se hoje!

-- (atualizando bastante)
