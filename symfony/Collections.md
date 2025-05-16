Inicializar las collections en el constructor como un new ArrayCollection();
Las colecciones se guardan en un atributo con una relación onetomany, etc.
Se renderizan con un template generado por form.{collection}.vars.prototype.
Normalmente quieres el widget:   {{ form_widget(_company.name, {'attr': {'class': 'col-4'}}) }}.
La información del modal se obtiene con los grupos de serialización, se carga con JavaScript
El modal se carga ya al principio en oculto. se rellena con llamadas de JavaScript con el init() de las clases.
#### ***FormCollectionHelper***
El __name__ que se añade luego será intercambiado por números para poder gestionarlo correctamente en el backend. 
El **FormCollectionHelper** recibe lo siguiente para funcionar.

#### Añadimos el javascript del modal
El Javascript del modal, se le añade un FormCollectionHelper de la siguiente manera: 
```
  companiesCollectionHelper: FormCollectionHelper.createFromCustomConfig({
    container: document.querySelector('#companies-container'),
    template: document.querySelector('#companies-template'),
    addButton: document.querySelector('#add-companies-btn'),
    form: document.querySelector('#form-tecnology'),
  }),
```
#### Luego hay que iniciarlo
```
    customInitCallback() {
    this.companiesCollectionHelper.init();
   },
```

## Atributos para el add del builder
### Prototype
Symfony genera un formulario vacío de cada tipo de entrada de la colección
### `by_reference`
Cuando Symfony maneja una colección de objetos, lo hace **por referencia**. Esto significa que cualquier cambio realizado en el formulario **afectará directamente al objeto original**

``` php
$builder->add('companies', CollectionType::class, [
    'entry_type' => null,            // ⚠️ Obligatorio: debes definirlo tú (por ejemplo, CompanyType::class)
    'entry_options' => [],           // No pasa ninguna opción extra a los formularios hijos por defecto
    'allow_add' => false,            // No permite agregar dinámicamente
    'allow_delete' => false,         // No permite eliminar dinámicamente
    'prototype' => true,             // ✔️ Está activado por defecto
    'prototype_name' => '__name__',  // Nombre del marcador usado en el HTML para clonar con JS
    'by_reference' => true,          // ⚠️ Usado para modificar directamente las referencias (ojo con entidades)
    'mapped' => true,                // El campo se mapea a la propiedad del objeto
    'required' => true,              // Se requiere al menos un valor (pero no siempre práctico en colecciones)
    'label' => null,                 // No se muestra una etiqueta por defecto
    'attr' => [],                    // No tiene atributos HTML extra por defecto
    'delete_empty' => false,         // No elimina elementos vacíos a menos que lo definas
    'error_bubbling' => false,       // Errores de validación no se propagan al campo padre
    
])
# keep_as_list - arregla los indices del array, para que sea predecible

```
## Hay que crear la ruta en la entity de la collection
creas ruta con uuid/form-data

## Ejemplo de form en php
``` php
  ->add('companies', CollectionType::class, [
                'entry_type' => CompanyType::class,
                'allow_add' => true,
               'entry_options' => [
                'label' => false,
                'attr' => ['class' => 'form-control mb-2']
            ],
                'allow_delete' => true,
                'by_reference' => false,
                'prototype' => true,/*  default false */
                'delete_empty' => true,
                'label' => 'Empresas',
                'required' => false,
            ])
```
## Ejemplo de javascript 

``` javascript
const tecnologyModal = CrudFormModalHelper.createFromCustomConfig({
        prefix: 'tecnology',
        companiesCollectionHelper: FormCollectionHelper.createFromCustomConfig({
          container: document.querySelector('#companies-container'),
          template: document.querySelector('#companies-template'),
          addButton: document.querySelector('#add-companies-btn'),
          form: document.querySelector('#form-tecnology'),
        }),
        customInitCallback() {
          this.companiesCollectionHelper.init();
          this.companiesCollectionHelper.setCustomPopulateCallback(
            (item, data) => {
              item.value=data.uuid;
            }
          )
        },
        preOpenForEditItemCallback(data) {
          this.companiesCollectionHelper.clear()
          this.companiesCollectionHelper.createItemsWithData(data.companies);
        },
        preOpenForNewItemCallback() {
          this.companiesCollectionHelper.clear()
          this.companiesCollectionHelper.addEmptyItems(1);
        },
        afterResetCustomCallback() {
          document.querySelector('#general-data-tab')?.click();
        },
}).init();
```
