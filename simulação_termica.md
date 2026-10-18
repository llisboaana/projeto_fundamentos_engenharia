# Simulação térmica com o Energy2D

*Autora:* Ana Carolina Lopes Lisboa ([@llisboaana](https://github.com/llisboaana)) · Engenharia térmica

> Projeto: Mini Rack/Data Center doméstico ou de laboratório: dissipação de calor, modelagem 3D e sustentabilidade
> Disciplinas: Fenômenos de Transporte e Ciências do Ambiente (CEUB)

Antes de partir para os cálculos, quisemos enxergar como o calor se move. Para isso usamos o Energy2D, um programa gratuito criado por Charles Xie, do Concord Consortium, que mostra na tela, em tempo real, o calor se espalhando. Ele surgiu de um projeto financiado pela National Science Foundation (EUA) em 2008, com a ideia de ensinar engenharia de um jeito prático, e hoje é usado por estudantes, da escola à pós-graduação.

O uso é simples: desenhamos o cenário, escolhemos os materiais e as temperaturas e apertamos "play". As cores mostram onde está mais quente e as setas mostram o ar em movimento. Dá para ver o calor passando por dentro dos sólidos (condução), sendo levado pelo ar (convecção) e saindo das superfícies (radiação). Por trás das imagens, o programa resolve as equações do calor e do movimento dos fluidos (XIE; HAZZARD, 2010), mas não precisamos dominar essa matemática para usá-lo.

No nosso projeto, ele ajuda a comparar o alumínio e o cobre. Podemos desenhar a base do dissipador com cada metal e ver, lado a lado, como o calor se espalha em cada um. Assim, entendemos o efeito da condutividade antes do cálculo formal. Esse uso em Fenômenos de Transporte é uma aplicação didática nossa: ele funciona como um laboratório virtual para o calor e o escoamento. A visualização interativa também ajuda a desfazer ideias erradas sobre calor e temperatura (XIE, 2012).

---

# Como o projeto foi feito, passo a passo

Esse projeto não nasceu pronto. Foi crescendo aos poucos, com uma pergunta puxando a outra: como um computador que fica ligado o dia inteiro consegue trabalhar dentro de um espaço pequeno sem esquentar demais? Foi assim que chegamos até aqui, na ordem em que aconteceu.

## 1. Começamos por uma máquina de verdade

Em vez de inventar números, partimos de um computador que existe: um ThinkCentre, que faz o papel de servidor no nosso mini rack. Pegamos a fita métrica e medimos a torre: 16,0 cm de largura, 35,5 cm de altura e 38,5 cm de comprimento. Multiplicando tudo, chegamos a 21,86 litros. Parece um detalhe, mas esse volume é o espaço de ar que o calor tem para se espalhar, e é a primeira pista de quanto cuidado o conjunto vai exigir.

![Medidas do ThinkCentre e temperaturas medidas](imagens/01-thinkcentre-medidas-e-temperaturas.jpg)

## 2. Descobrimos o quanto ele esquenta

Com a máquina trabalhando, fomos olhar as temperaturas. No pior momento, durante o teste de esforço, o processador chegou a 55 °C. O limite crítico do fabricante é 105 °C, então sobram 50 °C de folga. Em relação ao limite de 85 °C que adotamos no projeto, ainda sobram 30 °C. No uso do dia a dia, com o computador ligado 24 horas, a temperatura fica entre 38 e 40 °C, e a placa-mãe e o gabinete ficam em torno de 27,8 °C e 29,8 °C.

A conclusão foi tranquilizadora, mas incompleta: sozinho, o computador está bem. O desafio começa quando vários equipamentos passam a dividir o mesmo espaço.

## 3. Desenhamos as peças no FreeCAD

Antes de montar o rack, desenhamos em 3D as peças que mais pesam na conta do calor. Cada uma virou uma folha de desenho técnico, com vistas, cotas e legenda no padrão das normas:

- **Dissipador com ventoinha:** 100 × 100 mm, com 47 mm de altura.
- **Fonte de alimentação:** uma caixa de cerca de 150 mm de largura, com uma abertura redonda para o ar passar.
- **Placa-mãe:** 244 × 244 mm, com o encaixe do processador marcado em 50 mm.
- **Processador:** uma peça de 45 × 45 mm.
- **Equipamento plano de rede ou armazenamento:** 147 × 120 × 26 mm, com duas aberturas na lateral.

Desenhar peça por peça nos obrigou a pensar em medidas reais e, de quebra, mostrou onde o ar entra e onde ele sai em cada uma.

![Desenho do dissipador com ventoinha](imagens/06-desenho-dissipador-ventoinha.png)

![Desenho da fonte](imagens/07-desenho-fonte.png)

![Desenho da placa-mãe](imagens/08-desenho-placa-mae.png)

![Desenho do processador](imagens/09-desenho-processador.png)

![Desenho do equipamento plano](imagens/10-desenho-equipamento-plano.png)

## 4. Montamos o mini rack dentro do Energy2D

Depois das peças, foi a vez do cenário. No Energy2D, desenhamos o mini rack visto de cima: quatro blocos amarelos empilhados, que são o switch, dois Raspberry Pi e o servidor. Em volta deles colocamos paredes cinza com vãos, que fazem o papel das aberturas de ventilação. Numa das laterais colocamos um ventilador e, do outro lado, um termômetro virtual marcando os 22 °C do ambiente.

## 5. Apertamos o "play" e acompanhamos o calor

Com tudo montado, rodamos a simulação e fomos tirando fotos da tela.

No começo, o cenário inteiro está na mesma cor, o ambiente a 22 °C, e só as bordas dos blocos começam a esquentar.

![Início da simulação](imagens/02-energy2d-inicio.jpg)

Pouco depois, uma mancha quente aparece em volta do servidor e do segundo Raspberry, que são os que mais esquentam.

![O calor começando a aparecer](imagens/03-energy2d-calor-comecando.jpg)

Aos poucos, a mancha cresce, passa pelos vãos das paredes e vai ganhando o espaço ao redor.

![O calor se espalhando](imagens/04-energy2d-calor-se-espalhando.jpg)

No fim, o calor ocupa uma área enorme, empurrado para fora pelo lado do ventilador.

![Final da simulação](imagens/05-energy2d-final.jpg)

O que esse passeio de cores nos ensinou é que o ar quente sai principalmente pelos vãos e pela região do ventilador. Ou seja: onde ficam as aberturas e o ventilador importa tanto quanto o material do dissipador.

## 6. Juntamos tudo

Por fim, reunimos as peças. Comparamos o alumínio e o cobre nos cálculos, usamos o Energy2D para entender o comportamento do calor e ligamos tudo à parte ambiental, com o consumo de energia e a reciclabilidade dos materiais. Como a simulação é uma estimativa, o próximo passo natural é conferir os resultados com medições em um protótipo físico.

---

## Referências

- CONCORD CONSORTIUM. *Energy2D: interactive heat transfer simulation*. Disponível em: <https://energy.concord.org/~xie/index.html>.
- XIE, Charles. *Energy2D: a computational tool for learning heat transfer and fluid flow*. Disponível em: <https://energy.concord.org/energy2d/papers.html>.
