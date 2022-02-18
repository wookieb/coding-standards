# Desing

## General

* Method that returns anything or undefined SHOULD use `Maybe` monad

## Repository

* MUST contain only methods necessary for current repository
* Method that creates an entity which might fail due to UNIQUE violation MUST return `Maybe<TEntity>`
* Method performing search of single entity but that entity might not be found MUST return `Maybe<TEntity>`
* Repository MAY contain method for performing search based on specific Query object based on `@pallad/query` package

## CommandHandler

* MUST NOT contain business logic, only logic related to handling calls to services

## Services

* SHOULD accept `participant` of type `unknown` as first argument
    * `participant` is needed for handling access control logic
* SHOULD contain logic related to handling search based on query object 
