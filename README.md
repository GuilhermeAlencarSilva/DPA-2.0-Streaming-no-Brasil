DPA Framework™ 2.0
Poder Estrutural no Mercado de Streaming Brasileiro (2022–2024)
1. Contexto Estratégico

Nos últimos anos, o mercado brasileiro de streaming passou por:

Crescimento acelerado de demanda

Entrada de novos players globais

Aumento do custo de conteúdo

Pressão por rentabilidade

Consolidação estrutural

A pergunta central deixou de ser:

“Quem tem mais assinantes?”

E passou a ser:

“Quem possui poder estrutural sustentável?”

Este projeto responde exatamente isso.

2. Problema de Pesquisa

O mercado aparenta competição intensa.

Mas:

A receita é distribuída proporcionalmente à atenção?

A escala garante captura de margem?

Quem reinveste o suficiente para reforçar vantagem?

O setor está caminhando para consolidação?

Para responder, foi aplicado o:

DPA Framework™ 2.0

(Digital Power Architecture)

3. Tese Central

Poder digital não é apenas escala.

Poder estrutural é a capacidade cumulativa de:

Capturar atenção

Converter em receita

Preservar margem

Reinvestir para reforçar a própria posição

Sustentar vantagem ao longo do tempo

O DPA 2.0 mede exatamente isso.

4. Escopo do Projeto

Região: Brasil
Período: 2022–2024
Frequência: Trimestral

Empresas analisadas:

Netflix

Amazon Prime Video

Disney+

Globoplay

HBO Max / Max

5. Arquitetura Analítica

O modelo parte de uma lógica encadeada:

Atenção → Receita → Margem → Reinvestimento → Reforço Estrutural

Cada etapa representa uma dimensão do poder competitivo.

6. Métricas Fundamentais
6.1 Escala — Share_A

Participação relativa de atenção no mercado.

Representa capacidade de atrair audiência.

6.2 Eficiência — RAM

Revenue Attention Multiplier

RAM = Share_R / Share_A

Indica capacidade de converter atenção em receita proporcional.

RAM > 1 → Captura acima da atenção
RAM < 1 → Submonetização

6.3 Captura — MCR

Margin Capture Ratio

Avalia capacidade de transformar receita em margem estrutural.

6.4 Reforço — CRC

Capital Reinforcement Coefficient

Proxy de capacidade de reinvestimento relativo.

Mede o quanto a empresa reforça sua própria posição.

7. O Índice Composto
DSPI — Digital Structural Power Index

O DSPI sintetiza as quatro dimensões.

DSPI = Média Normalizada
(Escala + Eficiência + Captura + Reforço)

O índice não mede desempenho pontual.

Ele mede poder estrutural cumulativo.

8. MEDIDAS Dax

Receita Total Mercado
Receita Total Mercado =
CALCULATE(
    SUM(Fato_Stream[Receita]),
    ALL(Fato_Stream[Empresa])
)
Atenção Total Mercado
Atencao Total Mercado =
CALCULATE(
    SUM(Fato_Stream[Atencao]),
    ALL(Fato_Stream[Empresa])
)
Reinvestimento Total Mercado
Reinv Total Mercado =
CALCULATE(
    SUM(Fato_Stream[Reinvestimento]),
    ALL(Fato_Stream[Empresa])
)
📊 2. SHARE DE ATENÇÃO E RECEITA
Share_A
Share_A =
DIVIDE(
    SUM(Fato_Stream[Atencao]),
    [Atencao Total Mercado]
)
Share_R
Share_R =
DIVIDE(
    SUM(Fato_Stream[Receita]),
    [Receita Total Mercado]
)
📊 3. RAM — Revenue Attention Multiplier
RAM =
DIVIDE(
    [Share_R],
    [Share_A]
)
📊 4. MARGEM E CAPTURA
Margem Média
Margem Media =
AVERAGE(Fato_Stream[Margem])
MCR — Margin Capture Ratio
MCR =
DIVIDE(
    [Margem Media],
    CALCULATE(
        AVERAGE(Fato_Stream[Margem]),
        ALL(Fato_Stream[Empresa])
    )
)
📊 5. CRC — Capital Reinforcement Coefficient
CRC =
DIVIDE(
    SUM(Fato_Stream[Reinvestimento]),
    [Reinv Total Mercado]
)
📊 6. NORMALIZAÇÕES (MIN-MAX)
Share_A Normalizado
Share_A_Norm =
VAR MinVal =
    MINX(ALL(Fato_Stream[Empresa]), [Share_A])
VAR MaxVal =
    MAXX(ALL(Fato_Stream[Empresa]), [Share_A])
RETURN
DIVIDE([Share_A] - MinVal, MaxVal - MinVal)
RAM Normalizado
RAM_Norm =
VAR MinVal =
    MINX(ALL(Fato_Stream[Empresa]), [RAM])
VAR MaxVal =
    MAXX(ALL(Fato_Stream[Empresa]), [RAM])
RETURN
DIVIDE([RAM] - MinVal, MaxVal - MinVal)
MCR Normalizado
MCR_Norm =
VAR MinVal =
    MINX(ALL(Fato_Stream[Empresa]), [MCR])
VAR MaxVal =
    MAXX(ALL(Fato_Stream[Empresa]), [MCR])
RETURN
DIVIDE([MCR] - MinVal, MaxVal - MinVal)
CRC Normalizado
CRC_Norm =
VAR MinVal =
    MINX(ALL(Fato_Stream[Empresa]), [CRC])
VAR MaxVal =
    MAXX(ALL(Fato_Stream[Empresa]), [CRC])
RETURN
DIVIDE([CRC] - MinVal, MaxVal - MinVal)
📊 7. DSPI — Digital Structural Power Index
DSPI =
AVERAGEX(
    {
        [Share_A_Norm],
        [RAM_Norm],
        [MCR_Norm],
        [CRC_Norm]
    },
    [Value]
)
DSPI Médio Mercado
DSPI Medio Mercado =
AVERAGEX(
    VALUES(Fato_Stream[Empresa]),
    [DSPI]
)
Líder Estrutural (Nome)
Lider Estrutural =
TOPN(
    1,
    VALUES(Fato_Stream[Empresa]),
    [DSPI],
    DESC
)
📊 8. HHI — Herfindahl-Hirschman Index

⚠️ Versão corrigida (não trava em 10.000)

HHI =
SUMX(
    VALUES(Fato_Stream[Empresa]),
    POWER([Share_R], 2)
) * 10000
📊 9. ASSIMETRIA ATENÇÃO vs RECEITA
Gap Captura =
[Share_R] - [Share_A]
📊 10. VOLATILIDADE DO DSPI
Desvio Padrão do DSPI por Empresa
Volatilidade DSPI =
STDEVX.P(
    VALUES(Dim_Tempo[AnoTri]),
    [DSPI]
)
📊 11. RECEITA TOTAL POR EMPRESA
Receita Total =
SUM(Fato_Stream[Receita])
📊 12. RECEITA TOTAL MERCADO (DINÂMICA)
Receita Mercado =
SUMX(
    VALUES(Fato_Stream[Empresa]),
    [Receita Total]
)
📊 13. MÉDIA DE DSPI POR PERÍODO
AVERAGE([DSPI])

9. Evolução do Framework
DPA 1.0

Métricas isoladas

Análise estática

Foco em desempenho operacional

Sem integração sistêmica

DPA 2.0

Integração causal das variáveis

Normalização competitiva

Índice composto

Avaliação dinâmica temporal

Medição de reforço cumulativo

O 1.0 media performance.

O 2.0 mede poder.

10. Estrutura do Dashboard
Página 1 — Estrutura de Poder

<img width="1037" height="798" alt="pag1" src="https://github.com/user-attachments/assets/9ed95d6b-ba53-4927-9e34-f54f71bbbd84" />

HHI

Ranking DSPI

Assimetria Atenção vs Receita

RAM

Objetivo: identificar dominância estrutural.

Página 2 — Estrutura Econômica

<img width="1119" height="799" alt="pag2" src="https://github.com/user-attachments/assets/900983c9-57cb-4895-8274-128eac799edd" />

Margem média

MCR

CRC

Objetivo: entender captura e reforço.

Página 3 — Dinâmica Temporal

<img width="1368" height="799" alt="pag3" src="https://github.com/user-attachments/assets/bb3eb612-1f3e-41df-8f0f-b2f45f1f3692" />

Evolução do DSPI

Evolução do HHI

Receita por player

Objetivo: detectar consolidação.

Página 4 — Arquitetura de Poder

<img width="1167" height="681" alt="pag4" src="https://github.com/user-attachments/assets/4a181fc1-b1fb-479f-a3e6-0d4d2c445c5d" />

Escala vs Eficiência

Decomposição do DSPI

Gap de captura

Objetivo: entender a origem da vantagem.

Página 5 — Sustentabilidade

<img width="1167" height="734" alt="pag5" src="https://github.com/user-attachments/assets/a2cc6206-7ba7-4295-8412-85b56d193e3f" />

Margem vs CRC

DSPI vs CRC

Volatilidade do DSPI

Objetivo: avaliar estabilidade estrutural.

Página 6 — Metodologia

<img width="874" height="746" alt="pag6" src="https://github.com/user-attachments/assets/f6045909-d0b4-4527-8fd1-6514d9d19f10" />

Fundamentos conceituais

Evolução 1.0 → 2.0

Fórmula estrutural

Objetivo: legitimidade analítica.

11. Principais Resultados

A análise revelou:

Mercado estruturalmente concentrado

Liderança cumulativa clara

Assimetria relevante entre atenção e captura

Reinvestimento como vetor crítico de consolidação

O setor não está apenas competindo.

Está consolidando.

12. Limitações Metodológicas

Receita Brasil estimada por proxies regionais quando necessário

Normalização relativa ao período analisado

Dados agregados trimestralmente

O modelo é comparativo, não absoluto.

13. Conclusão Estratégica

O mercado brasileiro de streaming apresenta sinais de dominância estrutural consolidada.

A diferença entre escala e poder ficou evidente.

Nem todo grande player é estruturalmente dominante.
E nem todo player eficiente possui escala suficiente para consolidar poder.

O DPA 2.0 permite separar performance de poder.

Essa distinção é o principal valor estratégico do projeto.

14. Como Reproduzir

Importar arquivos CSV

Criar modelo estrela

Inserir medidas DAX documentadas

Replicar estrutura das páginas

Aplicar normalização min-max

15. Aplicações Futuras

O modelo pode ser replicado para:

Fintech

E-commerce

Marketplaces

EdTech

Super apps

Qualquer mercado digital baseado em atenção.

📜 Licença

Uso acadêmico e analítico. Framework proprietário DPA™ — Digital Power Asymmetry.

👤 Autor

Guilherme Alencar - linkedin: https://www.linkedin.com/in/guilherme-alencar-327413213/

Especialização em:

Estrutura de mercado

Economia digital

Modelagem competitiva

Business Intelligence estratégico
