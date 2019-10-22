What is the difference between CRUD and REST
============================================

-	[Original site](https://www.bmc.com/blogs/rest-vs-crud-whats-the-difference/)

###REST : HTTP request method POST, GET, PUT and DELETE

```
* Principles of REST
  - Client-Server Mandate
      REST is distributed approach via the natrue of separation between client and server.
      Each service has multiple capabilities and listens for requests. Requests are made by a consumer and accepted or rejected by the server.

  - Statelessness
      Due to the nature of statelessness, it is a guiding principle of RESTful architecture.
      Implementing stateless requests means the communication between consumer and service is initiated by the request,
      and the request contains all the information necessasry for the server to respond.

  - Cache
      To avoid re-submitting the same reqeust twice.

  - Interface / Uniform Contract
      RESTfule architecture follows the principles that define a Uniform Contract. This prohibits the use of multiple, self-contained interfaces within an API. Instead, one interface is distributed by bypermedia connections.

  - Layered System
      This principle is the one that makes RESTfule architecture so scalable. In a Layered System, multiple layers are used to grow and expand the interface. None of the layers can see into the other.
```

###CRUE : The standard database commands that are the foundation of CURD. By definition, CRUD is more of a cycle than an architectural system. On any dynamic webstie, there are likely multiple CRUD cycles that exist. CRUD is a smart way for applications to mitigate operational commands between clients and services.

```
CREATE, READ, UPDATE and DELETE

* Principles of CRUD
- Create
    CREATE procedures generate new records via INSERT statements

- Read / Retrieve
    READ procedures reads the data based on input parameters. Similarly, RETRIEVE procedures grab records based on input parameters.

- Update
    UPDATE procedures modify records without overwrting them.

- Delete
    DELETE procedures delete where specified.
```
