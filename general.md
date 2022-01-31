# General

## Naming conventions

* Regular variables SHOULD be `camelCased`
* Dates
    * for creation date always use name `createdAt`
    * for update date always use name `updatedAt`
    * for storing any date that is related to action other than `update` and `create` use format `[actionName]At`
    
* Booleans/Flags
    * Use following prefixes `is*`, `has*`, `was*`, `to*`
    * Other prefixes are prohibited
    * If an entity contains a lot of boolean flags, consider using other data types (lists, sets) to reflect entity data

```typescript
const isReady = true;
const hasItem = true;
const wasDeleted = true;
const toDelete = true;
```

## Actions

Action is an operation performed on something. To standarize them, the following action names MUST be used

* `create`
    * to create an entity
    * to create relation between non-standalone entities
* `delete`
    * to delete an entity
* `remove`
    * to remove relation between non-standalone entities
    * to remove entry (that is not an entity) from lists/sets/maps
* `update`
    * to update entity
* `add`
    * to add entry (that is not an entity) to lists/sets/maps
* `validate`
    * to perform extra validation on anything
* `find`
    * to perform any entity retrieving actions

Every action that is not covered and is not in conflict with this section can be added but MUST be `camelCased`.
