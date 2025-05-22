Los filtros se pueden crear personalizados.
Para crear botones que filtren automáticamente.
Creo que la mejor opción es enviar por opciones las entidades disponibles, para tener su nombre y su id.
Luego pasamos eso a la platilla de twig.
Cada botón asignará el valor al filtro del grupo de entidades que queramos.
Allí creamos botones que lancen el formSubmitted del formFilter con la id de las entidades seleccionadas.