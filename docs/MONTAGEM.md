# Montagem física

## Base

- largura: 200 mm;
- comprimento: 200 mm;
- espessura: 3 mm;
- material sugerido: acrílico, MDF ou PVC expandido.

## Vista superior sugerida

```text
                        FRENTE
       ┌────────────────────────────────┐
       │         [ HC-SR04 ]            │
       │                                │
  O====│ MOTOR E                 MOTOR D│====O
       │                                │
       │      ESP32       TB6612        │
       │                                │
       │       REG. 5V     BATERIA      │
       │                                │
       │             CASTER             │
       └────────────────────────────────┘
```

## HC-SR04

Monte o sensor em um suporte vertical na borda frontal.

Evite colocar:

- acrílico na frente dos transdutores;
- cabos cruzando a frente do sensor;
- o sensor apontando para baixo;
- rodas entrando no cone de medição.

## Ligações do ultrassom

```text
HC-SR04 VCC  -> 5V
HC-SR04 TRIG -> GPIO 18
HC-SR04 ECHO -> 1 kΩ -> GPIO 19
                         |
                        2 kΩ
                         |
                        GND
HC-SR04 GND  -> GND
```

## Ligações do TB6612FNG

| ESP32 | TB6612FNG |
|---|---|
| GPIO 25 | AIN1 |
| GPIO 26 | AIN2 |
| GPIO 27 | PWMA |
| GPIO 32 | BIN1 |
| GPIO 33 | BIN2 |
| GPIO 14 | PWMB |
| GPIO 13 | STBY |
| 3V3 | VCC |
| GND | GND |

Motor esquerdo: `AO1/AO2`.

Motor direito: `BO1/BO2`.

## Alimentação

```text
4 x AA
  |
  +------------> VM do TB6612FNG
  |
  +--> 5V regulado -> ESP32 + HC-SR04

GND comum entre bateria, regulador, ESP32, TB6612FNG e HC-SR04.
```

Não alimente os motores diretamente pelo ESP32.
