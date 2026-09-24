## João Vitor Alcântara Corrêa

Desenvolvedor backend — Java e Spring Boot.
Formado em Sistemas de Informação em dezembro de 2025, aberto a oportunidades.

### Projetos

| Projeto | O problema difícil |
|---|---|
| [**encurtador-links**](https://github.com/alcantarajv/encurtador-links) · [no ar](https://encurtador-links-rudi.onrender.com) | **Latência** no caminho quente: cache guardando uma projeção em vez da entidade, e o clique gravado fora da thread da requisição |
| [**reserva-quadras**](https://github.com/alcantarajv/reserva-quadras) · [no ar](https://reserva-quadras.onrender.com) | **Concorrência**: duas pessoas reservam o mesmo horário no mesmo instante — a garantia ficou numa constraint de exclusão do PostgreSQL |
| [**api-pedidos**](https://github.com/alcantarajv/api-pedidos) · [no ar](https://api-pedidos-yi5d.onrender.com) | **Consistência entre sistemas**: o webhook do gateway chega duas vezes, e gravar no banco e publicar na fila não cabe numa transação só |

Cada README explica a decisão tomada **e a alternativa que foi descartada**.

### Se você tem dois minutos

Quatro arquivos que mostram melhor do que qualquer descrição:

- [**`ReservaConcorrenteIT`**](https://github.com/alcantarajv/reserva-quadras/blob/main/src/test/java/com/joaoalcantara/reservas/reserva/ReservaConcorrenteIT.java) — *"com N threads no mesmo horário, exatamente uma reserva é criada"*, e também *"horários que não colidem são criados em paralelo, sem serializar a quadra"*. O segundo teste existe porque a solução fácil passa no primeiro e falha no segundo.
- [**`V4__impede_sobreposicao_de_reservas.sql`**](https://github.com/alcantarajv/reserva-quadras/blob/main/src/main/resources/db/migration/V4__impede_sobreposicao_de_reservas.sql) — a constraint de exclusão que dá essa garantia. São seis linhas de SQL no lugar onde não existe janela de corrida.
- [**`PedidoConcorrenteIT`**](https://github.com/alcantarajv/api-pedidos/blob/main/src/test/java/com/joaoalcantara/pedidos/pedido/PedidoConcorrenteIT.java) — *"mesma chave de idempotência em N requisições simultâneas cria um único pedido"* e *"N clientes disputando a última unidade: exatamente um leva"*.
- [**`ClickRecorder`**](https://github.com/alcantarajv/encurtador-links/blob/main/src/main/java/com/joaoalcantara/encurtador/service/ClickRecorder.java) — a gravação do clique fora da thread da requisição, com os dados copiados antes de atravessar a fronteira: o Tomcat reaproveita o `HttpServletRequest` assim que a resposta sai.

### Stack

Java 21 · Spring Boot 4 · Spring Security · PostgreSQL · Redis · RabbitMQ · Flyway · Testcontainers · Docker · GitHub Actions

### Contato

[LinkedIn](https://linkedin.com/in/joaovalcantara)
