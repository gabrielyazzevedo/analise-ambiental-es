# Impacto da Degradação de Manguezais após o Rompimento da Barragem de Mariana sobre a Pesca Artesanal no Litoral do Espírito Santo

Projeto Integrador III, Ciência da Computação.

Autores: Gabriely Barbosa da Silva Azevedo e Guilherme dos Santos Gonçalves Bispo

## Visão geral

Este projeto investiga, de forma quantitativa, a relação entre a degradação dos manguezais do Espírito Santo e a queda na produção pesqueira artesanal de espécies estuarino dependentes, com foco no rompimento da barragem de Fundão (Mariana, novembro de 2015) como ponto de quebra estrutural.

O Espírito Santo possui 411 km de litoral e uma das comunidades de pesca artesanal mais antigas e ativas do Brasil. Manguezais funcionam como berçário natural para espécies marinhas como o camarão sete barbas e o robalo. A hipótese central do projeto é que a degradação do manguezal, acelerada por Mariana, está associada à queda documentada nas capturas dessas espécies.

## Pergunta de pesquisa

A degradação dos manguezais do Espírito Santo, acelerada pelo desastre de Mariana, está associada à queda na produção pesqueira artesanal de espécies estuarino dependentes entre 2000 e 2023?

## Estrutura do repositório

```
ProjetoIII/
├── data/                                 dados brutos de entrada
│   ├── cobertura2009-2015.xlsx          Sea Around Us
│   ├── mapBiomas-coberturaManguezal.xlsx MapBiomas
│   └── relatorio-pesca.csv              PMAP-ES/UFES
├── dados_processados/                    séries exportadas pelo notebook
│   ├── serie_camarao_completa_2000_2023.csv
│   ├── serie_robalo_completa_2000_2023.csv
│   ├── serie_caranguejo_2000_2015.csv
│   ├── serie_manguezal_ES_1985_2023.csv
│   └── dados_cruzados_manguezal_pesca.csv
├── graficos_gerados/                     figuras fig01 a fig12
├── analise_pesca.ipynb                   notebook principal da análise
├── index.html                            landing page do projeto (GitHub Pages)
├── referencias.md                        fontes e bibliografia
└── README.md
```

## Fontes de dados

| Fonte | Período | Conteúdo |
|---|---|---|
| Sea Around Us | 2000 a 2015 | Reconstrução de capturas pesqueiras globais por espécie |
| PMAP ES/UFES | 2021 a 2023 | Boletim estatístico de pesca do Espírito Santo |
| MapBiomas Coleção 9 | 1985 a 2023 | Cobertura de manguezal no estado do ES |
| Boletim Estatístico da Pesca do ES (UFES, 2011) | referência | Contextualização histórica |

Existe uma lacuna de dados oficiais entre 2016 e 2020, reconhecida pela literatura (Musiello Fernandes et al., 2020; Braga et al., 2021) e tratada como limitação explícita do projeto, não como falha da análise.

## Metodologia

O notebook `analise_pesca.ipynb` está organizado nas seguintes seções:

1. **Configuração e importação de bibliotecas**: pandas, numpy, matplotlib, seaborn, scikit learn e statsmodels. A constante `MARIANA = 2015` é usada como ponto de quebra estrutural em todos os modelos.

2. **Carregamento e preparação dos dados**: leitura das bases Sea Around Us, PMAP ES e MapBiomas, tratamento de formatação numérica brasileira (separador de milhar e decimal), padronização de nomes de espécies e construção das séries combinadas de camarão, robalo e caranguejo.

3. **Análise exploratória**: série temporal de cobertura de manguezal, séries completas de captura por espécie, painel comparativo pré e pós Mariana, distribuição por município, sazonalidade mensal e correlação entre área de manguezal e captura de camarão.

4. **Modelagem estatística e de aprendizado de máquina**:
   - Regressão linear simples (baseline) da cobertura de manguezal
   - Regressão segmentada (Interrupted Time Series) pré e pós 2015, para manguezal e para camarão
   - Regressão múltipla OLS (statsmodels) relacionando área de manguezal, variável dummy pós Mariana e tendência temporal à captura de camarão
   - Regressão polinomial (graus 2, 3 e 4) para capturar a não linearidade da curva de manguezal
   - Projeção linear de captura de camarão para 2024 a 2026 com base nos pontos pós Mariana observados

5. **Insights e limitações**: painel consolidado de achados calculado diretamente das variáveis do notebook, e discussão explícita das limitações metodológicas.

6. **Exportação dos resultados**: geração dos arquivos CSV processados e das figuras fig01 a fig12.

7. **Conclusão**: síntese dos resultados, impacto social estimado e contribuição do projeto.

## Principais resultados

- **Manguezal**: crescimento de +24,1 ha/ano entre 1985 e 2015 (R² = 0,966), revertido para -16,5 ha/ano após 2015. O pico histórico de 5.286 ha (2014) nunca foi recuperado. Um modelo polinomial de grau 3 (R² = 0,935) confirma que essa inversão não é oscilação natural.

- **Camarão sete barbas**: queda de 43,3% já em 2012 (de 2.752 t para 1.560 t), antes mesmo do desastre. Entre 2021 e 2023, as capturas (375 a 418 t) representam menos de 15% do pico de 2011. Projeção para 2024 a 2026 indica continuidade da queda lenta.

- **Robalo**: declínio contínuo e acelerado, de aproximadamente 8,5 t no pico (2005 a 2006) para 0,21 t em 2023, redução superior a 96%.

- **Distribuição espacial**: Vitória concentra mais de 60% da captura estadual de camarão no período monitorado.

- **Sazonalidade**: o padrão sazonal histórico (pico em novembro, queda em janeiro e fevereiro por causa do defeso) se mantém, indicando que o problema é de volume de captura, não de abandono da atividade pesqueira.

## Impacto social estimado

A seção de conclusão do notebook traduz a queda de captura em estimativa de perda de renda para pescadores artesanais. Partindo da renda per capita de referência do IPEA/PNAD (proporção em relação ao salário mínimo) e aplicando a queda ponderada de captura de camarão e robalo sobre a parcela da renda associada a essas espécies, estima se uma perda de aproximadamente R$ 314,92 por mês por pescador, equivalente a cerca de 35% da renda mensal de referência. Cenários de perda agregada para 300 e 1.000 pescadores também são apresentados como referência de ordem de grandeza. Todas as premissas numéricas estão declaradas explicitamente no notebook e na landing page.

## Limitações declaradas

- Lacuna de dados oficiais entre 2016 e 2020 para o Espírito Santo.
- Dados do Sea Around Us são reconstruções com estimativas de subnotificação, não registros diretos (Pauly & Zeller, 2016).
- Os modelos identificam correlação e mudança de tendência, não causalidade estrita. O controle formal de variáveis adicionais, como efeitos fixos municipais e dados de temperatura da superfície do mar, é uma direção natural de aprofundamento, fora do escopo desta análise.
- Dados de caranguejo uçá disponíveis apenas até 2015, o que impede análise comparativa pré e pós Mariana para essa espécie.

## Como executar o notebook

1. Clone o repositório.
2. Instale as dependências: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `statsmodels`.
3. Abra `analise_pesca.ipynb` em Jupyter Notebook ou JupyterLab.
4. Execute as células em ordem. Os arquivos de dados de entrada devem estar na pasta `data/`.
5. As figuras e os CSVs processados são gerados automaticamente na seção 6 do notebook.

## Landing page

O arquivo `index.html` apresenta o projeto em formato de página web, com os principais achados, a linha do tempo do ponto de quebra de 2015 e a seção de impacto social. Está publicado via GitHub Pages em: https://gabrielyazzevedo.github.io/analise-ambiental-es/

## Vídeo de apresentação

[adicionar link do vídeo de apresentação]

## Referências

Ver `referencias.md` para a lista completa de fontes e bibliografia citadas no notebook e na landing page.
