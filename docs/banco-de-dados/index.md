### Modelo Entidade-Relacionamento (ME-R)

#### Identificações das Entidade

* **USUARIO**
* **IMOVEL**
* **RESERVA**
* **AVALIACAOIMOVEL**
* **AVALIACAOCLIENTE**
* **PAGAMENTO**

#### Descrições das Entidades (Atributos)

* **USUARIO** (<u>idUsuario</u>, nome, email, senha, {telefone}, cpf, imagemUsuario)
* **IMOVEL** (<u>idImovel</U>, tipo, enderecao(logradouro, numero, bairro, estado, cidade, CEP), descricao, quantidadeQuartos, quantidadeSuites,garagemm, quantidadeBanheiros,quantidadeSalas,areaExterna,piscina, churrasqueira, cidade, reserva, valor, {imagensImovel})
* **RESERVA** (<u>idReserva</u>, dataInicio, dataFim, status)
* **AVALIACAOIMOVEL** (<u>idAvaliacaoImovel</u>, notaImovel, comentarioImovel, dataAvaliacaoImovel)
* **AVALIACAOCLIENTE** (<u>idAvaliacaoCliente</u>, notaCliente, comentarioCliente, dataAvaliacaoCliente)
* **PAGAMENTO**(<u>idPagamento</u>, valorPagamento, dataPagamento, statusPagamento)

#### Descrição dos relacionamentos Relacionamentos

* **USUARIO tem IMOVEL**
    * **Descrição:** Esta relação representa a posse de um imóvel.
    *  **Regra de Negócio:** Um **USUARIO** (no papel de Proprietário) pode ser dono de vários **IMOVEIS**, mas um **IMOVEL** so pode pertencer a um *pertence a um e somente um **USUARIO**.
    * **Cardinalidade:** (N:N)
* **USUARIO reserva IMOVEL**
    * **Descrição:** Esta é a relação de negócio principal que dá origem à entidade `RESERVA`.
    * **Regra de Negócio:** Um **USUARIO** (no papel de Cliente) pode reservar vários **IMOVEIS** ao longo do tempo, e um mesmo **IMOVEL** pode ser reservado por vários **USUARIO**  (em datas diferentes).
    * **Cardinalidade:** (N:N)
* **RESERVA gera AVALIACAOIMOVEL**
    * **Descrição:** Define que uma avaliação do imóvel só pode existir no contexto de uma reserva.
    * **Regra de Negócio:** Uma **RESERVA** pode ter no máximo uma **AVALIACAOIMOVEL** (o hóspede pode ou não avaliar). Uma **AVALIACAOIMOVEL** pertence a uma e somente uma **RESERVA**.
    * **Cardinalidade:** (1:1)
* **RESERVA avaliaCliente AVALIACAOCLEINTE**
    * **Descrição:** Define que uma avaliação do cliente (hóspede) só pode existir no contexto de uma reserva.
    * **Regra de Negócio:** Uma ********RESERVA** pode ter no máximo uma **AVALIACAOCLIENTE** (o proprietário pode ou não avaliar o hóspede). Uma **AVALIACAOCLIENTE** pertence a uma e somente uma **RESERVA**.
    * **Cardinalidade:** (1:1)
* **RESERVA realiaza PAGAMENTO**
    * **Descrição:** Associa um ou mais pagamentos a uma reserva específica.
    * **Regra de Negócio:** Uma **RESERVA** pode exigir um ou vários **PAGAMENTOS** (por exemplo, um sinal para confirmar e o restante depois). Um **PAGAMENTO** específico refere-se a uma e somente uma **RESERVA**.
    * **Cardinalidade:** (1:1)

### Diagrama de Entidade-Relacionamento(DE-R)

![DE-R](./images/Conceitual_1.png)

### Diagrama Lógico de Dados(DLD)

![DLD](./images/Lógico_1.png)

### Modelo físico

### Histórico de Commits

|    Data    |   Tipo   |                     Descrição                    |
| :--------- | :------- | :----------------------------------------------- |
| 06/10/2025 | **feat** | Adiciona a descrição das entidades, diagrama de entidade-relacionamento, diagrama lógico de dados |