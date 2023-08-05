# Deployment do Quake III em OpenShift

# 1. Implantação:
* A Implantação é definida com o nome "quake".
* Especifica que uma réplica do servidor Quake será implantada.
* O modelo de pod define dois containers: um para o servidor Quake e outro para o servidor de conteúdo.
* O container do servidor Quake executa o comando "q3 server" com alguns argumentos adicionais.
* O container do servidor de conteúdo executa o comando "q3 content" com uma URL de conteúdo de referência (seed content).
* Ambos os containers utilizam a mesma imagem "quay.io/sebastienblanc0/quake:latest".
* Uma sonda de prontidão (readiness probe) é configurada para verificar a saúde do servidor Quake a cada 5 segundos após um atraso inicial de 15 segundos.
* Os containers montam os volumes "quake3-server-config" e "quake3-content" para acessar suas respectivas configurações e dados de conteúdo.

# 2. Serviço:
* O Serviço é definido com o nome "quake".
* Ele expõe o servidor Quake em um NodePort para permitir acesso externo.
* O Serviço encaminha o tráfego para três portas diferentes nos pods: 8080 para o cliente, 27960 para o servidor e 9090 para o servidor de conteúdo.

# 3. ConfigMap:
* O ConfigMap é definido com o nome "quake3-server-config".
* Ele contém a configuração do servidor Quake, como as configurações do jogo, nome do servidor, senha e mapas.

# 4. Rota:
* A Rota é definida com o nome "quake".
* Ela expõe o servidor Quake fora do cluster usando Rotas do OpenShift.
* A rota é direcionada para o Serviço com o nome "quake", segmentando a porta "client".
