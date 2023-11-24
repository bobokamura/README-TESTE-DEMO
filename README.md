# README - Deploy DEMO:

Este guia fornece instruções detalhadas sobre como realizar um deploy da aplicação em demo. Certifique-se de seguir cada etapa com atenção para garantir um processo de deploy seguro e bem sucedido.

## Passos para o Deploy

1. **Criando a branch**     
    - Crie a branch a partir da *develop* e de preferência com o nome do card que será feito o deploy.
      > Ex: TS-1234-develop
    - Dê um `git pull origin <NOME_DA_BRANCH>` na branch da nova versão;
    - Em caso de conflitos, verificar e resolver as alterações feitas do card;
    - Utilize o Maven para gerar o JAR:
        ```
        mvn clean compile install
        ```  

3. **FileZilla - Atualização dos JARs:**
    - `Endereço local`: apontar para diretório local onde está alocada a API e selecionar pasta *"target"*;
    - `Endereço remoto`: apontar para API que está sendo feito o deploy;
    - Renomear JAR atual:
      > - ctfl-respostaapi-1.0.jar
    - Para:
      > - ctfl-respostaapi-1.0.jar-10-07
    - Altere a data de modificação e excluia o JAR mais antigo;
    - ***EM CASO DE CARD QUE VOLTOU NO TESTE, APAGAR A PRÓPRIA VERSÃO DE TESTE;***
    - Em `Endereço local`, no diretório da pasta `target`, mover o JAR gerado anteriormente para onde estão os JAR's atuais(verifique se está movendo o tipo correto: `jar-arquivo`);
    - Utilize o FileZilla para transferir o JAR gerado para o servidor.
    - Remova o JAR antigo e renomeie o novo conforme a data de modificação.

4. **AWS - Buscar o Public IPv4 address da instância EC2:**
    - Acesse a AWS e copie o Public IPv4 address da instância EC2.
      - `EC2` -> `Instances` -> procure a API desejada;

5. **Abra o terminal:**
    - No terminal, acesse o diretório da Amazon e execute o comando:
      - `ssh -i ~/Amazon/api_auth.pem ubuntu@<COLE_O_PUBLIC_IPV4_ADDRESS>`;
    - Digite YES se for a primeira vez;
    - Comando `ls -la` para verificar o JAR que está rodando;
    - Execute o script de deploy: `./deploy.sh`.
    - Abra o navegador, cole o `<Public_IPv4_address>` + `:<PORTA>` + `/actuator/info`.
      - Por exemplo: [http://54.242.230.161:8888/actuator/info](http://54.242.230.161:8888/actuator/info).

6. **Observação:**
    - Certifique-se de seguir os passos com cuidado e sempre faça testes antes de aplicar em ambientes de produção. Este guia assume familiaridade com as ferramentas e conceitos mencionados.
