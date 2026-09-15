# TSPTW_results

Datos y resultados computacionales asociados al artículo **“Capturing the
logic of time windows: a dual-based path inequality approach”**, de Jorge
Riera-Ledesma e Inmaculada Rodríguez-Martín.

El repositorio contiene las instancias del Traveling Salesman Problem with
Time Windows (TSPTW), las soluciones utilizadas como cotas superiores
iniciales y los resultados de las ejecuciones del algoritmo branch-and-cut
descrito en el artículo. El material corresponde a los experimentos de la
sección **7. Computational study**.

## Contenido

```text
input/
├── instances/    Instancias TSPTW
└── UB/            Soluciones usadas para inicializar la cota superior

output/
├── No_UB/         Ejecuciones sin cota superior inicial
├── BH_UB/         Ejecuciones con la cota de la heurística básica
└── BK_UB/         Ejecuciones con la mejor cota superior conocida
```

Las carpetas de `input/UB` y `output/` están organizadas por familia de
instancias. Entre las familias distribuidas se encuentran `AFG`, `Dumas`,
`GendreauDumasExtended`, `Langevin`, `OhlmannThomas`, `SolomonPesant` y
`SolomonPotvinBengio`. Algunas cotas superiores también incluyen la familia
`da_Silva_Urrutia`.

## Instancias

Los ficheros de `input/instances/<familia>/` son las instancias originales de
los benchmarks TSPTW. Se conservan sus nombres y extensiones de origen, por
ejemplo:

```text
input/instances/AFG/rbg016b.tw
input/instances/Dumas/n100w20.001.txt
```

Los nombres suelen codificar la familia, el número de vértices, la anchura de
la ventana temporal u otras características definidas por los autores del
benchmark. Para conocer el formato exacto de cada familia debe consultarse la
documentación de su fuente original.

## Cotas superiores iniciales

En `input/UB/` se almacenan soluciones factibles en formato `.sol`. La misma
instancia puede disponer de una solución en una o ambas configuraciones:

- `BH_UB`: solución obtenida mediante la heurística básica descrita en la
	sección 6.2 del artículo.
- `BK_UB`: mejor solución factible conocida utilizada para inicializar el
	solver.

La configuración `No_UB` no necesita ficheros en `input/UB`, ya que la
ejecución comienza sin proporcionar un incumbente inicial.

## Resultados

Cada carpeta de `output/` corresponde a una configuración experimental y está
organizada por familia. Los resultados pueden incluir:

- ficheros `.log`, con el registro de CPLEX y de la búsqueda branch-and-cut;
- ficheros `.sol`, con las soluciones factibles encontradas durante la
	ejecución;
- otros ficheros auxiliares generados por la ejecución, cuando están
	disponibles.

La nomenclatura de los ficheros permite asociar cada salida con la instancia
correspondiente. Por ejemplo, los resultados de `n200w120.001.txt` bajo la
configuración `BH_UB` se encuentran dentro de `output/BH_UB/OhlmannThomas/`.

## Configuraciones experimentales

Las tres configuraciones permiten reproducir la comparación de la tabla 2 del
artículo:

| Configuración | Cota superior inicial | Propósito |
| --- | --- | --- |
| `No_UB` | Ninguna | Medir el comportamiento sin incumbente inicial |
| `BH_UB` | Heurística básica | Evaluar la configuración recomendada por el algoritmo |
| `BK_UB` | Mejor solución conocida | Medir el efecto de una cota superior idealizada |

En el estudio publicado, `BH_UB` y `BK_UB` resolvieron 248 de 261 instancias
(95,0 %), mientras que `No_UB` resolvió 243 (93,1 %). Estos valores son los
reportados en el artículo y sirven como referencia para comprobar una nueva
ejecución.

## Entorno experimental

El artículo informa de las siguientes condiciones de ejecución:

- Ubuntu 24.04 LTS;
- Intel Core i5-7500, un único núcleo;
- 20 GB de RAM;
- CPLEX 22.1 mediante Callable Library;
- compilación con `gcc 13.3.0` y `-O2`;
- límite de tiempo de 10.800 segundos por instancia, salvo indicación
	contraria.

Este repositorio contiene los datos y las salidas experimentales, pero no
incluye el código fuente del algoritmo branch-and-cut ni CPLEX. Para ejecutar
de nuevo el algoritmo se necesita disponer de una implementación compatible y
de una licencia de CPLEX.

## Referencia

J. Riera-Ledesma and I. Rodríguez-Martín, *Capturing the logic of time
windows: a dual-based path inequality approach*, 2026.

Los detalles matemáticos del verificador temporal, los certificados de Farkas,
las desigualdades iPEC y sus fortalecimientos tournament, fixed-endpoint e
híbrido se encuentran en el artículo asociado.

## Licencia

El contenido de este repositorio se distribuye bajo [CC0 1.0
Universal](LICENSE), salvo que se indique expresamente lo contrario para
algún fichero procedente de una fuente externa.
