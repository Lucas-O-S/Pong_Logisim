# Pong_Logisim
Pong made in Logisim

## Principais componentes do circuito
### 1. Pinos de Entrada (Pin)
Você tem vários pinos de entrada, rotulados como:
```Fix
"0", "1", "2", ..., "9"
```
Cada um desses pinos tem largura de 8 bits, ou seja, representam dados de 1 byte. Isso sugere que o circuito pode lidar com até 10 valores de entrada, cada um com 8 bits de informação.

### 2. Pinos de Saída
```Fix
"840, 150", "830, 160", ..., "810, 270"
```
Esses estão marcados como output = true, o que indica que são saídas do circuito. Estão conectados a um tipo de módulo de exibição, por isso, estão agrupados e conectados de forma ordenada.

### 3. Contador (Counter)
```Fix 
<comp lib="4" loc="(390,390)" name="Counter">
  <a name="width" val="4"/>
  <a name="max" val="0xf"/>
</comp>
```
Este é um contador de 4 bits, que vai de 0 até 15 (0xF em hexadecimal). Ele está sendo usado para escanear sequencialmente os 10 pinos de entrada. A cada pulso de clock, o contador incrementa e permite selecionar uma nova entrada.

### 4. Multiplexadores (Multiplexer)
Multiplexadores são componentes que recebem várias entradas e, com base em um sinal de seleção, escolhem uma delas para enviar como saída.
```Fix
<comp lib="2" loc="(580,490)" name="Multiplexer">
  <a name="select" val="4"/>
  <a name="width" val="4"/>
</comp>
```
Esse multiplexador está selecionando uma das entradas de 4 bits com base em uma linha de seleção de 4 bits (vindo do contador).
Em geral, os multiplexadores desse circuito estão sendo usados para selecionar qual entrada (de 0 a 9) será enviada para processamento e exibição.

### 5. Registro (Register)
```Fix
<comp lib="4" loc="(760,560)" name="Register">
  <a name="width" val="10"/>
</comp>
```
Este componente armazena dados temporariamente. Após uma entrada ser selecionada e processada, ela é armazenada no registro antes de ser enviada para a saída.

### 6. Flip-Flop e Clock
```Fix
<comp lib="4" loc="(320,590)" name="D Flip-Flop"/>
<comp lib="0" loc="(230,660)" name="Clock"/>
```
O Flip-Flop tipo D e o Clock trabalham juntos para sincronizar o funcionamento do circuito. Cada vez que o Clock envia um pulso, o Flip-Flop pode armazenar um novo valor.

### 7. Lógica com portas AND, OR e NOT
Essas portas lógicas são usadas para criar condições de controle. Por exemplo:

* Permitir a leitura de uma entrada só quando o pino “ENABLE” estiver ativo
* Resetar o circuito com base em alguma entrada
* Selecionar dinamicamente a próxima ação do circuito

### 8. Deslocador (Shifter)
```Fix
<comp lib="3" loc="(550,420)" name="Shifter">
  <a name="width" val="10"/>
  <a name="shift" val="lr"/>
</comp>
```
Esse componente realiza deslocamento de bits (shift lógico). Pode ser usado para dividir números, mover bits, ou preparar dados para exibição.

## Funcionamento
1. Recebe 10 entradas diferentes (dados de 8 bits)
2. Um contador percorre essas entradas de forma sequencial
3. Um multiplexador escolhe qual dessas entradas será processada
4. Os dados podem ser manipulados (ex: deslocamento, máscara com AND)
5. O resultado é armazenado num registro
6. Esse dado final é enviado para a saída (pinos conectados ao display)

Além disso, há sinais de controle como:<br>
CLOCK: controla o tempo <br>
ENABLE: habilita ou desabilita o funcionamento <br>
RESET: reinicia o circuito <br>

