# CPU 8-Bits
CPU 8 Bits com arquitetura SAP1 modificada. 

<img width="3002" height="2372" alt="8bit_cpu" src="https://github.com/user-attachments/assets/e4caab1e-b49e-45e5-9d39-5b66e0dd79b2" />

[Vídeo demonstração](https://drive.google.com/file/d/1WQ23KFo91ojvwqipOiyBRpFyOytN0BDc/view?usp=sharing)

Inclui o arquivo do circuito da CPU, assim como todos os componentes utilizados para constituir ela, como a própria ALU.

## Execução

1. Baixe todos os arquivos do repositório em uma mesma pasta. 
2. Instale o [Digital](https://github.com/hneemann/digital) e abra o arquivo *'8bit_cpu.dig'*.
3. Inicie a simulação.

## Operações em 8-bit
| OP | Operação |
|--- |---       |
| 0  | AC + N   |
| 1  | AC - N   |
| 2  | AC * N  (resultado 16-bit) |
| 3  | AC / N  (resto e quociente) |
| 4  | AC shift lógico esquerda |
| 5  | AC shift lógico direita |
| 6  | AC NAND N|
| 7  | AC XOR N |

## Arquitetura

Para construir uma CPU SAP, deve se usar apenas um barramento para a comunicação entre diversos componentes. Para controlar o fluxo desse barramento, se faz uso da Control Unit, que é responsável por gerenciar quais componentes e drivers estão ativos em cada momento, garantindo que não ocorram curtos ou processamento de dados incorretos.
Recomenda-se então o uso de um Ring Counter para auxiliar nesse processo, com cada um de seus estados sendo decodificado pela UC e permitindo um fluxo específico.

Nessa CPU, o ciclo FETCH é consistente com o de uma SAP comum, mas seus operandos estão armazenados sequencialmente, ou seja, para cada ciclo o próximo operando é sempre o próximo da lista, facilitando a busca. Além disso, todo ciclo da CPU possui as mesas etapas, incluindo na execução, uma vez que a ALU foi desenvolvida de modo que possuindo valor de N e OPCODE, qualquer operação pode ser realizada, simplificando ainda mais o fluxo da CPU.

### Estados da CPU
#### FETCH:
- T1: MAR <- PC
- T2: REG R <- ROM IR, PC <- PC + 1
- T3: REG N <- ROM OP

#### EXECUÇÃO:
- T4: REG MQ <- ALU LSB
- T5: REG AC <- ALU MSB

#### EXIBIÇÃO
- T6: (Exibição do resultado)
