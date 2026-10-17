# Modelagem 3D — FreeCAD

Esta pasta reúne a modelagem paramétrica tridimensional do mini rack/servidor Lenovo ThinkCentre Edge 72. Os componentes foram construídos no FreeCAD usando as bancadas **Sketcher**, **Part Design** e **Part**. O objetivo é representar tanto os elementos individuais quanto sua integração no gabinete, formando o Gêmeo Digital do conjunto.

**Responsável:** Tiago de Aquino Nunes

> **Formato:** `.FCStd`, formato nativo de documento do FreeCAD.  
> **Observação:** os arquivos representam modelos de engenharia do projeto; dimensões e detalhes devem ser conferidos no próprio documento e nas pranchas correspondentes antes de qualquer fabricação.

## Arquivos

| Arquivo | Componente e função |
|---|---|
| [`Dissipador_CPU.FCStd`](Dissipador_CPU.FCStd) | Modelo dedicado do conjunto dissipador do processador. |
| [`Dissipador_Thinkcenter.FCStd`](Dissipador_Thinkcenter.FCStd) | Geometria detalhada da base e das aletas do dissipador para análise de troca térmica. |
| [`Fonte.FCStd`](Fonte.FCStd) | Modelagem volumétrica da fonte de alimentação LITEON de 280 W, no formato ATX/SFF representado no projeto. |
| [`Gabinete.FCStd`](Gabinete.FCStd) | Estrutura do chassi, com furações, baias e aberturas de ventilação para o escoamento de ar (*airflow*). |
| [`HD.FCStd`](HD.FCStd) | Unidade de armazenamento mecânico de 3,5 polegadas Seagate de 1 TB. |
| [`Memoria_RAM.FCStd`](Memoria_RAM.FCStd) | Módulos UDIMM de memória DDR3. |
| [`Placa_Mae.FCStd`](Placa_Mae.FCStd) | Placa-mãe de arquitetura micro-ATX, compatível com LGA 1155 / chipset H61, incluindo furação de montagem. |
| [`Processador.FCStd`](Processador.FCStd) | Encapsulamento do Intel Core i3-3220, com dimensões de 37,5 mm × 37,5 mm e formato FCLGA1155. |
| [`ThinkCentre_Fisico.FCStd`](ThinkCentre_Fisico.FCStd) | Montagem completa (*Assembly*) do Gêmeo Digital, integrando os subcomponentes no gabinete. |

## Como abrir no FreeCAD

1. Instale e inicie o FreeCAD em uma versão compatível com os documentos `.FCStd`.
2. No FreeCAD, use **Arquivo → Abrir…** e selecione o arquivo desejado nesta pasta.
3. Para visualizar o conjunto integrado, abra `ThinkCentre_Fisico.FCStd`; para examinar uma peça isolada, abra o arquivo correspondente na tabela.
4. Na árvore do modelo, expanda os objetos para inspecionar esboços, recursos e sólidos. Alterne entre as bancadas **Sketcher**, **Part Design** e **Part** conforme a operação que deseja examinar.
5. Use **Ajustar tudo** (*Fit all*) para enquadrar a geometria na janela. A visibilidade dos objetos pode ser controlada pela árvore do modelo.

O FreeCAD é paramétrico: quando houver recursos e vínculos editáveis, os esboços e operações da árvore permitem compreender a construção da geometria. A montagem completa é a referência mais direta para visualizar a disposição física relativa dos componentes.

## Relação com as pranchas

As pranchas em PDF foram geradas na bancada **TechDraw**. Consulte [`Cotas/README.md`](../Cotas/README.md) para a relação entre PDFs e componentes, as normas técnicas consideradas e recomendações de visualização.
