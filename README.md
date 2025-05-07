# Desafio Qlik AutoML

## Resumo

- [License Summary](#license-summary)
- [Disclaimer](#disclaimer)
- [O Desafio](#introduction)
- [Docker image](#docker-image)
    - [Pulling Qlik Data Movement gateway docker image](#pulling-qlik-data-movement-gateway-docker-image)
    - [Build Qlik Data Movement Docker image](#build-qlik-data-movement-docker-image)
- [Setup Container](#setup-container)
- [Starting and stopping the Data Movement services](#starting-and-stopping-the-data-movement-services)
- [Upgrading Qlik Data Movement](#upgrading-qlik-data-movement)
- [Installing new ODBC drivers](#installing-new-odbc-drivers)

## License

This project is made available under a modified MIT license. See the [LICENSE](LICENSE) file.

## Disclaimer

1. This is **not** a Qlik Supported Project/Product.
2. Contributions such as Issues, Pull Request and additional codes are welcomed.
3. **Qlik Inc.** or **Qlik Support** has no affiliation with this project. The initial version was developed by [Pedro Bergo](https://www.linkedin.com/in/cleveranjos/) who is currently employed as Qlik Data Integration Senior Implementation Consultant at Qlik Data Professional Services Team.

## Introdução

Esse documento foi criado como desafio para uso do [Qlik AutoML](https://www.qlik.com/us/products/qlik-automl), possibilitando aos interessados entender e aplicar alguns dos recursos da plataforma Qlik Cloud (https://www.qlik.com).


## Cenário

A COM.ROUPAS é mundialmente conhecida pelo design inovador, qualidade de seus produtos e garantia de entrega. Seus produtos e sua marca alcançam diretamente 9 países e sua presença é conhecida em 83 importantes cidades no Brasil e mundo. 

O seu modelo de negócio é baseado em dois pilares: Preços fixos e prazo de entrega de 7 dias.

Essa estratégia permitiu forte expansão a partir de 2019, usando um inovador modelo de venda, entrega e forte atendimento aos clientes e publico consumidor, a empresa mantem-se à frente da concorrência e é caso de sucesso internacional.

Mesmo com toda vantagem adquirida, a empresa enfrenta enormes desafios no seu mercado, com pressão da concorrência, aumento dos custos de fornecedores e dificuldades na logística de entregas. 

Em 2025, suas vendas continuam em crescimento, mas a empresa viu recentemente uma redução nas margens de lucro, causadas pelo aumento de custos diretos e também pela operação de distribuição. O cenário conflituoso mundial apresenta um desafio adicional, e a diretoria decidiu investigar a fundo os motivos que causam os problemas nas entregas.

O primeiro ponto a ser investigado é os motivos que causam cancelamento nos Pedidos de Venda da empresa e você e sua equipe serão os responsáveis por entender e apresentar uma solução para isso.


### O Desafio

A empresa deseja identificar em tempo real cada pedido de venda pode ser cancelado ou não. Ela espera que seja possível reverter possíveis cancelamentos ou redirecionar os esforços de programação de e-ntregas para pedidos que sejam cancelados.

Ela disponibilizou sua base de dados para suas análises e elaboração de um modelo de ML que permita predizer se o pedido será ou não cancelado, além de identificar quais os atributos mais interferem no cancelamento.

### O que se espera

- Saber quais dados impactam no cancelamento de pedidos.
- Método (API ou outro) que realize previsão de cancelamento em tempo real para cada novo pedido.

### Base de dados

O modelo do banco de dados está apresentado a seguir.

![Modelo de Dados](derbasedados.png)

##### Base de dados Vendas - MySQL

O banco de dados está disponível no repositório docker e pode ser acessado através dos comandos a seguir para colocar o banco no ar e popular a base de dados.

``` bash
# Open bash (bash or powerbash)
docker run --name vendasodsdb -e MYSQL_ROOT_PASSWORD="mysql1234!" -e MYSQL_DATABASE=vendasods -e MYSQL_ROOT_HOST=% -e PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin -v /var/lib/mysql -p 3306:3306 -p 33060:33060 -d pedrobergo/vendasodsdb:latest
docker container exec -it -e MYSQL_ROOT_PASSWORD="mysql1234!" vendasodsdb sh -c "mysql -u root -p vendasods < /tmp/vendasods.sql"
```

A base VENDASODS no MySQL está disponível através das seguintes credenciais:
- Conexão: localhost
- Porta: 3306
- Usuário: root
- Senha: mysql1234!
- Database: vendasods

##### Docker Desktop

Recomenda-se utilizar plataforma Docker Desktop para rodar a base MySQL.
O Docker Desktop pode ser encontrado em https://www.docker.com/products/docker-desktop/

Para rodar o Docker Desktop tem é necessário Sistema operacional Windows 10/11, 4Gb de memória e WSL-Windows Subsystem for Linux 2.

Nesse link você encontra instruções de [instalação do Docker Desktop em Windows](https://docs.docker.com/desktop/setup/install/windows-install/).

