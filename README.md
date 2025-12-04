<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Atividade — Logística (Banco 50 questões)</title>

<style>
body{
  font-family: Arial, sans-serif;
  background:#f3f6fa;
  margin:0; padding:20px;
}
header{
  display:flex; align-items:center;
  background:white; padding:10px;
  border-radius:8px; margin-bottom:20px;
  box-shadow:0 2px 6px rgba(0,0,0,.1);
}
header img{height:60px;margin-right:15px;}
h1{margin:0;font-size:20px;}
.subtitle{color:#555;font-size:13px;margin-top:4px;}

.card{
  background:white;padding:15px;
  border-radius:8px;margin-bottom:20px;
  box-shadow:0 2px 6px rgba(0,0,0,.08);
}

.question{
  background:#eef4ff;padding:10px;
  border-left:4px solid #0d6efd;
  border-radius:6px;
}

.result{
  margin-top:8px;padding:8px;
  border-radius:6px;font-size:14px;
}
.correct{background:#e6ffed;border:1px solid #1fa25f;color:#0b6b38;}
.wrong{background:#ffe6e6;border:1px solid #d9534f;color:#8b1a1a;}

button{
  padding:10px 15px;border:none;
  border-radius:6px;color:white;
  background:#0d6efd;cursor:pointer;
}
button.secondary{background:#6c757d;}

.medal{font-size:45px;text-align:center;margin-top:10px;}

#timer{
  font-size:22px;
  font-weight:bold;
  color:#d9534f;
  text-align:right;
}
</style>

<script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.9.3/html2pdf.bundle.min.js"></script>
</head>

<body>

<div id="pdfArea">

<header>
  <img src="https://www.senairs.org.br/sites/default/files/styles/scale_sm/public/logos/avatares_sistema_fiergs_senai_cor.png?itok=fuuHGGm3">
  <div>
    <h1>Atividade — Logística de Distribuição</h1>
    <div class="subtitle">Professor: Luiz Eduardo Peixoto</div>
    <div class="subtitle">Banco de 50 questões • Sorteio de 15 • A atividade pode ser feita varias vezes, so atualizar a pagina</div>
  </div>
</header>

<div class="card" style="text-align:right;">
  <div id="timer">20:00</div>
</div>

<div class="card">
  <label><strong>Nome do aluno:</strong></label>
  <input id="studentName" type="text" style="width:100%;padding:8px;margin-top:6px">
</div>

<div id="questions"></div>

</div>

<div class="card">
  <button onclick="validateAll()">Validar respostas</button>
  <button class="secondary" onclick="resetAll()">Resetar</button>
  <button onclick="exportPDF()" style="float:right">Exportar PDF</button>
</div>

<script>
/* ========================= BANCO COM 50 QUESTÕES ========================= */

const questionBank = [
{q:"O método FIFO significa:",a:"Primeiro a entrar, primeiro a sair",
options:["Primeiro a entrar, primeiro a sair","Último a entrar, primeiro a sair","Primeiro a vencer","Último a sair"]},
{q:"O método LIFO é usado em:",a:"Baixa rotatividade",
options:["Perecíveis","Baixa rotatividade","Medicamentos","Alta rotatividade"]},
{q:"O método FEFO prioriza:",a:"Validade mais próxima",
options:["Itens mais pesados","Itens mais caros","Validade mais próxima","Itens maiores"]},
{q:"O WMS serve para:",a:"Gerenciar operações de armazém",
options:["Gerenciar frota","Gerenciar financeiro","Gerenciar operações de armazém","Emitir notas"]},
{q:"Picking significa:",a:"Separação de produtos",
options:["Carregamento","Separação de produtos","Inventário","Descarga"]},
{q:"Roteirização busca:",a:"Reduzir tempo e distância",
options:["Reduzir tempo e distância","Aumentar paradas","Carregar mais peso","Usar mais veículos"]},
{q:"Cubagem representa:",a:"Volume da carga",
options:["Peso da carga","Volume da carga","Temperatura da carga","Valor da carga"]},
{q:"OTIF mede:",a:"Entrega no prazo e completa",
options:["Custo operacional","Embalagem","Entrega no prazo e completa","Velocidade do separador"]},
{q:"O WMS reduz erros em:",a:"Picking",
options:["Financeiro","Picking","RH","Marketing"]},
{q:"PEPS equivale a:",a:"FIFO",
options:["LIFO","FEFO","FIFO","LEFO"]},

{q:"PVPS equivale a:",a:"FEFO",
options:["FIFO","FEFO","LIFO","PEPS"]},
{q:"Um layout em corredor único favorece:",a:"Baixa complexidade",
options:["Alta densidade","Baixa complexidade","Crossdocking","Múltiplas docas"]},
{q:"No picking em ondas, pedidos são agrupados por:",a:"Horários",
options:["Clientes","Horários","Motoristas","SKU"]},
{q:"Endereçamento serve para:",a:"Localizar produtos no estoque",
options:["Emitir notas","Localizar produtos no estoque","Transportar produtos","Pesar carga"]},
{q:"Inventário rotativo é feito:",a:"Durante o ano",
options:["Somente no fim do ano","Durante o ano","A cada 5 anos","Só quando há erros"]},

{q:"Armazenagem porta-palete é ideal para:",a:"Produtos variados",
options:["Apenas líquidos","Produtos variados","Somente perecíveis","Somente grandes volumes"]},
{q:"Crossdocking reduz:",a:"Estocagem",
options:["Transporte","Estocagem","Documentos","Peso da carga"]},
{q:"Lead time é:",a:"Tempo total do processo",
options:["Tempo de separação","Tempo total do processo","Tempo de deslocamento","Tempo parado"]},
{q:"Roteiro mal planejado gera:",a:"Aumento de custos",
options:["Redução de custos","Aumento de custos","Mais espaço","Mais motoristas"]},
{q:"No WMS, o mapa de armazém ajuda a:",a:"Localizar itens rapidamente",
options:["Emitir notas","Localizar itens rapidamente","Transportar carga","Criar romaneio"]},

{q:"Inventário cíclico detecta:",a:"Diferenças de estoque",
options:["Devoluções","Peso","Diferenças de estoque","Erros fiscais"]},
{q:"Método mais comum para perecíveis:",a:"FEFO",
options:["FIFO","FEFO","LIFO","LEFO"]},
{q:"Unitização facilita:",a:"Movimentação",
options:["Movimentação","Tributação","Marketing","Qualidade"]},
{q:"Pallet PBR é:",a:"Padrão brasileiro",
options:["Europeu","Americano","Padrão brasileiro","Descartável"]},
{q:"Caminhão baú é ideal para:",a:"Mercadorias protegidas",
options:["Grãos","Areia","Mercadorias protegidas","Carga a granel"]},

{q:"Rastreamento da frota permite:",a:"Controle em tempo real",
options:["Aumento de peso","Controle em tempo real","Remover rotas","Reduzir pedágios"]},
{q:"Janela de entrega é:",a:"Intervalo permitido para entrega",
options:["Horário do funcionário","Intervalo permitido para entrega","Tempo de carga","Tempo de descanso"]},
{q:"Embalagem primária protege:",a:"Produto",
options:["Pallet","Operador","Produto","Armazém"]},
{q:"Embalagem secundária é usada para:",a:"Agrupar produtos",
options:["Proteger operador","Agrupar produtos","Transportar frota","Criar pedidos"]},
{q:"Cubagem influencia:",a:"Ocupação do veículo",
options:["RH","Marketing","Ocupação do veículo","Inventário"]},

{q:"WMS controla:",a:"Armazenagem e separação",
options:["Transporte urbano","RH","Armazenagem e separação","TI"]},
{q:"FIFO evita:",a:"Produtos envelhecidos",
options:["Custo alto","Produtos envelhecidos","Demanda baixa","Erros fiscais"]},
{q:"FEFO evita:",a:"Perdas por validade",
options:["Avarias","Falta de estoque","Perdas por validade","Peso excessivo"]},
{q:"LIFO é adequado para:",a:"Materiais empilhados",
options:["Perecíveis","Materiais empilhados","Medicamentos","Refrigerados"]},
{q:"Picking por zona divide o armazém em:",a:"Setores",
options:["Cores","Setores","Turnos","Motoristas"]},

{q:"Mapa de calor no WMS mostra:",a:"Áreas de maior movimentação",
options:["Temperatura","Peso","Áreas de maior movimentação","Frota"]},
{q:"Roteirização considera:",a:"Capacidade do veículo",
options:["Clima","Cor da camisa","Capacidade do veículo","Altura do motorista"]},
{q:"Indicador de devolução mede:",a:"Retorno de mercadoria",
options:["Descarte","Retorno de mercadoria","Venda","Preço"]},
{q:"Lead time maior indica:",a:"Processo mais lento",
options:["Processo mais rápido","Processo mais lento","Mais motoristas","Mais espaço"]},
{q:"SKU significa:",a:"Unidade de manutenção de estoque",
options:["Unidade de manutenção de estoque","Caminhão urbano","Setor de qualidade","Sistema unificado"]},

{q:"Picking batch junta:",a:"Pedidos semelhantes",
options:["Clientes","Pedidos semelhantes","Motoristas","Cargas estranhas"]},
{q:"Packing é:",a:"Embalagem final",
options:["Separação","Expedição","Embalagem final","Inventário"]},
{q:"Conferência confere:",a:"Pedido com nota",
options:["Preço","Pedido com nota","Motorista","Temperatura"]},
{q:"Código de barras ajuda em:",a:"Rastreabilidade",
options:["Marketing","Rastreabilidade","RH","Tributos"]},
{q:"RFID usa:",a:"Ondas de rádio",
options:["Cabo","Luz","Ondas de rádio","Som"]},

{q:"Endereço 02-03-04 indica:",a:"Rua-corredor-nível",
options:["SKU","Motorista","Rua-corredor-nível","Peso"]},
{q:"Docas servem para:",a:"Carga e descarga",
options:["Contagem","Carga e descarga","Cubagem","Administração"]},
{q:"WMS comunica com:",a:"Coletores RF",
options:["Google","Coletores RF","Instagram","ERP de Marketing"]},
{q:"Roteiro circular retorna:",a:"Ao CD",
options:["Cliente","Loja","Ao CD","Pátio"]},
{q:"Curva ABC classifica por:",a:"Importância",
options:["Tamanho","Importância","Peso","Volume"]},

{q:"Classe A representa:",a:"Itens mais importantes",
options:["Itens baratos","Itens mais importantes","Itens sem giro","Itens descartáveis"]},
];

/* ========== Sorteio de 15 questões ========== */

let selected = [];

function drawQuestions(){
  selected = [];
  let bank = [...questionBank];
  for(let i=0;i<15;i++){
    const idx = Math.floor(Math.random()*bank.length);
    selected.push(bank[idx]);
    bank.splice(idx,1);
  }
}

drawQuestions();

/* ========== Renderização ========== */

function loadQuestions(){
  let html = "";
  selected.forEach((q,i)=>{
    html += `
      <div class="card">
        <div class="question"><strong>${i+1})</strong> ${q.q}</div>
        <div style="margin-top:10px;">
          ${q.options.map(op=>`
            <label style="display:block;margin:6px 0;">
              <input type="radio" name="q${i}" value="${op}"> ${op}
            </label>
          `).join("")}
        </div>
        <div id="res${i}" class="result" style="display:none"></div>
      </div>
    `;
  });

  document.getElementById("questions").innerHTML = html;
}

loadQuestions();

/* ========================= CRONÔMETRO 20 MIN ========================= */

let timeLeft = 20 * 60; // 20 min

const timerElement = document.getElementById("timer");

const timer = setInterval(() => {
  const min = Math.floor(timeLeft / 60);
  const sec = timeLeft % 60;

  timerElement.textContent = `${min}:${sec.toString().padStart(2,"0")}`;

  if(timeLeft <= 0){
    clearInterval(timer);
    alert("⏳ Tempo esgotado! A atividade será finalizada.");
    validateAll(true); // auto-finaliza
  }
  timeLeft--;
}, 1000);

/* ========================= VALIDAÇÃO ========================= */

let locked = false;

function validateAll(auto=false){
  if(locked) return;
  locked = true;
  clearInterval(timer);

  const student = document.getElementById("studentName").value.trim();
  if(!student && !auto){
    alert("Digite o nome do aluno.");
    locked=false;
    return;
  }

  let score = 0;

  selected.forEach((q,i)=>{
    const chosen=document.querySelector(`input[name="q${i}"]:checked`);
    const res=document.getElementById(`res${i}`);

    if(!chosen){
      res.style.display='block';
      res.className='result wrong';
      res.innerHTML='❌ Não respondida.';
      return;
    }

    if(chosen.value===q.a){
      score++;
      res.style.display='block';
      res.className='result correct';
      res.innerHTML='✔️ Correto!';
    } else {
      res.style.display='block';
      res.className='result wrong';
      res.innerHTML=`❌ Incorreto. Correto: <strong>${q.a}</strong>`;
    }
  });

  const percent = (score/15)*100;
  let medal="", msg="";
  if(percent>=80){ medal="🥇"; msg="Excelente! Medalha de OURO!"; }
  else if(percent>=50){ medal="🥈"; msg="Muito bom! Medalha de PRATA!"; }
  else { medal="🥉"; msg="Continue praticando! Medalha de BRONZE."; }

  const summary = `
    <div class="card">
      <h2>Resultado Final</h2>
      <p><strong>Aluno:</strong> ${student || "(tempo esgotado)"}</p>
      <p><strong>Pontuação:</strong> ${score} / 15 (${percent.toFixed(1)}%)</p>
      <div class="medal">${medal}</div>
      <p style="text-align:center;font-size:18px;">${msg}</p>
    </div>
  `;
  document.getElementById("questions").insertAdjacentHTML("afterend", summary);
}

/* ========================= RESET ========================= */

function resetAll(){ location.reload(); }

/* ========================= EXPORTAR PDF (CORRIGIDO) ========================= */

function exportPDF(){
  const element = document.getElementById("pdfArea");

  const opt = {
    margin: 0.4,
    filename: "atividade_logistica.pdf",
    image: { type: "jpeg", quality: 0.98 },
    html2canvas: { scale: 2, useCORS: true },
    jsPDF: { unit: "in", format: "a4", orientation: "portrait" }
  };

  html2pdf().set(opt).from(element).save();
}

</script>

</body>
</html>


