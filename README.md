# Chess System Java

Jogo de xadrez para dois jogadores no terminal, escrito em Java puro (sem dependências externas).
O tabuleiro é desenhado no console com cores ANSI e os lances são digitados em notação de coordenadas
(`e2` → `e4`).

```
8 R N B Q K B N R
7 P P P P P P P P
6 - - - - - - - -
5 - - - - - - - -
4 - - - - - - - -
3 - - - - - - - -
2 P P P P P P P P
1 R N B Q K B N R
  a b c d e f g h
```

## Funcionalidades

- Movimentação de todas as peças: Rei (K), Dama (Q), Torre (R), Bispo (B), Cavalo (N) e Peão (P)
- Destaque dos lances legais da peça selecionada
- Bloqueio de lances que deixam o próprio rei em xeque (incluindo peças cravadas)
- Detecção de **xeque**, **xeque-mate** e **afogamento** (empate)
- Lances especiais:
  - **Roque** pequeno e grande — não permitido com o rei em xeque nem atravessando casas atacadas
  - **En passant**
  - **Promoção** — o jogador escolhe Dama, Torre, Bispo ou Cavalo
- Lista de peças capturadas de cada lado

## Requisitos

- JDK 8 ou superior (o projeto Eclipse está configurado para Java 17)
- Terminal com suporte a cores ANSI (Windows Terminal, PowerShell 7, terminal do VS Code/IntelliJ,
  Linux, macOS). O `cmd.exe` antigo e o console do Eclipse podem exibir os códigos de cor como texto.

## Como executar

### Linha de comando

Na raiz do projeto:

```bash
javac -d bin $(find src -name "*.java")
```

```bash
java -cp bin application.Program
```

No PowerShell, para compilar:

```powershell
javac -d bin (Get-ChildItem -Recurse src -Filter *.java).FullName
```

### Eclipse / IntelliJ / VS Code

Importe a pasta como projeto Java existente (os arquivos `.project` e `.classpath` do Eclipse já estão
incluídos) e execute a classe `application.Program`.

## Como jogar

1. Em **Source**, digite a casa da peça que deseja mover (ex.: `e2`). Os lances possíveis ficam
   destacados em azul.
2. Em **Target**, digite a casa de destino (ex.: `e4`).
3. Para rocar, mova o rei duas casas (`e1` → `g1` ou `e1` → `c1`); a torre acompanha automaticamente.
4. Ao promover um peão, digite a letra da peça desejada: `Q` (Dama), `R` (Torre), `B` (Bispo) ou
   `N` (Cavalo).
5. Se um lance for inválido, a mensagem de erro é exibida — pressione **Enter** para continuar.

Peças brancas aparecem em branco e as pretas em amarelo. A partida termina em xeque-mate ou afogamento.

## Estrutura do projeto

O código é dividido em três camadas:

```
src/
├── boardgame/            # Camada de tabuleiro genérica (independente de xadrez)
│   ├── Board.java        # Matriz de peças, colocação e remoção
│   ├── Piece.java        # Peça abstrata com movimentos possíveis
│   ├── Position.java     # Posição linha/coluna na matriz
│   └── BoardException.java
├── chess/                # Regras do xadrez
│   ├── ChessMatch.java   # Partida: turnos, xeque, mate, afogamento, lances especiais
│   ├── ChessPiece.java   # Peça de xadrez (cor, contador de movimentos)
│   ├── ChessPosition.java# Conversão entre "e4" e posição da matriz
│   ├── Color.java
│   ├── ChessException.java
│   └── pieces/           # King, Queen, Rook, Bishop, Knight, Pawn
└── application/          # Interface de console
    ├── Program.java      # Loop principal da partida
    └── UI.java           # Desenho do tabuleiro e leitura de entrada
```

## Limitações conhecidas

- Não há empate por regra dos 50 lances, repetição de posição ou material insuficiente
- Não há desfazer lance, salvar partida nem jogo contra o computador
- Sem testes automatizados

## Créditos

Projeto desenvolvido como exercício do curso de Java do professor Nelio Alves (DevSuperior).
