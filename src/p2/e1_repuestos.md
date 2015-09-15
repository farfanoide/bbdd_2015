Dependencias Funcionales
------------------------

```
DF1: (idPais) -> nombrePais
DF2: (idMarca) -> nombreMarca
DF3: (idMarca, idModelo) -> nombreModelo, añoInicioFabricacion, añoFinFabricacion, idPais
DF4: (idRepuesto) -> descripcion, precio, idMarca, idModelo
```

Claves Candidatas
-----------------

```
CC: idRepuesto
```

Normalizacion
-------------

- La tabla `REPUESTO` no esta en BCNF porque `idPais` no es superclave de
`REPUESTO`.

```
R1: (_idPais_, nombrePais)
```
```
R2: REPUESTO - {nombrePais}
R2: (
  _idRepuesto_, descripcion, precio
  idMarca, nombreMarca,
  idModelo, nombreModelo, añoInicioFabricacion, añoFinFabricacion,
  idPais,
)
```

- `R1` esta en BCNF porque `idPais` es superclave de `R1`
- `R2` no esta en BCNF porq `idMarca` no es superclave de `R2`

```
R3: (_idMarca_, nombreMarca)
```
```
R4: `R2` - {nombreMarca}
R4: (
 _idRepuesto_, descripcion, precio
 idMarca,
 idModelo, nombreModelo, añoInicioFabricacion, añoFinFabricacion,
 idPais,
)
```

- `R3` esta en BCNF porque `idMarca` es superclave de `R3`
- `R4` no esta en BCNF porq `idModelo` no es superclave de `R4`

```
R5: (_idMarca_, _idModelo_, nombreModelo, añoInicioFabricacion, añoFinFabricacion, idPais)
```
```
R6: `R4` - {nombreModelo, añoInicioFabricacion, añoFinFabricacion, idPais}
R6: (idModelo, idMarca, _idRepuesto_, descripcion, precio)
```

- `R5` esta en BCNF porque `idMarca` e `idModelo` son superclaves de `R5`
- `R6` esta en BCNF porque `idRepuesto` es superclave de `R6`

Tablas Resultantes:
-------------------

```
R1: (_idPais_, nombrePais)
R3: (_idMarca_, nombreMarca)
R5: (_idMarca_, _idModelo_, nombreModelo, añoInicioFabricacion, añoFinFabricacion, idPais)
R6: (idModelo, idMarca, _idRepuesto_, descripcion, precio)
```
