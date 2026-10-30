<div align="center">

# Assembly MIPS

**Pequenos programas, grandes ideias sobre como um computador executa instruções.**

Uma coleção de exercícios de programação em Assembly para a arquitetura MIPS,
criada no início de 2021 com os simuladores SPIM e MARS.

[Comece aqui](#comece-aqui) · [Explore os exercícios](#mapa-dos-exercícios) · [Entenda o código](#um-passeio-pelo-código) · [Limitações](#limitações-conhecidas)

</div>

---

## O que há neste repositório?

Cada arquivo `.spim` é um exercício de estudo: alguns são programas completos,
outros são rotinas para chamar a partir de outro programa. Juntos, eles exploram
entrada e saída, operações aritméticas, decisões, laços, vetores, números de ponto
flutuante e manipulação de bits.

**Assembly** é uma linguagem de baixo nível cujas instruções se aproximam das
operações do processador. **MIPS** significa *Microprocessor without Interlocked
Pipeline Stages*: é uma família de arquiteturas de processadores muito usada no
ensino de organização de computadores. Um simulador permite executar e observar
essas instruções sem precisar de um processador físico MIPS.

> Os arquivos preservam exercícios e experimentos de aprendizagem. Consulte as
> [limitações conhecidas](#limitações-conhecidas) antes de usá-los como referência
> para um algoritmo completo ou para resultados em casos extremos.

## Comece aqui

### 1. Obtenha os arquivos

```bash
# Baixa o histórico e os arquivos do repositório para a pasta AssemblyMIPS.
git clone https://github.com/TyrionV8/AssemblyMIPS.git

# Entra na pasta criada pelo clone.
cd AssemblyMIPS
```

### 2. Escolha um simulador

- **[SPIM / QtSPIM](https://spimsimulator.sourceforge.net/)**: simulador MIPS com
  versões gráficas e de terminal. As instruções de linha de comando abaixo usam o
  programa `spim` disponível no sistema.
- **[MARS — MIPS Assembler and Runtime Simulator](https://github.com/dpetersanderson/MARS)**:
  ambiente gráfico de montagem e simulação, distribuído como arquivo Java. Consulte
  a página oficial para obter o arquivo e as instruções de execução.

No MARS, abra um arquivo `.spim` pelo menu **File → Open**; se necessário, selecione
«todos os arquivos» no seletor. Em seguida, use **Run → Assemble** para montar o
programa e **Run → Go** para executá-lo. A montagem traduz as instruções do arquivo
para uma representação que o simulador consegue executar. Forneça as entradas no
painel de execução quando solicitadas. No QtSPIM, carregue o arquivo, execute-o e
acompanhe a entrada e a saída no console.

Alguns exemplos usam *pseudoinstruções*: comandos aceitos pelo montador que podem
ser traduzidos em uma ou mais instruções MIPS. Use a configuração padrão do
simulador que as aceita. Execute um arquivo de cada vez; vários deles possuem seu
próprio ponto de entrada `main`.

### 3. Execute seu primeiro programa

No terminal, com o SPIM instalado e a partir da pasta do repositório:

```bash
# Carrega e executa o programa de saudação.
spim -file hello.spim
```

Após as mensagens de inicialização do simulador, a saída inclui:

```text
Ola Mundo
```

Agora experimente uma entrada interativa:

```bash
# Lê dois números inteiros e imprime a soma.
spim -file Soma2int.spim
```

Digite `7` e `5`, cada um em uma linha. O resultado é `12`. Os programas em geral
não mostram mensagens pedindo os valores: informe-os na ordem indicada abaixo.
A aparência da saída e o formato de números decimais podem variar entre simuladores.

## Mapa dos exercícios

As entradas são lidas na ordem apresentada. «Rotina» indica um trecho que precisa
ser chamado por outro código; nesses casos, o resultado pode ser observado nos
registradores, pequenas áreas de armazenamento do processador ou simulador.

| Arquivo | Ideia explorada | Entrada ou observação |
|---|---|---|
| [hello.spim](hello.spim) | Imprimir uma mensagem | Sem entrada; escreve `Ola Mundo`. |
| [Soma2int.spim](Soma2int.spim) | Soma de inteiros | Dois inteiros; imprime a soma. |
| [pneu.spim](pneu.spim) | Subtração de inteiros | Dois inteiros; imprime o primeiro menos o segundo. |
| [VelocidadeMedia.spim](VelocidadeMedia.spim) | Divisão com ponto flutuante | Distância em quilômetros e tempo em horas; imprime quilômetros por hora. |
| [MediaPonderada.spim](MediaPonderada.spim) | Laço e média ponderada | Quantidade de valores; depois, para cada valor, peso e valor. |
| [PrecoConsumidor.spim](PrecoConsumidor.spim) | Porcentagens e ponto flutuante | Preço de fábrica, percentual de lucro e percentual de impostos; imprime o preço acrescido. |
| [Teleferico.spim](Teleferico.spim) | Divisão inteira e arredondamento | Capacidade da cabine e número de passageiros; calcula viagens considerando um lugar reservado. |
| [BitParidade.spim](BitParidade.spim) | Contagem de bits e paridade | Um inteiro; imprime o bit de paridade e a saída calculada. |
| [DetectorOverflow.spim](DetectorOverflow.spim) | Tentativa de detectar transbordamento em soma | Primeiro um seletor (`0`: sem sinal; outro valor: com sinal), depois dois inteiros. Veja as limitações. |
| [Divisao.spim](Divisao.spim) | Divisão por subtrações e deslocamentos | Rotina `divfac`: recebe dividendo em `$a0` e divisor em `$a1`; coloca quociente em `LO` e resto em `HI`. |
| [Divisao2.spim](Divisao2.spim) | Experimento de divisão por deslocamentos | Lê dividendo e divisor; a rotina coloca resultados em `LO` e `HI`, mas não os imprime. |
| [Divisaobia.spim](Divisaobia.spim) | Experimento de divisão bit a bit | Lê dividendo e divisor; a rotina está incompleta e não retorna normalmente. |
| [NumDist.spim](NumDist.spim) | Experimento com elementos distintos | Rotina `elemDistintos`; recebe endereço do vetor em `$a0` e tamanho em `$a1`. |
| [NumDist2.spim](NumDist2.spim) | Experimento com valores repetidos em vetor | Usa um vetor fixo; calcula em `$v0`, sem imprimir. |
| [atividade 6 C para mips.spim](atividade%206%20C%20para%20mips.spim) | Condicionais e operações aritméticas | Usa os valores já presentes em `$s0` e `$s1`; não lê entrada. |
| [atividade 7 C para mips.spim](atividade%207%20C%20para%20mips.spim) | Laço para soma de valores | Lê uma quantidade e tenta somar valores; veja a limitação do contador. |

### Exemplos para experimentar

| Programa | Entradas, uma por linha | Resultado esperado no SPIM |
|---|---|---|
| `pneu.spim` | `32`, `26` | `6` |
| `VelocidadeMedia.spim` | `150`, `2` | `75` quilômetros por hora |
| `PrecoConsumidor.spim` | `100`, `10`, `20` | `130` |
| `MediaPonderada.spim` | `2`, `2`, `8`, `1`, `5` | `7` |
| `Teleferico.spim` | `5`, `10` | `3` viagens |
| `BitParidade.spim` | `7` | bit de paridade `1` e saída `135` |

Na média ponderada, por exemplo, a conta é **(2 × 8 + 1 × 5) ÷ (2 + 1) = 7**.
Em `Teleferico.spim`, uma cabine com capacidade para cinco pessoas transporta
quatro passageiros por viagem após reservar um lugar; dez passageiros exigem
três viagens.

## Um passeio pelo código

Em [`Soma2int.spim`](Soma2int.spim), a execução segue este caminho:

```text
ler o primeiro inteiro → guardar em $t0
ler o segundo inteiro  → guardar em $t1
somar os dois          → colocar o resultado em $a0
imprimir o resultado   → encerrar
```

A instrução `syscall` pede um serviço ao simulador. Nestes exercícios, o número em
`$v0` identifica o serviço; os argumentos e resultados usam registradores
específicos. Eis alguns dos serviços utilizados:

| Código em `$v0` | Serviço | Dado usado ou devolvido |
|---:|---|---|
| `1` | Imprimir inteiro | Inteiro em `$a0` |
| `2` | Imprimir número de precisão simples | Número em `$f12` |
| `3` | Imprimir número de precisão dupla | Número em `$f12` |
| `4` | Imprimir texto | Endereço do texto em `$a0` |
| `5` | Ler inteiro | Resultado em `$v0` |
| `6` | Ler número de precisão simples | Resultado em `$f0` |
| `7` | Ler número de precisão dupla | Resultado em `$f0` |
| `10` | Encerrar a execução | — |

Os registradores com prefixo `$f` armazenam dados usados em operações de ponto
flutuante. Precisão simples e dupla são formatos com capacidades diferentes para
representar números reais aproximados. As áreas especiais `HI` e `LO` aparecem
nos exercícios de divisão para guardar, respectivamente, resto e quociente.

**Sugestão de estudo:** execute `Soma2int.spim` passo a passo no simulador e observe
como `$v0`, `$t0`, `$t1` e `$a0` mudam. Depois compare com `MediaPonderada.spim`
para acompanhar um laço e registradores de ponto flutuante.

## Limitações conhecidas

- **Entradas e casos extremos:** os exemplos não fazem validação abrangente. Evite
  divisor zero, tempo zero, capacidade de cabine menor ou igual a um, quantidade
  não positiva na média e soma de pesos igual a zero. Operações com inteiros muito
  grandes também podem causar transbordamento (*overflow*), quando o resultado
  não cabe na representação usada.
- **Atividade 7:** o código decrementa `$t2`, mas a condição do laço usa `$t0`;
  com quantidade positiva, o laço não termina como pretendido.
- **Divisões e vetores:** são experimentos e não uma biblioteca validada. Em
  `Divisao2.spim` há uma inicialização de contador que o fluxo pula; em
  `Divisaobia.spim` faltam o retorno normal da rotina e tratamento completo de
  sinais. As rotinas de valores distintos também exigem revisão antes de confiar
  nos resultados para vetores arbitrários.
- **Paridade:** o código aceita valores até `128`, mas não rejeita negativos; a
  saída é calculada somando `128` quando a contagem de bits é ímpar. Use valores
  de `0` a `127` para estudar a inclusão do bit de paridade no oitavo bit.
- **Compatibilidade e texto:** os arquivos foram escritos para SPIM ou MARS, mas
  não há garantia de que todos se comportem da mesma forma em ambos. Alguns
  comentários usam uma codificação de texto antiga e podem apresentar caracteres
  estranhos em editores configurados para UTF-8. O SPIM 8.0 usado na revisão não
  concluiu `DetectorOverflow.spim` nos testes tentados; investigue a compatibilidade
  antes de utilizá-lo.

## Referências

- [SPIM: página do projeto e documentação](https://spimsimulator.sourceforge.net/)
- [MARS: repositório oficial e download](https://github.com/dpetersanderson/MARS)
- [Opções de linha de comando do SPIM](https://spimsimulator.sourceforge.net/SPIM_command-line.pdf)

## Licença

Este repositório não contém um arquivo de licença. Consulte o autor antes de
reutilizar ou distribuir o código em condições que exijam uma licença explícita.
