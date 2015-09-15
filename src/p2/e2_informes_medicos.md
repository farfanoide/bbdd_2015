Informe Medico
--------------

    INFORME_MEDICO (
      idMedico, apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM,
      idPaciente, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP,
      idObraSoc, nroAfiliado, nombreOS, direccionOS, teléfonoOS,
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

Dependencias Funcionales
------------------------

DF1: _idMedico_ -> apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM
DF2: idObraSoc -> nombreOS, direccionOS, teléfonoOS,
DF3: _idPaciente_ -> apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, idObraSoc, nroAfiliado
DF4: idorgano -> descripcion,
DF5: idEstudio -> idMedico, idPaciente, idOrgano, resultado, fechaEstudio, informe

> informe se lo adjudicamos al estudio, pero no esta especificado en ningun lado

Claves Candidatas
-----------------
CC: (idEstudio)

Normalizacion
-------------

La tabla INFORME_MEDICO no esta en BCNF porque `idMedico` no es superclave de
`INFORME_MEDICO`.

_IM1_:  (_idMedico_, apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM)
IM2: `INFORME_MEDICO` - {apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM}
IM2: (
 _idMedico_, idPaciente, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, idObraSoc, nroAfiliado, nombreOS, direccionOS, teléfonoOS, idorgano, descripcion, idEstudio, resultado, fechaEstudio, informe)



`IM1` esta en BCNF porque `idMedico` es superclave de `IM1`
`IM2` no esta en BCNF porq `idObraSoc` no es superclave de `IM2`

_IM3_: (_idObraSoc_, nombreOS, direccionOS, teléfonoOS,)
IM4: `IM2` - {nombreOS, direccionOS, teléfonoOS}
IM4: (
)

`IM3` esta en BCNF porque `idMarca` es superclave de `IM3`
`IM4` no esta en BCNF porq `idModelo` no es superclave de `IM4`

_IM5_: (_idMarca_, _idModelo_, nombreModelo, añoInicioFabricacion, añoFinFabricacion, idPais)
IM6: `IM4` - {nombreModelo, añoInicioFabricacion, añoFinFabricacion, idPais}
_IM6_: (_idModelo_, _idMarca_, _idRepuesto_, descripción, precio)

`IM5` esta en BCNF porque `idMarca` e `idModelo` son superclaves de `IM5`
`IM6` esta en BCNF porque `idRepuesto`, `idMarca` e `idModelo` es superclave
de `IM6`

