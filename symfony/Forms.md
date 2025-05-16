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

