# Monitor Hardware 🖥️

Um sistema de monitoramento de recursos de hardware em tempo real que registra o uso de CPU e memória com alertas automáticos.

## 📋 Descrição

Monitor Hardware é uma ferramenta Python que monitora continuamente o desempenho do sistema, rastreando o uso de CPU e memória em tempo real. O programa gera alertas quando os recursos atingem limites críticos e mantém um registro detalhado em arquivo de log.

## 🎯 Funcionalidades

- ✅ Monitoramento em tempo real de CPU
- ✅ Monitoramento em tempo real de Memória RAM
- ✅ Sistema de alertas quando limites são ultrapassados
- ✅ Registro persistente em arquivo de log
- ✅ Timestamps automáticos para rastreabilidade
- ✅ Interface de linha de comando clara
- ✅ Monitoramento contínuo com intervalo configurável

## ⚙️ Requisitos

- **Python 3.6+**
- **psutil** - Biblioteca para acesso a informações de sistema

### Instalação de dependências

```bash
pip install psutil
```

## 🚀 Como usar

### Iniciar o Monitor

```bash
python main.py
```

### Saída esperada

```
CPU: 25% | Memoria: 60%
CPU: 28% | Memoria: 62%
CPU: 95% | Memoria: 75% | ALERTA: CPU EM 95%
CPU: 92% | Memoria: 85% | ALERTA: CPU EM 92% | ALERTA: MEMORIA EM 85%
CPU: 45% | Memoria: 88% | ALERTA: MEMORIA EM 88%
```

## 📊 Configuração

### Ajustar Limites de Alerta

Edite os limites no arquivo `main.py`:

```python
LIMITE_CPU = 90        # Alerta quando CPU ultrapassar 90%
LIMITE_MEMORIA = 80    # Alerta quando memória ultrapassar 80%
```

### Ajustar Intervalo de Monitoramento

Altere o tempo entre verificações (em segundos):

```python
time.sleep(1)  # Verifica a cada 1 segundo (padrão)
time.sleep(5)  # Para verificar a cada 5 segundos
```

## 📁 Estrutura de Arquivos

```
monitor_hardware/
├── main.py                 # Script principal
├── logs/                   # Diretório de logs (criado automaticamente)
│   ├── hardware_2026-02-04.log
│   └── hardware_2026-02-05.log
└── README.md
```

## 📝 Estrutura do Código

### `main.py`

**Imports:**
- `psutil` - Acesso a informações de CPU e memória
- `time` - Controle de intervalo de monitoramento
- `datetime` - Timestamps para logs
- `os` - Criação de diretórios

**Constantes:**
```python
LIMITE_CPU = 90          # Percentual limite para alerta de CPU
LIMITE_MEMORIA = 80      # Percentual limite para alerta de memória
LOG_FILE = "logs/..."    # Caminho do arquivo de log
```

**Funções:**

| Função | Descrição |
|--------|-----------|
| `registrarLog(mensagem)` | Escreve mensagem no arquivo de log com timestamp |
| `monitorar()` | Verifica uso de CPU e memória, gera alertas e registra |

**Fluxo Principal:**
1. Criar diretório `logs/` se não existir
2. Loop infinito a cada segundo:
   - Obter uso atual de CPU
   - Obter uso atual de memória
   - Comparar com limites
   - Gerar alertas se necessário
   - Imprimir na tela
   - Registrar em arquivo de log

## 📊 Formato dos Logs

Os arquivos de log são criados no diretório `logs/` com o seguinte padrão:

```
[2026-02-04 14:23:45.123456] CPU: 25% | Memoria: 60%
[2026-02-04 14:23:46.234567] CPU: 28% | Memoria: 62%
[2026-02-04 14:23:47.345678] CPU: 95% | Memoria: 75% | ALERTA: CPU EM 95%
[2026-02-04 14:23:48.456789] CPU: 92% | Memoria: 85% | ALERTA: CPU EM 92% | ALERTA: MEMORIA EM 85%
```

## 💡 Casos de Uso

1. **Monitoramento de Servidor** - Rastrear saúde do sistema
2. **Detecção de Anomalias** - Identificar picos de uso
3. **Troubleshooting** - Investigar problemas de desempenho
4. **Análise Histórica** - Revisar padrões de uso
5. **Automação** - Base para scripts de resposta automática

## 🔧 Melhorias Possíveis

```python
# Monitorar outros recursos
# - Uso de disco
# - Temperatura
# - Processos top
# - Velocidade de rede

# Enviar alertas
# - Email
# - Webhook
# - SMS
# - Slack/Discord

# Interface avançada
# - GUI com tkinter
# - Dashboard web com Flask
# - Gráficos em tempo real

# Funcionalidades adicionais
# - Exportar relatórios
# - Comparação temporal
# - Limite dinâmico baseado em histórico
# - Integração com sistemas de monitoramento (Prometheus, Grafana)
```

## 📚 Conhecimentos Demonstrados

- ✅ Uso de bibliotecas externas (`psutil`)
- ✅ Operações com arquivos (I/O)
- ✅ Loops infinitos e controle de tempo
- ✅ Formatação de strings e f-strings
- ✅ Tratamento de diretórios
- ✅ Comparação de valores
- ✅ Listas e concatenação

## ⚠️ Considerações

1. **Performance** - Monitoramento contínuo pode usar recursos
2. **Espaço em Disco** - Logs podem crescer indefinidamente
3. **Limpeza de Logs** - Implemente rotação de arquivos para grandes volumes
4. **Permissões** - Pode necessitar de privilégios elevados em alguns sistemas
5. **Multiplataforma** - Funciona em Windows, Linux e macOS

## 🛠️ Dicas de Uso

### Executar em Background (Linux/macOS)
```bash
python main.py > /dev/null 2>&1 &
```

### Executar com `nohup` (Linux)
```bash
nohup python main.py &
```

### Executar como Serviço (Windows)
Use a tarefa agendada do Windows ou ferramentas como NSSM

### Monitorar o Monitor
```bash
# Terminal 1
python main.py

# Terminal 2
tail -f logs/hardware_*.log
```

## 📦 Expansão Futura

```python
# Exemplo de extensão com monitoramento de disco
def monitorar_disco():
    uso_disco = psutil.disk_usage('/').percent
    if uso_disco > 90:
        return f"ALERTA: DISCO EM {uso_disco}%"
    return f"Disco: {uso_disco}%"

# Exemplo com lista de processos top
def processos_top():
    procs = psutil.process_iter(['pid', 'name', 'cpu_percent'])
    top_5 = sorted(procs, key=lambda p: p.cpu_percent(), reverse=True)[:5]
    return top_5
```

## 📄 Licença

Este projeto não possui licença especificada.

## 👨‍💻 Autor

[deVictorS](https://github.com/deVictorS)

---

**Nota:** Este é um projeto educacional para fins de monitoramento de sistema. Use responsavelmente para otimizar e entender o desempenho de seus recursos.
