# Controle Wi-Fi pelo celular

O ESP32 cria a própria rede Wi-Fi e hospeda uma página de controle.

## Conexão

1. Ligue o robô.
2. No celular, conecte-se a `Robo-ESP32`.
3. Senha: `fiap2026`.
4. Abra `http://192.168.4.1`.

## Interface

A tela mostra:

- distância atual do HC-SR04;
- aviso de obstáculo;
- frente;
- ré;
- esquerda;
- direita;
- stop;
- controle de velocidade.

Quando o sensor entra em bloqueio, os botões de frente, esquerda e direita são desabilitados visualmente. A ré continua disponível.

## API HTTP

### Movimento

```text
GET /move?dir=F
GET /move?dir=B
GET /move?dir=L
GET /move?dir=R
GET /move?dir=S
```

### Velocidade

```text
GET /speed?value=180
```

### Estado

```text
GET /status
```

Exemplo:

```json
{
  "command": "S",
  "speed": 180,
  "clients": 1,
  "obstacle": true,
  "stopDistanceCm": 20.0,
  "releaseDistanceCm": 25.0,
  "distanceCm": 14.8
}
```

Quando há obstáculo, chamadas de `F`, `L` ou `R` retornam HTTP `423` e o robô permanece parado.
