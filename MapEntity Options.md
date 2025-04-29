The `#[MapEntity]` attribute in Symfony allows for automatic entity loading from route parameters. Below are the available options to customize its behavior:

---

## 1. `id`  
If an `id` option matches a route parameter, the resolver will fetch the entity by its primary key.

```php #[Route('/product/{product_id}')] public function show( #[MapEntity(id: 'product_id')] Product $product ): Response { } ```

---

## 2. `mapping`  
Allows fine-grained control by mapping route parameters to Doctrine entity fields (used with `findOneBy()`).

``` php 
#[Route('/product/{category}/{slug}/comments/{comment_slug}')] public function show( #[MapEntity(mapping: ['category' => 'category', 'slug' => 'slug'])] Product $product, #[MapEntity(mapping: ['comment_slug' => 'slug'])] Comment $comment ): Response { } 
```

---

## 3. `exclude`  
Use this to exclude certain route parameters from the automatic `findOneBy()` query.

```php #[Route('/product/{slug}/{date}')] public function show( #[MapEntity(exclude: ['date'])] Product $product, \DateTime $date ): Response { } ```

---

## 4. `stripNull`  
If set to `true`, null values from route parameters will be ignored in the query.

---

## 5. `objectManager`  
Specify a custom Doctrine object manager instead of the default one.

```php #[Route('/product/{id}')] public function show( #[MapEntity(objectManager: 'foo')] Product $product ): Response { } ```

---

## 6. `evictCache`  
If `true`, forces Doctrine to bypass the identity map and reload the entity from the database.

---

## 7. `disabled`  
If `true`, disables the automatic value resolution.

---

## 8. `message`  
Displays a custom message when a `NotFoundHttpException` is thrown (only visible in the dev environment).

```php #[Route('/product/{product_id}')] public function show( #[MapEntity(id: 'product_id', message: 'The product does not exist')] Product $product ): Response { } ```

---

> Use `#[MapEntity]` to keep controllers clean and declarative by letting Symfony handle entity fetching for you.