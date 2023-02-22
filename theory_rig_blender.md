# Rigging on blender

Basicamente unos shorcuts esenciales.

Para crear un rig necesitamos:
1. Añadir un objeto armature
2. Creamos los bones
3. Cuando esten creados, usamos el comando [Cntrl + P] y seleccionamos con influencias automaticas

## Creando pendientes

Creamos los pendientes (modelamos) y cuando esten creados (importados) hacemos lo siguiente:
1. Añadimos armature
2. El primer hueso lo rotamos 180º
3. Escalamos los huesos hasta el final del modelo. (Tener en cuenta juntas)
4. Linkamos huesos a mesh. Para ello: [Cntrl + P] y seleccionamos con influencias automaticas
5. Nos vamos a pose-mode y probamos que el rig funciona
6. Exportamos

## Physics in Spark

Una vez importado el objeto seguimos la siguiente estructura de nodos.

    Leyenda de creacion y union de nodos
        - A: Add
        - I: In
        - O: Out

        [Face Finder] O: Faces --> [Face Select] I: Faces

Para añadir fisicas (emuladas) al objeto, seguimos el siquiente esquema:

    0. Añadimos el Face_tracker al patch editor

    1. A: x2 [Unpack]
    2. [Face Tracker] O: 3D Rotation --> [Unpack] I: Value

    -- Hacer lo mismo por cada unpack --

        1. x2 A: [Exponential Smoothing] (Colocar uno debajo del otro)
        2. [Unpack] O: x --> [TOP Exponential Smoothing] I: Input | Damping (**valor_indicado_abajo**) 
        2. [Unpack] O: y --> [BOTTOM Exponential Smoothing] I: Input | Damping (**valor_indicado_abajo**) 