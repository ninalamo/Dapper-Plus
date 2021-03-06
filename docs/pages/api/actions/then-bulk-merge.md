---
permalink: then-bulk-merge
---

## Definition

The Dapper Plus ThenBulkMerge method allow to MERGE entities in a database table or a view using a lambda expression.

The lambda expression use the entity or the IEnumerable<TEntity> from the last Bulk[Action] or ThenBulk[Action] chained method. (The action can be an insert, update, delete or merge operation).

## Then Bulk Merge with "One to One" Relation

The Dapper Plus ThenBulkMerge method allow merging a related item with a "One to One" relation.

{% include template-example.html %} 
{% highlight csharp %}

//Merge an order and then the related invoice.
connection.BulkMerge(orderTransaction)
          .ThenBulkMerge(transaction => transaction.order)
          .ThenBulkMerge(order => order.Invoice);

//Merge a list of orders and then the related invoice to every order.
connection.BulkMerge(orderTransaction)
          .ThenBulkMerge(transaction => transaction.orders)
          .ThenBulkMerge(order => order.Invoice);
{% endhighlight %}

## Then Bulk Merge with "One to Many" Relation

The Dapper Plus ThenBulkMerge method allow merging related items with a "One to Many" relation.

{% include template-example.html %} 
{% highlight csharp %}

//Merge an order and then all related items.
connection.BulkMerge(orderTransaction)
          .ThenBulkMerge(transaction => transaction.order)
          .ThenBulkMerge(order => order.Items);

//Merge a list of orders and then all related items to every order.
connection.BulkMerge(orderTransaction)
          .ThenBulkMerge(transaction => transaction.orders);
          .ThenBulkMerge(order => order.Items);
{% endhighlight %}

## Then Bulk Merge Chaining

The Dapper Plus ThenBulkMerge method allow chaining multiple bulk action methods.

{% include template-example.html %} 
{% highlight csharp %}

//Merge an order and then all related items. Merge an invoice and then all related items.
connection.BulkMerge(orderTransaction)
          .ThenBulkMerge(transaction => transaction.order)
          .ThenBulkMerge(order => order.Items)
          .BulkMerge(invoiceTransaction)
          .ThenBulkMerge(transaction => transaction.invoice)
          .ThenBulkMerge(invoice => invoice.Items);

//Merge a list of orders and then all related items to every order. Merge a list of invoices and then all related items to every invoice.
connection.BulkMerge(orderTransaction)
          .ThenBulkMerge(transaction => transaction.orders)
          .ThenBulkMerge(order => order.Items)
          .BulkMerge(invoiceTransaction)
          .ThenBulkMerge(transaction => transaction.invoices)
          .ThenBulkMerge(invoice => invoice.Items);
{% endhighlight %}