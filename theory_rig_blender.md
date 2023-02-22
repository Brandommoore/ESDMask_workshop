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

    -- Hacer lo mismo por cada unpack (Colocar uno debajo del otro) --

        1. x2 A: [Exponential Smoothing] (Colocar uno debajo del otro)
        2. [Unpack] O: x --> [TOP Exponential Smoothing] I: Input | Damping (**valor_indicado_abajo**)
        3. [Unpack] O: y --> [BOTTOM Exponential Smoothing] I: Input | Damping (**valor_indicado_abajo**)
        4. A: [Pack]
        5. [TOP Exponential Smoothing] O: Output --> [Pack] I: Z Value
        6. [BOTTOM Exponential Smoothing] O: Output --> [Pack] I: X Value

        === Damping: 1º group --> Value = 200 / 1º group --> Value = 90 ===

    -- Cuando acabamos estos dos grupos identicos --

        1. A: [Substract] (Vec3)
        2. [TOP Pack (Group)] O: Out --> [Substract] I: First Value
        3. [BOTTOM Pack (Group)] O: Out --> [Substract] I: Second Value
        4. A: [Multiply] (Vec3)
        5. [Substract] O: Out --> [Multiply] I: First Value (Multiply value = 3) 

    -- Al tener todo este flujo, extraemos las rotaciones de cada bone y las unimos al [Multiply] OUT --