# Robô 2WD com ESP32

Projeto de um robô móvel 2WD controlado por **ESP32**, usando **Wi-Fi** e um driver de motores **TB6612FNG**.

O projeto foi estruturado para:

- rodar no ESP32 real;
- ser testado no Wokwi;
- ser controlado por celular sem precisar instalar um aplicativo;
- permitir testes pelo Serial Monitor;
- ficar pronto para versionamento no Git/GitHub.

## Arquitetura

```text
Celular
   |
   | Wi-Fi
   v
ESP32
   |
   | GPIO / PWM
   v
TB6612FNG
   |
   +----------+
   |          |
Motor A    Motor B
esquerdo   direito
```

No hardware real, o ESP32 cria a própria rede Wi-Fi:

- **SSID:** `Robo-ESP32`
- **Senha:** `fiap2026`
- **Painel:** `http://192.168.4.1`

O celular se conecta diretamente ao robô. Não é necessário roteador nem internet.

## Comandos

| Comando | Movimento |
|---|---|
| F | Frente |
| B | Ré |
| L | Girar para esquerda |
| R | Girar para direita |
| S | Parar |
| + | Aumentar velocidade no Serial |
| - | Diminuir velocidade no Serial |

O painel web possui botões direcionais e controle de velocidade de 0 a 255.

## Segurança

Há um `fail-safe` no firmware: se o ESP32 estiver movimentando o robô e deixar de receber comandos por aproximadamente 900 ms, os motores são parados automaticamente.

Isso evita que o robô continue andando caso:

- o Wi-Fi caia;
- a página seja fechada;
- o celular perca conexão;
- um comando fique preso.

## Estrutura

```text
robo-2wd-esp32/
├── sketch.ino
├── diagram.json
├── README.md
├── .gitignore
├── LICENSE
└── docs/
    ├── COMPONENTES.md
    ├── MONTAGEM.md
    ├── WOKWI.md
    └── CONTROLE_WIFI.md
```

## Pinos usados

| ESP32 | TB6612FNG | Função |
|---|---|---|
| GPIO 25 | AIN1 | Direção motor esquerdo |
| GPIO 26 | AIN2 | Direção motor esquerdo |
| GPIO 27 | PWMA | Velocidade motor esquerdo |
| GPIO 32 | BIN1 | Direção motor direito |
| GPIO 33 | BIN2 | Direção motor direito |
| GPIO 14 | PWMB | Velocidade motor direito |
| GPIO 13 | STBY | Habilita o driver |
| 3V3 | VCC | Alimentação lógica do driver |
| GND | GND | Terra comum |

## Teste rápido no Wokwi

1. Crie um projeto ESP32 no Wokwi.
2. Substitua o conteúdo do `sketch.ino` pelo arquivo deste projeto.
3. Substitua o `diagram.json`.
4. Inicie a simulação.
5. Aguarde o Wokwi carregar as dependências dos custom chips.
6. Abra o Serial Monitor.
7. Digite `F`, `B`, `L`, `R` ou `S`.

O diagrama usa um **TB6612FNG custom chip** e dois motores visuais. Como o Wokwi não possui motor TT DC nativo, dois `wokwi-stepper-motor` são usados apenas para mostrar o sentido e a velocidade de giro dos motores do robô.

Consulte [docs/WOKWI.md](docs/WOKWI.md) para detalhes.

## Hardware real

A ligação completa está em [docs/MONTAGEM.md](docs/MONTAGEM.md).

**Importante:** não alimente os motores diretamente pelo ESP32.

Use uma alimentação adequada para os motores e mantenha o **GND do ESP32 e o GND do TB6612FNG em comum**.

## Base do robô

A base sugerida é quadrada:

- **200 mm × 200 mm**
- espessura sugerida: **3 mm** em acrílico ou material equivalente.

O tamanho deixa espaço para:

- ESP32;
- TB6612FNG;
- suporte de baterias;
- cabeamento;
- sensores futuros.

Veja a distribuição sugerida em [docs/MONTAGEM.md](docs/MONTAGEM.md).

## Referências técnicas

- Wokwi ESP32 Wi-Fi: https://docs.wokwi.com/guides/esp32-wifi
- Formato `diagram.json`: https://docs.wokwi.com/diagram-format
- Hardware suportado pelo Wokwi: https://docs.wokwi.com/getting-started/supported-hardware
- Arduino-ESP32 Wi-Fi API: https://docs.espressif.com/projects/arduino-esp32/en/latest/api/wifi.html
- Arduino-ESP32 PWM/LEDC: https://docs.espressif.com/projects/arduino-esp32/en/latest/api/ledc.html
