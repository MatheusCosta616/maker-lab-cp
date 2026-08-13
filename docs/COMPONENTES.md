# Componentes

## Lista principal

| Qtd. | Componente | Observação |
|---:|---|---|
| 1 | ESP32 DevKit | ESP32 DevKit C / DevKit V1 equivalente |
| 1 | TB6612FNG | Driver duplo para os dois motores |
| 2 | Motor TT DC com redução | Faixa típica de projeto: 3 a 6 V |
| 2 | Roda para motor TT | Aproximadamente 65 mm |
| 1 | Roda boba / caster | Apoio frontal ou traseiro |
| 1 | Base quadrada | 200 × 200 mm |
| 2 | Suportes para motor TT | Compatíveis com os motores |
| 1 | Suporte de baterias | Ex.: 4 × AA |
| 1 | Conversor/regulador para 5 V | Para alimentar o ESP32 de forma estável |
| 1 | Chave liga/desliga | Alimentação principal |
| 1 | Protoboard pequena ou placa de distribuição | Opcional, mas útil no protótipo |
| 1 kit | Jumpers/fios | Ligações elétricas |
| 1 kit | Parafusos M3, porcas e espaçadores | Fixação |
| 1 | Capacitor eletrolítico 470 µF ou similar | Recomendado próximo à alimentação dos motores |
| 2 | Capacitores cerâmicos 100 nF | Opcionais nos terminais dos motores para reduzir ruído |

## Alimentação recomendada para o protótipo

Uma opção simples é:

```text
4 x AA
  |
  +-------------------------> VM do TB6612FNG
  |
  +--> regulador 5 V ------> 5V/VIN do ESP32

GND da bateria
  |
  +-------------------------> GND do TB6612FNG
  |
  +-------------------------> GND do ESP32
```

Durante os primeiros testes, o ESP32 também pode ser alimentado por USB enquanto os motores usam a bateria, desde que os terras sejam comuns.

## O que substitui o kit do slide

O kit 2WD tradicional normalmente fornece a parte mecânica:

- placa de acrílico;
- duas rodas;
- dois motores;
- roda boba;
- suporte de pilhas;
- ferragens.

Neste projeto, a placa original é substituída pela base quadrada de 200 × 200 mm e a eletrônica é montada separadamente.
