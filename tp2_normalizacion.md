Practica Nro. 2 - Normalizacion
===============================

Pautas de resolucion ­son las pautas requeridas para aprobar el tema en el parcial-

El proceso de normalizacion para un esquema R, usado y evaluado en la materia
consta de los siguientes pasos:

  1. Identificar en el esquema R la o las claves candidatas y escribirlas
     explícitamente poniendo los atributos que conforman cada una de ellas.

  2. Identificar las dependencias funcionales no triviales y mínimas validas en
     el esquema R y escribirlas explícitamente numerandolas en orden
     consecutivo. Tener en cuenta que el orden en la que se escriben no sera
     necesariamente el orden en el que posteriormente se usen en el paso 3 (LOS
     PASOS 1 Y 2 NO MANTIENEN UN ORDEN ESTRICTO, se pueden invertir)

  3. Iniciar el analisis del esquema R para normalizarlo hasta BCNF (o 3FN).
     Comprobando si el esquema R se halla en BCNF.

    1. Si no esta en BCNF, entonces intentar llevarlo a BCNF creando
       particiones del esquema R (ver Proceso de particionamiento de un esquema
       analizando desde BCNF)

    2. Si esta en BCNF detener el proceso

  4. Una vez finalizado el proceso escribir las particiones resultantes que se
     generan en el punto 3 (esquemas que estan en BCNF o 3FN según corresponda)

 5. Indicar la clave primaria resultante del proceso de normalizacion (tener en
    cuenta que debe haber quedado como clave primaria, alguna de las claves
    candidatas halladas en el punto 1)

  6. Una vez identificadas las tablas que luego de aplicar el proceso de
     particionamiento de un esquema analizando desde BCNF quedaron en BCNF (o
     3FN) analizar 4FN

    1. Si el proceso se realizo de acuerdo a lo propuesto en la materia, la
    única tabla que puede no estar en 4FN es la última que se hallo con el
    proceso.

      1. En caso de detectar que un esquema no se encuentra en 4FN, se debera
         aplicar un proceso que sera incluido en otro documento una vez
         introducido este concepto en las clases teoricas.

    2. Una vez llevadas las particiones a 4FN, escribir de manera explicita al
       final de todo el proceso cuales son las tablas que considera que han
       quedado en 4FN y no son proyecciones de otras tablas.

Ejemplos
========

Para los esquemas propuestos en cada ejercicio aplicar el proceso de
normalizacion. Todos los esquemas ya se encuentran en 1FN. Utilizar las claves
candidatas y Dependencias Funcionales provistas.

Librerias Asociadas
-------------------

LIBRERIAS_ASOCIADAS(idLibreria, nombreLibreria, idArticulo, nombreArticulo, idComponenteArticulo,
nombreComponenteArticulo, idFabricanteArticulo, idDueño)
Donde:

- Para cada librería se conoce su identificador, el cual es único. Ademas del
    identificador de a librería se conoce su nombre. El nombre de la librería
    puede repetirse en distintas librerías.
- Cada librería posee uno o varios dueños (idDueño)
- Cada librería registra los artículos (idArticulo) que tiene en su inventario.
    Para cada artículo de una librería se conoce su nombre.
- Los identificadores de artículos se pueden repetir en diferentes librerías,
    pero no dentro de una misma librería
- Los artículos de una librería estan compuestos por diversos componentes
    (idComponente).
- Los identificadores de componentes se pueden repetir en diferentes librerías
    para diferentes artículos, pero no para el mismo componente de un artículo
    dentro de una misma librería.
- Para cada componente de un artículo de una librería se conoce su nombre.
- Cada artículo de una librería tiene varios fabricantes que lo proveen
    (idFabricanteArticulo)

Clave Candidata:
Cc1: (idLibreria, idArticulo, idComponente, idFabricanteArtículoLibreria, idDueño)

DFs
idLibreria -> nombreLibreria
idLibreria, idArticulo -> nombreArticulo
idLibreria, idArticulo, idComponente -> nombreComponente

Empleado
--------
EMPLEADO(
  idEmpleado, nombreEmpleado,
  idOficina, nombreOficina,
  idResponsableOficina,
  cargaHorariaEnOficina,
  nombreResponsableOficina,
  añoIngresoOficina,
  idActividadEmpleadoOficina,
  nombreActividadOficina,
  dniEmpleado
)


Donde:

- El idEmpleado es único por oficina. El mismo idEmpleado no se repite en
  diferentes oficinas
- Cada empleado tiene asignada una única carga horaria para la oficina en la
  que trabaja e ingreso a la oficina en un año determinado
- El nombre del empleado no es único, es decir puede haber mas de un "Juan
  Perez" trabajando en una oficina
- El nombre del responsable de la oficina no es único, es decir puede haber mas
  de un "Juan Perez" responsable de una oficina
- En una oficina existen muchos responsables ( tener en cuenta que el esquema
  ya se encuentra en 1FN)
- Los responsables de oficina pueden repetirse para diferentes oficinas
- idActividadEmpleadoOficina, son todas las actividades que un empleado realiza
  en la oficina (tener en cuenta que el esquema ya se encuentra en 1FN)

Claves candidatas:

  Cc1: (idEmpleado, idResponsableOficina, idActividadEmpleadoOficina)
  Cc2: (dniEmpleado, idResponsableOficina, idActividadEmpleadoOficina)

Dependencias funcionales:

idOficina -> nombreOficina
idResponsableOficina, idOficina -> nombreResponsableOficina
idEmpleado -> nombreEmpleado, idOficina, añoIngresoOficina, dniEmpleado
dniEmpleado -> nombreEmpleado, idOficina, añoIngresoOficina, idEmpleado
idActividadEmpleadoOficina -> nombreActividadOficina

3. SUCURSALES(idSucursal, nroEmpleado, idOficina)
Donde:
   - Un empleado trabaja para muchas sucursales, sin embargo, un empleado en una sucursal trabaja en una
    única oficina.
   - En una sucursal hay muchas oficinas.
   - El idOficina es único en el sistema.
   - Una oficina pertenece a una única sucursal.
Claves candidatas:
Cc1: (idSucursal, idEmpleado)
Cc2: (idEmpleado, idOficina)
Dependencias funcionales:
idSucursal, idEmpleado -> idOficina
idOficina -> idSucursal
idEmpleado, idOficina -> idSucursal
Para los esquemas propuestos en cada ejercicio aplicar el proceso de normalizacion.
Todos los esquemas ya se encuentran en 1FN. Se deben hallar las claves candidatas y
dependencias funcionales / multivaluadas.

Ejercicios
==========

Repuesto
--------

    REPUESTO (
     idMarca, nombreMarca,
     idModelo, nombreModelo, añoInicioFabricación, añoFinFabricación,
     idPais, nombrePais,
     idRepuesto, descripción, precio
    )

Donde:
- Para un modelo de una marca se conoce su nombre, año en que se inicio su
  fabricacion, año en que se concluyo su fabricacion y el país donde se
  fabrico.
- Para un repuesto se conoce su descripcion, precio y para qué modelo de una
  marca es.

> [Solucion](src/p2/e1_repuestos.md)

Informe Medico
--------------

    INFORME_MEDICO (
      idMedico, apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM,
      idPaciente, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP,
      idObraSoc, nroAfiliado,
      nombreOS, direccionOS, teléfonoOS,
      idorgano, descripcion,
      idEstudio, resultado, fechaEstudio, informe
    )

 Donde:

  - De cada médico se conoce su nombre y apellido, tipo y número de documento,
    fecha de nacimiento, matricula, direccion y teléfono.
  - De cada paciente se conoce su nombre y apellido, tipo y número de
    documento, fecha de nacimiento, direccion, teléfono, y obra social.
  - De cada obra social se conoce su nombre, direccion y teléfono.
  - Para cada organo se conoce su descripcion
  - De cada estudio se registra a que paciente pertenece, que médico lo
    realizo, que organo se estudio, cual fue el resultado y en qué fecha se
    realizo.

> [Solucion](src/p2/e2_informes_medicos.md)

Aeropuerto
----------

    AEROPUERTO (#aeropuerto, #pista, fecha, #avion)

Donde:

   - `#aeropuerto` y `#avion` son únicos
   - El `#pista` se puede repetir para distintos aeropuertos.
   - `fecha` representa la fecha de despegue de un avion. Cada avion tiene como
     maximo un despegue diario en un mismo aeropuerto
   -  Un avion puede realizar despegues de distintos aeropuertos

Dispositivos
-------------

    DISPOSITIVOS (
      Marca_id, descripMarca,
      modelo_id, descripModelo,
      equipo_tipo_id, descripEquipoTipo,
      empresa_id, nombreEmpresa, cuit, direccionEmpresa,
      usuario_id, apyn, nro_doc, direccionUsuario, cuil,
      plan_id, descripPlan, importe,
      equipo_id, imei, fec_alta, fec_baja, observaciones,
      línea_id, nroContrato, fec_alta_linea, fec_baja_linea
    )

Donde:

  - De cada marca se conoce su descripcion
  - De cada modelo se conoce su descripcion y a que marca pertenece.
  - Para cada tipo de equipo se conoce la descripcion
  - Para cada empresa se registra el nombre, cuit y direccion
  - De cada usuario se registra su nombre y apellido, número de documento,
    direccion y cuil.
  - Para cada plan, se registra que empresa lo brinda, la descripcion e importe
    del mismo.
  - Para cada equipo interesa conocer su tipo, modelo, imei, fecha en que se
    dio de alta, fecha en que se da de baja y las observaciones que sean
    necesarias.
  - Para cada línea se necesita registrar el número de contrato, que plan
    posee, la fecha de alta de la línea, la fecha de baja, el equipo que la
    posee y el usuario de la misma.

Mapas publicados
----------------

5. MAPAS_PUBLICADOS(idMapa, proyeccion, escalaMapa, idSitioWeb, dominioSitioWeb, especialidadSitioWeb,
dueñoSitioWeb, fechaPublicacionMapa, valorPublicacion)
Donde
   - A un sitio web se le cobra un valor (valorPublicacion) por cada fecha (fechaPublicacionMapa) en la cual
   publique un mapa.
   - Un sitio web puede tener varios dueños (dueñoSitioWeb).
   - Un sitio web posee un único dominio (dominioSitioWeb).
   - El identificador de un mapa (idMapa) es único.
   - El identificador de un sitio web (idSitioWeb) es único.
   - Un mapa se genera con una proyeccion y a una escala.
   - especialidadSitioWeb es la especialidad de un sitio.

Tomas fotograficas 1
--------------------

6. TOMAS_FOTOGRAFICAS_1( idElemento, descripcionElemento, idFoto, fechaFoto, obturacionCamaraFoto,
 idCamara, caracteristicaTecnicaCamara, descripcionCaracteristica)
Cuando se toma una fotografía, se indican todos los elementos que aparecen en ella, se registra la camara con la que se
tomo, el valor de obturacion del lente de la camara y todas las características técnicas de la camara con la que se toma
la foto.
  - en una foto puede haber varios elementos, un elemento puede aparecer en varias fotos, pero en una misma foto
   solo parece una vez
  - El idElemento identifica a cada elemento y es único en el sistema.
  - El idFoto es único en el sistema.
  - obturacionCamaraFoto es la obturacion del lente de la camara usada en una foto
  - caracteristicaTecnicaCamara es una característica técnica de una camara. Una misma característica NO
   pertenece a mas de una camara. Dos caracteristicaTecnicaCamara pueden tener la misma descripcion pero
   perteneceran a camaras diferentes.

Infracciones registradas
-------------------------

7. INFRACCIONES_REGISTRADAS (idAuto, patente, modeloAuto, #seguroActual,
fechaVencimientoSeguroActual, empresaSeguroActual, idInfraccion, fechaInfraccion, tipoInfraccion)
   Cuando un vehículo genera una infraccion, ademas de la informacion propia de ésta, se registra informacion del
   seguro que tienen el auto involucrado en ese momento (un auto tiene solamente de un seguro actual)
    - un #seguroActual puede pertenecer a mas de un auto. Es decir en el mismo seguro se asegura a mas de
      una auto
    - un auto puede tener solamente un seguro actual, es decir que no puede repetirse para el mismo auto el
      #seguroActual
    - un auto tiene muchas infracciones pero una infraccion se libra sobre un solo auto

Tomas fotograficas 2
--------------------

8. TOMAS_FOTOGRAFICAS_2( idElemento, descripcionElemento, idFoto, fechaFoto, obturacionCamaraFoto,
idCamara, caracteristicaTecnicaCamara, descripcionCaracteristica)
Cuando se toma una fotografía, se indican todos los elementos que aparecen en ella, se regsistra la camara con la que
se tomo, el valor de obturacion del lente de la camara y todas las características técnicas de la camara con la que se
toma la foto.
  - en una foto puede haber varios elementos, un elemento puede aparecer en varias fotos, pero en una misma foto
   solo parece una vez
  - El idElemento identifica a cada elemento y es único en el sistema.
  - El idFoto es único en el sistema.
  - obturacionCamaraFoto es la obturacion del lente de la camara usada en una foto
  - caracteristicaTecnicaCamara representa una características técnica de una camara. Tener en cuenta que una
   camara tiene varias característica, y una característica puede corresponder a mas de una camara.

Empresa colectivo
------------------

9. EMPRESA_COLECTIVO (#Línea, #Ramal, #Colectivo, dniChofer, dniInspector, dniEmpleado, nombreLinea,
nombreChofer, nombreInspector, nombreEmpleado)
 Donde
   -  Una línea posee varios ramales
   -  Los #Ramal no se repiten en distintas líneas
   -  Los #Colectivo se repiten en distintas líneas
   -  Los choferes estan asignados a un único ramal
   -  Cada colectivo de una línea esta asignado a un único ramal.
   -  Para cada ramal existe al menos un chofer asignado.

Internacion
------------

10. INTERNACION (codHospital, cantidadHabitaciones, direccionInternacionPaciente,
telefonoInternacionPaciente, dniPaciente, domicilioPaciente, nombreApellidoPaciente, domicilioHospital,
ciudadHospital, directorHospital, fechaInicioInternacion, cantDiasIntenacion, doctorQueAtiendePaciente,
insumoEmpleadoInternacion)
Donde
   - cantidadHabitaciones es la cantidad de habitaciones que hay en cada hospital
   - direccionInternacionPaciente y telefonoInternacionPaciente, indican la direccion y el teléfono que deja un
   paciente cuando se interna
   - domicilioPaciente es el domicilio que figura en el dni del paciente
   - Un paciente para una internacion es atendido por muchos doctores (doctorQueAtiendePaciente)
   - Para una internacion de un paciente, se emplean varios insumos (insumoEmpleadoInternacion)
   - El codigo de hospital (codHospital) es único.
   - Existe un único director por hospital. Un director podría dirigir mas de un hospital
   - Un paciente en la misma fecha no puede estar internado en diferentes hospitales
   - En un domicilioHospital de una ciudad existe un único hospital

Reserva
--------

11. RESERVA (#Reserva, #Agencia, nombreAgencia, fechaReservaVuelo, ciudadOrigen, ciudadDestino,
tipoPago, nombreAerolínea, #Vuelo, dniPasajero, nombrePasajero, dirPasajero, telPasajero, clase, fechaPartida,
fechaLlegada, horaPartida, horaLlegada, modeloAvion, #Asiento, tipoComida, compañíaPasajero, dirCompañía,
telCompañía)
Donde
   - Una reserva puede involucrar uno o varios pasajeros (por ejemplo un tour).
   - Si bien todos los pasajeros de una reserva viajan en la misma clase del mismo vuelo, cada uno de ellos decide
   el tipo de pago de su asiento (El tipo de pago se refiere al la forma de pago: efectivo, tarjeta de crédito, etc.).
   Notar que para cada vuelo el tipo pago puede ser potencialmente diferente.
   - Una reserva puede involucrar muchos vuelos (por ejemplo para desplazarse de A a C se debe pasar por una
   escala intermedia B); tener en cuenta que no necesariamente todos los pasajeros de una reserva viajan en todos
   lo vuelos de esa reserva. Para cada vuelo de una reserva se conoce la fecha para la cual se realiza. Para una
   fecha puede haber varios vuelos de una o varias reservas.
   - La reserva es realizada a través de una única agencia de turismo.
   - Los pasajeros pueden estar independientemente involucrados en distintas reservas.
   - Cada aerolínea maneja su propia forma de asignar el #Reserva, con lo cual no hay garantía que estos no se
   repitan para las distintas aerolíneas.
   - Las aerolíneas siempre usan el mismo modelo de avion para el mismo vuelo. Y el mismo vuelo de una
   aerolínea siempre sale de la misma ciudad a la misma hora, y llega a la misma ciudad destino a la misma hora
   de llegada, los días que ese vuelo es ofrecido por la aerolínea.
   - El tipo de comida significa si corresponde desayuno, almuerzo, cena o merienda o cualquier combinacion de
   ellos para cada vuelo.
   - Para cada reserva de un pasajero se conoce el domicilio del pasajero y datos de su lugar de trabajo. Un
   pasajero puede trabajar en mas de una compañía, una compañía puede tener mas de una direccion y en cada
   direccion de una compañía puede haber mas de un teléfono.

Buque
------

12. BUQUE (nombreBuque, nYApDueño, dniDueño, tipoBuque, tonelaje, tipoCasco, #Viaje, puertoOrigen,
puertoDestino puertoIntermedio, nomPaísPuertoDestino, nombrePaisPuertoOrigen,
nombrePaisPuertoIntermedio, posicionActual, fechaPosicionActual, nYApPasajero, dniPasajero, dirPasajero,
puertoInicioPasajero, puertoFinalPasajero)
Donde
   - El #Viaje es un número consecutivo que identifica cada partida de cada buque.
   - Un buque hace varios viajes.
   - El #Viaje se repite para distintos buques
   - Un buque puede tener varios dueños.
   - El nombre del buque es único.
   - Un nombreBuque se asocia a un tipo de buque.
   - El tonelaje y el casco estan determinados por el tipo de buque.
   - Un buque reporta su posicion una vez por día independientemente del viaje.
   - Cada viaje de un buque tiene un puerto origen, un puerto destino y varios puertos intermedios.
   - Un buque en su viaje puede pasar por varios puertos intermedios sin repetirlos.
   - Un pasajero tiene una única direccion independientemente del viaje.
   - Un pasajero tiene un único puerto origen y puerto destino por cada viaje de un buque.

Evaluaciones
-------------

13. EVALUACIONES (idEvaluacion, fechaEvaluacion, descripcionEvaluacion, dniEvaluado, legajoEvaluado,
nombreEvaluado, apellidoEvaluado, idEvaluador, nombreEvaluador)
Donde
   - Cada evaluacion pertenece a una única persona, y es realizada por diversos evaluadores.
   - Un evaluador, realiza muchas evaluaciones
   - El legajo identifica a una persona unívocamente.
   - el dni identifica a una persona unívocamente
   - Una evaluacion se realiza en una única fecha y en una fecha se realizan diversas evaluaciones
   - Cada evaluacion pertenece a una única persona y una persona es evaluada muchas veces

Concursos
----------

14. CONCURSOS (idConcurso, idParticipante, idCategoria, descripcionCategoria, nombreConcurso, fechaInicio,
responsableConcurso )
Donde
   - En un concurso hay muchos participantes y un participante participa en muchos concursos
   - Dentro de un concurso, un participante participa en una sola categoría.
   - Cada categoría pertenece a un solo concurso, y de ella se conoce una descripcion. El idCategoría es único
    en el sistema.
   - De un concurso se conoce el nombre, fecha de inicio y su responsable.

Paciente
---------

15. PACIENTE (dni, nYAp, medicoQueLoAtiende, #HistoriaClinica)
Donde
   - #HistoriaClinica es única por paciente y a un paciente lo atienden varios médicos.
   - Una historia clínica es realizada por varios médicos.
   - medicoQueLoAtiende es una lista de medicos que atienden al paciente.

Concesionaria
--------------

16. CONCESIONARIA ( idConcesionaria, nombreConcesionaria, responsableConcesionaria, idAuto, marcaAuto,
modeloAuto, colorAuto, idVendedor, nombreVendedor, fechaNacVendedor, fechaIngresoVendedor)
Donde
   - El id Concesionaria es único por concesionaria.
   - El nombre de concesionaria puede repetirse para varios idConcesionaria
   - Cada concesionaria tiene muchos responsables y un responsable de concesionaria puede figurar en varias
   concesionarias.
   - El idVendedor es un identificador único en el sistema. El idVendedor no se repite en diferentes concesionarias.
   Un vendedor trabaja para varias concesionarias y en una concesionaria trabajan muchos vendedores.
   - fechaIngresoVendedor es la fecha en la que un vendedor ingreso a trabajar en una concesionaria
   - El idAuto es un identificador único que cada concesionaria le da a un auto. El idAuto se repite en diferentes
   concesionarias

Estadia
--------

17. ESTADIA (dniCliente, codHotel, cantidadHabitaciones, direccionHotel, ciudadHotel, dniGerente,
nombreGerente, nombreCliente, ciudadCliente, fechaInicioHospedaje, cantDiasHospedaje, #Habitacion,
servicioHabitacion)
Donde
   - servicioHabitacion es un servicio solicitado por un cliente durante una estadía para que sea entregado en su
   habitacion. Un cliente puede solicitar muchos servicios en la misma estadía.
   - Existe un único gerente por hotel.Un gerente podría gerenciar mas de un hotel.
   - Un cliente puede realizar la estadía sobre mas de una habitacion del hotel en la misma fecha. Para cada
   habitacion puede reservar diferentes cantidades de días.
   - cantidadHabitaciones indica la cantidad de habitaciones existentes en un hotel.
   - El codigo de hotel (codHotel) es único y no puede repetirse en diferentes ciudades.
   - Un cliente puede realizar reservas en diferentes hoteles para la misma fecha.
   - #Habitacion se puede repetir en distintos hoteles.
   - En la misma direccionHotel de una ciudadHotel no puede haber mas de un hotel funcionando

Exposicion
-----------

18. EXPOSICION (museo, ciudadMuseo, nombreGaleria, nombreObra, añoCreacion, autorObra, precioEntrada)
Donde
   - Cada museo se encuentra en una ciudad (ciudadMuseo), pero en una ciudad puede haber muchos museos.
   - En cada museo, hay muchas galerías donde se exponen obras. El nombre de las galerías (nombreGaleria)
   pueden repetirse en diferentes museos, no se repiten en un mismo museo.
   - Cada obra tiene un solo año de creacion, pero en un año pueden haberse creado varias obras.
   - Una obra tiene muchos autores.
   - El nombre para cada obra es único por obra.
   - Cada museo cobra un precio distinto (precioEntrada) por cada galería visitada

Infracciones realizadas
------------------------

19. INFRACCIONES_REALIZADAS (idAuto, modeloAuto, #seguroActual, fechaVencimientoSeguroActual,
empresaSeguroActual, idPropietario, idInfraccion, fechaInfraccion, tipoInfraccion)
Donde
  - un auto tiene mas de un seguro actual
  - un seguro no puede pertenecer a mas de un auto
  - un auto puede tener mas de un propietario y un propietario puede tener mas de un auto
  - un auto tiene muchas infracciones pero una infraccion se libra sobre un solo auto
  - para cada seguro se registran todos los propietarios del auto que se asegura, la fecha de vencimiento del mismo
   y la empresa aseguradora. El #seguroActual no se repite para diferentes empresas de seguro.
