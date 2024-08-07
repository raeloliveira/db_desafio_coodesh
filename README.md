# DBA Challenge 20240802 - Israel Pereira Oliveira


## Introdução

Nesse desafio trabalharemos utilizando a base de dados da empresa Bike Stores Inc com o objetivo de obter métricas relevantes para equipe de Marketing e Comercial.

Com isso, teremos que trabalhar com várioas consultas utilizando conceitos como `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `GROUP BY` e `COUNT`.

### Antes de começar
 
- O projeto deve utilizar a Linguagem específica na avaliação. Por exempo: SQL, T-SQL, PL/SQL e PSQL;
- Considere como deadline da avaliação a partir do início do teste. Caso tenha sido convidado a realizar o teste e não seja possível concluir dentro deste período, avise a pessoa que o convidou para receber instruções sobre o que fazer.
- Documentar todo o processo de investigação para o desenvolvimento da atividade (README.md no seu repositório); os resultados destas tarefas são tão importantes do que o seu processo de pensamento e decisões à medida que as completa, por isso tente documentar e apresentar os seus hipóteses e decisões na medida do possível.
 
 

## O projeto
 
- Criar as consultas utilizando a linguagem escolhida 
- Entregar o código gerado do Teste

### Modelo de Dados:

Para entender o modelo, revisar o diagrama a seguir:

![<img src="samples/model.png" height="500" alt="Modelo" title="Modelo"/>](samples/model.png)


## Selects

Construir as seguintes consultas:

- Listar todos Clientes que não tenham realizado uma compra;

/*todo registro de compra possui a chave do cliente que a realizou , sendo assim seleciono todos os clientes que não se encontram na tabela de compras ( pelo campo customer_id). */

select a.first_name||' '||a.last_name as customer_name from customers a where not exists (select 1 from 
orders b on b.customer_id = a.customer_id);
  
- Listar os Produtos que não tenham sido comprados

/*todo registro de compra possui um item de compra(order_items) sendo assim utilizei a mesma logica da consulta acima apenas consultando produtos que não existiam na tabela ordem_items.*/

select a.product_name from products a where not exists (select 1 from 
order_items b on b.product_id = a.product_id);
  
- Listar os Produtos sem Estoque;

/*selecionei apenas os produtos onde na tabela de estoque continham o campo quantidade = 0 (sem estoque).*/

select b.product_name from stocks a left join products b 
on a.product_id = b.product_id where a.quantity = 0;  
  
- Agrupar a quantidade de vendas que uma determinada Marca por Loja.

/*interpretei a partir da pergunta que gostariamos de ver a quantidade de vendas de uma determinada marca , sendo assim realcionei a marca através de todas as tabelas até a tabela de vendas , agrupei o volume pelo nome de cada loja que fez a venda de uma determinada marca ( nome da marca nesse caso será imputado pelo usuario).*/

  select b.store_name,count(a.*) as qtd_sales
  from orders a
  left join stores b on a.store_id = b.store_id
  left join stocks c on b.store_id = c.store_id
  left join products d on c.product_id = d.product_id
  left join brands e on d.brand_id = e.brand_id
  where e.brand_name = 'BRAND_NAME';
  
- Listar os Funcionarios que não estejam relacionados a um Pedido.

select a.* from staffs a where not exists (select 1 from 
orders b on b.staff_id = a.staff_id);

## Readme do Repositório

- Deve conter o título do projeto
- Uma descrição sobre o projeto em frase
- Deve conter uma lista com linguagem, framework e/ou tecnologias usadas
- Como instalar e usar o projeto (instruções)
- Não esqueça o [.gitignore](https://www.toptal.com/developers/gitignore)
- Se está usando github pessoal, referencie que é um challenge by coodesh:  

>  This is a challenge by [Coodesh](https://coodesh.com/)

## Finalização e Instruções para a Apresentação

1. Adicione o link do repositório com a sua solução no teste
2. Adicione o link da apresentação do seu projeto no README.md.
3. Verifique se o Readme está bom e faça o commit final em seu repositório;
4. Envie e aguarde as instruções para seguir. Sucesso e boa sorte. =)
