# Primeiro-projeto-logico-de-banco-de-dados
 Projeto da Dio de database criada no MySQL
-- Criação de Bancos de Dados poara o cénarioi de E-Commerce
create database ecommerce;
use ecommerce;

-- Criar Tabela Cliente

create table client(

          idclient int auto_increment primary key,
          Fname varchar(10),
          Minit char(3),
          Lname varchar(20),
          CPF char(11) not null,
          address varchar(10),
          constraint unique_cpf_client unique (CPF)
          
);

-- Criar tabela produto

create table product(

          idproduct int auto_increment primary key,
          Pname varchar(10) not null,
          Classification_kids bool default false,
          category enum("Eletronico", "Vestimenta", "Bringuedos", "Aliomentos", "Moveis") not null,
          avaliação float default 0,
          size varchar(10),
          constraint unique_cpf_client unique (CPF)
);

-- Criar tabela pedido

create table orders(

		  idorder int auto_increment primary key,
          idOrderClient int,
          OrderStatus enum("Cancelado","Confirmado","Em Processamento") default ("Processamento"),
          orderDescription varchar(255),
          sendValue float default 10,
          paymentCash bool default false,
          constraint fk_orders_client foreign key (idOrderClient) references clients(idClient)
            on update cascade
            
);
desc orders;
-- Criar Tabela Estoque

create table productStorage(

          iProdutStorage int auto_increment primary key,
          storageLocation varchar(255),
          quantity int default 0
);
-- Criar Tabela Fornecedor

create table supplier(

		  idSupplier int auto_increment primary key,
          Socialname varchar(255) not null,
		  CNPJ char(15) not null,
          contact char(11) default 0,
		  constraint unique_supplier unique(CPF),
          constraint unique_supplier unique(CNPJ)
);

-- Criar Tabela Vendedor

create table seller(

		  idSeller int auto_increment primary key,
          SocialName varchar(255) not null,
          abstName varchar(255),
          CNPJ char(15),
          CPF char(9),
          location varchar (255),
          contact char(11) not null,
          constraint unique_supplier unique(CPF),
          constraint unique_supplier unique(CNPJ)
);

create table productseller(

          idPseller int,
          idProduct int,
          Quantity int default 1,
          primary key(idPseller, idProduct),
          constraint fk_product_seller foreign key (idSeller) references seller(idseller),
          constraint fk_product_seller foreign key (idProduct) references product(idProduct)
);

create table productOrder(

          idPOproduct int,
		  idPOorder int,
		  poQuantity int default 1,
          poStatus enum("Disponivel","Sem Estoque") default "Disponivel",
          primary key (idPOproduct, idPOorder),
          constraint fk_productorder_seller foreign key (idPOprocuct) references product(idPOproduct),
          constraint fk_productorder_seller foreign key (idPOorder) references Poorder(idPOorder)
);

create table storagelocation(
		  idLproduct int,
          idLstorage int,
          location varchar(255) not null,
          primary key (idLproduct, idLstorage),
          constraint fk_storage_seller foreign key (idLproduct) references product(idproduct),
          constraint fk_storage_seller foreign key (idLstorag) references productstorage(productStorage)
);

create table productSupplier(

          idPsSupplier int,
          idPsproduct int,
          quntity int not null,
          primary key (idPsSupplier, idPsproduct),
          constraint fk_productSupplier_seller foreign key (idPsSupplier) references supplier(idproduct),
          constraint fk_productSupplier_seller foreign key (idPsproduct) references product(productStorage)
);

desc productSupplier;

show tables;

show databases;
use information_schema;
show tables;
desc referential_constraints;
select*from referential_constraints where constraint_schema
