# Symfony

---

# Controladores

En los controladores podemos declarar variables y llamarlas desde twig.

### Guardar en la base de datos

```php
public function save(){
$entityManager = $this->getDoctrine()->getManager();

$animal = new Animal();
$animal->setAtributo('ejemplo');

$entityManager->persist($animal);

$entityManager->flush();

return new Response('El animal guardado tiene el id: '.$animal->getId());
}
```

# Rutas

Así podemos llamar a la ruta : HomeController::ejemplo

## Parámetros opcionales en la url

path: /home/{nombre?}

<aside>
💡

defaults: {nombre: ‘andres‘}  para poner un valor predefinido

</aside>

Se pueden poner requirements para filtrar las variables de la url

## Redirecciones

redirectToRoute(’index’,

[’nombre’ ⇒ ‘Andres pi’])

redicrect(’web.com’)

## listar consolas

```bash
php bin/console debug:router
```

# Plantillas

## bloques

```html
{% block titulo%} Inicio {% endblock %} - Este es mi titulo
```

## Extender plantillas

{% extends ‘layout/ejemplo.html.twig’ %}

{ % block nombreBloque %}

{{parent()}} para poner el contenido del padre

contenido

{% endblock %}

### Establecer variables en plantillas

```html
{% set perro= 'Pastor aleman' %}
```

## Representar arrays

```html
{{ aves.tipo ~ ' - ' ~ aves.raza }}
```

```html
{% for animal in animales %}
<li>
{{animal}}
</li>
{% endfor%}
```

## Hay funciones predefinidas de Twig

https://twig.symfony.com/doc/3.x/

## include()

```html
{{ include('partials/funciones.html.twig', {'nombre': andres }) }}
```

## Filtros más importantes para variables

- trim
- length
- raw || aplica html

## Crear extensiones y filtros

src/Twig/filtro.php

```bash
php bin/console make:twig-extension Nombre
```

# Doctrine

Se puedej ejecutar SQL y DQL(a partir de entidades)

### crear base de datos

```bash
php bin/console doctrine:database:create
```

### crear entidad desde bbdd

```bash
php bin/console doctrine:mapping:convert --from-database yml ./src/Entity
```

```bash
php bin/console doctrine:mapping:import App\\Entity annotation --path=src/Entity
```

### Obtener geter y seter

```bash
php bin/console make:entity --regenerate App
```

### exportar a yml la entidad

```bash
php bin/console doctrine:mapping:import App\\Entity yml --path=src/Entity
```

### Mapear objetos con el atributo en la propia tabla

```php
#[ORM\OneToMany(targetEntity: Product::class, mappedBy: 'category')]
    private Collection $products;
```

<aside>
💡

Si sabes que vas a usar el otro objeto también, puedes llamarlo de esta manera:

```php
// src/Repository/ProductRepository.php

// ...
class ProductRepository extends ServiceEntityRepository
{
    public function findOneByIdJoinedToCategory(int $productId): ?Product
    {
        $entityManager = $this->getEntityManager();

        $query = $entityManager->createQuery(
            'SELECT p, c
            FROM App\Entity\Product p
            INNER JOIN p.category c
            WHERE p.id = :id'
        )->setParameter('id', $productId);

        return $query->getOneOrNullResult();
    }
}
```

</aside>

### Orphan removal(si eliminas la categoria se borran los productos)

```php
#[ORM\OneToMany(targetEntity: Product::class, mappedBy: 'category', orphanRemoval: true)]
private array $products;
```

# Entidad

### Crear entidad

```shell
php bin/console make:entity Usuario
```

### Generar tabla según entidad

```shell
php bin/console doctrine:migrations:diff
```

```bash
php bin/console doctrine:migrations:migrate
```

### Relaciones de entidades

Se relacionan bidireccionalmente para poder acceder a objetos desde ambas entidades

# Repositorios

### Obtener repositorio desde el controlador

```php
$animal_repo = $this->getDoctrine()->getRepository(Animal::class);
```

### find()

```php
$animal = $animal_repo->find($id);
```

### findAll()

```php
$animales = $animal_repo->findAll();
```

### findOneBy([]) || findBy([])

```php
$animal = $animal_repo->findOneBy([
	'tipo' => 'vaca'
],[
	'id' => 'DESC'
]);
```

### createQueryBuilder(’’)

```php
$qb = $animal_repo->createQueryBuilder('a)
									->andWhere("a.raza = :raza")
									->setParameter('raza', 'americana')
									->orderBy('a.id', 'DESC')
									->getQuery();
$resultset = $qb->execute();
```

# Formularios

Se crea una función en el controlador 

```php
public function create(){
$animal = new Animal();
$form = $this->createFormBuilder($animal)
							->setAction($this-ZgenerateUrl('animal_save'))
							->setMethod('POST') //por defecto
								->add('atributo', TextType_class)
								->add('submit', SubmitType::class,[
								'label' => 'Crear animal',
								'attr' => ['class' => 'btn']
								])
							->getForm();
		return $this->render('animal/crear-animal.html.twig',[
			'form'=>  $form->createView()
		)
}
```

### Recibir datos de formulario

```php
public function save(Request $request){
	var_dump($request-> get('form'));}
```

<aside>
💡

Se recibe el formulario en la mismo sitio que se crea.

```php
public function create(){
$animal = new Animal();
$form = $this->createFormBuilder($animal)
							//->setAction($this-ZgenerateUrl('animal_save'))
							//->setMethod('POST') //por defecto
								->add('atributo', TextType_class)
								->add('submit', SubmitType::class,[
								'label' => 'Crear animal',
								'attr' => ['class' => 'btn']
								])
							->getForm();
							
		$form->handleRequest($request);
		
		if($form->isSubmitted() && $form->isValid()){
			$em =$this->getDoctrine()->getManager();
			$em->persist($animal);
			$em->flush();
			
			return $this->redirectToRoute('crear_animal');
		}
		
		return $this->render('animal/crear-animal.html.twig',[
			'form'=>  $form->createView()
		)
}
```

</aside>

### mostrar formulario en las vistas

```php
{{form_start(form)}}
{{form_widget(form)}}
{{form_end(form)}}
```

### Validar formulario

Usar Asserts en la clase Entidad

```php
 #[Assert\Length(max: 255, message="tiene que tener texto")]
```

Se recomienda usar clases para los formularios src/form y se llaman EjemploType.php

## buildForm()

```php
public function buildForm(FormBuilderInterface $builder, array $options){
		$builder->add('atributo', TextType_class)
						->add('submit', SubmitType::class,[
								'label' => 'Crear animal',
								'attr' => ['class' => 'btn']
								]);
}
```

En el controlador hacer entonces solo hay que poner

```php
$form = $this->createForm(AnimalType::class, $animal);
```

### Validaciones aisladas

```php
public function validarEMail($email){
		$validator = Validation:createValidator();
		$errores = $validator->validate($email, [
		new Email()
	]);
if(count($errores)!=0){
echo "incorrecto";
}else{
echo "correcto";
}
}
```

# Login

- Hay que añadirlo en el security
- Hay que indicarle que entidad es el usuario
- Con app.user se accede al usuario autenticado en cualquier parte de la aplicación

# Control de acceso

access_control en security

# Authorization check
AuthorizationCheckerInterface para autorización de roles
# get User
TokenStorageInterface para obtener el usuario o datos

```php
 private AuthorizationCheckerInterface $authorizationCheckerInterface;

    private TokenStorageInterface $tokenStorageInterface;

  

    public function __construct(

        AuthorizationCheckerInterface $authorizationCheckerInterface,

        TokenStorageInterface $tokenStorageInterface

    ) {

        $this->authorizationCheckerInterface = $authorizationCheckerInterface;

        $this->tokenStorageInterface = $tokenStorageInterface;

    }
     $isAdmin = $this->authorizationCheckerInterface->isGranted('ROLE_ADMIN') ||

            $this->authorizationCheckerInterface->isGranted('ROLE_SUPER_ADMIN');;

        $user = $this->tokenStorageInterface->getToken()->getUser();

        /** @var \App\Entity\User $user */

        $employee = $user->getEmployee();
```