# Controle de LEDs com Interrupções e Botão

Este projeto utiliza a placa Raspberry Pi Pico para controlar três LEDs (vermelho, verde e amarelo) com base na interação com um botão. O comportamento dos LEDs é gerenciado por interrupções e callbacks, com temporização para desligar os LEDs sequencialmente após um determinado intervalo.

## Objetivo

- Acionar os LEDs em sequência ao pressionar um botão.
- Após a ativação do botão, os LEDs serão acesos e desligados em ordem, com um intervalo de 3 segundos entre eles.
- O uso de interrupções para detectar o pressionamento do botão e controlar os LEDs sem bloquear o fluxo do programa principal.

## Hardware

- **Placa:** Raspberry Pi Pico
- **Componentes:**
  - 3 LEDs (Vermelho, Verde, Amarelo)
  - 1 Botão (com pull-up interno)

### Pinos utilizados:

- **LED Vermelho:** GPIO 13
- **LED Verde:** GPIO 11
- **LED Amarelo:** GPIO 12
- **Botão:** GPIO 5

## Funcionamento

1. Ao pressionar o botão (GPIO 5), todos os LEDs acendem simultaneamente.
2. Depois de 3 segundos, o LED vermelho se apaga.
3. Após mais 3 segundos, o LED amarelo se apaga.
4. Finalmente, após mais 3 segundos, o LED verde se apaga.

As interrupções são usadas para detectar o pressionamento do botão e realizar a sequência de desligamento dos LEDs sem precisar de verificações constantes dentro do loop principal.

## Código

### Dependências

- Biblioteca `pico/stdlib.h` para manipulação de I/O e temporizadores da Raspberry Pi Pico.
- Funções do `hardware/timer.h` e `hardware/gpio.h` para controle de temporizadores e interrupções.

### Funções principais:

- **turn_off_last_led_callback:** Desliga o LED verde e marca a sequência como completa.
- **turn_off_second_led_callback:** Desliga o LED amarelo e agenda o próximo callback para desligar o LED verde.
- **turn_off_first_led_callback:** Desliga o LED vermelho e agenda o próximo callback para desligar o LED amarelo.
- **button_callback:** Função chamada quando o botão é pressionado, inicia a sequência de LEDs.

### Inicialização e configuração:

- Configura os LEDs como saídas e o botão como entrada com pull-up interno.
- Define uma interrupção para o botão, que chama a função `button_callback` quando o botão é pressionado.

## Como usar

1. Conecte os LEDs e o botão aos pinos conforme descrito no diagrama.
2. Carregue o código na Raspberry Pi Pico utilizando o ambiente de desenvolvimento de sua preferência.
3. Ao pressionar o botão, observe a sequência de LEDs.
