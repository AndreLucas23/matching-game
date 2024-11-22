<h1>Matching Game no Logsim</h1>

<h2>Do que se trata</h2>

<h2>Como instalar o Logsim</h2>

<h2>Como jogar(regras)</h2>

<h2>Funcionamento</h2>

<h3>Máquina de estado</h3>
<h3>Leds</h3>
<h3>Displays</h3>

<h3>Escolha dos displays</h3>
O jogador após posicionar o led aperta o botão "CONFIRMA", dessa maneira o display correspondente é aceso. 
Eis o mecanismo responsável por acender o display:

Quando o botão "CONFIRMA" é pressionado, ele gera um pulso que aciona o clock do registrador, passando por uma porta AND entre o pulso "CONFIRMA", o led (para acender o correspondente) e um estado 2 negado(será explicado melhor adiante). Esse registrador tem apenas um bit de dados e guarda a informação se o display foi escolhido.
Uma vez escolhido, ele passa a informação para um multiplexador e para um túnel "ligado", o qual será útil para verificar se o display já foi aceso ou não. O multiplexador libera o valor do número
correspondente no valor de entrada alto para o túnel "xy" (no caso da imagem, "00"), que se conecta ao display e o acende.
O mecanismo que guarda os números escolhidos pelos jogadores é mostrado a seguir:

Os números são as entradas do MUX, e o seletor é composto pela combinação dos bits da linha e coluna. Para guardar o primeiro número (no estado 0), assim que há o pulso do "CONFIRMA" também há a troca de estado para 1,
assim a partir da porta OR dos dois túneis, o clock do registrador é acionado e guarda o primeiro número escolhido. Para guardar o segundo é o mesmo mecanismo, exceto pelos túneis "estado 2" e "segundo num".
Os túneis "primeiro num" e "segundo num" são comparados, e quando a máquina passa pelo estado 3, surge um pulso no túnel "check",
<h3>Verificação</h3>

<h3>Pontuação (e próximo turno)</h3>
<h3>Restrição</h3>
<h3>Correção de eventuais bugs</h3>
<h3>Aleatoriedade</h3>
