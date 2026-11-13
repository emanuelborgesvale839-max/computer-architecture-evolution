## Comparação

Esta seção compara o MISD, objeto de estudo do Grupo 03, com duas outras classes da taxonomia de Flynn. As fontes estão no final e, de forma completa, em [references.md](references.md). Quando uma afirmação é interpretação do grupo, o texto indica.

### 1. Objetos Comparados

- **MISD (*Multiple Instruction, Single Data*):** objeto de estudo do projeto.
- **MIMD (*Multiple Instruction, Multiple Data*):** escolhida porque é a classe a que pertencem as plataformas reais do projeto: o ESP32 e o servidor Intel Xeon ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5); [eWeek, 2016](https://www.eweek.com/servers/intel-looks-to-drive-cloud-adoption-with-new-xeon-server-chips/)).
- **SIMD (*Single Instruction, Multiple Data*):** escolhida por ser o oposto direto do MISD na tabela de Flynn: em vez de várias instruções sobre um dado, uma instrução sobre vários dados ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)).

### 2. Critérios Utilizados

Finalidade, organização, processamento, paralelismo, comunicação e armazenamento, programação, desempenho, vantagens e limitações.

O critério de entrada e saída não foi usado, porque a taxonomia de Flynn não trata de interfaces de E/S. No projeto, a E/S está no ESP32 (sensor e Wi-Fi), e não na classe MISD.

### 3. Quadro Comparativo

| Critério | MISD | SIMD | MIMD |
| --- | --- | --- | --- |
| **Finalidade** | Fazer o dado passar por uma sequência de funções, ou garantir a correção do cálculo com unidades diferentes sobre o mesmo dado ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2); [RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) | Operar sobre estruturas regulares, como vetores e matrizes, muito comuns em computação científica ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Vários processadores cooperando para resolver um mesmo problema ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| **Organização** | Conjunto em pipeline, com as funções de cada etapa definidas antes da execução ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Processador de arranjo (elementos com memória própria, em sincronia) ou processador vetorial (um processador com unidades vetoriais) ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Vários processadores ligados por uma rede de interconexão; pode ser multithread, multicore ou ambos ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| **Processamento** | O dado atravessa as etapas, e cada uma repassa o resultado à seguinte ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Uma instrução é aplicada a vários elementos; instruções vetoriais como AVX e as de processadores ARM seguem essa ideia ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) | Cada processador executa de forma independente e cooperativa ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| **Paralelismo** | De etapas (pipeline) ou de verificação redundante | De dados | De instruções, laços, procedimentos e programas independentes ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| **Comunicação e armazenamento** | O dado flui de etapa em etapa ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | No arranjo, cada elemento tem memória privada e acessar a de outro é caro; no vetorial, há uma memória global e registradores vetoriais ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Memória distribuída (troca de mensagens) ou compartilhada, o que exige consistência de memória e coerência de cache ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| **Programação** | O programador define a função de cada etapa antes da execução ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Em geral o programador enxerga algo próximo de um SISD, com dados organizados em estruturas, e o compilador faz o mapeamento ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Exige código paralelo ([OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)); memória distribuída é mais simples de implementar, porém mais difícil de programar ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) |
| **Desempenho** | As fontes consultadas não trazem medições para MISD | Pipelines vetoriais profundos oferecem alta vazão, que unidades escalares não igualam ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | O ganho com mais núcleos é limitado por energia e pela paralelização da aplicação: 7,9 vezes em dez anos em premissas otimistas e 3,7 em conservadoras ([Esmaeilzadeh et al., CACM](https://cacm.acm.org/?p=49355)) |
| **Vantagens** | Adequado a um fluxo fixo de etapas e à verificação redundante | Muito bem-sucedido em ambientes científicos com dados regulares ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Presente em praticamente todos os processadores atuais, dos relógios aos supercomputadores ([OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)) |
| **Limitações** | Termo pouco usado, e a classificação de exemplos é debatida: o Springer inclui GPUs no MISD e o RoboticLab as trata como SIMT ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2); [RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) | Depende de dados regulares e de roteamento simples entre elementos; vetoriais antigos tinham alto custo de partida e banda de memória limitada ([Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Sincronização e coerência tornam o sistema mais complexo; em 8 de 12 programas de teste, o ganho ficou em no máximo 10 vezes mesmo com energia quase ilimitada ([Esmaeilzadeh et al., CACM](https://cacm.acm.org/?p=49355)) |
| **Exemplos** | Computadores de controle de voo do Ônibus Espacial ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) | Instruções SSE, AVX e vetoriais ARM; ILLIAC IV ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5); [Flynn, 2011](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2)) | Processadores x64 e ARM multicore e o ESP32 ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) |

### 4. Análise

Interpretação do grupo, a partir do quadro:

- **A diferença central está no que se repete.** No SIMD, a instrução se repete sobre muitos dados; no MISD, o dado é o que se mantém, e as operações mudam; no MIMD, tanto instruções quanto dados variam.
- **MISD e MIMD não competem no mesmo nível.** O MIMD descreve a máquina; o MISD, no projeto, descreve a lógica de análise sobre um dado. Por isso as duas classes coexistem no protótipo.
- **O MIMD cobra por sua flexibilidade.** Sincronização, coerência e programação paralela são o preço de ter processadores independentes.
- **Faltam dados para comparar desempenho do MISD.** Como ele é pouco usado, não há medições comparáveis nas fontes consultadas, e a comparação de desempenho ficou limitada ao SIMD e ao MIMD.

### 5. Aplicação ao Protótipo do Grupo 03

| Aspecto do protótipo | Classe que mais se aproxima | Observação |
| --- | --- | --- |
| Três análises (limite, histórico e anomalia) sobre a mesma temperatura | MISD, de forma conceitual | É uma demonstração em software, como o próprio README ressalva |
| ESP32 como plataforma de coleta e transmissão | MIMD | O ESP32 é citado como processador multicore ([RoboticLab](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5)) |
| Computador com Python | MIMD | Processadores atuais são multicore ([OpenStax](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures)) |
| Hipótese futura: vários sensores simultâneos | MIMD | Proposta do grupo, ainda não implementada |

### 6. Limitações desta Comparação

- As fontes são, em sua maioria, textos didáticos e de referência; não há medições próprias de desempenho.
- A classificação de GPUs e de outros exemplos varia conforme a fonte.
- Os artigos originais de Flynn (1966 e 1972) não foram consultados no texto integral.

### Referências

- Flynn, M. J. (2011). [Flynn's Taxonomy](https://link.springer.com/referenceworkentry/10.1007/978-0-387-09766-4_2). Encyclopedia of Parallel Computing, Springer.
- RoboticLab. [Processor Taxonomies, SISD, SIMD, MIMD, MISD, SIMT](https://roboticlab.eu/homelab/en/multiasm/cs/chapter_3_5).
- OpenStax. [Processor Architectures](https://openstax.org/books/introduction-computer-science/pages/5-6-processor-architectures). Introduction to Computer Science.
- Esmaeilzadeh, H. et al. [Dark Silicon and the End of Multicore Scaling](https://cacm.acm.org/?p=49355) (versão no CACM; original no ISCA, 2011).
- eWeek (2016). [Intel Looks to Drive Cloud Adoption with New Xeon Server Chips](https://www.eweek.com/servers/intel-looks-to-drive-cloud-adoption-with-new-xeon-server-chips/).
