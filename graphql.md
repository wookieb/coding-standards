# GraphQL

* All queries, mutations and subscriptions MUST start with `entity name` in singular or plural form
* `Entity name` MUST be in `camelCase` format
* `Entity name` in plural more MUST be used only for querying list of given entity
* All entity properties MUST be in `camelCase` format
* All types MUST be in `PascalCase` format and SHOULD use `_` as a separator between logical naming parts

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
Article_Query_Filters // child of `Article_Query` therefore separator is nedded
Article_CreateInput // no type `Article_Create` therefore separator is not needed
```

* Type related to entity MUST use `entity name` at the beginning in singular form

* Mutation name MUST be named in following format `[entityName]_[actionName](?_extraAction)*` where `actionName` is covered in [general](./general.md#actions)
    * `extraAction` can be anything that is needed for the app and is optional
    * `extraAction` MUST be in `camelCase` format
    * `entityName` MUST be in singular form
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

type Article_CreateInput {
  content: String!;
  title: String!;
}

type Article_UpdateInput {
  content: String;
  title: String;
}

mutation {
    article_create(input: Article_CreateInput!) {
        id
    }
    
    article_related_create(from: ID!, to: ID!) {
        id
    }
    
    article_related_remove(from: ID!, to: ID!) {
      
    }
    
    article_delete(input: Article_UpdateInput!)
    
    article_update {
    
    }
}
```

# Not covered

* There is no requirement for mutations to return whole entity or only part of it.
