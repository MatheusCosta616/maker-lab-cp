# Sensor ultrassônico frontal

O projeto utiliza um **HC-SR04** apontado para a frente do robô.

## Objetivo

Evitar que o robô continue se movendo na direção de um obstáculo próximo.

## Regra de segurança

- distância `<= 20 cm`: ativa bloqueio;
- o robô para imediatamente qualquer movimento;
- enquanto o bloqueio estiver ativo, apenas `B` e `S` são permitidos;
- distância `>= 25 cm`: libera os demais comandos.

A diferença entre 20 cm e 25 cm funciona como histerese e evita oscilações quando o objeto está no limite.

## Pinos

| HC-SR04 | ESP32 |
|---|---|
| VCC | 5V |
| TRIG | GPIO 18 |
| ECHO | GPIO 19 via divisor de tensão |
| GND | GND |

## Divisor do ECHO

```text
ECHO ---- 1 kΩ ----+---- GPIO 19
                   |
                  2 kΩ
                   |
                  GND
```

Com entrada próxima de 5 V, o nó do GPIO fica próximo de 3,3 V.

## Ciclo de leitura

O firmware mede a distância a cada 80 ms.

A leitura é realizada com:

1. pulso de 10 µs em `TRIG`;
2. `pulseIn()` no `ECHO`;
3. conversão aproximada `tempo_us / 58` para centímetros.

## Alterar a distância de parada

No `sketch.ino`:

```cpp
const float OBSTACLE_STOP_DISTANCE_CM = 20.0f;
const float OBSTACLE_RELEASE_DISTANCE_CM = 25.0f;
```

Se quiser que o robô pare mais cedo, aumente os valores.
