## Qual problema a aplicação resolve?

A aplicação foi desenvolvida para pessoas que estão em busca de uma nova oportunidade profissional e precisam adaptar seus currículos para diferentes vagas. Nesse processo, pode ser difícil entender o quanto o perfil do candidato está alinhado aos requisitos de cada oportunidade e quais informações do currículo precisam ser destacadas.

A plataforma ajuda a resolver esse problema ao analisar a vaga e compará-la com o currículo do candidato, apresentando um match de compatibilidade e indicando quais requisitos estão contemplados, quais possuem correspondência parcial e quais não foram identificados no currículo. A partir dessa análise, a aplicação também gera uma versão do currículo otimizada para ATS (Applicant Tracking System) e direcionada à vaga, reorganizando e destacando informações relevantes do currículo original para melhorar sua adequação aos critérios utilizados nesses sistemas.

Um princípio fundamental da aplicação é a transparência: nenhuma informação é inventada para aumentar artificialmente o match. Experiências, competências, ferramentas, formações ou qualquer outra informação adicionada ao currículo personalizado precisam estar presentes no currículo original ou ser explicitamente confirmadas pelo usuário.

Dessa forma, a plataforma não busca criar um candidato diferente para cada vaga, mas ajudar o candidato a apresentar melhor, para cada oportunidade, aquilo que ele realmente possui.

<img width="1917" height="867" alt="image" src="https://github.com/user-attachments/assets/313de252-8afb-4fc7-b2ba-a53439beccee" />

## Como é feita a análise

A aplicação permite que o candidato cole o link de uma vaga de emprego e compare os requisitos descritos no anúncio com as informações presentes em seu currículo.

A partir dessa comparação, a aplicação identifica:

- requisitos que possuem correspondência com o currículo;
- requisitos com correspondência parcial;
- requisitos que não foram identificados no currículo;
- palavras-chave relevantes para a vaga;
- pontos de atenção;
- oportunidades de adaptação do currículo.

O resultado apresenta não apenas o nível de compatibilidade, mas também as evidências encontradas no currículo que justificam cada correspondência - dessa forma, o candidato consegue entender de onde vem o resultado da análise e quais pontos pode melhorar ou esclarecer. Quando existe uma possível correspondência, mas não há informações suficientes para confirmá-la, a aplicação sinaliza a situação e permite que o usuário confirme ou complemente a informação antes que ela seja utilizada.

Após a análise, o usuário pode gerar uma versão do currículo otimizada para ATS (Applicant Tracking System) e direcionada à vaga. Essa versão reorganiza e destaca as informações mais relevantes para a oportunidade, utilizando somente dados presentes no currículo original ou informações explicitamente confirmadas pelo candidato.

## Requisitos da aplicação

Além das funcionalidades principais, a aplicação foi desenvolvida com foco em clareza, acessibilidade e facilidade de uso. A interface utiliza o shadcn/ui como design system e foi pensada para ser intuitiva e responsiva em diferentes dispositivos. A plataforma também possui suporte aos idiomas português e inglês, permitindo que o usuário alterne o idioma da interface conforme sua preferência. Outro requisito fundamental foi garantir a transparência das informações, evitando qualquer invenção ou alteração de dados do candidato durante a análise ou geração do currículo. As vagas são analisadas a partir de links externos fornecidos pelo próprio usuário, e o sistema sinaliza quando alguma informação não está disponível ou não pôde ser identificada.

## Prompts utilizados

O desenvolvimento da aplicação começou com um primeiro prompt direcionado ao ChatGPT, com o objetivo de estruturar os requisitos do projeto e transformá-los em um prompt completo para utilização no Lovable.

**Primeiro prompt — ChatGPT**

```
Chat, quero criar uma aplicação de matchmaking de vagas de emprego e criar versões do currículo do usuário que sejam ATS Friendly pra essa vaga. A aplicação será feita na lovable. Abaixo estão os requisitos da aplicação.

- Quero que você use o ShadCN como design system.
- O site deve ser de fácil entendimento, claro e intuitivo.
- O site não deve inventar nenhuma informação a cerca do currículo do candidato em relação a vaga.
- Transparência nas informações é fundamental.
- As vagas serão analisadas mediante links externos, coladas pelo candidato.

Me mande o prompt ÚNICO em formato markdown.
```
A partir desse direcionamento, foi criado um mega prompt específico para o Lovable, detalhando a estrutura da aplicação, fluxo de navegação, regras de negócio, componentes, critérios de análise, geração do currículo ATS e, principalmente, as regras de transparência e validação das informações.

**Segundo prompt — Lovable**

```
# Prompt para Lovable — Aplicação de Matchmaking de Vagas + Currículo ATS

Crie uma aplicação web de matchmaking entre candidatos e vagas de emprego, com geração de versões personalizadas e ATS-friendly do currículo do usuário para cada vaga analisada.

## 1. Objetivo principal

A aplicação deve ajudar o usuário a:

1. Cadastrar/importar seu currículo.
2. Colar o link de uma vaga de emprego.
3. Analisar o conteúdo real da vaga a partir do link fornecido.
4. Comparar os requisitos da vaga com as informações existentes no currículo.
5. Apresentar um diagnóstico transparente do nível de compatibilidade entre candidato e vaga.
6. Identificar competências, experiências e requisitos presentes ou ausentes.
7. Criar uma versão do currículo otimizada para ATS e direcionada àquela vaga.
8. Nunca inventar, extrapolar ou presumir informações sobre o candidato.
9. Mostrar claramente o que foi encontrado no currículo, o que foi encontrado na vaga e o que não foi possível determinar.

A aplicação deve priorizar **transparência, precisão, legibilidade e controle do usuário**.

---

# 2. Princípio fundamental

A regra mais importante do sistema é:

> **O currículo pode ser otimizado, mas nunca pode ser falsificado.**

O sistema NÃO deve:

- inventar experiências profissionais;
- inventar cargos;
- inventar empresas;
- inventar resultados ou métricas;
- inventar ferramentas utilizadas;
- inventar certificações;
- inventar idiomas;
- inventar formação;
- inventar competências;
- transformar uma habilidade desconhecida em uma habilidade comprovada;
- presumir que o candidato possui uma competência apenas porque ela é semelhante a outra;
- adicionar palavras-chave da vaga ao currículo sem evidência de que o candidato possui aquela competência;
- alterar datas, cargos ou informações factuais;
- criar experiências "prováveis" com base no perfil do usuário.

Quando uma informação necessária para a vaga não estiver no currículo, o sistema deve dizer explicitamente:

**"Não encontramos essa informação no seu currículo."**

Quando houver uma possível correspondência, mas não houver evidência suficiente, utilizar:

**"Possível correspondência — confirme se você possui essa experiência."**

O sistema nunca deve transformar uma possibilidade em fato.

---

# 3. Design System

Utilize obrigatoriamente **shadcn/ui** como design system principal.

Utilize os componentes do shadcn/ui sempre que houver um componente equivalente.

Priorizar:

- Button
- Card
- Badge
- Input
- Textarea
- Dialog
- Sheet
- Tabs
- Accordion
- Progress
- Alert
- Tooltip
- Select
- Dropdown Menu
- Separator
- Table
- Checkbox
- Switch
- Toast/Sonner
- Skeleton
- Avatar
- Scroll Area

O design deve ser:

- moderno;
- profissional;
- minimalista;
- claro;
- confiável;
- acessível;
- fácil de entender;
- visualmente organizado;
- com bastante espaço em branco;
- sem excesso de elementos decorativos.

Evite uma estética excessivamente "startup genérica".

A interface deve transmitir a sensação de uma ferramenta profissional de carreira e análise, não de um gerador mágico de currículo.

Utilize tipografia sans-serif.

Utilize hierarquia visual forte.

Utilize cards apenas quando eles ajudarem na organização das informações.

Não utilizar gradientes excessivos, glassmorphism exagerado, sombras pesadas ou animações desnecessárias.

---

# 4. Estrutura geral da aplicação

Criar as seguintes áreas:

## Dashboard

Página inicial após login.

Mostrar:

- saudação;
- resumo do currículo atual;
- quantidade de vagas analisadas;
- quantidade de currículos personalizados criados;
- histórico recente de vagas;
- botão principal "Analisar nova vaga".

Exemplo:

**Seu perfil**
Currículo atualizado em: DD/MM/AAAA

**Suas análises**
- 12 vagas analisadas
- 7 matches fortes
- 3 matches parciais
- 2 matches baixos

CTA:

**+ Analisar nova vaga**

---

# 5. Cadastro do currículo

Criar uma área chamada:

**Meu currículo**

O usuário poderá:

- fazer upload de currículo PDF;
- fazer upload de DOCX;
- colar o conteúdo do currículo;
- editar manualmente as informações extraídas.

Após o upload, o sistema deve estruturar as informações em:

### Informações pessoais
- Nome
- Localização
- Contato
- LinkedIn
- Portfólio
- Outros links profissionais

### Resumo profissional

### Experiência profissional
Para cada experiência:
- Cargo
- Empresa
- Período
- Descrição
- Responsabilidades
- Resultados

### Formação

### Competências

### Ferramentas

### Idiomas

### Certificações

### Cursos

### Projetos

### Outras informações

Após a extração, mostrar uma etapa de confirmação:

**"Revise suas informações antes de usar seu currículo nas análises."**

Permitir edição.

O usuário deve ser a fonte final de verdade sobre seu próprio currículo.

---

# 6. Análise de vaga

Criar uma tela chamada:

**Nova análise**

Campo principal:

**Cole o link da vaga**

Placeholder:

`https://empresa.com/vaga/...`

Botão:

**Analisar vaga**

A aplicação deve aceitar URLs externas de vagas.

O sistema deve tentar extrair:

- nome da empresa;
- cargo;
- localização;
- modalidade;
- senioridade;
- descrição;
- responsabilidades;
- requisitos obrigatórios;
- requisitos desejáveis;
- competências;
- ferramentas;
- idiomas;
- formação;
- experiência exigida;
- palavras-chave relevantes;
- benefícios, quando disponíveis;
- faixa salarial, quando disponível;
- outras informações relevantes.

Caso alguma informação não esteja disponível no anúncio, mostrar:

**"Não informado na vaga."**

Nunca preencher informações ausentes por inferência.

---

# 7. Transparência da análise da vaga

Depois de analisar o link, mostrar:

## Sobre a vaga

**Cargo:** Product Designer  
**Empresa:** Empresa X  
**Localização:** São Paulo, SP  
**Modalidade:** Híbrido  
**Senioridade:** Pleno

Abaixo:

### O que a vaga pede

Separar os requisitos em:

**Obrigatórios**

**Desejáveis**

**Responsabilidades**

**Competências**

**Ferramentas**

**Formação**

**Idiomas**

Cada informação deve ter indicação de origem.

Exemplo:

`Encontrado na descrição da vaga`

Caso não seja possível acessar ou interpretar corretamente a página:

Mostrar um alerta:

> **Não conseguimos analisar completamente esta vaga.**
>
> O site pode exigir login, bloquear acesso automático ou carregar o conteúdo dinamicamente.
>
> Para garantir uma análise transparente, não vamos inventar as informações ausentes.
>
> Você pode colar o texto da descrição da vaga abaixo.

Adicionar:

**[Colar descrição da vaga]**

---

# 8. Matchmaking

Criar uma tela de resultado chamada:

**Seu match com esta vaga**

Mostrar um indicador geral de compatibilidade.

Exemplo:

### 78%
**Compatibilidade estimada**

Importante: deixar claro que o percentual é uma estimativa baseada exclusivamente nas informações disponíveis.

Texto:

> "Este resultado representa a correspondência entre os requisitos identificados na vaga e as informações presentes no seu currículo. Não representa uma previsão de contratação."

Não apresentar o score como verdade absoluta.

---

# 9. Quebrar o match em categorias

Criar uma visualização detalhada:

### Experiência
78%

### Competências
90%

### Ferramentas
65%

### Formação
100%

### Idiomas
100%

### Requisitos específicos
50%

Cada categoria deve poder ser expandida.

---

# 10. Evidências do match

Esta é uma parte essencial da aplicação.

Para cada requisito da vaga, mostrar:

| Requisito da vaga | Evidência no currículo | Status |
|---|---|---|
| Figma | Experiência profissional X | Correspondência |
| UX Research | Projeto acadêmico X | Correspondência parcial |
| Inglês avançado | Não encontrado | Não identificado |
| 3 anos de experiência | Experiência total encontrada: 2 anos | Abaixo do requisito |

Utilizar badges:

### Correspondência
Verde ou neutro positivo.

### Correspondência parcial
Amarelo/neutro.

### Não identificado
Cinza.

### Não corresponde
Vermelho, mas sem linguagem punitiva.

---

# 11. Diferenciar ausência de informação de incompatibilidade

Isso é obrigatório.

Nunca tratar:

**"Não encontrado no currículo"**

como:

**"O candidato não possui essa competência."**

Exemplo:

Errado:

> "Você não sabe SQL."

Correto:

> "SQL não foi identificado nas informações disponíveis do seu currículo."

Essa distinção deve existir em toda a aplicação.

---

# 12. Área "Pontos fortes"

Mostrar quais requisitos da vaga possuem evidências claras no currículo.

Exemplo:

## Você atende bem a estes requisitos

- Figma
- Prototipação
- UX/UI
- Design Thinking
- Experiência em projetos digitais

Cada item deve apresentar a evidência correspondente.

Exemplo:

**Figma**
> Identificado na seção de competências do currículo.

---

# 13. Área "Pontos de atenção"

Mostrar requisitos:

- parcialmente atendidos;
- não encontrados;
- abaixo do nível solicitado.

Exemplo:

## Pontos de atenção

**Inglês avançado**
> O currículo informa inglês intermediário. A vaga solicita nível avançado.

**SQL**
> Não encontramos essa competência no currículo.

**Experiência em Product Design**
> Foram identificadas experiências relacionadas a UX/UI, mas não encontramos experiência explicitamente descrita como Product Design.

---

# 14. Área "Pergunte antes de editar"

Quando existir uma possível oportunidade de melhorar o currículo, mas a informação não estiver comprovada, o sistema deve perguntar ao usuário.

Exemplo:

> A vaga pede experiência com pesquisa com usuários.
>
> Encontramos projetos de UX no seu currículo, mas não há informação suficiente para afirmar que você realizou pesquisa com usuários.
>
> **Você possui essa experiência?**
>
> [Sim, adicionar] [Não] [Não tenho certeza]

Se o usuário responder "Sim", abrir campo:

> "Descreva brevemente essa experiência."

Somente depois da confirmação do usuário essa informação poderá entrar no currículo.

---

# 15. Otimização ATS

Criar botão:

**Criar currículo ATS para esta vaga**

Antes de gerar, mostrar um resumo:

> "Vamos reorganizar e adaptar seu currículo usando apenas informações confirmadas por você."

A versão ATS deve:

- utilizar estrutura simples;
- utilizar títulos convencionais;
- evitar tabelas complexas;
- evitar elementos gráficos;
- evitar ícones que possam prejudicar parsing;
- evitar colunas desnecessárias;
- utilizar palavras-chave relevantes da vaga quando elas forem comprovadas no currículo;
- reorganizar informações para destacar experiências relevantes;
- melhorar clareza textual;
- eliminar redundâncias;
- adaptar o resumo profissional;
- adaptar descrições de experiências;
- priorizar competências relevantes;
- manter todas as informações factualmente verdadeiras.

---

# 16. Regra de palavras-chave

O sistema deve identificar palavras-chave importantes da vaga.

Separar em:

### Palavras-chave encontradas no currículo

Podem ser utilizadas diretamente.

### Palavras-chave relacionadas

Podem ser utilizadas somente quando houver evidência suficiente de equivalência.

### Palavras-chave ausentes

Não devem ser adicionadas ao currículo automaticamente.

Exemplo:

A vaga pede:

**"Product Discovery"**

O currículo possui:

**"Pesquisa com usuários e definição de problemas."**

O sistema pode indicar:

> "Possível relação com Product Discovery. Confirme antes de utilizar o termo."

Nunca simplesmente substituir uma expressão pela outra sem confirmação.

---

# 17. Editor do currículo ATS

Criar editor dividido em duas áreas:

### Esquerda
Editor do currículo.

### Direita
Preview ATS.

Mostrar também uma barra superior com:

- Match atual;
- palavras-chave utilizadas;
- palavras-chave ainda não contempladas;
- alertas;
- status de validação.

Exemplo:

**ATS**
`92/100`

Mas deixar claro:

> "Score técnico de estrutura e cobertura de termos. Não representa probabilidade de contratação."

---

# 18. Alterações feitas pela IA

Mostrar um recurso:

**Ver alterações**

O usuário deve conseguir comparar:

### Antes
### Depois

Destacar:

- texto removido;
- texto reorganizado;
- texto reescrito;
- palavras-chave adicionadas;
- informações que permaneceram iguais.

Para cada alteração importante, mostrar o motivo.

Exemplo:

**Alteração**
> "Reorganizamos esta experiência para destacar Figma porque a ferramenta aparece como requisito da vaga."

---

# 19. Controle de confiança

Cada informação gerada pela aplicação deve possuir uma origem.

Criar estados:

### Confirmado
Informação explicitamente presente no currículo ou confirmada pelo usuário.

### Inferência possível
Existe relação provável, mas precisa de confirmação.

### Não identificado
Não há informação suficiente.

### Informação da vaga
Veio exclusivamente do anúncio da vaga.

Isso deve aparecer visualmente de forma simples.

---

# 20. Não inventar informações

Implementar uma camada de validação antes de salvar qualquer currículo personalizado.

Antes de gerar o currículo final, verificar:

- Todas as experiências existem no currículo original?
- Todas as empresas existem?
- Todos os cargos existem?
- Todas as datas permanecem iguais?
- Todas as ferramentas foram comprovadas?
- Todas as competências possuem origem?
- Todos os idiomas possuem origem?
- Todas as formações possuem origem?
- Todas as métricas/resultados possuem origem?
- Alguma palavra-chave foi adicionada sem evidência?
- Alguma experiência foi inferida?
- Alguma informação foi exagerada?

Se houver qualquer informação sem fonte:

**bloquear a geração automática e pedir confirmação.**

---

# 21. Histórico de análises

Criar página:

**Minhas análises**

Cada análise deve mostrar:

- empresa;
- cargo;
- data;
- score;
- status;
- currículo personalizado criado ou não.

Exemplo:

| Empresa | Vaga | Match | Data | Currículo |
|---|---|---:|---|---|
| Empresa A | UX Designer | 82% | 14/09/2026 | Criado |
| Empresa B | Product Designer | 67% | 12/09/2026 | Criado |
| Empresa C | UI Designer | 54% | 10/09/2026 | Não criado |

---

# 22. Página da análise

Ao abrir uma análise antiga, mostrar:

- informações da vaga;
- match;
- requisitos;
- evidências;
- pontos fortes;
- pontos de atenção;
- perguntas respondidas;
- currículo ATS gerado;
- histórico de alterações.

---

# 23. Dashboard inteligente

No dashboard, apresentar insights úteis sem exagerar.

Exemplo:

### Seus matches mais frequentes

**UX/UI**
8 vagas

**Product Design**
5 vagas

**Design de Produto**
4 vagas

Também mostrar:

### Competências mais solicitadas nas vagas analisadas

- Figma
- UX Research
- Prototipação
- Design Systems
- Product Discovery

E:

### Competências que aparecem nas vagas, mas ainda não estão identificadas no seu currículo

- SQL
- Analytics
- A/B Testing

Importante:

Não dizer que o usuário não possui essas competências.

Usar:

> "Não identificadas no seu currículo."

---

# 24. Segurança e privacidade

O currículo contém informações pessoais.

A aplicação deve:

- proteger dados do usuário;
- não expor currículo publicamente;
- não compartilhar dados sem consentimento;
- permitir exclusão dos dados;
- explicar de forma clara como os dados são utilizados;
- seguir boas práticas de privacidade e LGPD.

Criar uma área:

**Privacidade e dados**

Com:

- baixar meus dados;
- excluir meus dados;
- excluir currículo;
- excluir histórico de análises.

---

# 25. Estados de erro

Criar estados claros para:

### Link inválido

> "Este link não parece ser válido."

### Página inacessível

> "Não conseguimos acessar esta vaga."

### Conteúdo insuficiente

> "Conseguimos acessar a página, mas não encontramos informações suficientes sobre a vaga."

### Currículo vazio

> "Adicione seu currículo antes de realizar uma análise."

### Erro de processamento

> "Não conseguimos concluir a análise. Nenhuma informação foi adicionada ao seu currículo."

Nunca apresentar dados inventados como fallback.

---

# 26. UX Writing

A linguagem da aplicação deve ser:

- clara;
- humana;
- objetiva;
- profissional;
- fácil para pessoas que não entendem de ATS;
- sem excesso de termos técnicos.

Evitar:

"Seu NLP semantic embedding apresentou alta similaridade."

Preferir:

> "Encontramos uma boa correspondência entre esta exigência e seu currículo."

Sempre explicar termos técnicos quando forem necessários.

Exemplo:

**ATS**
> "Sistemas usados por empresas para organizar e filtrar currículos antes da análise humana."

---

# 27. Navegação

Sidebar desktop:

- Dashboard
- Meu currículo
- Nova análise
- Minhas análises
- Currículos
- Configurações

No mobile, utilizar navegação inferior ou menu responsivo.

CTA principal sempre evidente:

**Analisar nova vaga**

---

# 28. Responsividade

A aplicação deve ser totalmente responsiva.

Priorizar:

- desktop;
- tablet;
- mobile.

No mobile:

- transformar tabelas em cards;
- empilhar editor e preview;
- manter CTAs acessíveis;
- evitar textos excessivamente pequenos;
- preservar hierarquia visual.

---

# 29. Componentes importantes

Criar componentes reutilizáveis para:

- MatchScore
- RequirementCard
- EvidenceBadge
- SkillMatch
- ResumeSection
- ResumeEditor
- ResumePreview
- ChangeItem
- JobSummary
- AnalysisSummary
- ConfidenceBadge
- KeywordStatus
- EmptyState
- ErrorState
- LoadingState

---

# 30. Dados e arquitetura

Estruturar os dados de forma que exista separação clara entre:

### Candidate Data
Informações reais e confirmadas do candidato.

### Job Data
Informações extraídas da vaga.

### Match Data
Resultado da comparação entre os dois.

### Generated Resume
Versão personalizada criada a partir dos dados confirmados.

Nunca sobrescrever o currículo original ao criar uma versão personalizada.

O currículo original deve permanecer preservado.

Cada currículo personalizado deve possuir:

- ID;
- vaga relacionada;
- data de criação;
- versão;
- informações utilizadas;
- alterações realizadas.

---

# 31. Inteligência da aplicação

A IA deve funcionar como:

**analista + editor + assistente**

e não como:

**inventor de experiências.**

A lógica deve seguir:

`Currículo → Evidências → Vaga → Comparação → Perguntas de confirmação → Otimização → Validação → Currículo ATS`

Nunca:

`Vaga → preencher lacunas automaticamente`

---

# 32. Tela de resultado final

Após gerar o currículo:

Mostrar:

## Seu currículo está pronto

**Currículo: UX Designer — Empresa X**

### Otimizações realizadas

- Resumo profissional adaptado
- Experiências relevantes priorizadas
- Palavras-chave comprovadas destacadas
- Estrutura otimizada para ATS
- Informações não comprovadas não foram adicionadas

### Validação

**✓ Nenhuma informação nova foi adicionada sem confirmação**

Botões:

**[Editar currículo]**
**[Baixar PDF]**
**[Baixar DOCX]**
**[Ver alterações]**
**[Voltar para análise]**

---

# 33. Importante sobre PDF e DOCX

O currículo ATS deve priorizar uma estrutura textual simples.

Para exportação:

- PDF limpo;
- DOCX editável;
- sem elementos gráficos desnecessários;
- sem barras de proficiência;
- sem gráficos;
- sem ícones essenciais para interpretação;
- sem layouts que prejudiquem sistemas ATS.

---

# 34. Onboarding

Criar onboarding curto.

Tela 1:

**Encontre vagas que fazem sentido para você.**

Tela 2:

**Compare os requisitos com o que você realmente tem no currículo.**

Tela 3:

**Crie versões personalizadas sem inventar experiências.**

Tela 4:

**Você controla todas as informações antes de enviar.**

CTA:

**Começar**

---

# 35. Página inicial

Criar uma landing page simples.

Hero:

**Seu currículo não precisa dizer tudo.  
Ele precisa dizer o que é relevante para aquela vaga.**

Subheadline:

> Compare seu currículo com vagas reais, entenda onde você tem aderência e crie versões ATS-friendly sem inventar nenhuma informação.

CTA:

**Analisar uma vaga**

Segundo CTA:

**Conhecer como funciona**

Seções:

### Como funciona

1. Cole o link da vaga.
2. Compare a vaga com seu currículo.
3. Veja as evidências do match.
4. Confirme informações quando necessário.
5. Gere seu currículo personalizado.

### Transparência primeiro

Explicar:

> "A aplicação não preenche lacunas do seu currículo com suposições. Quando uma informação não é encontrada, nós mostramos que ela não foi identificada."

### ATS sem complicação

Explicar o conceito de ATS em linguagem simples.

---

# 36. Design visual

Criar uma identidade visual profissional e contemporânea.

Sugestão:

- fundo neutro;
- superfícies claras;
- texto escuro;
- uma cor de destaque;
- verde para correspondências;
- amarelo para atenção;
- vermelho apenas para incompatibilidades reais;
- cinza para informações não identificadas.

Não utilizar cores apenas como indicador de informação. Sempre acompanhar com texto, ícone ou badge para acessibilidade.

---

# 37. Microinterações

Utilizar animações discretas para:

- carregamento;
- mudança de score;
- expansão de requisitos;
- confirmação de ações;
- geração do currículo.

Não utilizar animações que atrasem a utilização.

Durante a análise da vaga, mostrar etapas:

**Acessando vaga...**

**Identificando requisitos...**

**Comparando com seu currículo...**

**Encontrando correspondências...**

**Preparando análise...**

---

# 38. Estado inicial sem dados

Se o usuário ainda não cadastrou currículo:

Mostrar:

**Comece pelo seu currículo**

> Para analisar uma vaga, precisamos saber quais informações você realmente possui.

CTA:

**Adicionar currículo**

Se já tiver currículo, mostrar:

**Seu currículo está pronto para análise.**

CTA:

**Analisar nova vaga**

---

# 39. Regras de negócio essenciais

Implementar obrigatoriamente:

1. Nunca inventar dados do candidato.
2. Nunca afirmar que o candidato possui uma habilidade sem evidência.
3. Nunca confundir ausência de informação com ausência de competência.
4. Nunca modificar dados factuais sem confirmação.
5. Nunca adicionar palavras-chave não comprovadas.
6. Sempre preservar o currículo original.
7. Sempre mostrar a origem das informações relevantes.
8. Permitir que o usuário corrija informações extraídas.
9. Pedir confirmação quando houver ambiguidade.
10. Informar quando a vaga não puder ser analisada completamente.
11. Não mascarar limitações da análise.
12. O score deve ser apresentado como estimativa, nunca como probabilidade de contratação.
13. O usuário deve poder revisar o currículo antes do download.
14. Toda informação gerada deve ser rastreável até uma informação do currículo ou uma confirmação explícita do usuário.
15. Se não houver evidência suficiente, a aplicação deve preferir dizer "não identificado" em vez de preencher a lacuna.

---

# 40. Stack

Utilizar:

- React
- TypeScript
- Tailwind CSS
- shadcn/ui
- Lucide Icons
- Supabase para autenticação e persistência, se necessário
- arquitetura modular e escalável

Organizar o código de maneira simples e sustentável.

Criar componentes reutilizáveis.

Evitar código duplicado.

Utilizar TypeScript de forma consistente.

---

# 41. Resultado esperado

O resultado deve parecer um produto real pronto para ser testado com usuários.

A experiência principal deve ser extremamente clara:

**Meu currículo → Link da vaga → Análise → Match → Evidências → Confirmações → Currículo ATS → Revisão → Download**

Priorize a confiança do usuário acima de qualquer tentativa de aumentar artificialmente o score.

A aplicação deve deixar claro que seu objetivo não é "fazer o candidato parecer perfeito para a vaga", mas sim:

> **mostrar com precisão o quanto o currículo atual corresponde à vaga e ajudar o candidato a apresentar melhor aquilo que ele realmente sabe e já fez.**

```
A principal preocupação durante a construção foi garantir que a aplicação utilizasse a IA para organizar, analisar e otimizar informações reais do candidato, e não para criar qualificações que não existem.
