# General

Make sure you got familiar with [naming cheatsheet](https://github.com/kettanaito/naming-cheatsheet) first. If something
in that documentatin isn't clear you should refer to naming conventions first.

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

Action is an operation to perform on anything (entity, database, table, collection, list etc). To standarize them, the
following action names MUST be used

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

Every action that is not covered, and is not in conflict with this section, MAY be used but MUST be in `camelCase`
format.

## Avoiding semantic double negations

You SHOULD avoid using flags named "disable", "hide" or similar that "turns off" certain behavior. This is because you
can easily end up in situation of double negation.

```typescript
class ArticleService {
    update(id: string, data: ArticleData) {
        this.performUpdate(data);
        this.updatePublishDate(id);
    }
}
```

Now you might need to disable updating publish date. You might be tempted to add options property
named `disableUpdatingPublishDate`.

```typescript
class ArticleService {
    update(id: string, data: ArticleData, options?: { disableUpdatingPublishDate?: boolean }) {
        this.performUpdate(data);
        // now you need to spend more time to logically analyze if operation is enabled
        if (!options?.disableUpdatingPublishDate) {
            this.updatePublishDate(id);
        }
    }
}
```

Not only you need to think a little bit more to make sure how to handle "disabling" flag but also you might end up
calling service that sets this flag to false which is a double negation logic harder to understand.

```typescript
// enable updating publish date but in order to understand that you need to think a little bit more
service.update(id, data, {disableUpdatingPublishDate: false})

// disable updating publish date
service.update(id, data, {disableUpdatingPublishDate: true})
```

It is far better to take opposite approach and name fields like "enable", "show" etc and give them correct defaults

```typescript
class ArticleService {
    update(id: string, data: ArticleData, options?: { updatePublishDate?: boolean }) {
        this.performUpdate(data);
        // easy right?
        if (options?.updatePublishDate ?? true) {
            this.updatePublishDate(id);
        }
    }
}
```

```typescript
// enable updating publish date
service.update(id, data, {updatePublishDate: true})

// disable updating publish date
service.update(id, data, {updatePublishDate: false})
```

Same rule applies to frontend world.

## FAQ

### What is standalone entity?

It is an entity that can live standalone without non-required relations.

For example `article` may have relation to other articles as "related", but removing that relation does not cause any
article to be removed.
