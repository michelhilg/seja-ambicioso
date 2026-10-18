<p align="center">
  <img src="assets/banner.png" alt="seja-ambicioso" width="100%">
</p>

# seja-ambicioso

Uma skill gratuita para o Claude que deixa o seu agente mais ambicioso quando você a chama.

Ela transforma o artigo de Felix Rieseberg [How to be more ambitious: a tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) ("Como ser mais ambicioso: um tutorial para humanos com modelos") em passos que um agente segue. Felix trabalha no Claude, na Anthropic. Todas as ideias são dele.

Esta é a versão 100% em português da skill [be-ambitious](https://github.com/robonuggets/be-ambitious), criada por Jay E | RoboNuggets.

## O que ela faz

A maioria de nós usa um modelo no tamanho da tarefa que digitou. O ponto de Felix: o modelo consegue fazer muito mais se você mirar mais alto, mais fundo ou mais amplo. Ele nomeia quatro tipos de ambição. A skill usa três deles:

| Tipo | A pergunta que ele faz | Exemplo |
|---|---|---|
| **Altitude** | Qual é o objetivo por trás do objetivo? | Não corrija um crash. Mantenha o app livre de crashes. |
| **Profundidade** | O que o melhor especialista da área faria, a partir dos dados brutos, e que verificação externa prova que está certo? | Não monte uma tabela em markdown. Carregue os dados num banco de dados e ajuste um modelo estatístico de verdade. |
| **Alcance** | Quais outras áreas ajudariam, e o que os especialistas delas fazem de fato? | Traga um jornalista, um editor e um short seller, e faça cada um executar o seu trabalho real. |

O quarto tipo, **Velocidade** (o mesmo trabalho em menos tempo), é como a maioria das pessoas já usa IA, então Felix pula esse tipo, e a skill também.

Quando você a chama, a skill:

1. Encontra o objetivo por trás do objetivo.
2. Escolhe os tipos que se encaixam na sua tarefa (normalmente um ou dois, não os três).
3. Escreve o plano ambicioso: uma escada de 3 degraus para Altitude, as quatro perguntas de especialista de Felix para Profundidade e a equipe para Alcance.
4. Lista os dados, as ferramentas e os acessos que o plano exige, e o que está faltando.
5. Reescreve o seu prompt nesse nível, terminando com uma verificação externa e o que conta como aprovado.
6. Executa o trabalho, se você passou uma tarefa. Para depois da reescrita, se você passou um prompt para melhorar.

Ela segue algumas regras firmes do artigo: melhor, não maior. Faça o que o especialista faz, não teatro. Nunca avalie o próprio trabalho. Trate a meta difícil como razoável e reporte com honestidade diante da verificação.

## Instalação

**Claude Code.** Coloque a skill numa pasta chamada `seja-ambicioso` dentro da sua pasta de skills.

Para todos os seus projetos:

```bash
git clone https://github.com/michelhilg/seja-ambicioso ~/.claude/skills/seja-ambicioso
```

Só para um projeto, rode isto a partir da pasta do projeto:

```bash
git clone https://github.com/michelhilg/seja-ambicioso .claude/skills/seja-ambicioso
```

A skill é um único arquivo, então copiar o `SKILL.md` para `~/.claude/skills/seja-ambicioso/` também funciona. No Windows, `~/.claude` é a pasta `.claude` dentro da sua pasta de usuário.

**claude.ai.** Compacte o `SKILL.md` e o `LICENSE` num .zip com uma pasta chamada `seja-ambicioso` e envie em Skills, nas configurações do claude.ai.

## Como usar

Digite `/seja-ambicioso` e a sua tarefa:

```text
/seja-ambicioso monta a apresentação da revisão trimestral a partir dos CSVs de vendas em /data
```

- **Uma tarefa para fazer** (corrigir, construir, analisar): você recebe o plano e o prompt reescrito, e então o agente começa pelo degrau que escolheu. Ele só pergunta antes se o degrau substituir o que você pediu, custar dinheiro ou não puder ser desfeito.
- **Um prompt para melhorar** ("reescreve este prompt", ou um prompt destinado a outra ferramenta): você recebe o plano e o prompt reescrito, e ela para.
- **Sem tarefa:** `/seja-ambicioso` sozinho usa o seu último pedido.

Você também pode pedir em linguagem natural, como "seja mais ambicioso com isso" ou "o que um especialista de ponta faria aqui?".

## Exemplo

Você digita:

```text
/seja-ambicioso o site de marketing leva 8 segundos para carregar, deixa ele mais rápido
```

Você recebe (de um teste real, resumido):

- **Objetivo por trás do objetivo:** nenhum visitante vai embora porque o site é lento.
- **Tipos:** Altitude e Profundidade. Alcance pulado, já que acelerar um site tem basicamente uma resposta certa.
- **Escada de Altitude:**
  1. Colocar a página abaixo de um tempo de carregamento definido, com medições de antes e depois.
  2. Encontrar todas as páginas lentas e corrigir as causas.
  3. Manter o site rápido: um orçamento de performance verificado a cada deploy, que quebra o build quando é ultrapassado.
- **Profundidade:** partir de um trace real, não de palpites. Usar Lighthouse, WebPageTest, a cascata de rede e um analisador de bundle. Meta difícil: cerca de 200 ms até o primeiro conteúdo útil, não 5 segundos.
- **Juiz externo:** execuções repetidas e medidas, e números de usuários reais.
- **Prompt reescrito:**

```text
Nosso site de marketing leva 8 segundos para carregar. Comece por um trace real
(Lighthouse, WebPageTest, a cascata de rede), não por palpites, e liste as maiores
causas por custo de tempo. Corrija na ordem, medindo depois de cada correção. Mire em
cerca de 200 ms até o primeiro conteúdo útil. Depois adicione um orçamento de
performance aos nossos deploys para que o site não fique lento de novo.
Aprovado = execuções de teste repetidas mostram a meta atingida, e a verificação do
deploy falha quando o orçamento é estourado. Reporte números reais, incluindo
qualquer meta não atingida.
```

Então ela começa: uma rodada base do Lighthouse no site no ar, as requisições mais lentas ranqueadas e a principal causa corrigida e medida de novo.

## Do que ela precisa

A observação de Felix, e ela importa: tudo isso exige um modelo com **um computador onde ele possa instalar software** e **acesso aos dados reais**, via conectores MCP (plug-ins que ligam o agente aos seus apps) ou outros meios. Sem isso, a skill diz exatamente o que falta e o que isso destravaria. Ela não inventa dados para tapar o buraco.

## Créditos

- **Jay E | [RoboNuggets](https://www.skool.com/robonuggets)** pela skill original em inglês, [be-ambitious](https://github.com/robonuggets/be-ambitious), da qual este repositório é um fork traduzido. A estrutura, os passos e os exemplos desta versão são dele.
- **Felix Rieseberg** pelo artigo em que a skill se baseia: [How to be more ambitious: a tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) (13 out. 2026). Os tipos, os exemplos, o prompt de Profundidade e os alertas são dele.
- **DannyMac180** pela versão anterior, só de prompt: [DannyMac180/skills](https://github.com/DannyMac180/skills/tree/main/be-ambitious). Ela encapsula o prompt "mais fundo, não maior" de Felix. A versão do RoboNuggets acrescentou Altitude e Alcance.
- **Tom Kelley e Jonathan Littman** pelo truque de trocar substantivos por verbos, de *A Arte da Inovação*, que Felix usa em Alcance.

Tradução e adaptação para o português por **Michel Hilg** ([@michelhilg](https://www.instagram.com/michelhilg/)).

## Licença

MIT, a mesma do projeto original. Veja o arquivo [LICENSE](LICENSE), que mantém o aviso de copyright original do RoboNuggets ao lado do da tradução. O texto da licença fica em inglês de propósito, porque é o texto oficial da licença MIT.

Feito por [@michelhilg](https://www.instagram.com/michelhilg/), a partir do trabalho de [RoboNuggets](https://www.skool.com/robonuggets).
