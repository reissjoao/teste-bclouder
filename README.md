# Teste SQL e Raciocínio - VAGA ESTÁGIO BCLOUDER JOÃO REIS

## TESTE SQL
1. Gere uma lista contendo nome e sobrenome dos vendedores da cidade de Curitiba

```sql
SELECT nome, sobrenome FROM vendedores WHERE cidade = 'Curitiba';
```

1. Gere uma lista com a quantidade de vendedores em cada cidade

```sql
SELECT cidade, COUNT(*) AS quantidade_de_vendedores FROM vendedores GROUP BY cidade;
```

1. Gere uma lista com todos os vendedores que tiveram vendas após o 31/12/2023

```sql
SELECT DISTINCT v.nome, v.sobrenome
FROM VENDEDORES v
INNER JOIN VENDAS vd ON vd.vendedor_id = v.id
WHERE vd.data > '2023-12-31'
AND vd.cancelada = 'NÃO';
```

4. Acrescente na lista gerada no ponto 1 a quantidade de notas fiscais de venda e devolução que tiveram no mês de janeiro de 2024

```sql
SELECT v.nome, v.sobrenome, v.cidade,
  COUNT(DISTINCT vd.nfVenda) AS quantidade_vendas,
  COUNT(DISTINCT vd2.nfDevolucao) AS quantidade_devolucoes,
  SUM(vd.valor) - SUM(COALESCE(vd2.valor, 0)) AS resultado_total
FROM VENDEDORES v
LEFT JOIN VENDAS vd ON vd.vendedor_id = v.id AND vd.data BETWEEN '2024-01-01' AND '2024-01-31'
LEFT JOIN DEVOLUCOES vd2 ON vd2.vendedor_id = v.id AND vd2.nfDevolucao = vd.nfVenda
GROUP BY v.id, v.nome, v.sobrenome, v.cidade
ORDER BY v.nome;
```

1. Gere uma lista com todos os vendedores da empresa e seu resultado total (vendas - devoluções) e ordene eles do maior para o menor resultado

```sql
SELECT v.nome, v.sobrenome,
  SUM(vd.valor) - SUM(COALESCE(vd2.valor, 0)) AS resultado_total
FROM VENDEDORES v
LEFT JOIN VENDAS vd ON vd.vendedor_id = v.id
LEFT JOIN DEVOLUCOES vd2 ON vd2.vendedor_id = v.id AND vd2.nfDevolucao = vd.nfVenda
GROUP BY v.id, v.nome, v.sobrenome
ORDER BY resultado_total DESC;
```

1. Considerando as informações apresentadas nas três tabelas, considera que existem falhas de integridade nos dados?
- Na tabela `VENDAS`, a venda de ID 5 está marcada como cancelada ("S"), mas não há registro de devolução na tabela `DEVOLUCOES`.
- Na tabela `DEVOLUCOES`, a devolução de ID 8 possui "vendedor" como valor nulo, o que pode indicar inconsistência na referência à tabela `VENDEDORES`.

## TESTE RACIOCÍNIO NUMÉRICO-LÓGICO

1. D) 113
2. D) 285
3. A) 2 metros a Leste.
4. B) 7
