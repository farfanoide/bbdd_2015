Informe Medico
==============

Dependencias Funcionales
------------------------

```
DF1: _idMedico_ -> apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM
DF2: _idObraSoc_ -> nombreOS, direccionOS, teléfonoOS,
DF3: _idPaciente_ -> apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, idObraSoc, nroAfiliado
DF4: idorgano -> descripcion,
DF5: idEstudio -> idMedico, idPaciente, idOrgano, resultado, fechaEstudio, informe
```

Claves Candidatas
-----------------
```
CC: (idEstudio)
```

Normalizacion
-------------

La tabla `INFORME_MEDICO` no esta en BCNF porque `idMedico` no es superclave de
`INFORME_MEDICO`.

```
IM1:  (_idMedico_, apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM)
```
```
IM2: `INFORME_MEDICO` - {apynMedico, tipoDocM, nroDocM, fechaNacM, matricula,
direccionM, teléfonoM}
IM2: (
  idMedico,
  idPaciente, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP,
  idObraSoc, nroAfiliado, nombreOS, direccionOS, teléfonoOS,
  idorgano, descripcion,
  _idEstudio_, resultado, fechaEstudio, informe
)
```

- `IM1` esta en BCNF porque `idMedico` es superclave de `IM1`
- `IM2` no esta en BCNF porq `idObraSoc` no es superclave de `IM2`

```
IM3: (_idObraSoc_, nombreOS, direccionOS, teléfonoOS,)
```
```
IM4: `IM2` - {nombreOS, direccionOS, teléfonoOS}
IM4: (
  idMedico,
  idPaciente, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, nroAfiliado,
  idObraSoc,
  idorgano, descripcion,
  _idEstudio_, resultado, fechaEstudio, informe
)
```

- `IM3` esta en BCNF porque `idObraSoc` es superclave de `IM3`
- `IM4` no esta en BCNF porq `idPaciente` no es superclave de `IM4`

```
IM5: (_idPaciente_, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, idObraSoc, nroAfiliado)
```
```
IM6: `IM4` - {apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, idObraSoc, nroAfiliado}
IM6: (
  idMedico,
  idPaciente,
  idorgano, descripcion,
  _idEstudio_, resultado, fechaEstudio, informe
)
```

- `IM5` esta en BCNF porque `idPaciente` es superclave de `IM5`
- `IM6` no esta en BCNF porq `idOrgano` no es superclave de `IM6`

```
IM7: (_idorgano_, descripcion)
```
```
IM8: `IM6` - {descripcion}
IM8: (_idEstudio_, resultado, fechaEstudio, informe, idorgano, idPaciente, idMedico)
```

- `IM7` esta en BCNF porque `idOrgano` es superclave de `IM7`
- `IM8` esta en BCNF porque `idEstudio` es superclave de `IM8`

Tablas Resultantes:
-------------------

```
IM1:  (_idMedico_, apynMedico, tipoDocM, nroDocM, fechaNacM, matricula, direccionM, teléfonoM)
IM3: (_idObraSoc_, nombreOS, direccionOS, teléfonoOS,)
IM5: (_idPaciente_, apynPaciente, tipoDocP, nroDocP, fechaNacP, direccionP, teléfonoP, idObraSoc, nroAfiliado)
IM7: (_idorgano_, descripcion)
IM8: (_idEstudio_, resultado, fechaEstudio, informe, idorgano, idPaciente, idMedico)
```
