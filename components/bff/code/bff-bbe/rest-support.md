---
title: 'Simplify backend development with native REST features'
description: Ballerina provides REST features like path/query parameters, HTTP headers, status codes, and complex JSON structures as first-class citizens within the language itself.
url: 'https://github.com/SasinduDilshara/BFF-Samples/tree/dev/ballerina_rest'
---
```
service /sales on new http:Listener(9090) {
    resource function get orders() returns Order[] {
        return orderTable.toArray();
    };

    resource function get orders/[string id]() returns Order|http:NotFound {
        if orderTable.hasKey(id) {
            return orderTable.get(id);
        }
        return {
            body: string `Order not found. ID: ${id};`
        };
    };

    resource function post orders(Order 'order) returns Order {
        orderTable.add('order);
        return 'order;
    };
}
```