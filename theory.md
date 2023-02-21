# How to generate a copy generator vertex in Blender.

    Al hablar de nodos, al añadir, y unir vamos a seguir la siguiente regla.

        - A: Add    --> Añadir new nodo
        - I: In     --> Entrada al nodo
        - O: Out    --> Salida del nodo

## Generando con geometry nodes.

Vamos a generar un matrix copy de objetos sobre un face de una mesh. Para ello vamos a hacer lo siguiente:

1. Generamos un nuevo **geometry_node** sobre un objeto (por ejemplo un rectangulo). (Creamos el rectangulo y le añadimos un modificador "_geometry_node_") 

2. Añadimos al graph los dos objetos que queremos clonar (el cloner, y el objeto a clonar).

3. Añadimos nodo --> Instance_to_points. Unimos el 