---
permalink: then-bulk-insert
---

## Definition

The Dapper Plus ThenBulkInsert method allow to INSERT entities in a database table or a view using a lambda expression.

The lambda expression use the entity or the IEnumerable<TEntity> from the last Bulk[Action] or ThenBulk[Action] chained method. (The action can be an insert, update, delete or merge operation).

## Then Bulk Insert with "One to One" Relation

The Dapper Plus ThenBulkInsert method allow inserting a related item with a "One to One" relation.

{% include template-example.html %} 
{% highlight csharp %}

//Insert an order and then the related invoice.
connection.BulkInsert(orderTransaction)
          .ThenBulkInsert(transaction => transaction.order)
          .ThenBulkInsert(order => order.Invoice);

//Insert a list of orders and then the related invoice to every order.
connection.BulkInsert(orderTransaction)
          .ThenBulkInsert(transaction => transaction.orders)
          .ThenBulkInsert(order => order.Invoice);
{% endhighlight %}

## Then Bulk Insert with "One to Many" Relation

The Dapper Plus ThenBulkInsert method allow inserting related items with a "One to Many" relation.

{% include template-example.html %} 
{% highlight csharp %}

//Insert an order and then all related items.
connection.BulkInsert(orderTransaction)
          .ThenBulkInsert(transaction => transaction.order)
          .ThenBulkInsert(order => order.Items);

//Insert a list of orders and then all related items to every order.
connection.BulkInsert(orderTransaction)
          .ThenBulkInsert(transaction => transaction.orders);
          .ThenBulkInsert(order => order.Items);
{% endhighlight %}

## Then Bulk Insert Chaining

The Dapper Plus ThenBulkInsert method allow chaining multiple bulk action methods.

{% include template-example.html %} 
{% highlight csharp %}

//Insert an order and then all related items. Insert an invoice and then all related items.
connection.BulkInsert(orderTransaction)
          .ThenBulkInsert(transaction => transaction.order)
          .ThenBulkInsert(order => order.Items)
          .BulkInsert(invoiceTransaction)
          .ThenBulkInsert(transaction => transaction.invoice)
          .ThenBulkInsert(invoice => invoice.Items);

//Insert a list of orders and then all related items to every order. Insert a list of invoices 
//and then all related items to every invoice.
connection.BulkInsert(orderTransaction)
          .ThenBulkInsert(transaction => transaction.orders)
          .ThenBulkInsert(order => order.Items)
          .BulkInsert(invoiceTransaction)
          .ThenBulkInsert(transaction => transaction.invoices)
          .ThenBulkInsert(invoice => invoice.Items);

{% endhighlight %}
