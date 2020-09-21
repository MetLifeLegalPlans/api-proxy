# api-proxy

## What this is

An easily deployable and configural Caddy container definition, designed to proxy requests from `/api` routes to an arbitrarily located backend.

## Why we need this

If we were deploying all of our services on ECS, we wouldn't - a standard application load balancer would be able to handle this easily.

Since our backend runs serverlessly however, we can't do that - there is no way to register an API gateway or Lambda function as a target group with the way that Zappa configures them.

## How this is deployed

In ECS, each frontend task definition consists of two containers: this one, and the actual frontend production server. The frontend isn't just a static bundle, it has server side rendering and all the other niceties of NextJS - so it needs a server to run on.

This container proxies all API requests to the backend URL, which is specified in the task definition environment variables. If it's not an API request, it's routed to the frontend container that's running on the same host.
