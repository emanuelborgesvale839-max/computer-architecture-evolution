# ENTREGA 04 — Armazenamento e Organização da Informação

Protótipo de Monitoramento de Temperatura Baseado no Conceito MISD

## 1. Visão Geral

Esta entrega apresenta como o protótipo mantém os dados, programas e informações necessárias ao seu funcionamento. A organização do armazenamento está concentrada principalmente na plataforma ESP32, que utiliza diferentes recursos de memória para armazenar o programa e manter dados durante a execução.

No contexto do projeto, o armazenamento pode ser dividido em duas funções principais:

Armazenamento permanente → Programa e configurações

Armazenamento temporário → Dados utilizados durante a execução

## 2. Organização do Armazenamento

O ESP32 possui recursos internos de processamento e memória utilizados durante o funcionamento do sistema. No protótipo, a organização pode ser representada da seguinte forma:
```text

                         [ ESP32 ]
                            |
              +-------------+-------------+
              |                           |
              v                           v
 [ Armazenamento do Programa ]   [ Memória de Execução ]
              |                            |
              v                 +----------+-----------+
 [ Instruções e Configurações ] |          |           |
                                v          v           v
                         [Temperatura [Leituras  [Valores de
                            Atual]    Anteriores] Referência]
                                             
                                    [Resultados Temporários]
```

Essa divisão permite que o sistema mantenha tanto as instruções necessárias para funcionar quanto os dados utilizados durante o monitoramento.

## 3. Armazenamento do Programa e das Configurações

O programa responsável pelo funcionamento do protótipo é gravado na memória não volátil disponível na plataforma. Esse armazenamento mantém as informações necessárias mesmo quando o sistema é desligado.

Entre as informações armazenadas estão:

1. instruções do programa;

2. configurações do funcionamento;

3. parâmetros utilizados nas análises;

4. valores definidos durante o desenvolvimento.

Quando o ESP32 é iniciado, as instruções armazenadas são utilizadas para iniciar o funcionamento do sistema.

Essa forma de armazenamento é fundamental porque permite que o protótipo execute o programa sem a necessidade de uma nova configuração completa a cada inicialização.

## 4. Armazenamento Temporário

Durante o funcionamento, o sistema precisa manter informações temporárias. Esses dados podem incluir:

a) temperatura atual;

b) leitura anterior;

c) valores utilizados como referência;

d) resultados intermediários.

Um exemplo ocorre na análise de alteração da temperatura. Para comparar duas leituras, o sistema precisa manter uma informação anterior disponível.

     [ Leitura Atual ]       [ Leitura Anterior ]
             |                       |
             |                       |
             +----------+------------+
                        |
                        v
                [ Processamento ]
                        |
                        v
          [ Resultado da Comparação ]

     [ Leitura Atual ] ---- Atualiza ----> [ Leitura Anterior ]

Após uma nova leitura, o valor atual pode substituir ou atualizar a informação anterior utilizada pelo sistema.

## 5. Tecnologias de Armazenamento

A plataforma ESP32 utiliza recursos internos de memória com funções diferentes. De forma simplificada, o projeto utiliza:

- Tipo de armazenamento

- Função no Projeto

- Memória não volátil

- Armazenamento do programa e configurações

- Memória de execução

- Armazenamento temporário dos dados

- Registradores

- Operações internas do processador

Esses recursos trabalham em conjunto durante a execução do protótipo. O programa fornece as instruções necessárias, enquanto a memória temporária mantém os dados utilizados durante o processamento.

## 6. Capacidade e Acesso

A capacidade exata de memória pode variar conforme o modelo específico do ESP32 utilizado na implementação. Por esse motivo, o projeto considera inicialmente os recursos de armazenamento internos da plataforma, sem estabelecer uma capacidade específica antes da definição do hardware final.

A memória de execução precisa permitir acesso rápido aos dados utilizados durante o monitoramento. Já o armazenamento do programa possui uma função diferente: manter as instruções disponíveis mesmo quando o sistema não está em funcionamento.

Essa diferença demonstra que o armazenamento não possui apenas a função de guardar informações, mas também influencia diretamente a velocidade e a continuidade da execução.

## 7. Limitações do Armazenamento

A organização proposta possui algumas limitações:

- a memória interna é limitada;

- grandes históricos de temperatura podem exigir armazenamento adicional;

- informações temporárias podem ser perdidas quando o sistema é desligado;

- o armazenamento de longo prazo exige uma estratégia específica de registro dos dados.

Para a proposta inicial, o armazenamento interno é suficiente para manter o programa e os dados necessários durante o monitoramento.

Caso o projeto seja ampliado para registrar temperaturas durante períodos maiores, poderão ser utilizados mecanismos externos ou serviços de armazenamento.

## 8. Relação entre Armazenamento e Funcionamento

O armazenamento é essencial para o funcionamento do protótipo. Sem o armazenamento permanente, o sistema não manteria as instruções necessárias para executar o programa.

Sem o armazenamento temporário, o sistema teria dificuldades para manter informações necessárias durante o processamento, como leituras anteriores.

O funcionamento pode ser representado pelo seguinte fluxo:
```
[ Programa Armazenado ]
           |
           v
        [ ESP32 ] <------- [ Dados do Sensor ]
           |
           |
           v
 [ Memória Temporária ]
           |
           v
      [ Resultados ]
```
A memória permite que o sistema mantenha as instruções e os dados necessários para transformar uma leitura de temperatura em uma informação útil para o monitoramento.

## Conclusão

O protótipo utiliza os recursos de armazenamento da plataforma ESP32 para manter tanto o programa quanto as informações utilizadas durante sua execução. O armazenamento permanente permite conservar as instruções e configurações do sistema, enquanto a memória temporária mantém dados como a temperatura atual, leituras anteriores e resultados intermediários.

Dessa forma, a organização do armazenamento contribui diretamente para a continuidade e o funcionamento do sistema, permitindo que as informações necessárias estejam disponíveis no momento adequado para o processamento e o monitoramento.

## REFERÊNCIAS

ESPRESSIF SYSTEMS. ESP32 Series Datasheet. Version 5.3. [S. l.]: Espressif Systems, [s. d.]. Disponível em: https://documentation.espressif.com/esp32_datasheet_en.html. Acesso em: 10 nov. 2026.

ESPRESSIF SYSTEMS. ESP32 Technical Reference Manual. Version 5.5. [S. l.]: Espressif Systems, [s. d.]. Disponível em: https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf. Acesso em: 10 nov. 2026.
