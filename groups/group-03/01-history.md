## 1. Antecedentes Históricos

Este documento trata da origem da classificação em que o MISD (*Multiple Instruction, Single Data*) está inserido: a taxonomia de Flynn. O MISD não é um processador ou produto comercial, e sim uma das quatro categorias propostas por Michael J. Flynn para classificar computadores. As fontes estão no final e, de forma completa, em [references.md](references.md).

### 1.1 Nome da Arquitetura

**MISD** (*Multiple Instruction, Single Data*), em português "Múltiplas Instruções, Um Único Dado". É uma categoria da **taxonomia de Flynn**, ao lado de SISD, SIMD e MIMD ([Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273)).

### 1.2 Ano de Criação

**1966**, com a publicação do artigo "Very high-speed computing systems" no *Proceedings of the IEEE*. A proposta foi ampliada em **1972**, no artigo "Some computer organizations and their effectiveness" ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

### 1.3 País

**Estados Unidos.** O registro bibliográfico do artigo de 1966 indica a Northwestern University, em Evanston, Illinois ([registro do artigo](https://manuscript.isc.ac/Inventory/49/885972.htm)). Esse registro é de um índice de terceiros e vale conferir a afiliação no IEEE Xplore.

### 1.4 Inventor(es)

**Michael J. Flynn.** Ele é o autor dos dois artigos que definem a classificação e também assina a entrada "Flynn's Taxonomy" da *Encyclopedia of Parallel Computing* ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

### 1.5 Organização / Empresa

A classificação surgiu na pesquisa acadêmica, e não em uma empresa. A afiliação do artigo de 1966 é a Northwestern University ([registro do artigo](https://manuscript.isc.ac/Inventory/49/885972.htm)). Não existe um fabricante do MISD. No protótipo do Grupo 03, a plataforma de hardware é o ESP32, da Espressif Systems, que não é uma implementação física de MISD.

### 1.6 Contexto Histórico

*O que estava acontecendo na computação quando essa arquitetura surgiu?*

Em meados da década de 1960, o artigo de Flynn discutia os componentes dos computadores (armazenamento, execução e tratamento de instruções) tomando como referência sistemas SISD com execução concorrente, em particular as séries CDC 6600 e IBM Modelo 90 ([Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273); resumo no [registro do artigo](https://manuscript.isc.ac/Inventory/49/885972.htm)).

O paralelismo já existia na prática: processadores paralelos foram construídos quase desde o primeiro uniprocessador, e as primeiras implementações foram multiprocessadores simples ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). O pipeline já era reconhecido no trabalho original de 1966 ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

Com o surgimento dos processadores de arranjo SIMD, como o ILLIAC IV (descrito em artigo de 1968), a necessidade de distinguir tipos de organização ficou clara ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

Quanto ao MISD, o mesmo autor observa que algumas das primeiras máquinas, da década de 1940, poderiam ser vistas como MISD: calculadoras programáveis por painéis de ligação, em que o dado passava por etapas em sequência ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). A associação do MISD com redundância, como nos computadores de controle de voo do Ônibus Espacial, aparece depois, em materiais didáticos ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5); sistema descrito em [Spector e Gifford, 1984](https://doi.org/10.1145/358234.358246)).

### 1.7 Problema a Resolver

*Quais limitações tecnológicas motivaram sua criação?*

O problema principal era conceitual: faltava uma forma simples de descrever e comparar os tipos de paralelismo oferecidos pelo hardware ou disponíveis em uma aplicação ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). O artigo de 1966 propôs classificar os computadores de alto desempenho pela quantidade de fluxos de instruções e de dados ([Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273)).

Havia também uma limitação técnica da época: o artigo de 1966 já mencionava a ideia de decodificar várias instruções ao mesmo tempo, mas a considerava inviável para a tecnologia disponível. Anos depois, essa restrição ficou conhecida como "gargalo de Flynn" ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

### 1.8 Principais Contribuições

- **O conceito de fluxo:** uma sequência de instruções ou de dados vista pela máquina, usada como critério de comparação ([Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273)).
- **As quatro classes:** SISD, SIMD, MISD e MIMD, que organizam as combinações de fluxos únicos e múltiplos ([Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273)).
- **Uma visão do programador:** a classificação parte do que o conjunto de instruções expõe, o que a torna aplicável tanto a máquinas quanto a aplicações ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
- **O MISD como pipeline de funções:** o dado atravessa etapas cujas funções são definidas antes da execução ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
- **Base para extensões:** por ser simples, a taxonomia inspirou várias propostas de outros autores ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

## 2. Evolução

Esta seção mostra como a taxonomia de Flynn e a categoria MISD mudaram desde 1966 e em que ponto estão hoje. Quando a fonte não afirma algo diretamente, o texto indica que é interpretação do grupo.

### 2.1 Antecedentes

- **Máquinas anteriores a 1960:** algumas calculadoras programáveis da década de 1940, em que o dado passava por etapas em sequência, podem ser vistas como MISD ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
- **Paralelismo desde cedo:** processadores paralelos foram construídos quase desde o primeiro uniprocessador, e as primeiras implementações eram multiprocessadores simples ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
- **Computadores de alto desempenho de 1966:** as séries CDC 6600 e IBM Modelo 90 serviam de referência no artigo original ([registro do artigo](https://manuscript.isc.ac/Inventory/49/885972.htm)).
- **Processadores de arranjo:** o ILLIAC IV tornou necessário distinguir as organizações ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). O contexto completo está em 1.6.

### 2.2 Principais Mudanças

1. **Ampliação em 1972:** o próprio Flynn revisou o trabalho original ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
2. **Extensões de outros autores:** por ser simples, a taxonomia recebeu propostas como as de Handler, Kuck e El-Rewini ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
3. **Superação do gargalo de emissão:** quase todas as máquinas passaram a usar pipeline e muitas emitem várias instruções por vez ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
4. **MIMD em dois tipos:** com múltiplas linhas de execução (*multithreading*) e com múltiplos núcleos, frequentemente combinados ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).
5. **Surgimento do SIMT:** definido originalmente como subconjunto do SIMD, permite ativar ou desativar threads selecionadas ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).

### 2.3 Evolução Tecnológica

| Período | Marco | Fonte |
| --- | --- | --- |
| Década de 1940 | Calculadoras programáveis por painéis, vistas como precursoras do MISD | [Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2) |
| 1966 | Artigo que propõe as quatro classes | [Flynn, 1966](https://doi.org/10.1109/PROC.1966.5273) |
| 1972 | Ampliação da proposta | [Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2) |
| A partir de 2004 | Fim da escala de Dennard e início da era multicore | [Esmaeilzadeh et al., CACM](https://cacm.acm.org/?p=49355); [OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures) |
| Anos seguintes | Aceleradores (GPUs, TPUs, FPGAs) ao lado dos núcleos de uso geral | [OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures) |
| 2014 e 2016 | Lançamento do ESP8266 e do ESP32, plataforma do protótipo | [Espressif, 2023](https://www.espressif.com/en/news/1_Billion_Chip_Sales) |
| 2023 | Espressif passa de 1 bilhão de chips enviados (dado da fabricante) | [Espressif, 2023](https://www.espressif.com/en/news/1_Billion_Chip_Sales) |
| 2023–2024 | Aprendizado de máquina em microcontroladores (TinyML) | [Lin et al.](https://arxiv.org/pdf/2403.19076) |
| 2026 | ESP32-S31, dois núcleos RISC-V voltado a aprendizado de máquina na borda | [Hackster](https://www.hackster.io/news/espressif-s-esp32-s31-dual-core-edge-smarts-microcontroller-hits-the-mainstream-launches-at-4-51-f616e6fc1716.amp) |

### 2.4 Possíveis Sucessores

Não há uma taxonomia oficial que tenha substituído a de Flynn. Ela continua em uso e foi complementada por extensões de outros autores ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)).

Quanto ao MISD, a entrada de Flynn aponta como organizações próximas os processadores de fluxo (*streaming*), as GPUs de uso geral e as máquinas de fluxo de dados, algumas já realizadas em FPGA ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)). Outras fontes tratam as GPUs como SIMT, subconjunto do SIMD ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)), e essa divergência está registrada.

Interpretação do grupo: o caminho mais provável para o legado do MISD é a especialização, com arquiteturas de domínio específico e aceleradores convivendo com núcleos de uso geral ([OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)).

### 2.5 Sistemas Relacionados

| Sistema | Relação com a taxonomia | Fonte |
| --- | --- | --- |
| CDC 6600 e IBM Modelo 90 | Referências SISD com execução concorrente | [registro do artigo](https://manuscript.isc.ac/Inventory/49/885972.htm) |
| ILLIAC IV | Processador de arranjo SIMD | [Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2) |
| Computadores do Ônibus Espacial | Exemplo de MISD ligado à redundância | [RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5); [Spector e Gifford, 1984](https://doi.org/10.1145/358234.358246) |
| Máquinas de fluxo de dados e GPUs de uso geral | Organizações próximas do MISD, segundo Flynn | [Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2) |
| Intel Xeon | Processadores multicore para servidores (MIMD) | [eWeek, 2016](https://www.eweek.com/servers/intel-looks-to-drive-cloud-adoption-with-new-xeon-server-chips/) |
| ESP32 | Citado como processador multicore (MIMD) | [RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5) |

### 2.6 Características que Permaneceram ou Foram Modificadas

| Característica | Situação | Observação |
| --- | --- | --- |
| Critério de fluxos de instruções e de dados | Permaneceu | Ainda usado em materiais atuais ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) |
| As quatro classes | Permaneceram | SISD, SIMD, MISD e MIMD continuam como linguagem básica |
| SIMD | Modificada | De processadores de arranjo para instruções vetoriais (AVX, NEON) e SIMT ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) |
| MIMD | Modificada | De multiprocessadores para vários núcleos em um chip, inclusive heterogêneos ([OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)) |
| MISD | Modificada e pouco usada | Lido como pipeline por Flynn e como redundância em materiais didáticos ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2); [RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) |
| Gargalo de emissão múltipla | Superada | Processadores superescalares emitem várias instruções ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| Visão apenas pelo conjunto de instruções | Limitada | A classificação omite sutilezas da implementação ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |

## Referências

- Flynn, M. J. (1966). [Very high-speed computing systems](https://doi.org/10.1109/PROC.1966.5273). Proceedings of the IEEE, 54(12), 1901–1909. *Texto integral não consultado; resumo conferido pelo registro abaixo.*
- Flynn, M. J. (1972). [Some computer organizations and their effectiveness](https://doi.org/10.1109/TC.1972.5009071). IEEE Transactions on Computers, C-21(9), 948–960. *Texto integral não consultado.*
- Flynn, M. J. (2011). [Flynn's Taxonomy](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2). Encyclopedia of Parallel Computing, Springer.
- [Registro bibliográfico de "Very high-speed computing systems"](https://manuscript.isc.ac/Inventory/49/885972.htm). Fonte secundária, usada para afiliação e resumo.
- RoboticLab. [Processor Taxonomies, SISD, SIMD, MIMD, MISD, SIMT](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5).
- Spector, A.; Gifford, D. (1984). [The space shuttle primary computer system](https://doi.org/10.1145/358234.358246). Communications of the ACM, 27(9). *Texto integral não consultado.*
- Esmaeilzadeh, H. et al. [Dark Silicon and the End of Multicore Scaling](https://cacm.acm.org/?p=49355) (versão no CACM; original no ISCA, 2011).
- OpenStax. [Processor Architectures](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures). Introduction to Computer Science.
- eWeek (2016). [Intel Looks to Drive Cloud Adoption with New Xeon Server Chips](https://www.eweek.com/servers/intel-looks-to-drive-cloud-adoption-with-new-xeon-server-chips/).
- Espressif Systems (2023). [Espressif Leads the IoT Chip Market with Over 1 Billion Shipments Worldwide](https://www.espressif.com/en/news/1_Billion_Chip_Sales).
- Hackster.io. [Espressif's ESP32-S31 Dual-Core Edge-Smarts Microcontroller](https://www.hackster.io/news/espressif-s-esp32-s31-dual-core-edge-smarts-microcontroller-hits-the-mainstream-launches-at-4-51-f616e6fc1716.amp).
- Lin, J. et al. [Tiny Machine Learning: Progress and Futures](https://arxiv.org/pdf/2403.19076). IEEE Circuits and Systems Magazine (arXiv, 2024).
