# Errors

## Throwing errors

* Throwing regular `Error` SHOULD be avoided if other common errors are more appropriate

```typescript

function findEntityById(id: string) {
    const entity = fetchEntityById(id);
    if (!entity) {
        // throw new Error("Entity not found"); // WRONG
        throw NotFoundError.entity("Entity", {id}); // GOOD
    }
}
```

* Types from `@pallad/common-errors` SHOULD be used whenever possible
* Using `alpha-errors` for assigning errors codes SHOULD be considered as a first choice for most places as they are
  very useful for unique identification
* Errors MUST NOT be thrown for parsing functions instead `Validation<Possible | Errors | Union, ParsingResult>` type
  MUST be used
