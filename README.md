Análise dos Dados do Datasus
![Datasus_capa](https://github.com/Raquelrs3/datasus/assets/98356094/86267024-544c-46b8-9dde-1779fffd34e1)


Este é um projeto acadêmico realizado com dados públicos disponibilizados no site [DATASUS](https://datasus.saude.gov.br/informacoes-de-saude-tabnet/).


## Desenvolvimento do trabalho
O objetivo deste trabalho é criar uma base de dados com os dados das internações hospitalares no período de 2019 a 2023, geograficamente agregados por Município.

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
|quantidade_município | O município referente aos dados de qualidade aprovada de saúde.|
|quantidade_ações_de_promoção_e_prevenção_em_saúde | A quantidade de ações de promoção e prevenção em saúde realizadas.|
|quantidade_procedimentos_com_finalidade_diagnóstica	| A quantidade de procedimentos com finalidade diagnóstica realizados.|
|quantidade_procedimentos_clínicos | A quantidade de procedimentos clínicos realizados.|
|quantidade_procedimentos_cirúrgicos	| A quantidade de procedimentos cirúrgicos realizados.|
|quantidade_transplantes_de_orgãos_tecidos_e_células	| A quantidade de transplantes de órgãos, tecidos e células realizados.
|quantidade_medicamentos	| A quantidade de medicamentos administrados ou distribuídos.|
|quantidade_órteses_próteses_e_materiais_especiais | A quantidade de órteses, próteses e materiais especiais utilizados ou fornecidos.|
|quantidade_ações_complementares_da_atenção_à_saúde	| A quantidade de ações complementares da atenção à saúde realizadas.|
|quantidade_total | O total de ocorrências relacionadas à qualidade aprovada de saúde.|
|quantidade_período	| O período de tempo ao qual os dados se referem.|
|quantidade_mês	| O mês ao qual os dados se referem.|
|quantidade_ano	| O ano ao qual os dados se referem.|
|quantidade_dia_mês	| O dia do mês ao qual os dados se referem.|
|valor_município	| O município referente aos dados de valor aprovado de saúde.|
|valor_procedimentos_com_finalidade_diagnóstica	| A quantidade de procedimentos com finalidade diagnóstica realizados.|
|valor_procedimentos_clínicos| A quantidade de procedimentos clínicos realizados.|
|valor_procedimentos_cirúrgicos	| A quantidade de procedimentos cirúrgicos realizados.|
|valor_transplantes_de_orgãos_tecidos_e_células	| A quantidade de transplantes de órgãos, tecidos e células realizados.|
|valor_medicamentos	A quantidade de medicamentos administrados ou distribuídos.|
|valor_órteses_próteses_e_materiais_especiais | A quantidade de órteses, próteses e materiais especiais utilizados ou fornecidos.|
|valor_ações_complementares_da_atenção_à_saúde | A quantidade de ações complementares da atenção à saúde realizadas.|
|valor_total | O total de ocorrências relacionadas ao valor aprovado de saúde.|
|valor_período	| O período de tempo ao qual os dados se referem.|
|valor_mês	| O mês ao qual os dados se referem.|
|valor_ano	| O ano ao qual os dados se referem.|
|valor_dia_mês	| O dia do mês ao qual os dados se referem.|
|quantidade_código_município | O código do município referente aos dados de qualidade aprovada de saúde.|
|valor_código_município | O código do município referente aos dados de valor aprovado de saúde.|
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
|quantidade_ações_de_promoção_e_prevenção_em_saúde|1.00|772.00|771.00|36.83|NaN|104.71|3.95|16.02|
|quantidade_procedimentos_com_finalidade_diagnóstica|1.00|22041351.00|22041350.00|13762.27|NaN|346803.56|49.75|2552.10|
|quantidade_procedimentos_clínicos|1.00|13734713.00|13734712.00|7672.79|NaN|212632.18|54.84|3075.83|
|quantidade_procedimentos_cirúrgicos|1.00|1160208.00|1160207.00|974.71|NaN|21758.09|44.31|1998.81|
|quantidade_transplantes_de_orgãos_tecidos_e_células|1.00|43331.00|43330.00|458.11|NaN|2993.88|11.60|141.94|
|quantidade_medicamentos|1.00|275271.00|275270.00|658.68|NaN|8888.01|24.89|652.16|
|quantidade_órteses_próteses_e_materiais_especiais|1.00|305423.00|305422.00|636.10|NaN|8815.67|27.32|761.94|
|quantidade_ações_complementares_da_atenção_à_saúde|1.00|4150572.00|4150571.00|2861.01|NaN|71258.38|49.29|2476.10|
|quantidade_total|1.00|40333989.00|40333988.00|22170.31|559.00|615454.31|54.77|3069.35|
|quantidade_ano|2019.00|2023.00|4.00|2021.00|2021.00|1.41|-0.01|-1.30|
|quantidade_dia_mês|1.00|12.00|11.00|6.49|6.00|3.45|0.00|-1.21|
|valor_procedimentos_com_finalidade_diagnóstica|1.00|93159293.75|93159292.75|90033.95|NaN|1826610.82|40.34|1688.13|
|valor_procedimentos_clínicos|4.85|581983001.17|581982996.32|255172.46|NaN|7096491.21|56.39|3319.90|
|valor_procedimentos_cirúrgicos|11.84|611874395.46|611874383.62|446079.67|NaN|10130066.01|45.84|2191.62|
|valor_transplantes_de_orgãos_tecidos_e_células|12.00|70987744.28|70987732.28|666738.37|NaN|4370405.92|11.77|146.64|
|valor_medicamentos|0.35|9678243.59|9678243.24|22720.88|NaN|303145.95|25.45|670.55|
|valor_órteses_próteses_e_materiais_especiais|8.05|162345594.45|162345586.40|332276.85|NaN|4584875.96|26.95|745.31|
|valor_ações_complementares_da_atenção_à_saúde|4.00|1066086609.23|1066086605.23|405950.41|NaN|10737712.62|59.56|4118.34|
|valor_total|44.22|2257909652.62|2257909608.40|1045680.15|NaN|29196272.50|55.92|3247.47|
|valor_dia_mês|1.00|12.00|11.00|6.49|NaN|3.45|0.00|-1.21|



 - Distribuição dos dados numéricos:
  ![dados numericos](https://github.com/Raquelrs3/datasus/assets/98356094/02150c88-7e4c-46d5-9529-9a74d7d5218b)

- distribuição dos dados categóricos:
  ![dados categoricos](https://github.com/Raquelrs3/datasus/assets/98356094/6c151b7e-782c-4819-8dcd-1ce0d39e3df2)


## 5. Metodologia de Desenvolvimento do Projeto
 O projeto está sendo desenvolvido através da técnica CRISP-DM
 * Versão END-TO_END da solução,
 * Velocidade na entrega de valor,
 * Mapeamento de todos os possíveis problems.


##### Passo 01 - Descrição dos dados: Conhecimento dos dados, tipos, métricas estatísticas para identificar outliers, analise das métricas estatísticas e ajustes em features do dataset (preenchimento de NA's).


##### Passo 02 - Feature Engineering: Desenvolvimento de mapa mental para analisar o fenômeno, as variáveis e os principais aspectos que impactam cada uma delas. (passos a ser desenvolvido)


##### Passo 03 - Filtragem dos dados: Filtragem das linhas e excluir as colunas que não são relevantes para o modelo ou não fazem parte do escopo do negócio. (passos a ser desenvolvido)


##### Passo 04 - Análise Exploratória dos dados: Exploração dos dados para encontrar insights. (passos a ser desenvolvido)

