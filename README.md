## 📌 Índice
- [Descrição do Projeto](#-Descrição-do-Projeto)
- [Descrição da API](#-Descrição-da-API)
- [Desenvolvimento e escolha do tema](#-Desenvolvimento-e-escolha-do-tema)
- [Intents utilizadas](#️-intents-utilizadas)
- [Estrutura de pastas](#-Estrutura-de-pastas)
- [Arquitetura AWS](#️-arquitetura-aws)
- [Como usar o sistema](#-como-usar-o-sistema)
- [Experiências obtidas](#-experiências-obtidas)
- [Tecnologias utilizadas](#-tecnologias-utilizadas)
- [Autores](#-autores)


## 📖 Descrição do Projeto
Construir um chat bot com livre escolha do tema, utilizando o Amazon Lex V2 e fazer o deploy em uma plataforma de mensageria. Além de integrar o AWS Lambda com o bot para funcionalidades mais elaboradas.


## 📖 Descrição da API
- <strong>Inicialização do Projeto</strong>: Utilizando do passo a passo fornecido, implementamos as dependências necessárias para desenvolver as futuras aplicações.
- <strong>Rota POST</strong>: Desenvolvimento da rota que permite que o usuário insira uma frase e tenha como retorno a mesa, uma URL com um aúdio da frase, a data de criação e um hash-code.
    - <strong>Hash</strong>: Aplicamos a biblioteca 'hashlib' para desenvolvermos uma verificação de Id para cada frase gerada, na qual cada sentença enviada recebe um identificador único. Na ocasião em que a frase já se encontra no nosso banco de dados, o programa irá retornar a URL original, sem salvar novamente.
    - <strong>DynamoDB</strong>: Utilizamos o DynamoDB para armazenarmos nossas infromações relacioandas as sentenças informadas, sendo elas: Id, Data de Criação, URL do S3 e a frase.
    - <strong>Polly</strong>: A rota POST, tuiliza do arquivo Polly.py para transformar a frase recebida em um aúdio e armazenar em um bucket da S3.
- <strong>Link da Rota</strong>: Segue o link para rota POST, a frase deve ser inserida após o símbolo de igualdade. https://s9uqg4t7c9.execute-api.us-east-1.amazonaws.com/v1/tts?phrase=

## ✔️ Intents utilizadas
- <strong>WelcomeIntent</strong>: Intent inicial, apresentação do bot e das opções disponíveis "Vagas", "Canais de comunicação", "Sobre Nós".
- <strong>AboutUsIntent</strong>: Fornece mais informações sobre a empresa Compass.
- <strong>CommunicationChannelsIntent</strong>: Redes sociais e canais de comunicação para contato com a Compass.
- <strong>JobsIntent</strong>: Intent de vagas do nosso chat bot que possibilita as ações "Consultar vagas", "Candidatar-se em uma vaga" e "Consultar aplicações".
    - <strong>ConsultJobIntent</strong>: Intent para consultar vagas disponíveis de acordo com as tags do departamento: "Fullstack Web Apps", "AI & ML", "Business Management", "Marketing".
    - <strong>RegisterJobIntent</strong>: Intent para cadastrar-se em uma vaga.
    - <strong>CheckIntent</strong>: Mostra as vagas que determinado usuário se cadastrou filtrando por nome e sobrenome.
- <strong>ConverToAudioIntent</strong>: Faz a conversão de escrita para áudio.
- <strong>FallbackIntent</strong>: Tratamento de erros.
- <strong>CancelIntent</strong>: Cancelar um intent/reiniciar o bot.


## 📂 Estrutura de pastas
 
```bash
api-tts/                                          # lógica da aplicação serveless
├─ .serveless/                                    # arquivos de config do serveless
├─├─ api-tts.zip                                  
├─├─ cloudformation-template-create-slack.json    
├─├─ cloudformation-template-update-stack.json    
├─├─ meta.json                                    
├─├─ serverless-state.json                        
├─ scripts/                                       # script para converter texto em áudio
├─├─ polly.py                                     
├─ handler.py                                     # integração com o banco de dados
├─ serveless.yml                                  # configuração serveless
assets/                                           # imagens utilizadas no Readme
chatbot/                                          # arquivos necessários para rodar o bot
README.md
```


## 🏗️ Arquitetura AWS
![Imagem|Diagrama](assets/sprints6-7.jpg)


## 🚀 Como usar o sistema
[Link](https://slack.com/oauth/v2/authorize?client_id=7467454754689.7452698991717&scope=chat:write,team:read,im:history&user_scope=) para testes
1. Pré-requisitos:
    - Python instalado
    - Conta Slack
    - AWS CLI configurado
2. Clone o repositório:
    ```bash
    git clone -b grupo-1 https://github.com/Compass-pb-aws-2024-ABRIL/sprints-6-7-pb-aws-abril.git
    cd sprints-6-7-pb-aws-abril
    git checkout grupo-1
    ```
3. Variáveis de ambiente:
    - Adicione em um arquivo .env as seguintes variáveis:
        - DYNAMOTABLENAME
        - S3BUCKETNAME

4. Executando a API:
    - Acesse a pasta `api-tts` e execute o seguinte comando:
    ```bash
    serverless deploy  
    ```

5. Como rodar:
    - Crie uma lambda e coloque o código que está no arquivo lambda.py.
    - Crie uma camada no lambda para conseguir importar a biblioteca httpx para o lambda.
    - Adicione essa camada no lambda criado anteriormente.
    - Faça o upload do arquivo .zip do bot encontrado na pasta 'chatbot' do projeto para o Amazon Lex V2 e execute a compilação do bot.
    - Vincule a lambda criada anteriormente ao bot.
    - Após isso crie uma conta no Slack e integre o bot Lex nele.

## 💻 Tecnologias utilizadas
1. Serviços AWS:
    - AWS S3: Para armazenamento de dados.
    - AWS Lambda: Salvar e puxar dados do S3. Integração do Lex com a API.
    - AWS Lex: Criação do bot.
    - AWS Polly: Transformar texto em áudio.
    - DynamoDB: Banco de dados. Salvando os áudios gerados pela Polly.
    - API Gateway: Realizar a parte de API da aplicação.

2. Tecnologias utilizadas para programação:
    - Python: Linguagem utilizada para toda a lógica da aplicação.
    - Boto 3: AWS SDK para a comunicação da AWS com o Python.

## ✍🏻 Autores
| [<img loading="lazy" src="https://avatars.githubusercontent.com/u/120669342?v=4" width=115><br><sub>José Acerbi Almeida Neto</sub>](https://github.com/JoseJaan) | [<img loading="lazy" src="https://avatars.githubusercontent.com/u/142454135?v=4" width=115><br><sub>Lívia Marques Rodrigues</sub>](https://github.com/livmrqs) | [<img loading="lazy" src="https://avatars.githubusercontent.com/u/137515142?v=4" width=115><br><sub>Rafael Alves Silva Rezende</sub>](https://github.com/rafa-rez) | [<img loading="lazy" src="https://avatars.githubusercontent.com/u/123120658?v=4" width=115><br><sub>Samuel de Oliveira Vanoni</sub>](https://github.com/SamuVanoni)
| :---: | :---: | :---: | :---: |
