# Java-Bootcamp--Day-29-Exercise-IntroductionToDatabase-

create database store;

create table countries(
    code int primary key ,
    name varchar(20) unique ,
    continent_name varchar(20) not null
);

create table users(
    id int primary key ,
    full_name varchar(20),
    email varchar(20) unique ,
    gender char(1) check ( gender='f' or gender='m' ),
    data_of_birth varchar(15),
    created_at datetime,
    country_code int ,
    foreign key (country_code) references countries(code)
);

create table orders(
    id int primary key ,
    user_id int,
    status varchar(6) check (status='start' or status='finish'),
    created_at datetime default current_timestamp,
    foreign key (user_id) references users(id)
);

create table products(
    id int primary key ,
    name varchar(10) not null ,
    price int default 0,
    status varchar(10) check ( status='valid' or status='expired' ),
    created_at datetime default current_timestamp
);

create table order_products(
    order_id int,
    product_id int,
    quantity int default 0,
    foreign key (order_id) references orders(id),
    foreign key (product_id) references products(id)
);


#  DML commands

insert into countries values(1,'Saudi Arabia','Asia');

insert into users values(11,'Mohammed','mohammed@gmail.com','m','2001-10-10',current_timestamp , '1');

insert into orders values(123,'11','start',current_timestamp);

insert into products values(456,'book','100','valid',current_timestamp);

insert into order_products values(123,456,2);

update countries set name='KSA' where code=1;

delete from products where id=456;
