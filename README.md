# projeto-Alura-robotica-
#vai ser útil para quem que aprender robótica
#um jogo de perguntas e respostas (*/ω＼*)
import requests  # Biblioteca para fazer requisições HTTP
from bs4 import BeautifulSoup  # Biblioteca para manipular conteúdo HTML

def get_quiz_data(http://quiz perguntas e respostas):  # Função para buscar dados do quiz
  """
  Esta função recebe a URL do quiz e retorna um dicionário contendo as perguntas e respostas.

  Argumentos:
      url (str): A URL da página que contém o quiz.

  Retorna:
      dict: Um dicionário com as perguntas e respostas do quiz.
  """

  response = requests.get(url)  # Faz uma requisição HTTP para a URL
  if response.status_code == 200:  # Verifica se a requisição foi bem-sucedida
    soup = BeautifulSoup(response.content, 'html.parser')  # Cria um objeto BeautifulSoup
  else:
    print(f'Erro ao acessar a URL: {response.status_code}')  # Mensagem de erro
    return None

  # Localizar os elementos HTML que contêm as perguntas e respostas
  questions_elements = soup.find_all('div', class_='question')  # Exemplo de classe CSS para perguntas
  answers_elements = soup.find_all('div', class_='answer')  # Exemplo de classe CSS para respostas

  # Extrair perguntas e respostas dos elementos HTML
  questions = []
  answers = []
  for question_element, answer_element in zip(questions_elements, answers_elements):
    question_text = question_element.text.strip()  # Pegar o texto da pergunta e remover espaços em branco
    answer_text = answer_element.text.strip()  # Pegar o texto da resposta e remover espaços em branco
    questions.append(question_text)  # Adicionar a pergunta à lista
    answers.append(answer_text)  # Adicionar a resposta à lista

  # Armazenar perguntas e respostas em um dicionário
  quiz_data = {
    'perguntas': questions,  # Chave 'perguntas' para a lista de perguntas
    'respostas': answers  # Chave 'respostas' para a lista de respostas
  }

  return quiz_data  # Retornar o dicionário contendo as informações do quiz

# Exemplo de uso
url = "https://exemplo.com/quiz"  # Substitua por URL real do quiz
quiz_data = get_quiz_data(url)

if quiz_data:
  print("Perguntas:")
  for question in quiz_data['perguntas']:
    print(question)

  print("\nRespostas:")
  for answer in quiz_data['respostas']:
    print(answer)
else:
  print("Falha ao obter dados do quiz.")
