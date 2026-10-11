# Lenguaje de programación con sintaxis española

Proyecto experimental para expresar instrucciones de programación mediante una sintaxis en español. Su objetivo es reducir la barrera entre una idea y su implementación; no elimina la necesidad de diseñar la lógica del programa.

## Estado comprobable

- Incluye un lexer, un frontend AST, un compilador escalar y una máquina virtual en binarios para Linux x86-64.
- El subconjunto compilable descrito permite expresiones aritméticas I64/F64 y asignaciones, con inspección del AST y validación semántica.
- La salida del compilador es bytecode IL v2 para una VM; no es código máquina de CPU.
- La sintaxis de datos/modelos AI puede validarse en un subconjunto estático; el runtime no ejecuta tensores, capas ni entrenamiento.
- La implementación fuente C y ensamblador no está incluida: se distribuyen artefactos nativos precompilados.
- Los binarios publicados son específicos de Linux x86-64; no hay build verificado para Android/Termux ni otras arquitecturas.

## Prueba rápida en Linux x86-64

Desde la raíz del repositorio:

```sh
chmod +x arino_ast_compiler arino_ast_compiler_scalar arino_vm
printf '%s' 'sumar 2 y 3' > suma.ari
./arino_ast_compiler --ast suma.ari
./arino_ast_compiler --check suma.ari
./arino_ast_compiler --compile suma.ari suma.arino
./arino_vm --verify suma.arino
./arino_vm --run suma.arino
```

`--compile` genera bytecode; `--verify` revisa su estructura y `--run` lo ejecuta en la VM. Los identificadores de artefactos y ejemplos se conservan para que los comandos correspondan a los archivos distribuidos.

## Pruebas y documentación técnica

La acción de integración continua comprueba los binarios ELF x86-64, las pruebas del lexer, la compilación y ejecución de fixtures IL v1/v2, y errores de validación del frontend. Las especificaciones detalladas permanecen en `docs/`; los identificadores internos y nombres de artefactos se conservan para mantener la documentación técnica alineada con los archivos.

## Límites

No es un compilador integral del lenguaje descrito: el frontend no compila bloques, ámbitos anidados, condiciones, bucles ni funciones de uso general. La validación AI no equivale a inferencia o entrenamiento. No se publican fuentes para reconstruir los binarios ni resultados de benchmarks que permitan afirmar rendimiento superior.
