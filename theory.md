# How to generate a copy generator vertex in Blender.

    HELPER!
    
    Al hablar de nodos, al añadir, y unir vamos a seguir la siguiente regla.

        - A: Add    --> Añadir new nodo
        - I: In     --> Entrada al nodo
        - O: Out    --> Salida del nodo

    Ejemplo:

    Para decir que hay que unir la propiedad location del nodo de la esfera a la propiedad geometry del nodo group geometry, lo hariamos de este modo:

        [Sphere] O: Location --> [Group geometry] I: Geometry

## Generando con geometry nodes.

Vamos a generar un matrix copy de objetos sobre un face de una mesh. Para ello vamos a hacer lo siguiente:

1. Generamos un nuevo **geometry_node** sobre un objeto (por ejemplo un rectangulo). (Creamos el rectangulo y le añadimos un modificador "_geometry_node_") 

2. Añadimos al graph los dos objetos que queremos clonar (el cloner [Cloner], y el objeto a clonar [OClo]).

3. A: Instance_on_Points.
    1. [Cloner] O: Geometry --> [Instance_on_Points] I: Points
    2. [OClo] O: Geometry --> [Instance_on_Points] I: Instance
    3. [Oclo] Original -> Relative

4. A: Normal
5. A: Align_Euler_to_Vector
    1. [Normal] O: Normal --> [Align_Euler_to_Vector] I: Vector
    2. [Align_Euler_to_Vector] O: Rotation --> [Instance_on_Points] I: Rotation





> Respecto al video:

> Cloning cube es el objeto a clonar

> Sphere es el cloner