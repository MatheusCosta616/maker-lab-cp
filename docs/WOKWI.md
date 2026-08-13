# Teste no Wokwi

## Componentes simulados

O `diagram.json` utiliza:

- ESP32 DevKitC V4;
- HC-SR04 nativo do Wokwi;
- 2 resistores para o divisor do ECHO;
- TB6612FNG como custom chip;
- 2 chips `stepper-esc`;
- 2 motores stepper usados apenas como visualização do giro dos motores TT DC.

## Como executar

1. Crie/abra um projeto ESP32 no Wokwi.
2. Substitua `sketch.ino` pelo arquivo do repositório.
3. Substitua `diagram.json` pelo arquivo do repositório.
4. Inicie a simulação.
5. Aguarde as dependências dos custom chips.
6. Abra o Serial Monitor.

## Comandos Serial

```text
F = frente
B = ré
L = esquerda
R = direita
S = stop
+ = aumenta a velocidade
- = diminui a velocidade
```

## Testar o ultrassom

O sensor começa em 400 cm.

1. Envie `F` algumas vezes para manter o robô em movimento.
2. Clique no HC-SR04.
3. Ajuste a distância para `15 cm`.
4. O firmware imprime a detecção e para os motores.
5. Tente `F`, `L` e `R`: devem ser bloqueados.
6. Envie `B`: a ré deve funcionar.
7. Ajuste o sensor para `30 cm`.
8. O bloqueio é removido.

O Wokwi permite mudar a distância simulada do HC-SR04 durante a execução.

## Observação sobre os motores

O Wokwi não possui um motor TT DC nativo. Por isso, o TB6612FNG custom controla dois `stepper-esc`, que transformam a saída da ponte H em movimento visual dos steppers.
