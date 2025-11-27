<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>Chatbot com Perguntas Visíveis</title>

<style>
    body {
        font-family: Arial, sans-serif;
        background: #001f3f;
        padding: 20px;
        color: white;
    }


    .container {
        display: flex;
        justify-content: center;
        gap: 30px;
        max-width: 1000px;
        margin: auto;
    }

    .chatbox {
        background: #ffffff;
        padding: 25px;
        border-radius: 12px;
        border: 2px solid #d4af37;
        box-shadow: 0 0 15px rgba(0,0,0,0.2);
        width: 350px;
        display: flex;
        flex-direction: column;
        justify-content: center; 
        align-items: center;     
        height: 250px;
        color: #001f3f;
        text-align: center;
    }

    button {
        margin-top: 15px;
        padding: 12px;
        width: 70%;
        cursor: pointer;
        background: #d4af37;
        color: #001f3f;
        border: none;
        border-radius: 10px;
        font-size: 18px;
        font-weight: bold;
        transition: 0.3s;
    }

    
    .perguntas-box {
        background: #ffffff;
        width: 350px;
        padding: 20px;
        border-radius: 12px;
        border: 2px solid #d4af37;
        color: #001f3f;
        box-shadow: 0 0 15px rgba(0,0,0,0.2);
    }

    .perguntas-box h3 {
        margin-bottom: 15px;
        font-weight: bold;
        color: #001f3f;
    }

    .perguntas-box ul {
        list-style: none;
        padding-left: 0;
    }

    .perguntas-box li {
        background: #f5f5f5;
        padding: 10px;
        margin-bottom: 10px;
        border-left: 4px solid #d4af37;
        border-radius: 6px;
        font-size: 15px;
    }
</style>

</head>
<body>

<div class="container">

    
    <div class="chatbox">
        <h2>Chatbot por Voz</h2>
        <button onclick="ouvir()">🎤 Clique aqui para falar</button>
    </div>

   
    <div class="perguntas-box">
        <h3>Perguntas que você pode fazer:</h3>
        <ul>
            <li>O que é o Apgar e quando ele é avaliado?</li>
            <li>Por que o contato pele a pele logo após o parto é tão importante?</li>
            <li>Qual é a importância da amamentação na primeira hora de vida?</li>
            <li>Como identificar precocemente sinais de sofrimento fetal intraparto?</li>
            <li>Qual é o papel da enfermagem na prevenção da hipotermia neonatal, especialmente em partos de risco?</li>
        </ul>
    </div>

</div>

<script>
const pergunta = [
    "avaliado",
    "por que o contato pele a pele logo após o parto é tão importante",
    "qual é a importância da amamentação na primeira hora de vida",
    "como identificar precocemente sinais de sofrimento fetal intraparto",
    "hipotermia neonatal"
];

const resposta = [
    "O Apgar é um método rápido para avaliar as condições do bebê logo após o nascimento. Ele é realizado no 1º e no 5º minuto de vida, analisando respiração, frequência cardíaca, cor da pele, tônus muscular e irritabilidade reflexa.",
    "Porque ajuda a estabilizar temperatura, respiração e batimentos do bebê, fortalece o vínculo com a mãe, reduz o estresse do recém-nascido e facilita o início da amamentação.",
    "Na primeira hora o bebê está mais alerta e com maior reflexo de sucção. Amamentar nesse período facilita a descida do leite, reduz risco de hemorragia materna e garante ao bebê o colostro rico em anticorpos.",
    "Por alterações na frequência cardíaca fetal, variabilidade reduzida, presença de mecônio espesso e padrões anormais no cardiotocógrafo. Esses sinais indicam possível hipóxia e exigem intervenção rápida.",
    "Secar o bebê imediatamente, manter o ambiente aquecido, realizar contato pele a pele, usar touca, evitar correntes de ar e, em prematuros ou casos instáveis, colocar em incubadora ou saco térmico. Isso previne hipoglicemia, acidose e desconforto respiratório."
];

function falar(texto) {
    const discurso = new SpeechSynthesisUtterance(texto);
    discurso.lang = "pt-BR";
    discurso.rate = 1;
    window.speechSynthesis.speak(discurso);
}

function ouvir() {
    const reconhecer = new webkitSpeechRecognition();
    reconhecer.lang = "pt-BR";
    reconhecer.start();

    reconhecer.onresult = function(event) {
        const textoFalado = event.results[0][0].transcript.toLowerCase();

        for (let i = 0; i < pergunta.length; i++) {
            if (textoFalado.includes(pergunta[i])) {
                falar(resposta[i]);
                return;
            }
        }

        falar("Desculpe, eu não entendi.");
    };
}
</script>

</body>
</html>
