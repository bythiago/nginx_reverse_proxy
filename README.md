## Leia-me

**Docker Nginx Reverse Proxy**

Este projeto utiliza o Docker Compose para configurar um proxy reverso usando o Nginx.

**Serviços**

* **nginx** (nome do container: `nginx_reverse_proxy`)
  * **Imagem:** `nginx:stable-alpine` (Usa a última imagem estável do Alpine Linux para Nginx)
  * **Portas:**
    * `80:80` (Mapeia a porta 80 do container para a porta 80 do host, fornecendo acesso público ao proxy reverso)
  * **Volumes:**
    * `./conf.d/default.conf:/etc/nginx/conf.d/default.conf` (Monta o arquivo `default.conf` do diretório local do projeto para a localização `/etc/nginx/conf.d/default.conf` do container. Isso permite que você personalize a configuração do Nginx para suas necessidades específicas.)
  * **Redes:**
    * `my_network` (Conecta o container Nginx à rede `my_network`)

**Redes**

* **my_network**
  * **Externo:** `true` (Indica que esta rede é uma rede externa existente em seu host Docker. Certifique-se de ter uma rede chamada `my_network` criada antes de executar `docker-compose up`.)

**Começando**

1. **Pré-requisitos:**
   * Docker e Docker Compose instalados em seu sistema. ([https://docs.docker.com/get-started/](https://docs.docker.com/get-started/))
   * Uma rede externa existente chamada `my_network` em seu host Docker. Você pode criar uma usando `docker network create my_network`.

2. **Configuração:**
   * Edite o arquivo `./conf.d/default.conf` para configurar as configurações do proxy reverso. Este arquivo especifica como o Nginx deve rotear as solicitações recebidas para seus serviços back-end. Consulte a documentação do Nginx para opções de configuração detalhadas: [https://nginx.org/en/docs/](https://nginx.org/en/docs/)

3. **Executar o aplicativo:**
   * Abra um terminal no diretório do projeto e execute `docker-compose up -d`. Isso criará a imagem Nginx se necessário, criará os serviços e a rede (se ainda não existirem) e os iniciará em modo separado (plano de fundo).

4. **Acesse seu aplicativo:**
   * Seu aplicativo agora deve estar acessível através de `http://localhost`. O comportamento específico dependerá da sua configuração em `./conf.d/default.conf`.

**Observações Adicionais**

* Para armazenamento de dados persistente dentro dos containers, considere usar volumes do Docker.
* Para parar os containers, execute `docker-compose down`.
* Para reiniciar os containers com qualquer alteração, execute `docker-compose up -d`.

Este Leia-me fornece uma visão geral abrangente da configuração do projeto e instruções para executar seu proxy reverso usando o Docker Compose. Sinta-se à vontade para personalizá-lo ainda mais com base em seus requisitos específicos.
