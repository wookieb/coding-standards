# General

Make sure you got familiar with [naming cheatsheet](https://github.com/kettanaito/naming-cheatsheet) first. If something in that documentatin isn't clear you should refer to naming conventions first.

## Naming conventions

* Regular variables MUST be in `camelCase` format
* Dates
    * for creation date MUST use name `createdAt`
    * for update date MUST use name `updatedAt`
    * for storing any date that is related to action other than `update` and `create` MUST use format `[actionName]At`
        * action name MUST be in past tense

```typescript
const article = {
    createdAt: new Date(),
    updatedAt: new Date(),
    publishedAt: new Date(),
    scheduledForDeletionAt: new Date()
}
```

* Booleans/Flags
    * MUST use one of following prefixes
      * `is`
      * `has`
      * `was`
      * `to`
      * `should`
    * If an entity contains a lot of boolean flags, consider using other data types (lists, sets, strings, enums) to
      reflect entity data

```typescript
const isReady = true;
const hasItem = true;
const wasDeleted = true;
const toDelete = true;
const shouldBeRemoved = false;
```

* Usage of `null` MUST be avoided

## Actions

Action is an operation to perform on anything (entity, database, table, collection, list etc).
To standarize them, the following action names MUST be used

* `create`
    * to create an entity
    * to create relation between standalone entities
* `delete`
    * to delete an entity
* `remove`
    * to remove relation between standalone entities
    * to remove entry from lists/sets/maps
* `update`
    * to update entity
* `add`
    * to add entry to lists/sets/maps
* `validate`
    * to perform validation on anything
* `find`
    * to perform queries on database
    * to perform any search on lists/sets
* `compose`
  * to create something from other things

Every action that is not covered, and is not in conflict with this section, MAY be used but MUST be in `camelCase` format.

## FAQ

### What is standalone entity?

It is an entity that can live standalone without non-required relations.

For example `article` may have relation to other articles as "related", but removing that relation does not cause any
article to be removed.