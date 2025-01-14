# Projeto Banco de Dados - Grupo 1
## Modelo lógico:
![Modelo Logico](./modelo%20logico.png)
## Criação do banco de dados:
```
create database quiz_campanha;

create table funcionario
(
   id serial primary key,
   nome varchar(255) not null,
   email varchar(100) unique not null,
   departamento varchar(100) default 'TI'
);

create table quiz
(
   id serial primary key,
   tema varchar(100) not null,
   descricao varchar(400) not null,
   prazo date
);

create table pergunta
(
   id serial primary key,
   quiz_id int,
   enunciado varchar(400) not null,
   opcao_a varchar(200) not null,
   opcao_b varchar(200) not null,
   opcao_c varchar(200) not null,
   opcao_d varchar(200) not null,
   resposta_correta char(1) not null,
   foreign key (quiz_id) references quiz(id)
);

create table resposta
(
   id serial primary key,
   funcionario_id int,
   pergunta_id int,
   resposta_funcionario char(1) not null,
   data_resposta date default current_date,
   foreign key (funcionario_id) references funcionario(id),
   foreign key (pergunta_id) references pergunta(id)
);
```
## População de dados:
```
insert into funcionario (nome, email, departamento)
values
('Cesar Guerra', 'cesargpmuller@gmail.com', 'RH'),
('Ícaro Gaspar', 'ikaro460@gmail.com', default),
('Laura Smith', 'laurasmith@example.com', 'Financeiro'),
('Pedro Gonçalves', 'pedrogoncalves@example.com', 'Marketing'),
('Mariana Silva', 'marianasilva@example.com', 'Vendas'),
('Lucas Rodrigues', 'lucasrodrigues@example.com', 'RH'),
('Gabriela Pereira', 'gabrielapereira@example.com', default),
('Rafael Costa', 'rafaelcosta@example.com', 'Financeiro'),
('Ana Carvalho', 'anacarvalho@example.com', 'Marketing'),
('Diego Santos', 'diegosantos@example.com', 'Vendas'),
('Camila Silva', 'camilasilva@example.com', default),
('Bruno Oliveira', 'brunooliveira@example.com', 'RH'),
('Carolina Gonçalves', 'carolinagoncalves@example.com', 'Financeiro'),
('João Pereira', 'joaopereira@example.com', 'Marketing'),
('Amanda Silva', 'amandasilva@example.com', 'Vendas');

insert into quiz (tema, descricao, prazo)
values 
('Matemática - Álgebra Linear', 'Teste de conhecimentos básicos sobre álgebra linear', '2024-04-05'),
('História - Revolução Francesa', 'Quiz sobre os eventos e figuras importantes da Revolução Francesa', '2024-04-07'),
('Literatura - Romantismo Brasileiro', 'Perguntas sobre obras e autores do período romântico brasileiro', '2024-04-10'),
('Ciências - Química Orgânica', 'Teste de conceitos fundamentais em química orgânica', '2024-04-12'),
('Geografia - Capitais do Mundo', 'Quiz para testar o conhecimento das capitais de países ao redor do mundo', '2024-04-15');

insert into pergunta (quiz_id, enunciado, opcao_a, opcao_b, opcao_c, opcao_d, resposta_correta) 
values
(1, 'Qual é a definição de matriz identidade?', 'Uma matriz com todos os elementos iguais a zero.', 'Uma matriz com todos os elementos iguais a um.', 'Uma matriz quadrada com uns na diagonal principal e zeros em todos os outros elementos.', 'Uma matriz quadrada com zeros na diagonal principal e uns em todos os outros elementos.', 'c'),
(1, 'Qual é a função da determinante de uma matriz?', 'Indicar o número de linhas e colunas da matriz.', 'Indicar se a matriz é simétrica ou não.', 'Indicar se a matriz é inversível ou não.', 'Calcular a área de um vetor.', 'c'),
(1, 'Qual é a operação básica de multiplicação entre matrizes?', 'Multiplicação ponto a ponto.', 'Adição elemento a elemento.', 'Multiplicação de cada elemento pelo inverso.', 'Multiplicação de linhas por colunas e soma dos produtos.', 'd'),
(1, 'Qual é o resultado da multiplicação de uma matriz por sua inversa?', 'A matriz identidade.', 'A matriz nula.', 'Uma matriz triangular superior.', 'Uma matriz triangular inferior.', 'a'),
(1, 'O que é um espaço vetorial?', 'Um espaço com apenas uma dimensão.', 'Um espaço onde todos os vetores são paralelos entre si.', 'Um espaço onde se pode realizar operações de adição e multiplicação por um escalar.', 'Um espaço onde todos os vetores têm o mesmo módulo.', 'c'),
(2, 'Quem foi o rei da França durante a Revolução Francesa?', 'Luís XIV', 'Luís XVI', 'Napoleão Bonaparte', 'Carlos II', 'b'),
(2, 'Qual foi o principal evento que marcou o início da Revolução Francesa?', 'A Tomada da Bastilha', 'A Noite das Longas Facas', 'A Queda do Muro de Berlim', 'O Golpe de Estado de Napoleão', 'a'),
(2, 'Quem liderou o governo revolucionário conhecido como Comitê de Salvação Pública?', 'Maximilien Robespierre', 'Napoleão Bonaparte', 'Joana d''Arc', 'Miguel Hidalgo', 'a'),
(2, 'Qual foi o nome do sistema de governo adotado durante o período do Terror?', 'Monarquia Absolutista', 'República Parlamentarista', 'Ditadura Militar', 'Ditadura do Proletariado', 'a'),
(2, 'O que foi o período conhecido como "Reinado do Terror"?', 'Um período de estabilidade política após a Revolução Francesa.', 'Um período de perseguição política e execuções em massa durante a Revolução Francesa.', 'Um período de governo autoritário liderado por Napoleão Bonaparte.', 'Um período de transição entre a monarquia e a república na França.', 'b'),
(3, 'Quem foi o autor do livro "Iracema"?', 'Machado de Assis', 'José de Alencar', 'Cecília Meireles', 'Guimarães Rosa', 'b'),
(3, 'Qual obra abaixo não é um romance de José de Alencar?', '"Senhora"', '"Dom Casmurro"', '"Lucíola"', '"O Guarani"', 'b'),
(3, 'Qual é o nome do personagem principal do livro "O Guarani"?', 'Peri', 'Capitu', 'Machado de Assis', 'Iracema', 'a'),
(3, 'Qual é a principal característica da prosa romântica brasileira?', 'Racionalismo e objetividade.', 'Predominância de elementos realistas e naturalistas.', 'Ênfase nas emoções e subjetividade.', 'Crítica social e política.', 'c'),
(3, 'Qual obra abaixo é considerada um marco do romance indianista?', '"Dom Casmurro"', '"O Guarani"', '"Memórias Póstumas de Brás Cubas"', '"O Cortiço"', 'b'),
(4, 'Qual é a fórmula molecular do etanol?', 'CH4', 'C2H6', 'C6H12O6', 'C2H5OH', 'd'),
(4, 'O que é um composto orgânico?', 'Um composto que contém carbono.', 'Um composto que não contém carbono.', 'Um composto que contém oxigênio.', 'Um composto que contém hidrogênio.', 'a'),
(4, 'Qual é a função principal dos alcanos na química orgânica?', 'Acidez', 'Alcalinidade', 'Elasticidade', 'Saturação', 'd'),
(4, 'O que é um isômero na química orgânica?', 'Um composto que contém apenas carbono e hidrogênio.', 'Um composto que possui a mesma fórmula molecular, mas estruturas diferentes.', 'Um composto que não pode ser quebrado por processos químicos.', 'Um composto que não possui ligações químicas.', 'b'),
(4, 'Qual é a função principal dos alcenos na química orgânica?', 'Ligações duplas', 'Ligações triplas', 'Ligações simples', 'Ligações quádruplas', 'a'),
(5, 'Qual é a capital do Brasil?', 'Buenos Aires', 'Rio de Janeiro', 'São Paulo', 'Brasília', 'd'),
(5, 'Qual é a capital da Argentina?', 'Santiago', 'Buenos Aires', 'Lima', 'Montevidéu', 'b'),
(5, 'Qual é a capital da França?', 'Londres', 'Madri', 'Paris', 'Berlim', 'c'),
(5, 'Qual é a capital do Japão?', 'Seul', 'Pequim', 'Tóquio', 'Bangcoc', 'c'),
(5, 'Qual é a capital da Rússia?', 'Moscovo', 'São Petersburgo', 'Kiev', 'Varsóvia', 'a');

insert into resposta (funcionario_id, pergunta_id, resposta_funcionario, data_resposta)
values 
(1, 1, 'b', default),
(1, 2, 'd', default),
(1, 3, 'a', default),
(1, 4, 'c', default),
(1, 5, 'a', default),
(2, 1, 'a', default),
(2, 2, 'b', default),
(2, 3, 'c', default),
(2, 4, 'd', default),
(2, 5, 'a', default),
(3, 1, 'c', default),
(3, 2, 'a', default),
(3, 3, 'b', default),
(3, 4, 'd', default),
(3, 5, 'c', default),
(4, 1, 'd', default),
(4, 2, 'c', default),
(4, 3, 'b', default),
(4, 4, 'a', default),
(4, 5, 'd', default),
(5, 1, 'b', default),
(5, 2, 'c', default),
(5, 3, 'a', default),
(5, 4, 'd', default),
(5, 5, 'b', default),
(6, 1, 'c', default),
(6, 2, 'a', default),
(6, 3, 'b', default),
(6, 4, 'd', default),
(6, 5, 'c', default),
(7, 1, 'a', default),
(7, 2, 'b', default),
(7, 3, 'c', default),
(7, 4, 'd', default),
(7, 5, 'a', default),
(8, 1, 'b', default),
(8, 2, 'a', default),
(8, 3, 'c', default),
(8, 4, 'd', default),
(8, 5, 'b', default),
(9, 1, 'a', default),
(9, 2, 'b', default),
(9, 3, 'c', default),
(9, 4, 'd', default),
(9, 5, 'a', default),
(10, 1, 'c', default),
(10, 2, 'a', default),
(10, 3, 'b', default),
(10, 4, 'd', default),
(10, 5, 'c', default),
(11, 1, 'a', default),
(11, 2, 'b', default),
(11, 3, 'c', default),
(11, 4, 'd', default),
(11, 5, 'a', default),
(12, 1, 'a', default),
(12, 2, 'b', default),
(12, 3, 'c', default),
(12, 4, 'd', default),
(12, 5, 'a', default),
(13, 1, 'a', default),
(13, 2, 'b', default),
(13, 3, 'c', default),
(13, 4, 'd', default),
(13, 5, 'a', default),
(14, 1, 'a', default),
(14, 2, 'b', default),
(14, 3, 'c', default),
(14, 4, 'd', default),
(14, 5, 'a', default),
(15, 1, 'a', default),
(15, 2, 'b', default),
(15, 3, 'c', default),
(15, 4, 'd', default),
(15, 5, 'a', default),
(1, 6, 'b', default),
(1, 7, 'c', default),
(1, 8, 'a', default),
(1, 9, 'd', default),
(1, 10, 'b', default),
(2, 6, 'd', default),
(2, 7, 'a', default),
(2, 8, 'c', default),
(2, 9, 'b', default),
(2, 10, 'a', default),
(3, 6, 'a', default),
(3, 7, 'b', default),
(3, 8, 'd', default),
(3, 9, 'c', default),
(3, 10, 'a', default),
(4, 6, 'c', default),
(4, 7, 'a', default),
(4, 8, 'b', default),
(4, 9, 'd', default),
(4, 10, 'c', default),
(5, 6, 'd', default),
(5, 7, 'b', default),
(5, 8, 'a', default),
(5, 9, 'c', default),
(5, 10, 'd', default),
(6, 6, 'b', default),
(6, 7, 'c', default),
(6, 8, 'a', default),
(6, 9, 'd', default),
(6, 10, 'b', default),
(7, 6, 'a', default),
(7, 7, 'c', default),
(7, 8, 'b', default),
(7, 9, 'd', default),
(7, 10, 'a', default),
(8, 6, 'b', default),
(8, 7, 'a', default),
(8, 8, 'c', default),
(8, 9, 'd', default),
(8, 10, 'b', default),
(9, 6, 'a', default),
(9, 7, 'b', default),
(9, 8, 'c', default),
(9, 9, 'd', default),
(9, 10, 'a', default),
(10, 6, 'c', default),
(10, 7, 'a', default),
(10, 8, 'b', default),
(10, 9, 'd', default),
(10, 10, 'c', default),
(11, 6, 'a', default),
(11, 7, 'b', default),
(11, 8, 'c', default),
(11, 9, 'd', default),
(11, 10, 'a', default),
(12, 6, 'a', default),
(12, 7, 'b', default),
(12, 8, 'c', default),
(12, 9, 'd', default),
(12, 10, 'a', default),
(13, 6, 'a', default),
(13, 7, 'b', default),
(13, 8, 'c', default),
(13, 9, 'd', default),
(13, 10, 'a', default),
(14, 6, 'a', default),
(14, 7, 'b', default),
(14, 8, 'c', default),
(14, 9, 'd', default),
(14, 10, 'a', default),
(15, 6, 'a', default),
(15, 7, 'b', default),
(15, 8, 'c', default),
(15, 9, 'd', default),
(15, 10, 'a', default),
(1, 11, 'a', default),
(1, 12, 'b', default),
(1, 13, 'c', default),
(1, 14, 'd', default),
(1, 15, 'a', default),
(2, 11, 'b', default),
(2, 12, 'c', default),
(2, 13, 'd', default),
(2, 14, 'a', default),
(2, 15, 'b', default),
(3, 11, 'c', default),
(3, 12, 'd', default),
(3, 13, 'a', default),
(3, 14, 'b', default),
(3, 15, 'c', default),
(4, 11, 'd', default),
(4, 12, 'a', default),
(4, 13, 'b', default),
(4, 14, 'c', default),
(4, 15, 'd', default),
(5, 11, 'a', default),
(5, 12, 'b', default),
(5, 13, 'c', default),
(5, 14, 'd', default),
(5, 15, 'a', default),
(6, 11, 'b', default),
(6, 12, 'c', default),
(6, 13, 'd', default),
(6, 14, 'a', default),
(6, 15, 'b', default),
(7, 11, 'c', default),
(7, 12, 'd', default),
(7, 13, 'a', default),
(7, 14, 'b', default),
(7, 15, 'c', default),
(8, 11, 'd', default),
(8, 12, 'a', default),
(8, 13, 'b', default),
(8, 14, 'c', default),
(8, 15, 'd', default),
(9, 11, 'a', default),
(9, 12, 'b', default),
(9, 13, 'c', default),
(9, 14, 'd', default),
(9, 15, 'a', default),
(10, 11, 'b', default),
(10, 12, 'c', default),
(10, 13, 'd', default),
(10, 14, 'a', default),
(10, 15, 'b', default),
(11, 11, 'c', default),
(11, 12, 'd', default),
(11, 13, 'a', default),
(11, 14, 'b', default),
(11, 15, 'c', default),
(12, 11, 'd', default),
(12, 12, 'a', default),
(12, 13, 'b', default),
(12, 14, 'c', default),
(12, 15, 'd', default),
(13, 11, 'a', default),
(13, 12, 'b', default),
(13, 13, 'c', default),
(13, 14, 'd', default),
(13, 15, 'a', default),
(14, 11, 'b', default),
(14, 12, 'c', default),
(14, 13, 'd', default),
(14, 14, 'a', default),
(14, 15, 'b', default),
(15, 11, 'c', default),
(15, 12, 'd', default),
(15, 13, 'a', default),
(15, 14, 'b', default),
(15, 15, 'c', default),
(1, 16, 'a', default),
(1, 17, 'b', default),
(1, 18, 'c', default),
(1, 19, 'd', default),
(1, 20, 'a', default),
(2, 16, 'b', default),
(2, 17, 'c', default),
(2, 18, 'd', default),
(2, 19, 'a', default),
(2, 20, 'b', default),
(3, 16, 'c', default),
(3, 17, 'd', default),
(3, 18, 'a', default),
(3, 19, 'b', default),
(3, 20, 'c', default),
(4, 16, 'd', default),
(4, 17, 'a', default),
(4, 18, 'b', default),
(4, 19, 'c', default),
(4, 20, 'd', default),
(5, 16, 'a', default),
(5, 17, 'b', default),
(5, 18, 'c', default),
(5, 19, 'd', default),
(5, 20, 'a', default),
(6, 16, 'b', default),
(6, 17, 'c', default),
(6, 18, 'd', default),
(6, 19, 'a', default),
(6, 20, 'b', default),
(7, 16, 'c', default),
(7, 17, 'd', default),
(7, 18, 'a', default),
(7, 19, 'b', default),
(7, 20, 'c', default),
(8, 16, 'd', default),
(8, 17, 'a', default),
(8, 18, 'b', default),
(8, 19, 'c', default),
(8, 20, 'd', default),
(9, 16, 'a', default),
(9, 17, 'b', default),
(9, 18, 'c', default),
(9, 19, 'd', default),
(9, 20, 'a', default),
(10, 16, 'b', default),
(10, 17, 'c', default),
(10, 18, 'd', default),
(10, 19, 'a', default),
(10, 20, 'b', default),
(11, 16, 'c', default),
(11, 17, 'd', default),
(11, 18, 'a', default),
(11, 19, 'b', default),
(11, 20, 'c', default),
(12, 16, 'd', default),
(12, 17, 'a', default),
(12, 18, 'b', default),
(12, 19, 'c', default),
(12, 20, 'd', default),
(13, 16, 'a', default),
(13, 17, 'b', default),
(13, 18, 'c', default),
(13, 19, 'd', default),
(13, 20, 'a', default),
(14, 16, 'b', default),
(14, 17, 'c', default),
(14, 18, 'd', default),
(14, 19, 'a', default),
(14, 20, 'b', default),
(15, 16, 'c', default),
(15, 17, 'd', default),
(15, 18, 'a', default),
(15, 19, 'b', default),
(15, 20, 'c', default),
(1, 21, 'a', default),
(1, 22, 'b', default),
(1, 23, 'c', default),
(1, 24, 'd', default),
(1, 25, 'a', default),
(2, 21, 'b', default),
(2, 22, 'c', default),
(2, 23, 'd', default),
(2, 24, 'a', default),
(2, 25, 'b', default),
(3, 21, 'c', default),
(3, 22, 'd', default),
(3, 23, 'a', default),
(3, 24, 'b', default),
(3, 25, 'c', default),
(4, 21, 'd', default),
(4, 22, 'a', default),
(4, 23, 'b', default),
(4, 24, 'c', default),
(4, 25, 'd', default),
(5, 21, 'a', default),
(5, 22, 'b', default),
(5, 23, 'c', default),
(5, 24, 'd', default),
(5, 25, 'a', default),
(6, 21, 'b', default),
(6, 22, 'c', default),
(6, 23, 'd', default),
(6, 24, 'a', default),
(6, 25, 'b', default),
(7, 21, 'c', default),
(7, 22, 'd', default),
(7, 23, 'a', default),
(7, 24, 'b', default),
(7, 25, 'c', default),
(8, 21, 'd', default),
(8, 22, 'a', default),
(8, 23, 'b', default),
(8, 24, 'c', default),
(8, 25, 'd', default),
(9, 21, 'a', default),
(9, 22, 'b', default),
(9, 23, 'c', default),
(9, 24, 'd', default),
(9, 25, 'a', default),
(10, 21, 'b', default),
(10, 22, 'c', default),
(10, 23, 'd', default),
(10, 24, 'a', default),
(10, 25, 'b', default),
(11, 21, 'c', default),
(11, 22, 'd', default),
(11, 23, 'a', default),
(11, 24, 'b', default),
(11, 25, 'c', default),
(12, 21, 'd', default),
(12, 22, 'a', default),
(12, 23, 'b', default),
(12, 24, 'c', default),
(12, 25, 'd', default),
(13, 21, 'a', default),
(13, 22, 'b', default),
(13, 23, 'c', default),
(13, 24, 'd', default),
(13, 25, 'a', default),
(14, 21, 'b', default),
(14, 22, 'c', default),
(14, 23, 'd', default),
(14, 24, 'a', default),
(14, 25, 'b', default),
(15, 21, 'c', default),
(15, 22, 'd', default),
(15, 23, 'a', default),
(15, 24, 'b', default),
(15, 25, 'c', default);
```
## Consulta SQL:
### Inserção:
```
insert into funcionario (nome, email, departamento) values ('João Silva', 'joao.silva@example.com', 'RH');

insert into quiz (tema, descricao, prazo) values ('Matemática Básica', 'Quiz sobre conceitos fundamentais de matemática', '2024-12-31');

insert into pergunta (quiz_id, enunciado, opcao_a, opcao_b, opcao_c, opcao_d, resposta_correta) 
values (1, 'Qual é o resultado de 2 + 2?', '3', '4', '5', '6', 'b');

insert into resposta (funcionario_id, pergunta_id, resposta_funcionario, data_resposta) 
values (1, 1, 'b', '2024-03-25');

insert into funcionario (nome, email, departamento) values ('Adriano Imperador', 'adrianojogamuito@example.com', default);
```
### Atualização:
```
update funcionario set nome = 'Clarisse Falcão' where id = 3;

update quiz set prazo = '2024-12-15' where id = 1;

update resposta set resposta_funcionario = 'c' where id = 1;
```
### Exclusão:
```
delete from funcionario where id = 17;

delete from resposta where id = 376;

delete from pergunta where id = 26;

delete from quiz where id = 6;
```
### Consulta de dados:
```
select * from funcionario;

select * from quiz;

select * from pergunta;

select * from resposta;
```
## Consultar os funcionários que participaram de uma determinada campanha de quiz e sua pontuação:
```
select 
f.id as funcionario_id,
f.nome as nome_funcionario,
q.id as quiz_id,
q.tema as tema_quiz,
sum(case when r.resposta_funcionario = p.resposta_correta then 1 else 0 end) as pontuacao_total
from 
funcionario f
inner join 
resposta r on f.id = r.funcionario_id
inner join 
pergunta p on r.pergunta_id = p.id
inner join 
quiz q on p.quiz_id = q.id
group by 
f.id, q.id
order by 
funcionario_id;
```
## Consultar os funcionários que obtiveram a maior pontuação:
```
select 
f.nome as nome_funcionario,
sum(case when r.resposta_funcionario = p.resposta_correta then 1 else 0 end) as pontuacao_total
from 
funcionario f
inner join 
resposta r on f.id = r.funcionario_id
inner join 
pergunta p on r.pergunta_id = p.id
group by 
f.id
order by 
pontuacao_total desc
limit 3;
```
