# Banco-de-Dados-a-partir-do-Excel
Importando bibliotecas
import pandas as pd import sqlite3

Ler a planilha em Excel
df = pd.read_excel('caminho/do/arquivo.xlsx')

Obter os nomes das colunas e seus tipos de dados
colunas = df.columns tipos_de_dados = df.dtypes

Criar a conexão com o banco de dados
conn = sqlite3.connect('nome_do_banco_de_dados.db') cursor = conn.cursor()

Cria a tabela com as mesmas colunas do arquivo em Excel
query = 'CREATE TABLE IF NOT EXISTS nome_da_tabela (' for coluna, tipo_de_dado in zip(colunas, tipos_de_dados): if tipo_de_dado == 'int64': tipo_de_dado_sql = 'INTEGER' elif tipo_de_dado == 'float64': tipo_de_dado_sql = 'REAL' elif tipo_de_dado == 'object': tipo_de_dado_sql = 'TEXT' else: tipo_de_dado_sql = 'TEXT' # Defina o tipo de dado padrão como TEXT

query += f'{coluna} {tipo_de_dado_sql}, '
query = query.rstrip(', ') + ')' cursor.execute(query)

Inserir os dados na tabela
df.to_sql('nome_da_tabela', conn, if_exists='replace', index=False)

Fechar a conexão com o banco de dados
conn.close()
