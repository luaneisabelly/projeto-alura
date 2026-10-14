# projeto-alura
1. Estrutura dos arquivos
Crie uma pasta chamada criando-sua-aventura com esta estrutura:

text
criando-sua-aventura/
├── index.html
├── styles.css
├── script.js
└── img/
    ├── cenario-passo1-rio-de-janeiro.png
    ├── cenario-passo2-pista.png
    ├── cenario-passo3-amazonas.png
    ├── cenario-passo4-rio.png
    └── cenario-passo11-cidade-perdida.png
As imagens são arquivos que você precisa adicionar à pasta img. O código abaixo funciona mesmo sem elas, mas as ilustrações não aparecerão até você colocar os arquivos com esses nomes.

2. Código do index.html

<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Aventura: Cidade Perdida</title>
    <link rel="stylesheet" href="styles.css">
    <script src="script.js" defer></script>
</head>
<body>
    <header>
        <h1>A Cidade Perdida</h1>
        <p>Uma aventura cheia de mistérios espera por você!</p>
    </header>

    <main>
        <section class="aventura">
            <img
                id="imagem-cenario"
                src="img/cenario-passo1-rio-de-janeiro.png"
                alt="Paisagem do Rio de Janeiro"
            >

            <h2 id="titulo-cenario">O início da aventura</h2>

            <p id="texto-cenario">
                Você está no Rio de Janeiro e encontra pistas sobre
                uma cidade perdida escondida na floresta amazônica.
                O que deseja fazer?
            </p>

            <div id="opcoes" class="opcoes">
                <button onclick="escolherCaminho('pista')">
                    Procurar a pista no topo do pico
                </button>

                <button onclick="escolherCaminho('desistir')">
                    Desistir da aventura
                </button>
            </div>

            <button id="reiniciar" class="reiniciar" onclick="reiniciarAventura()">
                Recomeçar aventura
            </button>
        </section>
    </main>

    <footer>
        <p>Projeto educativo de aventura interativa.</p>
    </footer>
</body>
</html>
3. Código do styles.css
Este arquivo deixa a página organizada, com cores de aventura e adaptação para celulares.

css

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #102820, #315b42);
    color: #ffffff;
    min-height: 100vh;
    padding: 20px;
}

header {
    text-align: center;
    padding: 30px 10px;
}

header h1 {
    color: #f4d58d;
    font-size: 2.5rem;
    margin-bottom: 10px;
}

header p {
    font-size: 1.1rem;
}

.aventura {
    background-color: #ffffff;
    color: #24352b;
    max-width: 750px;
    margin: 0 auto;
    padding: 25px;
    border-radius: 16px;
    box-shadow: 0 8px 24px #00000040;
    text-align: center;
}

#imagem-cenario {
    display: block;
    width: 100%;
    max-height: 350px;
    object-fit: cover;
    border-radius: 12px;
    margin-bottom: 20px;
}

#titulo-cenario {
    color: #24613d;
    margin-bottom: 15px;
    font-size: 1.7rem;
}

#texto-cenario {
    line-height: 1.7;
    margin-bottom: 25px;
}

.opcoes {
    display: flex;
    flex-direction: column;
    gap: 12px;
}

button {
    background-color: #287447;
    color: white;
    border: none;
    border-radius: 8px;
    padding: 15px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.2s, transform 0.2s;
}

button:hover {
    background-color: #1b5232;
    transform: translateY(-2px);
}

.reiniciar {
    margin-top: 20px;
    background-color: #8b5e34;
}

.reiniciar:hover {
    background-color: #674323;
}

footer {
    text-align: center;
    padding: 25px 10px;
    font-size: 0.9rem;
}

@media (max-width: 600px) {
    body {
        padding: 10px;
    }

    header h1 {
        font-size: 2rem;
    }

    .aventura {
        padding: 16px;
    }
}
4. Código do script.js
Aqui fica a lógica da aventura. O código permite seguir as escolhas até chegar à cidade perdida e corrige o nome da imagem final para cenario-passo11-cidade-perdida.png.

javascript

const titulo = document.getElementById("titulo-cenario");
const texto = document.getElementById("texto-cenario");
const imagem = document.getElementById("imagem-cenario");
const opcoes = document.getElementById("opcoes");

const cenarios = {
    inicio: {
        titulo: "O início da aventura",
        texto: "Você está no Rio de Janeiro e descobre pistas sobre uma cidade perdida na Amazônia. Onde deseja procurar?",
        imagem: "img/cenario-passo1-rio-de-janeiro.png",
        alt: "Paisagem do Rio de Janeiro",
        escolhas: [
            { texto: "Procurar a pista no topo do pico", destino: "pista" },
            { texto: "Desistir da aventura", destino: "desistir" }
        ]
    },

    pista: {
        titulo: "Uma pista misteriosa",
        texto: "No topo do pico, você encontra um mapa antigo que aponta para a floresta amazônica. É hora de seguir as pistas!",
        imagem: "img/cenario-passo2-pista.png",
        alt: "Mapa antigo com pistas da aventura",
        escolhas: [
            { texto: "Seguir para o Amazonas", destino: "amazonas" },
            { texto: "Voltar ao Rio de Janeiro", destino: "inicio" }
        ]
    },

    amazonas: {
        titulo: "Chegando ao Amazonas",
        texto: "Você chega à Amazônia e encontra um rio que parece levar até a cidade perdida. Qual caminho seguirá?",
        imagem: "img/cenario-passo3-amazonas.png",
        alt: "Floresta amazônica",
        escolhas: [
            { texto: "Seguir pelo rio à esquerda", destino: "rio" },
            { texto: "Voltar para procurar outra pista", destino: "pista" }
        ]
    },

    rio: {
        titulo: "O caminho pelo rio",
        texto: "Depois de navegar pelo rio, você encontra vestígios de uma antiga civilização escondida entre as árvores.",
        imagem: "img/cenario-passo4-rio.png",
        alt: "Rio cercado pela floresta amazônica",
        escolhas: [
            { texto: "Explorar cidade perdida", destino: "cidade" },
            { texto: "Voltar pelo rio", destino: "amazonas" }
        ]
    },

    cidade: {
        titulo: "A Cidade Perdida!",
        texto: "Dentro da cidade perdida, você descobre tesouros inimagináveis e decide se dedicar a estudar e preservar este lugar.",
        // Nome corrigido conforme a aula:
        imagem: "img/cenario-passo11-cidade-perdida.png",
        alt: "Uma cidade maravilhosa perdida no Amazonas",
        escolhas: [
            { texto: "Começar uma nova aventura", destino: "inicio" }
        ]
    },

    desistir: {
        titulo: "Fim da aventura",
        texto: "Você decide voltar para casa. As pistas continuarão esperando por um futuro explorador!",
        imagem: "img/cenario-passo1-rio-de-janeiro.png",
        alt: "Paisagem do Rio de Janeiro",
        escolhas: [
            { texto: "Tentar novamente", destino: "inicio" }
        ]
    }
};

function mostrarCenario(nome) {
    const cenario = cenarios[nome];

    titulo.textContent = cenario.titulo;
    texto.textContent = cenario.texto;
    imagem.src = cenario.imagem;
    imagem.alt = cenario.alt;

    // Caso uma imagem não exista, mostra uma mensagem no lugar dela.
    imagem.onerror = function () {
        this.style.display = "none";
    };

    imagem.onload = function () {
        this.style.display = "block";
    };

    opcoes.replaceChildren();

    cenario.escolhas.forEach(function (escolha) {
        const botao = document.createElement("button");

        botao.textContent = escolha.texto;
        botao.addEventListener("click", function () {
            escolherCaminho(escolha.destino);
        });

        opcoes.appendChild(botao);
    });
}

function escolherCaminho(destino) {
    mostrarCenario(destino);
}

function reiniciarAventura() {
    mostrarCenario("inicio");
}

mostrarCenario("inicio");
5. Como testar a aventura
Abra o arquivo index.html no navegador e siga este caminho:

Rio de Janeiro

Procurar a pista no topo do pico

Seguir para o Amazonas

Seguir pelo rio à esquerda

Explorar cidade perdida

Ao chegar ao final, deverá aparecer o título “A Cidade Perdida!”, o texto sobre os tesouros e a imagem final, desde que o arquivo esteja na pasta img com o nome correto.

6. Como publicar no GitHub
Você precisa ter uma conta no GitHub para realizar estas etapas.

Entre no GitHub pelo site 
github.com .

Clique no sinal + e escolha New repository.

Digite criando-sua-aventura como nome do repositório e selecione Public.

Clique em Create repository.

Escolha upload an existing file e envie index.html, styles.css, script.js e a pasta img com suas imagens.

Em Commit changes, escreva Projeto final e confirme.

Entre em Settings → Pages. Em Build and deployment, escolha a opção de publicar a partir de uma branch, selecione main e a pasta / (root), e clique em Save.

Aguarde a publicação e abra o endereço exibido na seção Pages.
Pronto! Você terá o código armazenado no GitHub e poderá publicar a aventura como um site usando o GitHub Pages.

Importante: o projeto acima é uma versão funcional baseada no texto da aula. Para ficar visualmente igual ao projeto original, você ainda precisará adicionar as imagens originais dos cenários à pasta img.


