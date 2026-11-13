## 9. Legado

Esta seção relaciona o legado da taxonomia de Flynn, em especial da categoria MISD, ao protótipo do Grupo 03: um sensor de temperatura ligado a um ESP32, que envia o dado por Wi-Fi a um programa em Python, o qual aplica três análises ao mesmo valor (limite, histórico e anomalia). As fontes estão listadas ao final e, de forma completa, em [references.md](references.md).

### 9.1 Importância Histórica

Em 1966, Michael J. Flynn propôs classificar computadores pelo número de fluxos de instruções e de dados, o que gerou as classes SISD, SIMD, MISD e MIMD ([Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273)). Em 1972, ele ampliou o trabalho ([Flynn, 1972](https://doi.org/10.1109/TC.1972.5009071)).

A importância histórica está em ter dado à área um vocabulário comum para comparar organizações de computadores. O próprio Flynn descreve a classificação como um atalho útil que omite sutilezas de cada implementação ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

A categoria MISD é a menos usada das quatro ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). Por isso, estudá-la exige cuidado: o grupo a utiliza como objeto de estudo conceitual, não como arquitetura física do ESP32.

### 9.2 Contribuições Científicas

- **Critério de classificação:** a ideia de "fluxo" (sequência de instruções ou de dados vista pela máquina) permite comparar máquinas muito diferentes.
- **Duas leituras do MISD:** Flynn descreve a classe como um conjunto em pipeline, com a função de cada etapa definida antes da execução e o dado passando de etapa em etapa ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). Materiais didáticos destacam outra leitura: várias unidades sobre o mesmo dado para garantir a correção do cálculo ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).
- **Limites reconhecidos:** mesmo um processador SISD pode ser muito paralelo internamente, e a classificação ignora esses detalhes ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

No protótipo, o mesmo dado de temperatura entra em três processos distintos, o que se aproxima da ideia de múltiplas instruções sobre um único dado. Como o README já observa, isso é uma demonstração conceitual em software e não comprova uma arquitetura MISD física.

### 9.3 Impacto Industrial

Na indústria, o MISD aparece de forma pontual, associado à redundância e à tolerância a falhas, com os computadores de controle de voo do Ônibus Espacial como exemplo citado ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5); sistema descrito em [Spector e Gifford, 1984](https://doi.org/10.1145/358234.358246)).

O que dominou o mercado foi o MIMD. A partir de 2004, com o fim da escala de Dennard, a indústria passou a aumentar o número de núcleos por chip ([Esmaeilzadeh et al., CACM](https://cacm.acm.org/?p=49355); [OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)).

A plataforma do projeto está nesse cenário: o ESP32 é citado como exemplo de processador multicore, portanto MIMD ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)). A fabricante Espressif informou ter passado de 1 bilhão de chips enviados em setembro de 2023, dado autodeclarado ([Espressif, 2023](https://www.espressif.com/en/news/1_Billion_Chip_Sales)).

### 9.4 Impacto Social

O impacto social do projeto, nesta etapa, é principalmente educacional: o grupo acompanha todo o caminho de um dado, da coleta à análise, usando componentes acessíveis (sensor, ESP32 e Python).

Em aplicações reais, monitoramento de temperatura com microcontroladores de baixo custo pode apoiar o acompanhamento de ambientes e equipamentos. O protótipo, porém, não foi validado para esse uso e, conforme o escopo do projeto, não se destina ao controle de equipamentos industriais.

### 9.5 Influência na Computação Moderna

As categorias de Flynn convivem hoje dentro de um mesmo sistema. Processadores x86 e ARM atuais combinam núcleos independentes (MIMD) com instruções vetoriais (SIMD) ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).

Os limites de potência levaram a sistemas heterogêneos, com aceleradores como GPUs, TPUs e FPGAs ao lado dos núcleos de uso geral ([OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)). Um estudo de referência projetou que o ganho com mais núcleos seria limitado pela energia ([Esmaeilzadeh et al., CACM](https://cacm.acm.org/?p=49355)).

Da família do próprio ESP32, o ESP32-S3 inclui instruções vetoriais para acelerar redes neurais ([Espressif, 2023](https://www.espressif.com/en/news/1_Billion_Chip_Sales)). A influência direta do MISD é mais conceitual: a ideia de submeter um mesmo dado a vários processos para verificá-lo ou transformá-lo.

### 9.6 Lições Aprendidas

- **Conceito não é implementação:** executar várias análises sobre o mesmo valor em Python demonstra a ideia, mas não prova uma arquitetura MISD física.
- **Fontes divergem:** a entrada de Flynn no Springer inclui GPUs na classe MISD, enquanto o RoboticLab as trata como SIMT, subconjunto de SIMD. Por isso priorizamos fontes primárias e registramos as divergências.
- **O caminho do dado importa:** o problema envolve sensor, ESP32, Wi-Fi, Python, armazenamento e apresentação. Falhas podem surgir em qualquer etapa, o que justifica os testes da seção 12.
- **Critérios precisam ser definidos:** limite, histórico e anomalia dependem de valores escolhidos pelo grupo, e é preciso testá-los com casos abaixo, próximos e acima do limite.

### 9.7 Perspectivas Futuras

As propostas abaixo são ideias do grupo para trabalhos futuros, ainda não validadas.

- **Análise no próprio ESP32:** técnicas de aprendizado de máquina em microcontroladores (TinyML) já permitem inferência e até treinamento no dispositivo, apesar de limites de memória ([Lin et al.](https://arxiv.org/pdf/2403.19076)). A detecção de anomalia poderia rodar no ESP32, reduzindo o tráfego Wi-Fi.
- **Chips mais capazes:** o ESP32-S31, com dois núcleos RISC-V, é voltado a aprendizado de máquina na borda ([Hackster](https://www.hackster.io/news/espressif-s-esp32-s31-dual-core-edge-smarts-microcontroller-hits-the-mainstream-launches-at-4-51-f616e6fc1716.amp)).
- **Aproximar-se do MISD real:** usar mais de um sensor ou mais de um processo independente sobre a mesma leitura, com comparação dos resultados, aproximaria o protótipo da leitura de redundância.
- **Escalar:** vários sensores e fluxos simultâneos seriam naturalmente um sistema MIMD.

### 9.8 Conceitos que Permaneceram

- **A ideia de fluxos de instruções e de dados:** continua sendo usada para descrever sistemas paralelos, e as quatro siglas aparecem até em materiais didáticos atuais sobre ESP32, x86 e ARM ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).
- **SIMD e MIMD:** sobreviveram como realidade cotidiana. Instruções vetoriais (SIMD) e núcleos independentes (MIMD) convivem nos processadores atuais ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).
- **Pipeline e fluxo de dados por etapas:** é a leitura que o próprio Flynn dá ao MISD, e o pipeline hoje faz parte da maioria dos processadores ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2); [OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)).
- **Redundância para garantir a correção do cálculo:** permanece como motivação de sistemas críticos ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).

### 9.9 Características Abandonadas

- **MISD como categoria de máquina de uso geral:** o termo é pouco usado e a categoria quase não aparece em produtos comerciais ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). Para a maioria dos problemas, SIMD e MIMD se mostraram mais adequados.
- **A premissa de que emitir várias instruções por vez era inviável:** o trabalho de 1966 já a tratava como um gargalo para a tecnologia da época, e processadores com múltiplas emissões (superescalares) a superaram ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
- **A classificação isolada como retrato completo da máquina:** por ser simples, a taxonomia recebeu várias extensões de outros autores, e a própria entrada de Flynn reconhece que ela omite sutilezas ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

### 9.10 Relevância Técnica

Tecnicamente, a taxonomia ajuda a perguntar o que se repete e o que muda em um sistema: quantas sequências de instruções existem e quantos dados fluem por elas. Essa leitura orienta a escolha entre vetorização, núcleos independentes e redundância.

A classificação parte da visão do programador de linguagem de máquina e pressupõe que o conjunto de instruções representa bem a microarquitetura ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). Por isso, ela descreve melhor a organização lógica do que o hardware interno.

Para o projeto do Grupo 03, isso reforça a distinção já feita no README: as três análises sobre a mesma temperatura são organização de software. A plataforma ESP32, por sua vez, é citada como MIMD ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)). Para caracterizar um MISD físico, seria preciso mais de uma unidade de execução operando sobre o mesmo dado.

### Fontes desta seção

- Flynn, M. J. (1966). [Very high-speed computing systems](https://doi.org/10.1109/PROC.1966.5273). Proceedings of the IEEE, 54(12). *Referência: texto integral não consultado.*
- Flynn, M. J. (1972). [Some computer organizations and their effectiveness](https://doi.org/10.1109/TC.1972.5009071). IEEE Transactions on Computers, C-21(9). *Referência: texto integral não consultado.*
- Flynn, M. J. (2011). [Flynn's Taxonomy](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2). Encyclopedia of Parallel Computing, Springer.
- Spector, A.; Gifford, D. (1984). [The space shuttle primary computer system](https://doi.org/10.1145/358234.358246). Communications of the ACM, 27(9). *Referência: texto integral não consultado.*
- Esmaeilzadeh, H. et al. [Dark Silicon and the End of Multicore Scaling](https://cacm.acm.org/?p=49355) (versão no CACM; original no ISCA, 2011).
- OpenStax. [Processor Architectures](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures). Introduction to Computer Science.
- RoboticLab. [Processor Taxonomies, SISD, SIMD, MIMD, MISD, SIMT](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5).
- Espressif Systems (2023). [Espressif Leads the IoT Chip Market with Over 1 Billion Shipments Worldwide](https://www.espressif.com/en/news/1_Billion_Chip_Sales).
- Hackster.io. [Espressif's ESP32-S31 Dual-Core Edge-Smarts Microcontroller](https://www.hackster.io/news/espressif-s-esp32-s31-dual-core-edge-smarts-microcontroller-hits-the-mainstream-launches-at-4-51-f616e6fc1716.amp).
- Lin, J. et al. [Tiny Machine Learning: Progress and Futures](https://arxiv.org/pdf/2403.19076). IEEE Circuits and Systems Magazine (arXiv, 2024).
