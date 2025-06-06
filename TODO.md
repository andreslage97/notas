
puedes modificar el request apara añadir información creando una nueva y haciendo new request [...request, 'userId' => $user-getId()]
Luego en apply filters se añade la función. if get['userId] y aplicamos el filtro correspondiente


#### 28/05
- [x] Crear reserva al clickar
- [x] Solo ver reservas aceptadas.
- [x] arreglar el menu
- [x] deja clickar en los reservados
- [x] mirar si 'created' se puede dejar asignado por defecto
- [x] crear reservas
	- [x] No puede haber una aceptada para ese puesto en el rango de fechas
- [x] filtros empleado no van en reservations
- [x] revisar filtros
- [x] si está reservada, no aplicar conflicto o removerlo
- [x] clicks ya no van en empleado. ver como arreglarlo
#### 02/06
- [x] Hacer un type específico para employees, ya que no pueden modifcar las consultas ya aceptadas o canceladas.
- [x] Los botones de editar no le salen al administrador, pero me parece funcional de esta manera.
#### 06/06
- [x] document-definition
- [x] estado de la definicion en el documento
### cvs
 - [x] arreglar que manda filtros de checkbox automáticamente
 - [x] arreglar arrays en filtro, no filtra bien
 - [x] no introducir fichero al editar
 - [x] state creado no se desaplica del filtro porque si que lo aplica en el filtro y lo deja allí.
 - [x] no se agrega la información en el strong
 - [x] aplicar filtros a la búsqueda del panel
 - [x] total no se rellena
 - [x] revisar pull request de github
 - [x] Mostrar fecha y hora de inserción en el listado.
 - [x] Intereses está funcionando raro
 ### Ofertas de trabajo
 - [x] Revisar plantillas y cambiar en el resto.
 - [x] filtros y varios
 - [x] Chequear si necesitan lifecyclecallbacks
 - [x] revisar datetimes para cambiar por datetimeinmutable
### Cv 
 - [x] No funciona array de varios valores de enum
 - [x] revisar filtros
 - [x] hacer pull request
 - [x] Revisar Absence por AbsenceType
 - [x] revisar validatorOf en user
 - [x] revisar filtros
- [x] REtocar 26+27
#### notas
podemos enviar variables desde el controlador.
Luego en los scripts de twig asignamos la variable a una constante.
Luego la tenemos disponible en la datatable.

##### Checks
- [ ] boton borrar permiso
- [ ] rutas con guion medio
- [ ] tipo de dato a las constantes
- [ ] cambiar por indentifier en controller, y quitar grupo del uuid