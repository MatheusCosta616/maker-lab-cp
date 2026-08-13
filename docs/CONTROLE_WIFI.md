# Controle Wi-Fi pelo celular

O projeto não exige um aplicativo Android/iOS separado.

O próprio ESP32 hospeda uma página web com os controles do robô.

## Passo a passo

1. Ligue o robô.
2. Abra as configurações de Wi-Fi do celular.
3. Conecte-se à rede:

```text
Robo-ESP32
```

4. Digite a senha:

```text
fiap2026
```

5. Abra o navegador.
6. Acesse:

```text
http://192.168.4.1
```

## Interface

A página possui:

```text
       ▲
    ◀ STOP ▶
       ▼

Velocidade: 0 ---------------- 255
```

Os botões funcionam enquanto estão pressionados.

Ao soltar o botão, o navegador envia `STOP`.

## API HTTP

Além da interface gráfica, o firmware também possui uma API HTTP simples.

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

Valores aceitos:

```text
0 a 255
```

### Estado

```text
GET /status
```

Exemplo de resposta:

```json
{
  "command": "S",
  "speed": 180,
  "clients": 1
}
```

## Aplicativo futuro

Se posteriormente for necessário criar um aplicativo mobile de verdade, ele pode reutilizar exatamente os mesmos endpoints HTTP.

Por exemplo, um app em:

- Flutter;
- React Native;
- Android nativo;
- MIT App Inventor;

poderá simplesmente chamar `/move`, `/speed` e `/status`.

Portanto, a arquitetura atual não precisa ser descartada caso a disciplina passe a exigir um app.
