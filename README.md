Just a test bot for OpenAI translating tech pages

Use the following in a Jupyter Notebook or Python env:

#Install the necessary libs. Take out the ! if using dieectly into your terminal env

!pip install requests beautifulsoup4 openai langchain-openai


# Code to be put into .py file to test the extraction of text
import requests
from bs4 import BeautifulSoup

def extract_text_from_url(url):
  response = requests.get(url)

  if response.status_code == 200:
    soup = BeautifulSoup(response.text, 'html.parser')
    for script in soup(['script', 'style']):
      script or style.decompose()
    text = soup.get_text(separator= ' ')
    #clean text
    linhas = (line.strip() for line in text.splitlines())
    parts = (phrase.strip() for line in linhas for phrase in line.split("  "))
    text = '\n'.join(part for part in parts if part)
    return text
  else:
      print(f"Failed to fetch the URL. Status code: {response.status_code}")
      return None

  text = soup.get_text()
  return text

extract_text_from_url('https://dev.to/kenakamu/azure-open-ai-in-vnet-3alo')

from langchain_openai.chat_models.azure import AzureChatOpenAI

client = AzureChatOpenAI(
    azure_endpoint = ""
    api_key = ""
    api_version = "2023-07-01-preview"
    deployment_name = "gpt-35-turbo"
)
