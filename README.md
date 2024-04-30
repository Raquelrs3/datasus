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

- Estatistica descritiva dos dados numéricos:
  
|index|min|max|range|mean|median|std|skew|kurtosis|
|---|---|---|---|---|---|---|---|---|
|qa\_ações\_de\_promoção\_e\_prevenção\_em\_saúde|0\.0|772\.0|772\.0|0\.2781181558592775|0\.0|9\.641832767200151|48\.71511225791572|2645\.7807294862932|
|qa\_procedimentos\_com\_finalidade\_diagnóstica|0\.0|22041351\.0|22041351\.0|11236\.367198026115|180\.0|313411\.03457659384|55\.05718026995659|3126\.4256951910284|
|qa\_procedimentos\_clínicos|0\.0|13734713\.0|13734713\.0|7652\.968589725819|169\.0|212357\.66456236376|54\.91400837814016|3083\.8086543702952|
|qa\_procedimentos\_cirúrgicos|0\.0|1160208\.0|1160208\.0|634\.2640348202157|15\.0|17557\.826469134776|54\.93173773934537|3073\.1934543026505|
|qa\_transplantes\_de\_orgãos\_tecidos\_e\_células|0\.0|43331\.0|43331\.0|24\.336247955421253|0\.0|697\.6485807144024|50\.52686018070818|2730\.471234901263|
|qa\_medicamentos|0\.0|275271\.0|275271\.0|150\.00839455518283|0\.0|4250\.529074525467|52\.17241572421471|2874\.1577591079968|
|qa\_órteses\_próteses\_e\_materiais\_especiais|0\.0|305423\.0|305423\.0|159\.26254331734634|0\.0|4419\.7188224006|54\.597322992067866|3051\.728285261035|
|qa\_ações\_complementares\_da\_atenção\_à\_saúde|0\.0|4150572\.0|4150572\.0|2312\.827678744698|105\.0|64078\.843642112064|54\.81644820050376|3063\.6602349659506|
|qa\_total|1\.0|40333989\.0|40333988\.0|22170\.31280530066|559\.0|615454\.3079614354|54\.76756899583936|3069\.346324036978|
|qa\_ano|2019\.0|2023\.0|4\.0|2021\.0038479665104|2021\.0|1\.4131689723376004|-0\.006086324413953958|-1\.2979045808749547|
|qa\_dia\_mês|1\.0|12\.0|11\.0|6\.490028000332678|6\.0|3\.446149907584252|0\.002508973270863884|-1\.2135358571509796|
|va\_procedimentos\_com\_finalidade\_diagnóstica|0\.0|93159293\.75|93159293\.75|47307\.33689166861|NaN|1324821\.405293989|55\.649371768141734|3215\.1856069253063|
|va\_procedimentos\_clínicos|0\.0|581983001\.17|581983001\.17|254532\.9546456413|NaN|7087604\.560371395|56\.46179209623588|3328\.2507791242037|
|va\_procedimentos\_cirúrgicos|0\.0|611874395\.46|611874395\.46|293144\.6409578939|NaN|8214693\.274254715|56\.54503684641804|3336\.2933765201624|
|va\_transplantes\_de\_orgãos\_tecidos\_e\_células|0\.0|70987744\.28|70987744\.28|35563\.51995497743|NaN|1020419\.506022346|51\.126546616857645|2805\.690601422351|
|va\_medicamentos|0\.0|9678243\.59|9678243\.59|5174\.223828248888|NaN|144977\.90005544102|53\.33582815523455|2954\.6381297430503|
|va\_órteses\_próteses\_e\_materiais\_especiais|0\.0|162345594\.45|162345594\.45|82053\.15212859155|NaN|2282876\.183238872|54\.240404814104615|3026\.9318790937546|
|va\_ações\_complementares\_da\_atenção\_à\_saúde|0\.0|1066086609\.23|1066086609\.23|327904\.31763165776|NaN|9651804\.466863737|66\.26589483059479|5098\.585239812265|
|va\_total|44\.22|2257909652\.62|2257909608\.4|1045680\.1460386795|NaN|29196272\.495469738|55\.9181553631844|3247\.474447685956|
|va\_dia\_mês|1\.0|12\.0|11\.0|6\.490019628064806|NaN|3\.4461576272099355|0\.002515792310230712|-1\.2135421391980987|

 - Distribuição dos dados numéricos:
   ![dados numericos](https://github.com/Raquelrs3/datasus/assets/98356094/1b864707-975f-46e5-af49-2ca946b9ce1f)

- distribuição dos dados categóricos:
  ![dados categoricos](https://github.com/Raquelrs3/datasus/assets/98356094/85ca9160-33e1-4ffb-bea4-5fd5f18485c1)


## 5. Metodologia de Desenvolvimento do Projeto
 O projeto está sendo desenvolvido através da técnica CRISP-DM
 * Versão END-TO_END da solução,
 * Velocidade na entrega de valor,
 * Mapeamento de todos os possíveis problems.


##### Passo 01 - Descrição dos dados: Conhecimento dos dados, tipos, métricas estatísticas para identificar outliers, analise das métricas estatísticas e ajustes em features do dataset (preenchimento de NA's).


##### Passo 02 - Feature Engineering: Desenvolvimento de mapa mental para analisar o fenômeno, as variáveis e os principais aspectos que impactam cada uma delas. (passos a ser desenvolvido)


##### Passo 03 - Filtragem dos dados: Filtragem das linhas e excluir as colunas que não são relevantes para o modelo ou não fazem parte do escopo do negócio. EX: Dias em que as lojas estavam fevhadas ou inoperantes. (passos a ser desenvolvido)


##### Passo 04 - Análise Exploratória dos dados: Exploração dos dados para encontrar insights. (passos a ser desenvolvido)

