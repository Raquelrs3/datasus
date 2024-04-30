Análise dos Dados do Datasus
![Datasus_capa](https://github.com/Raquelrs3/datasus/assets/98356094/86267024-544c-46b8-9dde-1779fffd34e1)


Este é um projeto acadêmico realizado com dados públicos disponibilizados no site [DATASUS](https://datasus.saude.gov.br/informacoes-de-saude-tabnet/).


## Desenvolvimento do trabalho
O objetivo deste trabalho é criar uma base de dados com os dados das internações hospitalares no período de 2019 a 2023 na unidade temporal de mês, geograficamente agregados por Município.

## 1. Captação de dados
#### Biblioteca Selenium e Beautiful Soup
Ao decidir sobre os métodos de coleta de dados em um determinado site, considerei vários fatores que influenciaram minha escolha das bibliotecas Selenium e Beautiful Soup. A análise preliminar do site revelou que a interface era rica em elementos interativos, como botões de seleção e cliques, tornando o Beautiful Soup por si só insuficiente para extrair efetivamente os dados necessários.

A complexidade da interação exige o uso do Selenium, que proporciona uma forma flexível e precisa de navegar no site, selecionar as opções necessárias e simular os cliques necessários para acessar conteúdos relevantes. Portanto, todas as etapas de seleção e interação são concluídas com sucesso usando Selenium.

Porém, ao chegar às etapas finais do processo de coleta, enfrentei alguns outros desafios. Ao tentar baixar os dados através do botão de download disponibilizado no site, constatei que o arquivo obtido apresentava problemas de formatação, delimitadores incorretos e células contaminadas com sujeira. Mesmo ao tentar salvar diretamente no conjunto de dados, a qualidade dos dados não é a esperada.

Diante desse obstáculo, optei por usar o Beautiful Soup para extrair o conteúdo HTML diretamente da página final de download. O que me permitiu identificar e selecionar apenas classes específicas que contenham os dados necessários. Coonseguindo assim superar inconsistências nos arquivos baixados pelo botão de download e realizar a extração dos dados de forma mais limpa e eficiente.


## 2. Criação as bases de dados - Qualidade aprovada e Valor aprovado
#### Dataframe
Ao preparar os bancos de dados de Qualidade de Aprovada e Valor de Aprovado, adotei uma estratégia de incorporar os dados diretamente em um dataframe. Devido à natureza única dos dados, optei por processá-los primeiro individualmente e depois juntá-los horizontalmente.

Depois de preparar cada conjunto de dados individualmente, passei para a etapa de concatenação horizontal. Esta abordagem permitiu-me combinar os dados de qualidade e valor em um único dataframe, preservando a distinção entre os dois tipos de informação. 


## 3. Definição das variáveis - Dicionário de Dados


| VARIÁVEL | DEFINIÇÃO | 
| -------------------  | ------------------- |
|qa_município | O município referente aos dados de qualidade aprovada de saúde.|
|qa_ações_de_promoção_e_prevenção_em_saúde | A quantidade de ações de promoção e prevenção em saúde realizadas.|
|qa_procedimentos_com_finalidade_diagnóstica	| A quantidade de procedimentos com finalidade diagnóstica realizados.|
|qa_procedimentos_clínicos | A quantidade de procedimentos clínicos realizados.|
|qa_procedimentos_cirúrgicos	| A quantidade de procedimentos cirúrgicos realizados.|
|qa_transplantes_de_orgãos_tecidos_e_células	| A quantidade de transplantes de órgãos, tecidos e células realizados.
|qa_medicamentos	| A quantidade de medicamentos administrados ou distribuídos.|
|qa_órteses_próteses_e_materiais_especiais | A quantidade de órteses, próteses e materiais especiais utilizados ou fornecidos.|
|qa_ações_complementares_da_atenção_à_saúde	| A quantidade de ações complementares da atenção à saúde realizadas.|
|qa_total | O total de ocorrências relacionadas à qualidade aprovada de saúde.|
|qa_período	| O período de tempo ao qual os dados se referem.|
|qa_mês	| O mês ao qual os dados se referem.|
|qa_ano	| O ano ao qual os dados se referem.|
|qa_dia_mês	| O dia do mês ao qual os dados se referem.|
|va_município	| O município referente aos dados de valor aprovado de saúde.|
|va_procedimentos_com_finalidade_diagnóstica	| A quantidade de procedimentos com finalidade diagnóstica realizados.|
|va_procedimentos_clínicos| A quantidade de procedimentos clínicos realizados.|
|va_procedimentos_cirúrgicos	| A quantidade de procedimentos cirúrgicos realizados.|
|va_transplantes_de_orgãos_tecidos_e_células	| A quantidade de transplantes de órgãos, tecidos e células realizados.|
|va_medicamentos	A quantidade de medicamentos administrados ou distribuídos.|
|va_órteses_próteses_e_materiais_especiais | A quantidade de órteses, próteses e materiais especiais utilizados ou fornecidos.|
|va_ações_complementares_da_atenção_à_saúde | A quantidade de ações complementares da atenção à saúde realizadas.|
|va_total | O total de ocorrências relacionadas ao valor aprovado de saúde.|
|va_período	| O período de tempo ao qual os dados se referem.|
|va_mês	| O mês ao qual os dados se referem.|
|va_ano	| O ano ao qual os dados se referem.|
|va_dia_mês	| O dia do mês ao qual os dados se referem.|
|qa_código_município | O código do município referente aos dados de qualidade aprovada de saúde.|
|va_código_município | O código do município referente aos dados de valor aprovado de saúde.|
|CODIGO_MUNICIPIO | O código do município.|
|LONGITUDE | A longitude geográfica do município.|
|LATITUDE | A latitude geográfica do município.|
|NU_Populacao | O número de habitantes do município.|
 
## 4. Qualidade dos dados
Para verificar a qualidade dos dados, utilizei estatísticas descritivas para identificar outliers, missing values e outros tipos de anomalias.

Primeiramente, verifiquei a presença de dados nulos. Identifiquei que, nesse caso, os dados ausentes eram representados por um caractere "-", os quais substituí por 0, pois não afetariam as análises futuras. Além disso, procedi à correção dos tipos de dados, garantindo que estivessem corretamente categorizados como inteiros, ponto flutuante ou objetos. No entanto, enfrentei uma dificuldade ao tentar converter a data para o formato de dataframe, uma vez que estava no padrão "Jan/2019". Por isso, optei por separar esses dados em colunas distintas referentes aos seus respectivos meses e anos.

Em relação às anomalias, observei a presença de totais agregados nos conjuntos de dados, os quais foram removidos para evitar distorções nas análises. Além disso, alguns nomes de municípios estavam acompanhados de códigos, o que exigiu um processo de limpeza e organização para atribuir os dados às colunas corretas.

No notebook, realizei uma análise descritiva detalhada, calculando medidas centrais principais para compreender o comportamento dos dados e identificar possíveis outliers. Isso proporcionou uma visão abrangente da distribuição dos dados e permitiu a identificação de padrões e discrepâncias que poderiam influenciar as análises posteriores.

 
## 5. Metodologia de Desenvolvimento do Projeto
 O projeto está sendo desenvolvido através da técnica CRISP-DM
 * Versão END-TO_END da solução,
 * Velocidade na entrega de valor,
 * Mapeamento de todos os possíveis problems.


##### Passo 01 - Descrição dos dados: Conhecimento dos dados, tipos, métricas estatísticas para identificar outliers, analise das métricas estatísticas e ajustes em features do dataset (preenchimento de NA's).


##### Passo 02 - Feature Engineering: Desenvolvimento de mapa mental para analisar o fenômeno, as variáveis e os principais aspectos que impactam cada uma delas. (passos a ser desenvolvido)


##### Passo 03 - Filtragem dos dados: Filtragem das linhas e excluir as colunas que não são relevantes para o modelo ou não fazem parte do escopo do negócio. EX: Dias em que as lojas estavam fevhadas ou inoperantes. (passos a ser desenvolvido)


##### Passo 04 - Análise Exploratória dos dados: Exploração dos dados para encontrar insights. (passos a ser desenvolvido)

