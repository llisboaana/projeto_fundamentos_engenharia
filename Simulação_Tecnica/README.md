# Simulação Térmica — Energy2D

**Projeto acadêmico interdisciplinar — Fenômenos de Transporte e Ciências do Ambiente**  
**Engenharia · UniCEUB · Brasília · 2026**

**Responsável pelo projeto:** Ana Carolina Lisboa

Esta pasta reúne as capturas e os materiais de simulação térmica do mini rack no **Energy2D**. O arquivo [`energy2d.pdf`](energy2d.pdf) compila as imagens utilizadas como referência visual para a análise do escoamento de ar e da distribuição de temperatura no gabinete.

> **Escopo dos resultados:** as imagens permitem uma análise qualitativa dos caminhos preferenciais do ar e das regiões relativamente mais quentes ou frias no modelo. Elas não substituem medições experimentais nem constituem, por si só, uma previsão quantitativa calibrada da temperatura de cada componente.

## 1. Introdução à simulação térmica

O **Energy2D**, desenvolvido por Charles Xie no **Concord Consortium**, é um ambiente de simulação numérica bidimensional voltado ao ensino e à exploração de fenômenos térmicos. O programa representa a transferência de energia em uma seção do sistema e permite visualizar campos de temperatura e movimento do fluido.

Na modelagem, a condução de calor é representada pela equação de energia discretizada numericamente, enquanto o movimento do ar é descrito por uma aproximação das equações de conservação de massa, quantidade de movimento e energia para o fluido, associadas à dinâmica de Navier–Stokes. Dependendo das propriedades e das condições definidas no modelo, também podem ser consideradas trocas por radiação térmica entre superfícies.

Essa abordagem permite observar, de forma integrada:

- **Condução:** propagação de energia através de sólidos, como placas, paredes e componentes representados no modelo;
- **Convecção:** transporte de energia pelo movimento do ar, natural ou induzido por ventilação;
- **Radiação:** troca de energia térmica entre superfícies, quando habilitada e parametrizada na simulação.

A visualização antes da prototipagem física auxilia a identificar possíveis caminhos de recirculação, regiões pouco ventiladas e acúmulos de calor. Com isso, o modelo serve como apoio à análise de posicionamento dos equipamentos e de aberturas de entrada e exaustão do gabinete.

> **Interpretação de engenharia:** uma simulação bidimensional é uma representação simplificada de um sistema tridimensional. Seus resultados dependem da geometria, das propriedades dos materiais, das potências térmicas, das temperaturas de contorno, das condições de ventilação e das hipóteses selecionadas. A comparação quantitativa exige que esses parâmetros sejam documentados e que o modelo seja validado com medições.

## 2. Cenários e mapeamento de calor

### 2.1 Disposição dos componentes internos

As capturas representam os nós de computação e rede organizados verticalmente no gabinete. A disposição analisada é:

| Região no gabinete | Componente representado | Papel térmico no modelo |
|---|---|---|
| Topo | `switch` | Nó de rede; sua posição deve ser considerada em relação à saída do ar aquecido. |
| Região intermediária | `raspberry` / `raspberry pi` | Nó compacto de computação, representado entre o equipamento de rede e o servidor. |
| Base ou fundo | `servidor` / `ThinkCentre` | Nó de maior porte, incluindo o servidor de laboratório como referência do conjunto. |

O empilhamento afeta o escoamento: obstáculos internos podem restringir a passagem do ar, enquanto espaços livres e aberturas alinhadas podem favorecer a ventilação. A distribuição final de temperaturas depende das fontes de calor atribuídas a cada bloco e das condições de contorno utilizadas.

### 2.2 Gradiente térmico e escala de cores

O mapa de cores representa a temperatura calculada em diferentes regiões do domínio. Em termos gerais, as cores mais frias — como azul e verde — indicam regiões relativamente mais frias, próximas às condições ambientais definidas; as cores mais quentes — amarelo, vermelho e, conforme a escala, branco — destacam temperaturas relativamente maiores e possíveis regiões de concentração térmica.

| Aparência na escala | Leitura qualitativa |
|---|---|
| Azul / verde | Regiões de menor temperatura relativa no campo representado. |
| Amarelo / vermelho | Regiões mais aquecidas, associadas à proximidade de fontes térmicas ou à remoção de calor menos eficiente. |
| Branco ou tom extremo da escala | Faixa de temperatura mais alta exibida na legenda específica da captura; deve ser interpretada consultando os limites numéricos da própria escala. |

As cores não devem ser tratadas como temperaturas absolutas sem a leitura dos valores mínimo e máximo da barra de escala. A mesma cor pode corresponder a temperaturas diferentes entre simulações se a faixa da legenda tiver sido alterada.

### 2.3 Escoamento: convecção natural e forçada

Na **convecção natural**, o ar aquecido tende a subir por empuxo, pois sua densidade diminui em relação à do ar mais frio. Em um gabinete vertical, esse movimento pode transportar calor das regiões inferiores para as superiores e favorecer a formação de uma zona quente no alto, especialmente quando a saída de ar é insuficiente.

Na **convecção forçada**, ventiladores impõem ou reforçam o movimento do ar. A eficácia depende do caminho completo entre entrada e exaustão, da posição dos ventiladores, da resistência oferecida pelos componentes e da existência de recirculação. Um fluxo que contorne os componentes sem atravessar as regiões críticas pode deixar zonas de estagnação térmica (*hotspots*).

As capturas devem, portanto, ser examinadas para identificar:

1. se o ar mais frio consegue alcançar as regiões próximas às fontes de calor;
2. se o ar aquecido dispõe de um caminho desobstruído até as aberturas de exaustão;
3. se o empilhamento dos nós cria recirculação ou bolsões de ar com pouca renovação;
4. se aberturas nas extremidades do gabinete favorecem uma entrada e uma saída coerentes com o sentido do escoamento observado.

> **Implicação para o projeto:** aberturas de ventilação eficientes devem permitir a renovação do ar e reduzir zonas de estagnação. A posição e a área dessas aberturas precisam ser avaliadas em conjunto com o arranjo interno; aumentar a área aberta isoladamente não garante um fluxo útil sobre os componentes.

## 3. Limitações e boas práticas de interpretação

- Tratar as capturas como visualização de um modelo 2D, não como reprodução completa do campo tridimensional no gabinete.
- Consultar a escala numérica de cada imagem antes de associar uma cor a uma temperatura.
- Diferenciar resultados calculados no modelo de temperaturas obtidas por medição física.
- Não inferir temperatura de junção, cápsula ou interior de um componente a partir da temperatura do ar ao redor.
- Registrar as condições de contorno e os parâmetros de simulação antes de comparar cenários.
- Validar conclusões de projeto com sensores e ensaios físicos, mantendo comparáveis a carga, o ambiente e a configuração de ventilação.

## Material da pasta

| Arquivo | Descrição |
|---|---|
| [`energy2d.pdf`](energy2d.pdf) | Compilação de capturas do Energy2D usadas como referência visual para a análise térmica. |