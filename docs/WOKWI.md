# Teste no Wokwi

## O que esta versão simula

O diagrama usa componentes visuais de verdade para a eletrônica do projeto:

- ESP32 DevKit C V4;
- TB6612FNG como **Custom Chip**;
- dois conversores `stepper-esc`;
- dois motores visuais `wokwi-stepper-motor`.

O Wokwi não possui atualmente um motor DC TT genérico nativo. Por isso, cada motor TT do robô real é representado por um `wokwi-stepper-motor`. O `stepper-esc` converte os sinais do TB6612FNG em movimento visual, permitindo ver sentido e velocidade do motor na simulação.

## Dependências do diagram.json

```json
"dependencies": {
  "chip-tb6612fng": "github:drf5n/Wokwi-Chip-TB6612FNG@1.0.0",
  "chip-stepper-esc": "github:drf5n/Wokwi-Chip-stepper-esc@1.0.0"
}
```

Não é necessário copiar manualmente os arquivos `.chip.c` e `.chip.json` quando o projeto é aberto no Wokwi.com: as dependências são carregadas pelo próprio simulador.

## Fluxo simulado

```text
ESP32
  |
  | GPIO / PWM
  v
TB6612FNG
  |
  +-------- canal A --------> stepper-esc ---> motor esquerdo
  |
  +-------- canal B --------> stepper-esc ---> motor direito
```

## Pinos

| ESP32 | TB6612FNG |
|---|---|
| GPIO 25 | AIN1 |
| GPIO 26 | AIN2 |
| GPIO 27 | PWMA |
| GPIO 32 | BIN1 |
| GPIO 33 | BIN2 |
| GPIO 14 | PWMB |
| GPIO 13 | nSTBY |
| 3V3 | VCC |
| 5V | VMOT (representação da alimentação no simulador) |
| GND | GND/GND1/GND2 |

## Teste pelo Serial Monitor

Inicie a simulação e envie:

```text
F = frente
B = ré
L = esquerda
R = direita
S = parar
+ = aumentar velocidade
- = diminuir velocidade
```

### Importante sobre o fail-safe

O firmware para o robô depois de aproximadamente 900 ms sem receber outro comando de movimento.

Então, para observar o motor girando continuamente pelo Serial Monitor, envie `F` ou outro comando novamente antes do timeout. No controle Web isso acontece automaticamente enquanto o botão estiver pressionado.

## Controle pelo celular

No ESP32 físico:

1. Conecte o celular ao Wi-Fi `Robo-ESP32`.
2. Senha: `fiap2026`.
3. Abra `http://192.168.4.1`.
4. Use os botões direcionais e o controle de velocidade.

No Wokwi, a parte elétrica/mecânica pode ser validada diretamente no diagrama e pelo Serial Monitor. O acesso externo ao servidor HTTP simulado depende da configuração de rede/gateway utilizada no Wokwi.

## Hardware real

Na montagem física, retire da cadeia os dois `stepper-esc` e os motores stepper. Eles existem apenas para visualização no Wokwi.

A ligação real é:

```text
ESP32 -> TB6612FNG -> 2 motores TT DC
```
