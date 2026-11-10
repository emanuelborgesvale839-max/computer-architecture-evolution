# ENTREGA 08 — Integração, Limitações e Desempenho

**Protótipo de Monitoramento de Temperatura com Referência ao Conceito MISD**

## 1. Visão Geral

Esta entrega integra os principais aspectos analisados nas etapas anteriores do projeto. O protótipo foi desenvolvido para realizar o monitoramento de temperatura por meio da integração entre aquisição de dados, processamento, armazenamento e comunicação.

A arquitetura utiliza o DS18B20 para obter a temperatura e o ESP32 como plataforma central para executar o programa, processar as informações e disponibilizar os resultados.

## 2. Integração dos Componentes

Os componentes trabalham de forma sequencial e integrada. O processo inicia no ambiente monitorado, onde o sensor identifica a temperatura. O dado é transmitido ao ESP32, processado de acordo com as instruções do programa e transformado em resultados que podem ser apresentados localmente ou enviados para uma interface externa.

```text
       [ Ambiente ]
            |
            v
       [ DS18B20 ]
            |
         1-Wire
            |
            v
        [ ESP32 ] <------> [ Memória ]
            |
            v
    [ Processamento ]
            |
            v
     [ Resultados ]
            |
       +----+--------------+
       |                   |
       v                   v
   [ Serial ] [ Wi-Fi / Interface Externa ]
```

A integração entre esses elementos permite transformar uma informação física em um resultado digital utilizado para o monitoramento.

## 3. Características que Favorecem o Funcionamento

A arquitetura proposta apresenta características adequadas ao objetivo do projeto.

**a) Aquisição digital**

O DS18B20 fornece uma leitura digital da temperatura, facilitando a integração com a plataforma de processamento.

**b) Processamento integrado**

O ESP32 concentra recursos de processamento, memória e interfaces de comunicação, reduzindo a necessidade de componentes adicionais.

**c) Comunicação**

A utilização do protocolo 1-Wire permite a comunicação entre o sensor e o processador, enquanto o Wi-Fi possibilita a expansão do sistema para interfaces externas.

**d) Funcionamento automático**

Após a configuração, o sistema pode realizar ciclos repetitivos de monitoramento sem a necessidade de intervenção humana constante.

## 4. Limitações e Gargalos

Apesar das características favoráveis, o protótipo possui limitações relacionadas aos recursos disponíveis.

| Área | Limitação ou Gargalo |
| --- | --- |
| Aquisição | Dependência da correta comunicação com o sensor |
| Processamento | Recursos limitados de um sistema embarcado |
| Memória | Capacidade limitada para históricos extensos |
| Comunicação | Dependência da disponibilidade e estabilidade da rede Wi-Fi |
| Alimentação | Interrupções podem interromper o monitoramento |

Para a proposta atual, que utiliza uma quantidade reduzida de dados e operações simples, essas limitações não impedem o funcionamento do protótipo.

## 5. Fatores que Influenciam o Desempenho

O desempenho do sistema não depende apenas da velocidade do processador. Os principais fatores são:

- frequência das leituras de temperatura;
- tempo necessário para a comunicação com o sensor;
- quantidade de operações executadas;
- disponibilidade de memória;
- tempo necessário para transmitir os resultados;
- estabilidade da alimentação e das conexões.

Para uma aplicação de monitoramento de temperatura, não é necessário processar grandes quantidades de dados em intervalos extremamente curtos.

Dessa forma, o desempenho deve ser avaliado de acordo com a finalidade do sistema.

## 6. Processamento e Paralelismo

O ESP32 possui recursos de processamento adequados para executar as tarefas previstas pelo protótipo. Dependendo do modelo utilizado, a plataforma pode possuir mais de um núcleo de processamento.

Entretanto, o funcionamento básico do projeto não depende de processamento paralelo.

O ciclo principal pode ser executado de forma sequencial:

```text
  [ Leitura ]
       |
       v
[ Processamento ]
       |
       v
 [ Resultado ]
```

Caso o projeto seja ampliado, recursos de paralelismo poderão ser utilizados para separar tarefas, como o processamento das informações e a comunicação com sistemas externos.

A existência de múltiplos núcleos, entretanto, não caracteriza automaticamente o protótipo como uma arquitetura MISD.

## 7. Decisões Arquiteturais

As principais decisões do projeto foram:

- utilizar o DS18B20 como unidade de aquisição;
- utilizar o ESP32 como plataforma central;
- utilizar o protocolo 1-Wire para comunicação com o sensor;
- utilizar a memória interna para informações temporárias;
- utilizar interfaces serial e Wi-Fi para disponibilização dos resultados.

Essas decisões priorizam uma arquitetura simples, integrada e adequada para um protótipo de monitoramento.

O conceito MISD é utilizado como referência acadêmica para o estudo da organização de instruções e dados, sem classificar a implementação física como uma arquitetura MISD.

## 8. Questão Central — Característica Mais Importante

A característica que mais influencia a capacidade do protótipo de realizar sua função é a integração entre a aquisição confiável dos dados e a capacidade de processamento do ESP32.

O objetivo principal do sistema é monitorar a temperatura. Para que isso ocorra corretamente, a informação precisa ser obtida pelo sensor e disponibilizada ao processamento de forma confiável.

O ESP32 possui capacidade suficiente para executar as operações necessárias, mas seu processamento depende da disponibilidade correta dos dados de entrada.

Assim, a comunicação entre sensor, processamento e mecanismos de saída é fundamental para transformar a temperatura medida em uma informação útil.

## 9. Fluxo Integrado do Sistema

O funcionamento completo do protótipo pode ser resumido da seguinte forma:

```text
       [ Temperatura do Ambiente ]
                   |
                   v
             [ Aquisição ]
              [ DS18B20 ]
                   |
                   v
            [ Comunicação ]
               [ 1-Wire ]
                   |
                   v
            [ Processamento ]
               [ ESP32 ]
                   |
             +-----+-----+
             |           |
             v           v
        [ Memória ] [ Análise dos Dados ]
                          |
                          v
                   [ Resultados ]
                          |
                    +-----+--------+
                    |              |
                    v              v
              [ Monitoramento [ Comunicação
                  Local ]       Externa ]
```

## Conclusão

O protótipo integra diferentes componentes para realizar uma tarefa específica: o monitoramento da temperatura. O DS18B20 fornece os dados de entrada, o ESP32 executa o processamento e a memória mantém as informações necessárias durante a execução. Os resultados podem ser disponibilizados localmente ou transmitidos para sistemas externos.

O desempenho do projeto deve ser analisado de acordo com sua finalidade. Para um sistema de monitoramento de temperatura, a capacidade de realizar leituras confiáveis, processar os dados corretamente e disponibilizar os resultados é mais importante do que alcançar altas velocidades de processamento.

Dessa forma, a integração entre aquisição, comunicação e processamento representa a principal característica que permite ao protótipo realizar adequadamente o trabalho para o qual foi projetado.

## REFERÊNCIAS

ANALOG DEVICES. **DS18B20: programmable resolution 1-wire digital thermometer**. Rev. 6. [S. l.]: Analog Devices, 2019. Disponível em: https://www.analog.com/media/en/technical-documentation/data-sheets/ds18b20.pdf. Acesso em: 10 nov. 2026.

ESPRESSIF SYSTEMS. **ESP32 Series Datasheet**. Version 5.3. [S. l.]: Espressif Systems, [s. d.]. Disponível em: https://documentation.espressif.com/esp32_datasheet_en.html. Acesso em: 10 nov. 2026.

ESPRESSIF SYSTEMS. **Wi-Fi Driver: ESP-IDF Programming Guide**. [S. l.]: Espressif Systems, [s. d.]. Disponível em: https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-guides/wifi.html. Acesso em: 10 nov. 2026.
