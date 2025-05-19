
puedes modificar el request apara añadir información creando una nueva y haciendo new request [...request, 'userId' => $user-getId()]
Luego en apply filters se añade la función. if get['userId] y aplicamos el filtro correspondiente


dashboard
 - [ ] probar a enviar los filtros por parámetro y obtenerlos en el controlador.

### cvs
 - [x] arreglar que manda filtros de checkbox automáticamente
 - [x] arreglar arrays en filtro, no filtra bien
 - [x] no introducir fichero al editar
 - [x] state creado no se desaplica del filtro porque si que lo aplica en el filtro y lo deja allí.
 - [x] no se agrega la información en el strong
 - [x] aplicar filtros a la búsqueda del panel
 - [x] total no se rellena
 - [x] revisar pull request de github
 - [ ] Mostrar fecha y hora de inserción en el listado.
 - [ ] Intereses está funcionando raro
 ### Ofertas de trabajo
 - [ ] Revisar plantillas y cambiar en el resto.
 - [ ] filtros y varios
 - [ ] Chequear si necesitan lifecyclecallbacks
 - [ ] 
 - [ ] 
 - [ ] 



check 
```twig
{% block form_modal_footer_save_button %}

    {% if enable_save is not defined or enable_save == true %}

        <button type="submit" id="{{ prefix }}-save-modal-button" form="{{ _formId }}"

                class="btn btn-success btn-modal-form-submit">

            {{ "default.save"|trans }}

        </button>

    {% endif %}

{% endblock %}
```

```twig
{% extends 'backend/partials/crud/form_filter_modal.html.twig' %}

{% set _formId = 'form_filter_' ~ _entity %}

{% block form_modal_body_content %}

    {{ form_start(form, {'attr': {'id': 'form_filter_' ~ _entity}}) }}

    {{ form_rest(form) }}

  

    {% block form_modal_body_extra %}

    {% endblock %}

{% endblock %}
```