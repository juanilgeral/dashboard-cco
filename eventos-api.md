# Mapeamento de Eventos — TrucksControl API → Dashboard CCO JUANIL

Fonte: `RequestMensagemCB` (e macros relacionadas)

## Eventos de Macro (dMac / tfrID)

| Macro típica                  | Status no Dashboard     | Observação |
|-------------------------------|-------------------------|------------|
| INICIO DE VIAGEM / REINICIO   | EM VIAGEM               |            |
| CHEGADA CLIENTE               | NA LOJA                 |            |
| ABERTURA BAÚ / INICIO DESCARREGAMENTO | BAÚ ABERTO     |            |
| FECHAMENTO BAÚ                | NA LOJA                 |            |
| FIM DE VIAGEM / FIM FINAL     | FIM ou RETORNO CD       | Depende do destino |
| RETORNO                       | RETORNO CD              |            |
| PARADA REFEICAO               | ALMOÇO                  |            |

## Eventos de Sensor (evtX)

| evt | Significado                          | Uso no Dashboard |
|-----|--------------------------------------|------------------|
| evt5 / evt31 | Botão de pânico                     | Alerta crítico   |
| evt10        | Trava de baú destravada             | Baú              |
| evt14        | Porta do baú aberta                 | BAÚ ABERTO       |
| evt74–77     | Tempo de porta de baú excedido      | Alerta           |
| evt12        | Porta do carona aberta              | Porta            |
| evt13        | Porta do motorista aberta           | Porta            |
| evt34 / evt72| Velocidade excedida                 | Alerta           |
| evt35        | RPM excedido                        | Alerta           |
| evt4         | Ignição ligada/desligada            |                  |
| evt8 / evt27 | Desengate de carreta                |                  |

## Campos de Posição

- `lat` / `lon` — coordenadas
- `mun` / `uf` — município / estado
- `vel` — velocidade (-1 = não informada)
- `dt` — data/hora do evento
- `veiID` — ID do veículo (cruzar com `RequestVeiculo` para obter placa)

## Fluxo de Integração Sugerido

1. `RequestVeiculo` → mapa veiID → placa + motorista
2. Polling `RequestMensagemCB` (guardar último `mId`)
3. Converter mensagens em eventos do dashboard
4. Servir JSON para o `index.html`

Credenciais fornecidas (não commitar):
- Usuario: 31382336000190
- Senha: ********
