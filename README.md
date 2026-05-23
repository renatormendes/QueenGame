<img width="353" height="244" alt="Captura de tela_2026-05-23_16-24-45" src="https://github.com/user-attachments/assets/5f2b1f55-9b13-4dbb-90ba-b6962f97087f" />
<img width="353" height="244" alt="Captura de tela_2026-05-23_16-26-25" src="https://github.com/user-attachments/assets/fb6a48b9-1535-48fd-abac-f094baae2626" />
<img width="353" height="244" alt="Captura de tela_2026-05-23_16-28-02" src="https://github.com/user-attachments/assets/2469064f-8d8d-41bd-8223-404ed0562202" />
<img width="353" height="244" alt="Captura de tela_2026-05-23_16-29-10" src="https://github.com/user-attachments/assets/986e9801-5fd7-4d2c-a553-f3ab1f07644e" />

# Jogo de Damas Oficial (Padrão MVC)

Um jogo de Damas totalmente funcional desenvolvido em **Java 2D** aplicando o padrão de arquitetura **MVC (Model-View-Controller)**. O projeto conta com inteligência artificial para o oponente, histórico de lances interativo, regras avançadas para as Damas e persistência de dados.

---

## 🚀 Funcionalidades Implementadas

*   **Dama Longa (Dama Voadora):** Movimentação livre por qualquer número de casas vazias nas diagonais.
*   **Capturas Múltiplas em Zigue-Zague:** Algoritmo recursivo que calcula saltos consecutivos mudando de direção em 90° graus. Peças capturadas permanecem bloqueando o caminho como "fantasmas" até o término da jogada.
*   **Lei da Maioria:** Sistema que força obrigatoriamente o jogador (ou a IA) a escolher a rota que elimine a maior quantidade de peças adversárias no turno.
*   **Design Vetorial:** Ícone de uma coroa dourada desenhado nativamente com polígonos sobre as peças promovidas a Dama.
*   **Persistência de Estado (Save Game):** Botão para interromper a partida incompleta, exportando a matriz do tabuleiro, turno e histórico para um arquivo binário (`partida_salvada.dat`).
*   **Histórico e Retrocesso:** Painel lateral que lista todas as jogadas em notação oficial (Ex: `E3 -> F4`) com suporte a desfazer lances (*Undo*).
*   **Níveis de Dificuldade:** Oponente controlado por IA com três modos de jogo (Fácil, Normal e Difícil).

---

## 📂 Estrutura de Pastas (MVC)

O projeto foi dividido em pacotes isolados para separar a lógica de negócio da interface gráfica:

```text
QueenGame/
├── src/
│   └── com/
│       └── damas/
│           ├── model/
│           │   ├── DamasModel.java     # Regras de jogo, capturas e tabuleiro
│           │   └── EstadoJogo.java     # Estrutura serializável para salvamento
│           │
│           ├── view/
│           │   └── DamasView.java       # Interface gráfica e desenho vetorial 2D
│           │
│           └── controller/
│               └── TabuleiroDamasJava2D.java # Ponto de entrada (Main) e eventos
│
├── partida_salvada.dat                  # Arquivo de save (gerado ao salvar)
└── README.md                            # Documentação do projeto
```

---

## 🛠️ Pré-requisitos

*   **Sistema Operacional:** Linux Lite 7.8 (ou distribuições baseadas em Ubuntu/Debian).
*   **Java Development Kit (JDK):** Versão 11 ou superior instalada.
*   **Editor:** Sublime Text 4200 (com Build System customizado).

---

## 💻 Como Compilar e Executar

### Opção 1: Pelo Terminal do Linux
Abra o seu terminal na pasta raiz do projeto (`QueenGame/`) e execute os comandos:

```bash
# Compilar todos os pacotes respeitando a estrutura do MVC
javac -d . src/com/damas/model/*.java src/com/damas/view/*.java src/com/damas/controller/*.java

# Executar a classe principal do Controlador
java -cp . com.damas.controller.TabuleiroDamasJava2D
```

### Opção 2: Pelo Sublime Text 4200
Para compilar diretamente pelo atalho **`Ctrl + B`** no Sublime Text, configure um sistema de build próprio:

1. No Sublime Text, vá em `Tools` > `Build System` > `New Build System...`.
2. Cole a seguinte configuração:
```json
{
    "shell_cmd": "javac -d . src/com/damas/model/*.java src/com/damas/view/*.java src/com/damas/controller/*.java && java -cp . com.damas.controller.TabuleiroDamasJava2D",
    "working_dir": "\${folder}",
    "selector": "source.java",
    "file_regex": "^(...*?):([0-9]*):?([0-9]*)"
}
```
3. Salve o arquivo como `Java_MVC_Damas.sublime-build`.
4. Abra a pasta `QueenGame` no Sublime usando `File` > `Open Folder...`.
5. Selecione o build system em `Tools` > `Build System` > `Java_MVC_Damas` e aperte **`Ctrl + B`**.

---

## 🧠 Detalhes Técnicos da Lógica

*   **Recursão em Profundidade (DFS):** O método `calcularCaminhosCaptura` no modelo utiliza um tabuleiro simulado temporário para prever todas as combinações de zigue-zague possíveis da Dama e do Peão, limpando as simulações (*backtracking*) após encontrar a rota ideal.
*   **Tipagem Forte Encadeada:** Utilização de estruturas de dados parametrizadas (`Map<Point, List<Point>>`) para rastrear qual coordenada final de clique corresponde a quais peças específicas devem ser eliminadas do tabuleiro real.
*   **Encapsulamento Swing:** O painel de renderização (`PainelTabuleiro`) foi embutido como uma classe interna oculta de `DamasView`, permitindo uma comunicação direta e segura com os componentes de tela sem expor as rotas globais do sistema.

---
Desenvolvido como projeto prático de aprofundamento em Java Avançado e Programação Orientada a Objetos.
