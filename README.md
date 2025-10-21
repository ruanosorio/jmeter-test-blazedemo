# Projeto de Testes de Performance com JMeter

## Descrição:

Validar o desempenho da aplicação de compra de passagens aéreas [BlazeDemo](https://www.blazedemo.com) conforme o critério de aceitação:

- **250 requisições por segundo com tempo de resposta (90th percentil) inferior a 2 segundos.**

Os testes são executados utilizando o **Apache JMeter** e divididos em dois tipos:
- **Teste de Carga**: jmeter-load-test-blazedemo.jmx
- **Teste de Pico**: jmeter-spike-test-blazedemo.jmx

## Composição do projeto:

- **Ferramenta:** Apache JMeter 5.6.3  
- **Modo de execução:** Headless (linha de comando)  
- **Sistema alvo:** API ou endpoint de compra de passagens aéreas  
- **Relatórios:** HTML gerado automaticamente  

## Teste de Carga: (jmeter-load-test-blazedemo.jmx)

### Configuração:
| Parâmetro | Valor | Descrição |
|------------|--------|-----------|
| Usuários Virtuais (Threads) | 250 | Número de usuários simultâneos simulados |
| Tempo de Inicialização (Ramp-up) | 120 s | Tempo para iniciar gradualmente as 250 threads |
| Contador de Iteração | Infinito | Cada thread faz requisições até o fim do teste |
| Duração Total (Agendador) | 300 s (5 minutos) | Tempo total do teste |
| **Temporizador de Vazão Constante (Constant Throughput Timer)** | **15000 amostras/minuto** | Equivalente a 250 requisições/segundo |
| Cálculo de Vazão | Todos os usuários ativos | Distribui a carga igualmente entre as threads |

### Execução via Linha de Comando:
```
bash
jmeter.bat -n -t "..\jmeter-test-blazedemo\jmeter-load-test-blazedemo.jmx" -l "..\jmeter-test-blazedemo\results_load_test.jtl" -e -o "..\jmeter-test-blazedemo\report_load_test"
```

## Teste de Pico: (jmeter-spike-test-blazedemo.jmx)

### Configuração:
| Parâmetro | Valor | Descrição |
|------------|--------|-----------|
| Usuários Virtuais (Threads) | 300 | Número de usuários simultâneos simulados |
| Tempo de Inicialização (Ramp-up) | 10 s | Tempo para iniciar todas as 300 threads |
| Contador de Iteração | 1 | Cada thread executa apenas uma vez|
| Duração Total (Agendador) | 300 s (5 minutos) | Tempo do teste |

### Execução via Linha de Comando:
```
bash
jmeter.bat -n -t ".\jmeter-test-blazedemo\jmeter-spike-test-blazedemo.jmx" -l "..\jmeter-test-blazedemo\results_spike_test.jtl" -e -o "..\jmeter-test-blazedemo\report_spike_test"
```
