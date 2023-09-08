# Backend Developer Exercise

## Introduction

- your task is to implement a simple single-user blogging engine in Node.js
- you don't have to complete all subtasks, just do what you have the time and skills for
- the goal here is not just to see if you can do an app, but how you do it. So please write it as if it were a big production app, that includes code structure, validations, usage of git, documentation, tests, linting, etc.
- we realize that some subtasks can be very time consuming, if you just don't have the time, you can write short text description of how would you solve the problem
- on the flip side, you can improve on many things, if you have the time. For example, we don't need you to implement user registration, but you are free to do so
- feel free to use this exercise (including the instruction) for evaluation by other companies

## Technology suggestions

### Common

- we use Docker for containerization, Swagger/OpenAPI for API documentation (or in case of GraphQL - Playground or Apollo Sandbox)

### Node.js

- we prefer NestJS, Apollo, PostgreSQL, TypeORM or Prisma, Jest and of course TypeScript
- but if you know other technologies and don't want to learn/use any of our favorites, feel free to do so

## The Exercise

- design the API yourself and document it
  - ideally, create both REST and GraphQL (GraphQL is preferred)
  - document the API - REST in Swagger, GraphQL with documentation comments in schema
  - for GraphQL, expose Apollo Sandbox or GraphQL Playground
- dockerize your app
  - create a Dockerfile for your app
  - create a docker-compose file that can be used to run your app with all dependencies
- implement login
  - the user should just need a password to login
  - seed the database with user data
- create simple CRUD for blog posts (articles)
  - each article should have title, perex, content, author and timestamp at minimum
- add the possibility to add comments to articles
  - think of what the comment needs as fields
- add the possibility to vote on comments (Reddit-style + and -)
  - votes should identified by IP address and unique
- add the option to make commenting and voting realtime
  - via GraphQL Subscriptions or WebSockets
- present your ability to test the code
  - We expect reasonable unit tests coverage
  - You can also include some integration and e2e tests for bonus points

# Frontend Developer Exercise

## Introduction

- your task is to implement a simple single-user blogging engine frontend in React or Angular
- you don't have to complete all subtasks, just do what you have the time and skills for
- the goal here is not just to see if you can do an app, but how you do it. So please write it as if it were a big production app, that includes code structure, validations, usage of git, documentation, tests, etc.
- we realize that some subtasks can be very time consuming, if you just don't have the time, you can write short text description of how would you solve the problem
- on the flip side, you can improve on many things, if you have the time. For example, we don't need you to implement user registration, but you are free to do so
- feel free to use this exercise (including the instruction) for evaluation by other companies

## Technologies

### Common

- TypeScript is preferred
- Jest is preferred for unit tests, TestCafe, Cypress or Playwright for e2e tests
- Sass for styling
- don't worry too much about styling, you can use Bootstrap, MaterialUI or some other library
- Webpack for bundling

### React

- Next.js is welcome
- React Router/next router for routing
- Redux, hooks or Apollo Link for state management
- Axios for HTTP requests
- Tailwind/ChakraUI

### Angular

- NgRx for state management

## The Exercise

- check out the API [here](api.yml)
- check out the WS API [here](ws.json)
- implement the [wireframes](https://www.figma.com/file/VagZOrr3TjTAxGCpCUTSrO/Applifting-|-Full-Stack-Cvičení "[clickable](https://www.figma.com/proto/VagZOrr3TjTAxGCpCUTSrO/Applifting-%7C-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=2%3A3&viewport=148%2C245%2C0.12103988230228424&scaling=min-zoom")

### User Perspective

- Article List [Article List Wireframe](https://www.figma.com/file/VagZOrr3TjTAxGCpCUTSrO/Applifting-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=2%3A3)

  - display a list of all articles, ordered by date descending
  - each article should show title, perex and publication date
  - each article should have a link to the full text

- Article View [Article View Wireframe](https://www.figma.com/file/VagZOrr3TjTAxGCpCUTSrO/Applifting-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=2%3A75)

  - display an article
  - article should be in markdown, take care of proper rendering

- New Article View [New Article View Wireframe](https://www.figma.com/file/VagZOrr3TjTAxGCpCUTSrO/Applifting-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=14%3A2255)

  - display a page with form to add new article
  - the form should take title, perex and content
  - the content should be in markdown, you can use some existing markdown editor
  - add necessary validations
  - this page should be protected by password

- Add Comment functionality
- display comments on Article View page
- each comment should have content, timestamp and author
- add comment form to Article View page
- comment form should take author and content

- Add Comment voting functionality
  - add the ability to vote on comments (+/-)
  - display score on each comment

### Admin Perspective

- Login Screen [Login Screen Wireframe](https://www.figma.com/proto/VagZOrr3TjTAxGCpCUTSrO/Applifting-%7C-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=14%3A2693&scaling=min-zoom)

  - implement login
  - after successful login redirect to next screen
  - on unsuccesful login display error message

- My Article List [My Article List Wireframe](https://www.figma.com/proto/VagZOrr3TjTAxGCpCUTSrO/Applifting-%7C-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=9%3A0&scaling=min-zoom)

  - display table of all articles
  - display a button to create new article
  - implement edit and delete buttons
  - optionally implement article ordering

- Article Detail View [Article Detail Wireframe](https://www.figma.com/proto/VagZOrr3TjTAxGCpCUTSrO/Applifting-%7C-Full-Stack-Cvi%C4%8Den%C3%AD?node-id=14%3A2622&scaling=min-zoom)

  - display editable sections of article
  - implement publish button
  - use some existing Markdown editor, unless you really want to implement your own

## Multitenancy and accessing the API

The Applifting Blog Engine has **multitenancy API** - multiple users can use the same application and access their own blog data separately from everyone else. In other words, your content (articles, comments, images) will be available only to you.

In order to access your own “space” in the app, you need to create a tenant first. 

**Creating a tenant**

To do so, send the following request to the API:

`POST https://fullstack.exercise.applifting.cz/tenants`

The request should contain a JSON body with the following fields:

```json
{
	"name": "your-new-tenant-name",
	"password": "your-new-tenant-password"
}
```

The response will contain `apiKey` field. The API key is used to identify your tenant when using any other API endpoint - make sure to write it down!

**NOTE**: The key serves purely as an identifier and as such is not considered to be a secret. That means you can store it in your repository without worrying about security.

**Logging in**

You can now log in with your new tenant. Send the following request:

`POST https://fullstack.exercise.applifting.cz/login`

With this body:

```json
{
	"username": "your-new-tenant-name",
	"password": "your-new-tenant-password"
}
```

You will also need to identify your tenant - this is done by adding a new header to the request:

```
X-API-KEY: "your-tenant-API-key"
```

If successful, you will receive a response with `access_token` field. This token expires in an hour and is used to access protected API capabilities (e.g. uploading images).

**Accessing protected resource**

Whenever you want to access a protected endpoint, you will need to supply:

- `apiKey` to identify your tenant
- `access_token` to authorize yourself

For example, if you want to upload a new image:

`POST https://fullstack.exercise.applifting.cz/images`

you will need to provide the following headers:

```
X-API-KEY: "your-tenant-API-key"
Authorization: "your-access-key"
```
