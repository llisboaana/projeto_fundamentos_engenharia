# Mini Rack / Data Center Doméstico ou de Laboratório: Dissipação de Calor, Modelagem 3D e Sustentabilidade

> **Projeto acadêmico interdisciplinar** — Fenômenos de Transporte e Ciências do Ambiente  
> Engenharia · UniCEUB · Brasília · 2026

[![Projeto acadêmico](https://img.shields.io/badge/Projeto-acad%C3%AAmico-163a5f)](#)
[![Modelagem](https://img.shields.io/badge/Modelagem-FreeCAD-2b7a78)](Arquivos_FCStd/README.md)
[![Desenhos técnicos](https://img.shields.io/badge/Desenhos-PDF%20%2F%20TechDraw-6b5b95)](Cotas/README.md)

**Autores:** Ana Carolina Lisboa, Ana Luíza Lagos e Tiago de Aquino Nunes.

## Visão geral

Este projeto estuda a dissipação de calor e a sustentabilidade de um mini rack/servidor doméstico ou de laboratório por meio de uma abordagem multidisciplinar. O trabalho combina:

- dimensionamento térmico teórico de dissipadores, incluindo condução bidimensional por diferenças finitas, resistência térmica e simulação no Energy2D;
- modelagem paramétrica tridimensional e montagem do **Gêmeo Digital** no FreeCAD;
- auditoria experimental de um servidor real **Lenovo ThinkCentre Edge 72**, com chipset Intel H61 (“Mahobay”) e soquete LGA 1155;
- análise de consumo energético, impacto ambiental e alternativas de mitigação.

As análises, os gráficos e as simulações em Python estão no [notebook do Google Colab](https://colab.research.google.com/drive/1X3opMWMkOxm0MP2yfDHxNptV3Cb9l-x2). Os modelos tridimensionais e as pranchas estão organizados em [`Arquivos_FCStd/`](Arquivos_FCStd/README.md) e [`Cotas/`](Cotas/README.md).

## Fenômenos de Transporte e materiais

### Circuito térmico

O modelo de resistências térmicas em série é:

$$
T_j = T_a + P \times (R_{jc} + R_{cs} + R_{sa})
$$

Para o caso teórico adotado — potência `P = 65 W`, temperatura ambiente `Ta = 35 °C`, limite de junção `Tj,max = 85 °C`, resistência junção-cápsula `Rjc = 0,3 °C/W` e cápsula-dissipador `Rcs = 0,1 °C/W` — a resistência térmica máxima admissível entre o dissipador e o ambiente (`Rsa,max`) é obtida isolando `Rsa` na equação do circuito térmico:

$$
R_{sa,\max}
= \frac{T_{j,\max}-T_a}{P}-R_{jc}-R_{cs}
= \frac{85-35}{65}-0{,}3-0{,}1
= 0{,}3692\,^\circ\text{C/W}
\approx 0{,}37\,^\circ\text{C/W}
$$

### Comparativo de materiais

Valores de referência adotados no estudo, com base em MatWeb, LME e na relação de Wiedemann–Franz:

| Material | Condutividade térmica \(k\) | Densidade \(\rho\) | Calor específico \(c_p\) | Custo indicativo | Considerações |
|---|---:|---:|---:|---:|---|
| Alumínio 6063-T5 | 209 W/(m·K) | 2,70 g/cm³ | 900 J/(kg·K) | US$ 3.036/t | Custo acessível, excelente extrudabilidade e economia energética de 95,5% na reciclagem. |
| Cobre C11000 (ETP) | 391 W/(m·K) | 8,90 g/cm³ | 394 J/(kg·K) | US$ 14.741/t | Cerca de 1,87× mais condutivo; indicado quando a condução pela base é prioritária. O transporte de elétrons livres contribui para sua elevada condutividade. |

## Validação experimental e telemetria

A caracterização do equipamento foi realizada com análises no Google Colab e telemetria Linux usando `lm-sensors`, `turbostat` (RAPL) e `dmidecode`.

| Subsistema | Medição / configuração | Referência e observações |
|---|---|---|
| CPU | Intel Core i3-3220, 22 nm, TDP de 55 W; média em repouso de 36,0 °C e pico estabilizado de 56,0 °C sob carga de 100%. Potência média RAPL em idle: 2,90 W. | Para o limite crítico, `Tpico = 56,0 °C < Tcrit = 105,0 °C`, com margem de `Tcrit - Tpico = 49,0 °C`. O valor `Tcase = 65,3 °C` é uma referência da temperatura da cápsula; não se calcula margem em relação a ele sem uma medição correspondente na cápsula. |
| Placa-mãe / chipset | PCB FR4 / Intel H61; estabilizada em 29,8 °C sob estresse. | Limite seguro contínuo adotado: 60,0 °C; limite crítico ACPI: 106,0 °C. |
| Memória RAM | 8 GB (2 × 4 GB), DDR3 Synchronous, 1600 MT/s, Dual-Channel. | Operação síncrona 1:1, sem gargalo identificado com o IMC da CPU e o barramento H61. |
| Armazenamento | HDD Seagate ST1000VM002 de 1 TB a 34,0 °C. | Abaixo do teto ideal de 40,0 °C adotado para longevidade mecânica. |

### Curva estimada do cooler

A leitura de `hwmon` é bloqueada pelo Embedded Controller da BIOS Lenovo. Por isso, a curva PWM do cooler de 92 mm foi estimada por interpolação linear a partir das quatro zonas abaixo:

| Zona | Temperatura de referência | Rotação estimada |
|---|---:|---:|
| Silent | 38 °C | 1.013 RPM |
| Normal | 65 °C | 2.000 RPM |
| Performance | 85 °C | 3.000 RPM |
| Full Speed | 105 °C | 3.200 RPM |

Os pontos representam a estimativa adotada no estudo, não uma leitura direta de rotação obtida via `hwmon`.

## Ciências do Ambiente, energia e sustentabilidade

### Auditoria energética

A fonte avaliada é uma **LITEON PS-5281-02VA** de 280 W, 80 PLUS Básico, com eficiência informada de 82%, fabricada em 2009 (17 anos de uso em 2026). O consumo medido na tomada foi de 43,78 W em idle e 107,32 W sob carga. O estudo estima em **19,32 W** a potência desperdiçada como calor.

### Impacto estimado

O cenário informado utiliza PUE doméstico de 1,3, rotina diária de 16 h em idle e 8 h sob carga, tarifa de R$ 0,85/kWh e fator de emissão do ONS de 0,0842 kgCO₂/kWh.

| Indicador reportado | Valor |
|---|---:|
| Consumo mensal | 60,80 kWh/mês |
| Consumo anual | 739.78 kWh/ano |
| Custo anual | R$ 628,81/ano |
| Pegada de carbono anual | 62,290 kgCO₂/ano |

> **Nota de consistência dos dados:** os valores mensal e anual foram mantidos conforme reportados no estudo. Eles são compatíveis com convenções de período diferentes: 60,80 kWh corresponde aproximadamente a 30 dias, enquanto 739,75 kWh corresponde a 365 dias; por isso, multiplicar o valor mensal por 12 não reproduz o anual. A partir das potências informadas, 16 h em idle e 8 h sob carga resultam em cerca de 569,05 kWh/ano antes do PUE; multiplicando por 1,3, obtém-se aproximadamente 739,76 kWh/ano (diferença de 0,01 kWh atribuível a arredondamento). O custo anual e a emissão informados são compatíveis com o total anual reportado.

### Medidas de mitigação propostas

- substituir a fonte por uma unidade **80 PLUS Gold** (eficiência de referência de 92%);
- adotar um painel solar de 200 W;
- substituir HDDs por SSDs para reduzir consumo e calor;
- encaminhar equipamentos e componentes ao fluxo de descarte de resíduos eletroeletrônicos conforme a **ABNT NBR 16156**.

O estudo também considera a **ISO/IEC 30134-2** no contexto de indicadores de eficiência de data centers; a escala doméstica/laboratorial e as hipóteses utilizadas devem ser consideradas ao interpretar a comparação.

## Conteúdo do repositório

| Caminho | Conteúdo |
|---|---|
| [`Arquivos_FCStd/`](Arquivos_FCStd/README.md) | Modelos FreeCAD dos componentes e montagem do Gêmeo Digital. |
| [`Cotas/`](Cotas/README.md) | Pranchas PDF produzidas no TechDraw e referências de desenho técnico. |
| [Notebook Google Colab](https://colab.research.google.com/drive/1X3opMWMkOxm0MP2yfDHxNptV3Cb9l-x2) | Análises, gráficos e simulações em Python. |

## Como explorar

1. Abra os arquivos `.FCStd` com o FreeCAD para visualizar ou inspecionar os modelos paramétricos.
2. Consulte os PDFs da pasta `Cotas/` em um leitor de PDF compatível com suas camadas vetoriais e anotações.
3. Acesse o notebook Google Colab para acompanhar os cálculos e resultados computacionais.

Para detalhes sobre os arquivos e instruções de abertura, consulte os READMEs específicos de [modelagem FreeCAD](Arquivos_FCStd/README.md) e [desenhos técnicos](Cotas/README.md).