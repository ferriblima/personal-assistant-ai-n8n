Agora quero que você se baseie no modelo de README.md colado nesta mensagem para gerar um novo README.md baseado na descrição do meu projeto. Crie-o todo em inglês.
Crie uma sessão de funcionamento da aplicação.
Crie uma sessão de setup da aplicação.

# personal-assistant-ai
A personal assistant to manage your emails, calendar and other functionalities through Telegram (Free Template). Created with n8n and Open AI LLM.

Descrição do meu projeto:
O que foi realizado. Se você já possui um servidor ativo com n8n em um subdomínio https, avance para a explicação do n8n em "3. Setup dos fluxos no n8n".
1. Setup de servidor AWS e instalação do n8n.
Por que tive que subir a aplicação em um servidor?
A API do telegram somente aceita comunicação através de https, porta 443.
Por que escolhi o servidor AWS?
Porque não implicavam em custos.
Vídeo que segui sobre como instalar o n8n na AWS através de docker: https://www.youtube.com/watch?v=-gyIdyy3X0Y
Dar os créditos para https://github.com/henrylle que é o instrutor do vídeo sobre como instalar o n8n através de docker na AWS.
Passo a passo para criação do servidor e instalação do n8n:
    1. Entrar em Security Groups na AWS e criar um grupo com a permissão para a porta 443.
    2. Entrar em EC2 instances e criar uma nova instância. Na criação da instância, utilizar o Security Group criado e inserir o código de instalação docker do arquivo scripts/server_ec2_user_setup.sh.
    3. Entrar na instância.
    4. Acessar com o usuário ec2-user com o comando sudo su ec2-user
    5. Acessar a pasta do projeto pelo comando cd /home/ec2-user
    6. Criar a pasta n8n com o comando mkdir n8n
    7. Entrar na pasta n8n com o comando cd n8n
    8. Criar os arquivos .env e docker-compose.yml como estão no repositório git
    9. Editar o arquivo .env com suas informações. O domínio e subdomínio serão criados por você ao registrar o domínio.
    10. Rodar o comando para subir o docker, docker docker-compose up -d.
    Obs.: Não será necessário criar redirecionamento de subdomínio em Route 53 pois o redirecionamento será feito pelo duckDNS
Documentação do n8n sobre como instala-lo e configura-lo no servidor através de docker: https://docs.n8n.io/hosting/installation/server-setups/docker-compose/#1-install-docker

2. Setup do subdomínio na duckDNS
Por que escolhi a duckDNS?
Porque não implicavam em custos.
Site do duckDNS: https://www.duckdns.org/domains
Passo a passo para criação do subdomínio através do duckDNS:
    1. Acesse o site da duckDNS
    2. Crie um subdomínio a sua escolha
    3. Utilize o nome do subdomínio e domínio criados no arquivo .env do servidor. Ex: n8n.duckdns.org -> Domínio: duckdns, Subdomínio: n8n.
    4. Insira o Ip público do servidor no campo de redirecionamento do site da duckDNS. O Ip público do servidor pode ser obtidio através da página de instâncias da AWS ou através do comando curl ifconfig.me.

3. Criação do Chat bot no telegram
    1. Abra a conversa com o BotFather (gerenciador de bots do Telegram).
    2. Peça para ele criar um novo bot através da mensagem /newbot.
    3. Reesponda às perguntas feitas pelo BotFather com o nome do seu bot e username.
    4. Salve sua api key do telegram gerada.
    5. Acesse seu bot para poder iniciar uma conversa.

4. Setup dos fluxos no n8n
Passo a passo para setup dos fluxos no n8n:
    1. Se as etapas anteriores foram concluídas com êxito, você consegue acessar sua página do n8n através do site configurado por você. Exemplo: subdomain.example.com.
    2. Após acessar o site, crie uma conta no n8n.
    3. Crie um novo workflow para cada um dos arquivos .js de workflow n8n da pasta n8n/workflowFiles e importe-os nos workflows criados.
    4. O workflow principal que fará o roteamento da requisição para os workflows Agentes será o Personal Assistant, neste workflow crie a credencial de comunicação com o telegram no nó trigger através di telegram. Documentação n8n e Telegram: https://docs.n8n.io/integrations/builtin/app-nodes/n8n-nodes-base.telegram/
    5. Crie uma conta na Open AI (você ganhará US$ 5,00 para testes), crie uma chave API e então crie uma crdencial da Open AI no seu fluxo n8n no nó da Open AI.
    6. No workflow principal crie novamente os nós dos agentes através do tipo de nó Call n8n Workflow Tool. Seu name deve ser o respectivo nome de agente contido no prompt do nó Ultimate Assistant.
    7. Abra os workflows dos agentes e crie as credenciais necessárias. Nos casos de credenciais google, deve-se fazer através de autenticação OAuth2 (conta de serviço não funcionará de forma trivial) e habilite as APIs correspondentes aos agentes no seu projeto do Google Cloud (Exemplo: API Gmail, API Calendar).
Vídeo tutorial de Nate Herk: https://www.youtube.com/watch?v=9FuNtfsnRNo
Dar os créditos para Nate Herk (https://www.youtube.com/@nateherk)

Funcionamento da aplicação:
1. O usuário faz uma pergunta para seu chat bot do Telegram.
2. Dependendo da pergunta o usuário recebe uma resposta do LLM ou tem a sua requisição realizada.
Exemplos de requisições: 
- Agente um evento para o dia todo no dia 15 de março.
- Cancele o evento aniversário Pedro do dia 01 de abril.
- Escreva um rascunho de email para example@gmail.com com uma mensagem de bom dia.
- Envie um email...
Obs.: Os comandos podem ser por texto ou voz.

Modelo README.md:
# Teachers AI Project

## About The Project

Teachers AI Project is a web application designed to integrate artificial intelligence functionalities, using the OpenAI API, to create a virtual assistant aimed at curious children. Users can interact with the assistant through a chat interface to get educational content and assistance.

### Preview

Below are some screenshots demonstrating the interface of the project:

#### Home Page
![Home Page Screenshot](public/images/home_page.png)

#### Chat Interface and Example of a Conversation
![Chat Interface Screenshot](public/images/chat_interface.png)

### Creator's Message
The project was entirely created using **GPT 4.0**, from code to images and documentation. Total development time was approximately **8 hours and 30 minutes**, with the following major challenges:
- API integration issues.
- Generating suitable images.
- Testing and styling the UI (positioning blocks, images, and buttons).

## Built With

- ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
- ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

## Getting Started

### Prerequisites

- PHP installed on your system.
- Composer to manage PHP dependencies.
- Chat GPT account to provide the API key.

### Installation

1. Rename the `.env.example` file to `.env`.
2. Add your OpenAI API key to the `.env` file:
   ```env
   OPENAI_API_KEY=your_api_key
   ```
   OpenAI Documentation: [https://platform.openai.com/docs/quickstart](https://platform.openai.com/docs/quickstart)
3. Install the PHP dependencies:
   ```bash
   composer install
   ```
4. Open the `app/index.html` file in your browser, or start a local PHP server and navigate to the project directory.

## Usage

This project uses a chat interface to interact with a virtual assistant for educational purposes. The assistant:
- Answers questions.
- Engages children in a fun and interactive way.

### Main Files
- **proxyOpenAi.php**: A PHP script that acts as a proxy to interact with the OpenAI API, securing the API key.
- **index.js** and **chat.js**: Handle user interaction and requests to the backend.

## Roadmap

- [x] Basic integration with OpenAI API.
- [ ] Add voice interaction support.
- [ ] Create a mobile-friendly interface.

See the [open issues](https://github.com/ferriblima/teachers-ai/issues) for more features and known issues.

## Contributing

Contributions are welcome and greatly appreciated! Here’s how you can contribute:
1. Fork the project.
2. Create your feature branch (`git checkout -b feature/AmazingFeature`).
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`).
4. Push to the branch (`git push origin feature/AmazingFeature`).
5. Open a Pull Request.

## License

Distributed under the **Unlicense License**. See `LICENSE.txt` for more information.

## Contact

**Fernando Lima**  
[LinkedIn](https://www.linkedin.com/in/fernandoribeirolima/) - ferriblima@gmail.com  

Project Link: [https://github.com/ferriblima/teachers-ai](https://github.com/ferriblima/teachers-ai)

## Acknowledgments and References

- [OpenAI](https://openai.com)
- [Markdown Guide](https://www.markdownguide.org)
- [Best README Template](https://github.com/othneildrew/Best-README-Template)
- [Python Application Layouts: A Reference](https://realpython.com/python-application-layouts/)
