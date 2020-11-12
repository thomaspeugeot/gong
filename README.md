# Gong

*insert image of the bookstore*

## About Gong

Gong is about making fullstack development more fun and less boring.

What is fun and boring stuff?
- Fun stuff:
  - business logic and gui design.
- Boring stuff:
  - database structure/access
  - API controllers
  - standard Angular Material Components
  - documentation with UML diagrams
- *Very* boring stuff:
  - maintaining the above boring stuff

Gong is a set of 2 compilers:
- the first compiler compiles the business logic written in `go` and generates the boring code in `go` and `ng`
- the second compiler generates UML diagrams from `go` code

Gong stands for "go + ng", a go backend and an angular frontend.

## Description

Gong is a programming langage that is a subset of the go langage. 

A set of go `foo/go/models` go package written following the *gong* langage constraints can be compiled by the `gongc` compiler into a stack of integrated component in go for the backend and angular for the front end. 

This stack can be packaged ino a reusable gong library to be used in another full stack developpemnent (an example is provided).

- a `foo/go/orm` package, leveraging gorm, the fantastic go ORM, for the persistance into GORM supported database (sqlite3 in memory, sqlite3 file, postgres, ...)
- a `foo/go/controllers` package, leveraging the gin framework, an HTTP web framework written in Go (Golang)
- a `foo/go/controllers/foo.yaml` open api 2.0 interface definition (thks to go-swagger), it provides a RESTful interface for  developing and consuming an API of the gong package


- a `foo/ng/projects/foo` angular service library for accessing gong object with some an angular material library with commonly used material components: table, editor, presentation, splitter presentation, arborescence presentation

if a gong variable data is created on the backend, a constraint is to register all instances on a store.

## An example

Bookstore is a simple fullstack application. some of its code is generated by gong

The bookstore code architecture is as follow.
```
README.md       (this file)
go/             (the application backend, in go)
    go.mod          (file created by the command 
                    `go mod init github.com/thomaspeugeot/metabaron/examples/bookstore/go`)
    go.sum          (idem)

    docs.go         (Descrption of the module, a boring part, generated by gong)

    cmd/            (a fun part, hand written by the programmer)

        main.go     (the backend logic)
    
    models/          (fun part, hand written by the programmer, parsed by metabaron)

        Area.go             (contains struct Area)
        Editor.go           (contains struct Editor)
        Book.go             (contains struct Book)

    controllers/    (boring part, all generated by metabaron, ...
                    ... based on the gin framework)
    
        bookstoreapi.yml    (the description of the api, usefull for tests with Postman or openapi...
                                ... is used by openapi generator to generate api controllers ...)
        errors.go           (controllers error codes)
        Area.go             (controller for struct Area)
        Editor.go           (controller for struct Editor)
        Book.go             (controller for struct Book)

    orm/            (boring part, all generated by metabaron ...
                    ... based on the gorm framework)
        
        Area.go             (orm for struct Area)
        Editor.go           (orm for struct Editor)
        Book.go             (orm for struct Book)
        setup.go            (setup of the connection to the sqllite3 db)

ng/                 (the application front end, in angular ...
                    ... this directory was created by `ng new ng`)

    ...                 misc. files create by the ng & npm metabaron commands
    app-routing.module.ts   (patched to account for generated ng material components)

    src/app/            (the fun part, contains the frontend application logic)

        area-adder/         (the boring parts, generated ng material components...)
        areas-tables/
        books-table/
        book-adder/
        ...

        app.component.html   (the fun part, to be extended)

api/            (boring part, front api controllers node module ...
                ... generated by openapi generator)

```