# GraphQL

* All queries, mutations and subscriptions MUST start with `entity name` in singular or plural form`
* `Entity name` MUST be `camelCased`
* All entity properties MUST be `camelCased`
* All types MUST be `PascalCased` and can use `_` as a separator between logical naming parts
```
✅
Article_Query
Article_Query_Filters

❌
ArticleQuery
ArticleQuery_Filters
ArticleQueryFilters
```
* If a type is a child of parent type then it must be separated with `_`
```
✅
Article_Query
Article_Query_Filters // child of `Article_Query` therefore separator IS nedded
Article_CreateInput // no type `Article_Create` therefore separator is not needed
```
* Mutation name MUST be named in following format `[entityName]_[actionName](?_extraAction)*` where `entityName` is already covered in other points and `actionName` is covered in [general](./general.md#actions) standard
  * `extraAction` can be anything that is needed for the app and is optional
  * `extraAction` MUST be `camelCased`
  * If mutation contains more than one `extraAction` then those MUST be separated with `_`
* Mutation SHOULD return unique identifier to created entity, relation, resource if possible

# Examples
```
query {
    // fetches one article
    article  {
        
    }
    
    // fetches list of articles
    articles  {

    }
}

// defines type of articles query endpoint
type Article_Query {
    filters: Article_Query_Filters
}

type Article_Query_Filters {
    name: String!
}

mutation {
    article_create {
        id
    }
    
    article_delete {
    
    }
    
    article_update {
    
    }
}
```

# Not covered
* There is no requirement regard created entity should return whole entity or only part of it
