Na aula 4 foi apresentado o conceito de ponteiro, no qual podemos armazenar valores e endereços de outras variáveis e acessá-las indiretamente. Para fixação desse conteúdo foi proposto o desenvolvimento de um semáforo, contruido com 3 LEDS (vemelho, verde e amarelo) de modo que o led_vermelho fica ligado por 6s, o led_amarelo por 2s e o led_verde por 4s. Para ligação dos LEDs também foram utilizados resistores de 330 Ohms, conectados entre o pino positivo do LED e a porta de entrada do microcontrolador; já o pino negatico do LED foi conectado ao GND da placa. O código foi construido no microcontrolador (ESP32).

Abaixo segue o código utilizado, bem como um vídeo de demonstração:

```C++
// Definição da portas a serem utilizadas
#define led_vermelho 18
#define led_amarelo 17
#define led_verde 16

// Foi criada uma estrutura para relacionar o pino com a seu delay correto 
struct Luz {
  int pino;
  int tempo;
};

// Parâmetros de delay para cada pino
Luz semaforo[] = {
  {led_vermelho, 6000},
  {led_amarelo, 2000},
  {led_verde, 4000}
};

// Cria o ponteiro, podendo ser chamado para relacionar a cor do LED ou o seu delay
Luz* pont = semaforo;

void setup() {
  
  // Cria um for para definir todos os pinos como saída
  for (int i = 0; i < 3; i++) {
    pinMode((pont + i)->pino, OUTPUT);
  }
}

void loop() {
  
  // Cria um for, para relacionar cada LED com a lógica de acender, esperar o instante correto e desligar
  for (int i = 0; i < 3; i++) {
    digitalWrite((pont + i)->pino, HIGH);
    delay((pont + i)->tempo);
    digitalWrite((pont + i)->pino, LOW);
  }
}

```

![Vídeo Demo](./video_demo.mp4)

| Componentes| Descrição| Especificações Principais| Observações |
|-------------|------------|----------------------------|--------------|
| **LED** (diodo emissor de luz) | Dispositivo semicondutor que emite luz quando percorrido por corrente elétrica. | • Tensão direta (Vf): 1.8 V a 2.2 V (vermelho) <br> • Corrente típica: 10 mA a 20 mA <br> • Polaridade: Ânodo (+) e Cátodo (–) | Necessita de resistor em série para limitar a corrente.     |
| **Resistor de 330 Ω**          | Componente que limita a corrente elétrica no circuito, protegendo o LED.        | • Resistência: 330 Ω ±5% <br> • Potência: ¼ W (0.25 W) <br> • Material: Filme de carbono                                       | Valor ideal para limitar a corrente de um LED ligado a 5 V. |
