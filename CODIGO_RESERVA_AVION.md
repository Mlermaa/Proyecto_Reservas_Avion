## PROYECTO - MANEJO DE RESERVAS DE UN AVIÓN

PRESENTADO POR: LERMA ALDANA MARIO GERLEY

Se quiere crear un programa que tenga como objetivo el manejo de reservas de un avión. Este avión cuenta con un número fijo de 50 sillas. De ellas, 8 son de clase ejecutiva, mientras que el resto son de clase económica. Cada silla puede ser asignada a un pasajero que cuenta con un nombre y una cédula. Este último dato es la entrada principal para poder consultar una reserva o eliminarla del sistema. Cuando se asigna una silla es necesario conocer las preferencias del usuario. Este puede elegir la posición de la silla, ventana, pasillo o centro, y la clase, ejecutiva o económica. En el caso especial de las sillas ejecutivas, solo es posible elegir las posiciones: ventana o pasillo. Las sillas son asignadas de forma secuencial según su ubicación y su clase. De igual forma, el programa permite buscar la reserva de un pasajero y visualizar los datos de la reserva.

El programa debe permitir al usuario:

1. Asignar una silla a un pasajero
2. Consultar una reserva
3. Eliminar reserva
4. Buscar pasajero
5. Calcular el porcentaje de ocupación del avión.
6. Consultar el valor total de ventas por concepto de sillas ocupadas en el avión.
7. Consultar el valor promedio de venta por concepto de sillas ocupadas / pasajero en el avión.

## PLANTEAMIENTO:
Para comenzar, crea una estructura para representar cada silla del avión, que contenga la siguiente información: número de silla, clase (ejecutiva o económica), posición (ventana, pasillo o centro), estado (disponible o asignada), pasajero (nombre y cédula). Además, se podría crear una matriz para representar las 50 sillas del avión, donde cada fila represente una silla, y cada columna represente uno de los atributos mencionados anteriormente.

Crea un menú menú de opciones que permita al usuario interactuar con el programa de la siguiente manera:

1.	Asignar una silla a un pasajero:

        •	Pedir al usuario que ingrese el número de la silla.

        •	Ingresar el nombre del pasajero.

        •	Ingresar la cedula del pasajero.

        •	Ingrese la posición de la silla (ventana, pasillo, centro).

        •	Ingresar la clase de la silla (Ejecutiva o Económica).
      

2.	Consultar una reserva:

        •	Pedir al usuario que ingrese el número de cédula del pasajero.
        
        •	Buscar en la matriz la silla que corresponde al pasajero, y mostrar su información.
        

3.	Eliminar reserva:

        •	Pedir al usuario que ingrese el número de cédula del pasajero.
        
        •	Buscar en la matriz la silla que corresponde al pasajero, cambiar su estado a "disponible", y borrar la información del pasajero.
        

4.	Buscar pasajero:

        •	Pedir al usuario que ingrese el nombre del pasajero.
        
        •	Buscar en la matriz la silla que corresponde al pasajero, y mostrar su información.
        

5.	Calcular el porcentaje de ocupación del avión:

        •	Recorrer la matriz de sillas contando las sillas asignadas, y calcular el porcentaje de ocupación del avión.
        

6.	Consultar el valor total de ventas por concepto de sillas ocupadas en el avión:

        •	Recorrer la matriz de sillas sumando el costo de la silla (dependiendo de la clase) para todas las sillas asignadas.
        

8.	Salir del programa.
