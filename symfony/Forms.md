![[Captura de pantalla 2025-04-25 093550.png]]

Renderizar resto del documento con ***`{{ form_rest(form) }}`***
Para editar el html del input por ejemplo, luego dentro podemos rellenarlo de la siguiente manera:
- `field_name()`
- `field_value()`
- `field_label()`
- `field_help()`
- `field_errors()`
- `field_choices()`
Uso 
```
<input
name="{{ field_name(form.username) }}">
```
Acceso a valores individuales cuando renderizamos "a mano": {{ form.task.vars.id }}

### Array de texto
```php
->add('studies', CollectionType::class, [
                'entry_type' => TextType::class,
                'allow_add' => true,
                'allow_delete' => true,
                'by_reference' => false,
                'label' => 'default.study',
                'entry_options' => ['label' => 'default.studies'],
            ])
```
### Entidad singular
```php
->add('document', EntityType::class, [
                    'class' => Documentation::class,
                    'label' => 'default.document_type',
                    'choice_label' => 'name',
                    'required' => true,
                    'multiple' => false,
                    'placeholder' => 'default.select_placeholder',
                    'label_attr' => ['class' => 'd-flex align-items-center fs-5 fw-bold mb-2'],
                    'attr' => ['class' => 'form-select-solid', 'data-control' => 'select2', 'title' => 'default.no_selection'],
                     ])
```