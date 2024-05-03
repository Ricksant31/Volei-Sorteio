<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Lista de Time de Vôlei</title>
<link rel="stylesheet" href="styles.css">
<style>
body {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  background-image: url('fundo volei.jpg'); /* Substitua pelo caminho da sua imagem */
  background-size: cover;
}

</style>
</head>
<body>
<img src="logo volei.png" alt="Logo" class="logo">
  
<div class="header">
    
  <h1>Lista de Time de Vôlei</h1>

</div>
<!-- Formulário de login para administradores -->
<center>
  <h2>Login de Administrador:</h2>
  <input type="password" id="senha" placeholder="Digite a senha">
  <button onclick="login()">Login</button>

<!-- Formulário para adicionar nome ao time (visível para todos) -->
<h2>Adicionar nome ao time:</h2>
<input type="text" id="nome" placeholder="Digite o nome">
<div id="divHabilidade" style="display:none;">
  <select id="habilidade">
    <option value="1">Nível 1</option>
    <option value="2">Nível 2</option>
    <option value="3">Nível 3</option>
  </select>
</div>
<button onclick="adicionarJogador()">Adicionar</button>

<!-- Lista de jogadores (visível para todos) -->
<h2>Lista de jogadores:</h2>
<ul id="listaJogadores">
</ul>

<!-- Formulário para editar habilidade (visível apenas para administradores) -->
<div id="formEditarHabilidade" style="display:none;">
  <h2>Editar habilidade:</h2>
  <input type="text" id="editarNome" placeholder="Digite o nome">
  <select id="editarHabilidade">
    <option value="1">Nível 1</option>
    <option value="2">Nível 2</option>
    <option value="3">Nível 3</option>
  </select>
  <button onclick="editarHabilidade()">Editar</button>
</div>

<!-- Botão para limpar todos os nomes (visível apenas para administradores) -->
<div id="formLimparJogadores" style="display:none;">
  <h2>Limpar todos os nomes:</h2>
  <button onclick="limparTodosJogadores()">Limpar</button>
</div>

<!-- Botão para remover um nome (visível apenas para administradores) -->
<div id="formRemoverJogador" style="display:none;">
  <h2>Remover um nome:</h2>
  <input type="text" id="removerNome" placeholder="Digite o nome">
  <button onclick="removerJogador()">Remover</button>
</div>

<!-- Botão para sortear times (visível para todos) -->
<h2>Sortear times:</h2>
<button onclick="sortearTimes()">Sortear</button>

<!-- Grupos de times (visível para todos) -->
<div id="gruposTimes">
</div>

<!-- Script JavaScript -->
<script>
// Senha do administrador
var senhaAdmin = "admin123";

// Flag para verificar se o administrador está autenticado
var adminAutenticado = false;

// Array para armazenar os jogadores
var jogadores = [];

// Função para adicionar jogador (visível para todos)
function adicionarJogador() {
  var nome = document.getElementById("nome").value;
  var habilidade = document.getElementById("habilidade").value;
  jogadores.push({nome: nome, habilidade: habilidade});
  salvarJogadores(); // Salva os jogadores no armazenamento local
  atualizarListaJogadores();
  document.getElementById("nome").value = ''; // Limpa o campo de entrada após adicionar o jogador
}

// Função para atualizar lista de jogadores na página (visível para todos)
function atualizarListaJogadores() {
  var listaJogadores = document.getElementById("listaJogadores");
  listaJogadores.innerHTML = "";
  jogadores.forEach(function(jogador) {
    var itemLista = document.createElement("li");
    itemLista.textContent = jogador.nome + (adminAutenticado ? " (Nível " + jogador.habilidade + ")" : "");
    listaJogadores.appendChild(itemLista);
  });
}

// Função para salvar jogadores no armazenamento local
function salvarJogadores() {
  localStorage.setItem('jogadores', JSON.stringify(jogadores));
}

// Função para carregar jogadores do armazenamento local
function carregarJogadores() {
  var jogadoresSalvos = localStorage.getItem('jogadores');
  if (jogadoresSalvos) {
    jogadores = JSON.parse(jogadoresSalvos);
    atualizarListaJogadores();
  }
}

// Carregar jogadores ao carregar a página
carregarJogadores();

// Função para realizar login de administrador
function login() {
  var senhaDigitada = document.getElementById("senha").value;
  if (senhaDigitada === senhaAdmin) {
    adminAutenticado = true;
    document.getElementById("formEditarHabilidade").style.display = "block"; // Exibir formulário de edição
    document.getElementById("formLimparJogadores").style.display = "block"; // Exibir botão para limpar todos os nomes
    document.getElementById("formRemoverJogador").style.display = "block"; // Exibir formulário para remover um nome
    document.getElementById("divHabilidade").style.display = "block"; // Exibir campo de habilidade
  } else {
    alert("Senha incorreta. Tente novamente.");
  }
}

// Função para editar habilidade (visível apenas para administradores)
function editarHabilidade() {
  var nome = document.getElementById("editarNome").value;
  var habilidade = document.getElementById("editarHabilidade").value;
  for (var i = 0; i < jogadores.length; i++) {
    if (jogadores[i].nome === nome) {
      jogadores[i].habilidade = habilidade;
      salvarJogadores(); // Salva os jogadores atualizados no armazenamento local
      break;
    }
  }
  atualizarListaJogadores();
}

// Função para limpar todos os nomes (visível apenas para administradores)
function limparTodosJogadores() {
  jogadores = []; // Limpa a lista de jogadores
  salvarJogadores(); // Salva a lista vazia no armazenamento local
  atualizarListaJogadores(); // Atualiza a lista de jogadores na página
}

// Função para remover um nome (visível apenas para administradores)
function removerJogador() {
  var nome = document.getElementById("removerNome").value;
  jogadores = jogadores.filter(function(jogador) {
    return jogador.nome !== nome; // Remove o jogador com o nome especificado
  });
  salvarJogadores(); // Salva a lista atualizada no armazenamento local
  atualizarListaJogadores(); // Atualiza a lista de jogadores na página
}
</script>
</center>
</body>
</html>
