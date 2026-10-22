# Anamnese — Preenchimento guiado

Formulário de anamnese para biorressonância, desenvolvido em **HTML, CSS e JavaScript reunidos em um único arquivo**. Permite preencher o histórico em etapas curtas, revisar as respostas e baixar um PDF ao finalizar.

## Recursos

- 39 etapas de preenchimento, com no máximo quatro campos por etapa, seguidas de revisão final.
- 128 campos sobre dados pessoais, histórico clínico, tratamentos, alergias e sistemas do organismo.
- Navegação com **Continuar**, **Voltar** e **Editar esta etapa** na revisão.
- Barra de progresso e animações de transição.
- Layout adaptado para computador e celular.
- Fonte Roboto, com Arial como alternativa.
- Ícone da aba do navegador embutido no HTML.
- Cálculo automático da idade a partir da data de nascimento.
- Seleção de estado com as 27 UFs brasileiras.
- Formatação automática de CPF e telefones.
- Download de PDF em A4, com paginação e espaços para assinatura.

## Como abrir

1. Salve o arquivo `Anamnese.html` no computador.
2. Abra o arquivo com um navegador moderno, com JavaScript ativado.
3. Comece o preenchimento. Não é necessário instalar programas, dependências ou configurar um servidor para usar o arquivo local.

O formulário e a geração do PDF funcionam localmente. A fonte Roboto é solicitada ao Google Fonts e depende de acesso à internet; se não estiver disponível, o navegador utiliza uma fonte alternativa.

## Como preencher

1. Informe os dados apresentados na primeira etapa.
2. Clique em **Continuar** para avançar. Use **Voltar** quando precisar corrigir algo.
3. Nas perguntas de saúde, selecione **Sim**, **Não** ou **Não sei**, conforme o caso.
4. Ao chegar à revisão final, expanda cada etapa para conferir as respostas.
5. Para corrigir uma resposta, clique em **Editar esta etapa**. Depois avance novamente até a revisão.
6. Marque a declaração de veracidade das informações.
7. Clique em **Salvar informações em PDF** e confira o arquivo na pasta de downloads do navegador.

Campos em branco são registrados no PDF como **Não informado**. Os campos não são obrigatórios; quando preenchidos, alguns deles são verificados pelo navegador, como e-mail, CPF, telefone e data de nascimento.

### Idade automática

A idade é calculada considerando a data atual do dispositivo e se o aniversário já ocorreu no ano. Enquanto houver uma data de nascimento preenchida, a idade fica bloqueada para edição manual. Sem a data de nascimento, ela pode ser informada manualmente.

### Formatação dos dados

Digite os números; a pontuação é aplicada automaticamente.

| Campo | Exemplo de entrada | Resultado |
| --- | --- | --- |
| CPF | `11111111111` | `111.111.111-11` |
| Celular com DDD | `11989919526` | `(11) 98991-9526` |
| Telefone fixo com DDD | `1134567890` | `(11) 3456-7890` |

A máscara de CPF verifica o formato, mas não valida os dígitos verificadores nem consulta a situação cadastral. Os telefones utilizam o formato nacional com DDD, sem o código de país `+55`.

## PDF gerado

O PDF é criado diretamente no navegador, sem bibliotecas externas de geração de PDF. Inclui as perguntas e respostas, a data de geração, a declaração final, a numeração das páginas e espaços para assinatura do paciente e do profissional responsável.

O nome segue o padrão `Anamnese-Nome-do-paciente.pdf`. Quando o nome não é informado, o arquivo se chama `Anamnese-paciente.pdf`.

O documento usa uma apresentação própria, organizada por etapas; não reproduz exatamente a diagramação do formulário original. A fonte do PDF é Helvetica, independentemente da fonte usada na página.

A confirmação no formulário não é uma assinatura digital. O Termo de Consentimento Livre e Esclarecido deve ser assinado separadamente antes do exame.

## Dados e armazenamento

As respostas permanecem apenas na memória da página durante o preenchimento. O código não envia as respostas para um servidor e não utiliza banco de dados, cookies ou armazenamento local para salvá-las.

**Baixe o PDF antes de atualizar ou fechar a página.** Não há salvamento automático nem recuperação do preenchimento. O navegador pode exibir um aviso ao sair, mas não dependa dele para preservar os dados.

O carregamento da Roboto faz uma solicitação externa ao Google Fonts, sem incluir as respostas do formulário. O PDF baixado contém os dados preenchidos; guarde-o no local adequado para seu atendimento.

## Personalização do código

Abra `Anamnese.html` em um editor de texto ou código.

| Elemento | Onde alterar |
| --- | --- |
| Título da aba | Elemento `<title>` |
| Ícone da aba | Elemento `<link rel="icon">`, com SVG embutido |
| Cores principais | Variáveis CSS dentro de `:root` |
| Aparência e animações | Bloco `<style>` |
| Etapas e perguntas | Array `steps` no bloco `<script>` |
| Lista de UFs | `stateField.options` |
| Cálculo da idade | Funções `calculateAge()` e `syncAge()` |
| Máscaras | Funções `formatCPF()` e `formatPhone()` |
| Conteúdo e layout do PDF | Função `makePDF()` |
| Nome do arquivo PDF | Função `downloadPDF()` |

Ao adicionar perguntas, mantenha os identificadores `id` únicos e limite cada etapa a quatro campos. Algumas funções localizam campos pelo texto de seus rótulos; ao renomear nascimento, idade, UF ou CPF, atualize também as referências correspondentes no JavaScript. O nome usado no download do PDF é obtido de `answers.f0`.

Para hospedar em um serviço de páginas estáticas, pode-se usar uma cópia do arquivo com o nome `index.html`. O formulário não exige backend.

## Solução de problemas

| Situação | O que conferir |
| --- | --- |
| O formulário não aparece | Verifique se abriu o HTML em um navegador e se o JavaScript está ativado. |
| Não consigo avançar | Confira se algum campo preenchido apresenta formato inválido ou data de nascimento futura. |
| A idade está incorreta | Confira a data de nascimento e a data configurada no dispositivo. |
| Não consigo gerar o PDF | Na revisão final, marque a declaração de veracidade antes de clicar no botão. |
| O PDF não foi encontrado | Confira a lista de downloads e as permissões de download do navegador. |
| A fonte está diferente | Sem acesso ao Google Fonts, a página usa uma fonte alternativa. |
| Os dados desapareceram | Atualizar ou fechar a página encerra o preenchimento; não há recuperação automática. |

## Tecnologias

HTML5, CSS3 e JavaScript puro, com APIs nativas do navegador para criar e baixar o PDF. Sem processo de compilação ou instalação de pacotes para executar o arquivo entregue.
