# Backend Engineering from First Principles — The Roadmap

*Post 1 of 31 · [Series index](README.md)*

I’m brushing up on backend fundamentals for an entry-level developer interview. I wanted a way to check whether I could explain what happens after someone clicks a button, where a request can fail, and how I’d figure out what went wrong.

Imagine buying the last copy of a book online. You click **Place order** at almost exactly the same time as another customer. Both requests reach the store, both customers have valid accounts, and there’s only one copy left.

Which order goes through? What does the other customer see? If the winning customer’s confirmation email fails to send, should their order fail too?

A small checkout button hides a surprising number of engineering decisions. This series follows those decisions, from the moment a request leaves the browser to the work of deploying and operating the service that handles it. The series is based on Sriniously’s [roadmap video](https://www.youtube.com/watch?v=0Rwb4Xmlcwc), with a bookstore as our running example.

## Follow one request

A framework can route a request, parse JSON, or open a database connection in a few lines of code. When something breaks, you need to know which of those steps failed. A browser that sends the wrong HTTP method, a server that rejects a malformed body, and a database that times out can all leave a customer staring at the same error screen.

We’ll start with the path from browser to server and back. Then we’ll look at HTTP, routing, and serialization before asking what the server can trust. Authentication establishes who is calling. Authorization determines which records that person may access. Validation checks whether the request contains values the application can use. Middleware, request context, and controllers give each of those responsibilities a place in the application.

## Build an API around rules that hold up

A bookstore can expose an endpoint for placing orders in a few lines. Making it safe to use under real traffic requires more thought. If two requests both read an inventory count of one before either writes, both can appear to succeed. We’ll use that race to explore what a transaction guarantees and which rules the database should enforce.

The same store will give us examples for CRUD, REST design, and business logic. We’ll ask which operations should be exposed, how to return predictable errors, and where to put a purchasing rule so it applies whether the order came from a customer or a staff tool. When we get to caching, we’ll compare the consequences of showing a slightly stale book description with showing stale inventory at checkout.

## Separate checkout from work that can happen later

The bookstore needs to record a successful order before confirming it. Sending the receipt can happen afterward. A background worker can retry an email when the provider is unavailable, but it needs a way to handle the same job more than once without sending duplicate receipts. We’ll use that example to cover transactional email, queues, and scheduling together.

Search presents a different problem. A shopper may type part of a title, misspell a word, or look for books by subject. We’ll explore how a search index supports those queries and what happens when the index temporarily falls behind the catalog.

## Learn to operate the system

Once people use the store, the hardest questions often come from production. A checkout is slow. A new deployment starts while someone is placing an order. A service stops responding after accepting work. We’ll look at error handling, configuration, observability, graceful shutdown, and security through situations like these. Then we’ll use measurements to reason about performance, scaling, concurrency, and parallelism.

The final stretch covers large files, real-time updates, testing, the Twelve-Factor App, OpenAPI, webhooks, and DevOps. Each topic extends the same system. Book covers need storage, order status needs a way to reach customers, integrations need contracts, and deployments need a repeatable way to get tested code into production.

## Where we start

Before we worry about two customers competing for the last copy, let’s follow one person opening a book page. Post 2 traces that request from the browser to the application and database, then back to the screen.

[View all 31 posts in the series index](README.md).
