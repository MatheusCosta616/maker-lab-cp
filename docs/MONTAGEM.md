# Montagem

## Base

Dimensão adotada:

**200 mm × 200 mm**

Espessura sugerida:

**3 mm**

Material:

- acrílico;
- MDF fino;
- PVC expandido;
- chapa impressa/fabricada em outro material rígido.

## Distribuição sugerida

```text
                    FRENTE
      ┌──────────────────────────────┐
      │                              │
      │            CASTER            │
      │              O               │
      │                              │
      │     ESP32       TB6612       │
      │                              │
 O====│ MOTOR E      MOTOR D         │====O
RODA  │                              │   RODA
      │        BATERIA / FONTE       │
      │                              │
      └──────────────────────────────┘
                    TRASEIRA
```

As rodas podem ficar parcialmente para fora dos 200 mm da placa.

## Ligação ESP32 -> TB6612FNG

### Canal A - motor esquerdo

| ESP32 | TB6612 |
|---|---|
| GPIO 25 | AIN1 |
| GPIO 26 | AIN2 |
| GPIO 27 | PWMA |

### Canal B - motor direito

| ESP32 | TB6612 |
|---|---|
| GPIO 32 | BIN1 |
| GPIO 33 | BIN2 |
| GPIO 14 | PWMB |

### Controle do driver

| ESP32 | TB6612 |
|---|---|
| GPIO 13 | STBY |
| 3V3 | VCC |
| GND | GND |

### Motores

| TB6612 | Destino |
|---|---|
| A01 / A02 | Motor esquerdo |
| B01 / B02 | Motor direito |
| VM | Positivo da bateria dos motores |
| GND | Negativo da bateria / terra comum |

## Alimentação

Não ligue os motores nos pinos 3V3 ou 5V do ESP32.

A corrente dos motores deve vir da alimentação de potência ligada ao `VM` do TB6612.

O ESP32 e o driver precisam compartilhar o mesmo GND.

## Se um motor girar invertido

Há duas opções:

1. inverter os dois fios daquele motor no TB6612;
2. inverter o sentido correspondente no firmware.

Para uma montagem inicial, inverter fisicamente os fios costuma ser mais simples.

## Furos na placa

Além dos furos específicos dos motores, é recomendável criar uma pequena malha de furos M3 para permitir reposicionamento.

Sugestão:

- distância entre furos: 10 ou 20 mm;
- evitar furar muito próximo às bordas;
- deixar espaço para abraçadeiras e passagem de fios.
