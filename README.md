import datetime
import os
import time
from github import Github

# Acesse seu repositório no GitHub usando o token pessoal
token = "SEU_TOKEN_DO_GITHUB"
repo_name = "usuario/nome-do-repositorio"
g = Github(token)
repo = g.get_repo(repo_name)

# Defina o padrão do jogo da cobrinha no gráfico de contribuições
# Exemplo: a cobrinha será representada por uma lista de dias (ano, mês, dia)
snake_pattern = [
    ("2025", "04", "20"), ("2025", "04", "21"), ("2025", "04", "22"),
    ("2025", "04", "23"), ("2025", "04", "24"), ("2025", "04", "25")
]

# Função para fazer um commit em um dia específico
def make_commit(date_tuple):
    year, month, day = date_tuple
    date_str = f"{year}-{month}-{day}"
    today = datetime.date.today()
    if today > datetime.date(int(year), int(month), int(day)):
        file_name = f"commit_{date_str}.txt"
        with open(file_name, "w") as f:
            f.write(f"Commit para o jogo da cobrinha no GitHub. Data: {date_str}")
        # Realiza o commit
        repo.create_file(file_name, f"Commit para o dia {date_str}", f"Commit para o jogo da cobrinha no dia {date_str}", branch="main")
        os.remove(file_name)
        print(f"Commit realizado em {date_str}")
        time.sleep(1)  # Delay para evitar muitos commits rápidos

# Realiza o commit para cada data no padrão da cobrinha
for date_tuple in snake_pattern:
    make_commit(date_tuple)
