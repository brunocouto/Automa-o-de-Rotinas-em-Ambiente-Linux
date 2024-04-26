# Automação-de-Rotinas-em-Ambiente-Linux
automação de rotinas em ambiente Linux usando Python.
Identificação de Tarefas:
Backup de diretórios importantes
Verificação de espaço em disco
Monitoramento de logs do sistema
Gerenciamento de permissões de arquivos
Atualização automática de pacotes do sistema
Desenvolvimento de Scripts:
a) Backup de diretórios importantes:
python
import os
import shutil
import datetime

# Diretórios a serem backupados
diretórios_backup = ['/home/usuario/documentos', '/etc', '/var/log']

# Diretório de destino do backup
diretorio_backup = '/backup'

# Criar diretório de backup se não existir
if not os.path.exists(diretorio_backup):
    os.makedirs(diretorio_backup)

# Data e hora atual para nomear o backup
data_hora = datetime.datetime.now().strftime('%Y-%m-%d_%H-%M-%S')
arquivo_backup = os.path.join(diretorio_backup, f'backup_{data_hora}.tar.gz')

# Criar o backup
with tarfile.open(arquivo_backup, 'w:gz') as tar:
    for diretorio in diretórios_backup:
        tar.add(diretorio)

print(f'Backup concluído: {arquivo_backup}')

b) Verificação de espaço em disco:
python
import shutil

# Obter informações sobre o sistema de arquivos
disk_usage = shutil.disk_usage('/')

# Calcular o espaço livre em gigabytes
espaco_livre_gb = disk_usage.free / (1024.0 ** 3)

# Definir o limite de espaço livre (ex: 10 GB)
limite_espaco_livre = 10

if espaco_livre_gb < limite_espaco_livre:
    print(f'Atenção! Espaço livre em disco abaixo do limite de {limite_espaco_livre} GB.')
else:
    print(f'Espaço livre em disco: {espaco_livre_gb:.2f} GB')

c) Integração com Cron Jobs:
Para agendar a execução periódica dos scripts, você pode usar o utilitário Cron do Linux. Siga estes passos:
Abra o editor de tarefas Cron:
crontab -e

Adicione as linhas para executar os scripts Python:
0 2 * * * /usr/bin/python3 /caminho/para/script_backup.py
30 * * * * /usr/bin/python3 /caminho/para/script_verificacao_disco.py

Essa configuração executará o script de backup às 2h da manhã todos os dias e o script de verificação de disco a cada meia hora.
