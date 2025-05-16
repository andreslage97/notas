```php
class ProductController extends AbstractController
{
    #[Route('/product/{id}')]
    public function show(Product $product): Response
    {
        // use the Product!
        // ...
    }
}
```
Si la ruta coincide con alguna propiedad de la entidad, se busca automáticamente por la misma.
```php
#[Route('/product/{id}')]
```
