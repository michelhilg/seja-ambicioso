---
name: seja-ambicioso
description: Deixa uma tarefa ou um prompt mais ambicioso usando os tipos de ambição de Felix Rieseberg, Altitude (mirar no resultado, o objetivo por trás do objetivo), Profundidade (trabalhar como o melhor especialista da área, a partir dos dados brutos, validado por um juiz externo) e Alcance (trazer outras áreas e fazer o que os especialistas delas fazem). Escreve o plano ambicioso e um prompt reescrito, e depois executa o trabalho quando recebeu uma tarefa. Use quando o usuário digitar /seja-ambicioso, disser "seja mais ambicioso", "mira mais alto", "vai mais fundo nisso", "qual é o objetivo por trás do objetivo", "o que um especialista de ponta faria aqui", "sobe a régua", ou pedir para deixar um prompt mais ambicioso.
license: MIT
metadata:
  author: Michel Hilg (@michelhilg)
  original: be-ambitious, de Jay E | RoboNuggets (https://github.com/robonuggets/be-ambitious)
  source: https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/
---

# Seja ambicioso

Todas as ideias aqui vêm do artigo de Felix Rieseberg [How to be more ambitious: a tutorial for humans with models](https://felixrieseberg.com/how-to-be-more-ambitious-a-tutorial-for-humans-with-models/) ("Como ser mais ambicioso: um tutorial para humanos com modelos", 13 out. 2026). Felix trabalha no Claude, na Anthropic. Esta skill transforma o artigo dele em passos que um agente consegue seguir. As citações abaixo são traduções livres do original em inglês.

A maioria das pessoas usa um modelo no tamanho da tarefa que digitou. As habilidades dos modelos crescem de forma desigual, "impressionantes em algumas direções, insuficientes em outras" (Terence Tao), então o único jeito de achar as partes impressionantes é mirar mais alto do que parece razoável.

## As regras que mais importam

1. **Melhor, não maior.** Cada tipo eleva alguma coisa: o resultado (Altitude), o padrão de qualidade (Profundidade) ou o conjunto de perspectivas (Alcance). Nenhum deles significa mais entregas, mais funcionalidades ou missões paralelas. Se uma sugestão deixa o trabalho maior sem deixá-lo melhor, descarte.
2. **Faça o que o especialista faz, não como ele fala.** Quando trouxer uma área, use os métodos e os instrumentos dela. Trocar o vocabulário sem trocar os métodos é teatro: a conversa fica mais estranha e o resultado continua o mesmo.
3. **Um juiz externo decide se funcionou.** Nunca avalie o próprio trabalho. Encontre algo que não seja você nem o usuário para mostrar que o resultado está certo: um teste, um benchmark, uma reprodução, dados separados para validação, uma medição. O melhor de tudo é uma ferramenta que você possa rodar para ter feedback na hora.
4. **Trate a meta difícil como razoável.** Se um objetivo parece impossível, assuma que tem solução e siga em frente. Metas específicas e difíceis superam o "faça o seu melhor" (a revisão de Locke e Latham sobre 35 anos de pesquisa em definição de metas, citada por Felix). Reporte com honestidade diante do juiz: uma meta difícil não alcançada, com números reais, é um bom resultado. Uma meta forjada, não.
5. **Consiga o acesso, não finja.** Tudo isso exige um computador onde você possa instalar software e acesso aos dados reais, via conectores MCP (plug-ins que ligam um agente a outros apps) ou outros meios. Se faltar algum dos dois, diga exatamente o que falta e o que isso destravaria. Nunca invente uma fonte, ferramenta ou resultado para tapar o buraco.

## Entrada

A tarefa é o que vier depois de `/seja-ambicioso`. Se não vier nada, use o pedido mais recente do usuário. Se não houver nenhum, peça a tarefa em uma linha e pare.

Depois, decida o que você recebeu:

- **Uma tarefa para fazer** (conserta isso, constrói isso, analisa isso): planeje no nível ambicioso e depois execute.
- **Um prompt para melhorar** (um pedido de reescrita, ou uma tarefa destinada a outro agente ou ferramenta): pare depois do prompt reescrito.

Se não der para saber qual dos dois, pare depois do prompt reescrito.

## Escolha os tipos que se encaixam

Felix nomeia quatro tipos de ambição. **Velocidade** (o mesmo trabalho em menos tempo) é como a maioria das pessoas já usa IA e não exige criatividade, então ele pula esse tipo, e esta skill também. Use os outros três só onde fizerem sentido. A maioria das tarefas precisa de um ou dois.

| Tipo | Serve quando | Pule quando |
|---|---|---|
| Altitude | A tarefa serve a um resultado. Um bom sinal: as pessoas vão fazer reuniões sobre isso | Trabalho criativo sem resultado além de si mesmo |
| Profundidade | A tarefa precisa ser muito bem feita | Trabalho descartável |
| Alcance | O resultado precisa convencer pessoas, ou a área óbvia ficou sem ideias | Uma correção pontual com uma única resposta certa |

### Altitude: mire no resultado

Pergunte o que o usuário quer que aconteça depois. Qual é o objetivo por trás do objetivo? Felix costumava pedir ao Claude para corrigir crashes isolados. Depois passou a pedir para manter os apps livres de crashes.

Monte uma escada de três degraus, cada um mais ambicioso que o anterior. O exemplo de Felix é uma apresentação de revisão trimestral de negócios (QBR):

1. **Entenda, não só preencha.** Não fique só atualizando os números do template. Absorva todos os dados que conseguir e descubra "o que mudou neste trimestre, por quê, e o que deveríamos fazer a respeito".
2. **Chegue às decisões.** "Descubra quais são as três decisões mais urgentes diante de tudo o que você aprendeu e comece a trabalhar em possíveis caminhos, com argumentos a favor e contra."
3. **Substitua o ritual.** "A revisão existe para que a liderança detecte problemas cedo e direcione dinheiro e pessoas para os lugares certos. Desenhe um jeito melhor de fazer isso do que uma apresentação trimestral, mostre com o nosso próprio histórico que ele teria detectado as coisas antes, e rode-o em paralelo ao atual por um trimestre."

O degrau mais alto é onde vivem os fluxos de trabalho duradouros, aqueles que tiram o humano do circuito. Eles costumam exigir preparação antes. Para o Claude conseguir manter os apps de Felix livres de crashes, ele precisou buscar os relatórios de crash, mapear cada versão do app para o seu commit no git e usar máquinas Windows, macOS e Linux para reproduzir e verificar as correções. Inclua essa preparação como parte do plano.

Conheça o teto. "Vá ganhar dinheiro" ainda é alto demais para a maioria das empresas. Se um degrau não tem juiz externo, desça um degrau.

### Profundidade: trabalhe como os melhores da área

Desça um nível abaixo da tarefa, até os dados, as ferramentas e os problemas que estão por baixo dela. Continue avançando até que mesmo os melhores profissionais da área possam aprender algo com o trabalho.

- **Use os instrumentos do especialista.** Não só as palavras dele. Onde você usaria uma tabela em markdown, um cientista de dados de ponta usa um banco de dados e um modelo estatístico. O usuário não precisa saber o que os especialistas usam. Você normalmente sabe.
- **Defina uma meta absurda e trate-a como razoável.** A página carrega em 10 segundos e o usuário pediu 5? Mire em 200 milissegundos.
- **Questione o que todo mundo acredita.** Pegue os dados brutos e teste a crença de forma adversarial: "Acreditamos que o churn é um problema de onboarding. Tente reproduzir isso a partir dos dados brutos."
- **Produza conhecimento novo.** Quando estiver fundo nos dados, procure pontos cegos: "Construa uma simulação dos nossos clientes que reproduza o último ano a partir dos nossos logs. Depois encontre o sinal mais precoce de churn que ainda não conhecemos e mostre que ele prevê em dados que nunca viu."
- **Traga um juiz externo** (regra 3).

Passe toda análise de Profundidade pelo prompt de Felix:

> Quero uma versão mais profunda desta tarefa, não uma maior. Antes de reescrevê-la: (1) diga o que um profissional de ponta desta área faria aqui que eu não estou pedindo; (2) aponte o material mais bruto de onde ele partiria, em vez do que já chegou digerido para mim; (3) cite os métodos e as ferramentas específicas que ele usaria; (4) diga o que, além de você ou de mim, mostraria que o resultado está certo. Depois reescreva o meu prompt pedindo exatamente isso.

### Alcance: traga outras áreas

Olhe para o trabalho através de mais áreas do que antes era viável. Todo filme de assalto gasta os primeiros 30 minutos montando a equipe. É aqui que Felix vê mais mágica, e é o que exige mais criatividade.

- **Troque os substantivos por verbos.** Um truque de *A Arte da Inovação*, de Tom Kelley e Jonathan Littman. Uma revisão trimestral não é "uma apresentação". É "fazer pessoas ocupadas acreditarem numa história de causa e efeito, e decidirem sob incerteza, em 30 minutos". Os verbos mostram quais áreas podem ajudar.
- **Monte a equipe.** Aumente o que está em jogo: a apresentação precisa ser incrível ou os alienígenas explodem a Terra, então quem a humanidade envia? Para qualidade: um analista, um jornalista e um editor. Se for apresentada ao vivo: um motion designer e um designer de áudio. Como red team: um vendedor a descoberto (short seller) e um contador forense.
- **Pegue as ferramentas emprestadas.** Uma área traz o seu software, não só as suas ideias. Alex Albert, colega de Felix, renderiza projetos de design de interiores no Blender, uma ferramenta 3D.
- **Faça, não interprete** (regra 2). Não escreva como um short seller. Faça o que um short seller faz para pesquisar uma posição. Se você puder rodar subagentes, dê a cada área o seu próprio subagente, com o método e as ferramentas daquela área.

## Saída

Dimensione a saída de acordo com a tarefa: um prompt de uma linha recebe poucas linhas de plano, porque o prompt reescrito é o produto. Nesta ordem:

1. **O objetivo por trás do objetivo**, em uma linha.
2. **Os tipos que se encaixam**, uma linha para cada explicando o porquê, mais os que você pulou.
3. **O plano** para cada tipo escolhido. Altitude: a escada de três degraus. Profundidade: as quatro respostas do prompt de Felix e a meta difícil. Alcance: os verbos, depois a equipe com a área, o trabalho que ela faria de verdade e o método ou a ferramenta que usaria para isso.
4. **Do que precisa**: os dados, as ferramentas e os acessos, marcados como já disponíveis ou faltando.
5. **O prompt reescrito** em um único bloco cercado que o usuário possa copiar, escrito do jeito que ele digitaria, terminando com o juiz externo e o que conta como aprovado.
6. **Próximo passo.** Escolha o degrau mais alto que você consegue concluir e verificar com o acesso que tem agora. Para um prompt a melhorar, nomeie esse degrau e pare. Para uma tarefa a fazer, nomeie-o em uma linha e comece. Se até o primeiro degrau exigir um acesso que você não tem, peça e pare. Pergunte antes, também, quando o degrau substituir o que o usuário pediu em vez de elevá-lo, gastar dinheiro ou não puder ser desfeito. Ambição eleva o padrão, não as permissões.

## Um exemplo curto

`/seja-ambicioso corrige o crash na tela de login`

- **Objetivo por trás do objetivo:** as pessoas sempre conseguem fazer login.
- **Tipos:** Altitude e Profundidade. Alcance pulado, já que a correção de um crash tem uma única resposta certa.
- **Escada de Altitude:** (1) corrigir este crash com um teste que falha antes e passa depois; (2) encontrar todos os crashes desse tipo nos relatórios e corrigir a causa, não o sintoma; (3) manter o login livre de crashes: buscar os relatórios de crash, mapear versões para commits, reproduzir em todas as plataformas, corrigir e verificar sem esperar alguém pedir.
- **Profundidade:** partir dos dumps de crash e dos logs brutos, não do relato do bug. Reproduzir antes de corrigir. Meta: zero crashes de login na próxima versão, não "menos crashes".
- **Juiz externo:** o teste que falhava fica verde, e a taxa de crashes na ferramenta de monitoramento cai para zero naquela build.

## Por que isso funciona

Felix fecha falando de autoeficácia: pessoas que acreditam nas próprias capacidades realizam mais, e essa crença pode ser hackeada. George Dantzig resolveu dois problemas de estatística em aberto em 1939 porque achou que eram lição de casa. Roger Bannister quebrou a barreira da milha em quatro minutos em 1954, e outra pessoa quebrou de novo 46 dias depois. *O Jogo Interior do Tênis* defende que você joga melhor quando para de se esforçar tanto. O mesmo vale para o usuário e para o modelo: diga que a coisa difícil é possível e dê permissão para falhar diante de um juiz honesto.
