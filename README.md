# Tabela de Pesquisa das Áreas de Abrangência das Unidades Locais de Saúde (ULS) - Versão 2024

## Introdução

Este repositório disponibiliza uma tabela de referência para mapear a relação entre divisões administrativas portuguesas (municípios e freguesias) e as unidades de saúde (ACES e ULS). A ferramenta foi desenvolvida para facilitar a integração e análise de dados geográficos no âmbito do Sistema Nacional de Saúde (SNS), sendo particularmente útil para investigadores, profissionais de saúde, analistas de dados e gestores públicos. 

A tabela inclui informações atualizadas até ao fim de 2024, contemplando mudanças recentes na organização territorial das unidades de saúde e os novos códigos NUTS (Nomenclatura das Unidades Territoriais para Fins Estatísticos). O objetivo principal é permitir uma consulta eficiente e a associação de diferentes níveis administrativos às suas respetivas áreas de influência no SNS.

## Estrutura dos Dados

O ficheiro `sns-geo-lookup.csv` contém as seguintes colunas, organizadas por categoria:

### Identificação Geográfica
- `pais`: Nome do país
- `pais_cod`: Código do país
- `distrito_2013`: Nome do distrito em 2013
- `distrito_2013_cod`: Código do distrito em 2013
- `municipio_2013`: Nome do município em 2013
- `municipio_2013_cod`: Código do município em 2013
- `municipio_2002_cod`: Código do município em 2002
- `municipio_2024`: Nome do município em 2024
- `freguesia_2013`: Nome da freguesia
- `dicofre_2013`: Código DICOFRE da freguesia

### Regiões Estatísticas (NUTS)
- `nuts1_2013`: Nome da região NUTS1 em 2013
- `nuts1_2013_cod`: Código da região NUTS1 em 2013
- `nuts2_2013`: Nome da região NUTS2 em 2013
- `nuts2_2013_cod`: Código da região NUTS2 em 2013
- `nuts3_2013`: Nome da região NUTS3 em 2013
- `nuts3_2013_cod`: Código da região NUTS3 em 2013
- `nuts3_2002_cod`: Código da região NUTS3 em 2002
- `nuts1_2024`: Nome da região NUTS1 em 2024
- `nuts1_2024_cod`: Código da região NUTS1 em 2024
- `nuts2_2024`: Nome da região NUTS2 em 2024
- `nuts2_2024_cod`: Código da região NUTS2 em 2024
- `nuts3_2024`: Nome da região NUTS3 em 2024
- `nuts3_2024_cod`: Código da região NUTS3 em 2024

### Saúde
- `ars_2023`: Nome da Administração Regional de Saúde (ARS) em 2023
- `ars_2023_cod`: Código da ARS em 2023
- `aces_2023`: Nome do ACES (Agrupamento de Centros de Saúde) em 2023
- `aces_2023_cod`: Código do ACES em 2023
- `uls_2024`: Nome da Unidade Local de Saúde (ULS) em 2024

## Como Utilizar

### 1. No Excel

O ficheiro pode ser carregado diretamente no Excel para consultas manuais:

1. Abra o Excel e clique em **Ficheiro > Abrir**.
2. Selecione `sns-geo-lookup.csv`.
3. Utilize a função `PROCV` para encontrar a ULS ou ACES correspondente a um município ou freguesia.

**Exemplo de PROCV para encontrar a ULS pelo município:**

```excel
=PROCV("Lisboa"; A:B; 2; FALSO)
```

Onde:

- "Lisboa" é o nome do município que queremos pesquisar;
- A:B é o intervalo de pesquisa (coluna com os municípios e colunas com as ULS);
- `2` indica que queremos a segunda coluna do intervalo de pesquisa;
- `FALSO` assegura que a correspondência é exata.

### 2. No R com Tidyverse

Pode carregar e utilizar a tabela com `tidyverse` para consultas mais avançadas.

#### Instalar pacotes necessários (se ainda não tiver instalado)

```r
install.packages("tidyverse")
```

#### Carregar e pesquisar a tabela

```r
library(tidyverse)

# Carregar os dados
sns_geo_lookup <- read_csv("sns-geo-lookup.csv")

# Procurar a ULS e ACES de uma freguesia específica
sns_geo_lookup %>%
  filter(freguesia_2013 == "Almada") %>%
  select(municipio_2013, aces_2023, uls_2024)
```

#### Juntar a tabela a outro dataset com `left_join()`

Caso tenha um conjunto de dados com informação de freguesias e queira adicionar a ULS correspondente:

```r
outros_dados <- data.frame(freguesia_2013 = c("Lisboa", "Porto", "Braga"))

dados_com_uls <- outros_dados %>%
  left_join(sns_geo_lookup, by = "freguesia_2013")
```

## Contribuições e Atualizações

Este projeto é de acesso livre. Caso encontre erros ou tenha sugestões de melhorias, pode submeter uma *issue* ou um *pull request* neste repositório.
