## PROYECTO - MANEJO DE RESERVAS DE UN AVIÓN

PRESENTADO POR: LERMA ALDANA MARIO GERLEY



<p align="center">
  <img src="https://user-images.githubusercontent.com/114120562/236731932-043b5941-e603-4c03-aab6-c5c100aee23c.gif">
</p>


Se quiere crear un programa que tenga como objetivo el manejo de reservas de un avión. Este avión cuenta con un número fijo de 50 sillas. De ellas, 8 son de clase ejecutiva, mientras que el resto son de clase económica. Cada silla puede ser asignada a un pasajero que cuenta con un nombre y una cédula. Este último dato es la entrada principal para poder consultar una reserva o eliminarla del sistema. Cuando se asigna una silla es necesario conocer las preferencias del usuario. Este puede elegir la posición de la silla, ventana, pasillo o centro, y la clase, ejecutiva o económica. En el caso especial de las sillas ejecutivas, solo es posible elegir las posiciones: ventana o pasillo. Las sillas son asignadas de forma secuencial según su ubicación y su clase. De igual forma, el programa permite buscar la reserva de un pasajero y visualizar los datos de la reserva.

El programa debe permitir al usuario:

1. Asignar una silla a un pasajero
2. Consultar una reserva
3. Eliminar reserva
4. Buscar pasajero
5. Calcular el porcentaje de ocupación del avión.
6. Consultar el valor total de ventas por concepto de sillas ocupadas en el avión.
7. Consultar el valor promedio de venta por concepto de sillas ocupadas / pasajero en el avión.

## 1. PLANTEAMIENTO:
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


## 2. CODIGO C++:
                 #include <iostream>
        #include <string>
        using namespace std;

        struct Pasajero {
            string nombre;
            string cedula;
        };

        struct Silla {
            bool ocupada;
            Pasajero pasajero;
            string posicion;
            string clase;
        };

        const int NUM_SILLAS = 50;
        const int NUM_EJECUTIVAS = 8;
        const int NUM_ECONOMICAS = NUM_SILLAS - NUM_EJECUTIVAS;
        Silla sillas[NUM_SILLAS];

        void asignarSilla() {
            string nombre, cedula, posicion, clase;
            int numSilla = -1;
            bool sillaValida = false;
            while (!sillaValida) {
                cout << "Ingrese el número de silla (1-50): ";
                cin >> numSilla;
                if (numSilla < 1 || numSilla > NUM_SILLAS) {
                    cout << "Número de silla inválido. Intente de nuevo." << endl;
                } else if (sillas[numSilla-1].ocupada) {
                    cout << "La silla ya está ocupada. Intente de nuevo." << endl;
                } else {
                    sillaValida = true;
                }
            }
            cout << "Ingrese el nombre del pasajero: ";
            cin >> nombre;
            cout << "Ingrese la cédula del pasajero: ";
            cin >> cedula;
            bool posicionValida = false;
            while (!posicionValida) {
                cout << "Ingrese la posición de la silla (ventana, pasillo, centro): ";
                cin >> posicion;
                if (posicion != "ventana" && posicion != "pasillo" && posicion != "centro") {
                    cout << "Posición inválida. Intente de nuevo." << endl;
                } else if (sillas[numSilla-1].clase == "ejecutiva" && posicion == "centro") {
                    cout << "No se puede asignar una silla en el centro de una clase ejecutiva. Intente de nuevo." << endl;
                } else {
                    posicionValida = true;
                }
            }
            bool claseValida = false;
            while (!claseValida) {
                cout << "Ingrese la clase de la silla (ejecutiva, económica): ";
                cin >> clase;
                if (clase != "ejecutiva" && clase != "económica") {
                    cout << "Clase inválida. Intente de nuevo." << endl;
                } else if (clase == "ejecutiva" && (posicion == "centro" || posicion == "ventana")) {
                    cout << "Solo se pueden asignar sillas en el pasillo de la clase ejecutiva. Intente de nuevo." << endl;
                } else {
                    claseValida = true;
                }
            }
            sillas[numSilla-1].ocupada = true;
            sillas[numSilla-1].pasajero.nombre = nombre;
            sillas[numSilla-1].pasajero.cedula = cedula;
            sillas[numSilla-1].posicion = posicion;
            sillas[numSilla-1].clase = clase;
            cout << "Silla asignada exitosamente." << endl;
        }

        void consultarReserva() {
            string cedula;
            cout << "Ingrese la cédula del pasajero: ";
            cin >> cedula;
            bool reservaEncontrada = false;
            for (int i = 0; i < NUM_SILLAS; i++) {
                if (sillas[i].ocupada && sillas[i].pasajero.cedula == cedula) {
                    cout << "Reserva encontrada:" << endl;
                    cout << "Silla: " << i+1 << endl;
                    cout << "Nombre: " << sillas[i].pasajero.nombre << endl;
                    cout << "Cédula: " << sillas[i].pasajero.cedula << endl;
                    cout << "Posición: " << sillas[i].posicion << endl;
                    cout << "Clase: " << sillas[i].clase << endl;
                    reservaEncontrada = true;
                    break;
                }
            }
            if (!reservaEncontrada) {
                cout << "No se encontró ninguna reserva con esa cédula." << endl;
            }
        }

        void eliminarReserva() {
            string cedula;
            cout << "Ingrese la cédula del pasajero: ";
            cin >> cedula;
            bool reservaEncontrada = false;
            for (int i = 0; i < NUM_SILLAS; i++) {
                if (sillas[i].ocupada && sillas[i].pasajero.cedula == cedula) {
                    sillas[i].ocupada = false;
                    sillas[i].pasajero.nombre = "";
                    sillas[i].pasajero.cedula = "";
                    sillas[i].posicion = "";
                    sillas[i].clase = "";
                    cout << "Reserva eliminada exitosamente." << endl;
                    reservaEncontrada = true;
                    break;
                }
            }
            if (!reservaEncontrada) {
                cout << "No se encontró ninguna reserva con esa cédula." << endl;
            }
        }

        void buscarPasajero() {
            string nombre;
            cout << "Ingrese el nombre del pasajero: ";
            cin >> nombre;
            bool pasajeroEncontrado = false;
            for (int i = 0; i < NUM_SILLAS; i++) {
                if (sillas[i].ocupada && sillas[i].pasajero.nombre == nombre) {
                    cout << "Reserva encontrada:" << endl;
                    cout << "Silla: " << i+1 << endl;
                    cout << "Nombre: " << sillas[i].pasajero.nombre << endl;
                    cout << "Cédula: " << sillas[i].pasajero.cedula << endl;
                    cout << "Posición: " << sillas[i].posicion << endl;
                    cout << "Clase: " << sillas[i].clase << endl;
                    pasajeroEncontrado = true;
                }
            }
            if (!pasajeroEncontrado) {
                cout << "No se encontró ninguna reserva con ese nombre." << endl;
            }
        }

        void calcularPorcentajeOcupacion() {
            int numOcupadas = 0;
            for (int i = 0; i < NUM_SILLAS; i++) {
                if (sillas[i].ocupada) {
                    numOcupadas++;
                }
            }
            double porcentajeOcupacion = (double)numOcupadas / NUM_SILLAS * 100;
            cout << "Porcentaje de ocupación del avión: " << porcentajeOcupacion << "%" << endl;
        }

        void consultarValorVentas() {
            int valorTotal = 0;
            for (int i = 0; i < NUM_SILLAS; i++) {
                if (sillas[i].ocupada) {
                    if (sillas[i].clase == "ejecutiva") {
                        valorTotal += 500;
                    } else {
                        valorTotal += 200;
                    }
                }
            }
            cout << "Valor total de ventas por concepto de sillas ocupadas en el avión: $" << valorTotal << endl;
        }

        void consultarValorPromedio() {
            int valorTotal = 0;
            int numOcupadas = 0;
            for (int i = 0; i < NUM_SILLAS; i++) {
                if (sillas[i].ocupada) {
                    if (sillas[i].clase == "ejecutiva") {
                        valorTotal += 500;
                    } else {
                        valorTotal += 200;
                    }
                    numOcupadas++;
                }
            }
            double valorPromedio = (double)valorTotal / numOcupadas;
            cout << "Valor promedio de venta por concepto de sillas ocupadas / pasajero en el avión: $" << valorPromedio << endl;
        }

        int main() {
            for (int i = 0; i < NUM_SILLAS; i++) {
                sillas[i].ocupada = false;
                sillas[i].pasajero.nombre = "";
                sillas[i].pasajero.cedula = "";
                if (i < NUM_EJECUTIVAS) {
                    sillas[i].posicion = "pasillo";
                    sillas[i].clase = "ejecutiva";
                } else {
                    sillas[i].posicion = "";
                    sillas[i].clase = "económica";
                }
            }
            int opcion = 0;
            while (opcion != 8) {
                cout << endl;
                cout << "Menú de opciones:" << endl;
                cout << "1. Asignar una silla a un pasajero" << endl;
                cout << "2. Consultar una reserva" << endl;
                cout << "3. Eliminar reserva" << endl;
                cout << "4. Buscar pasajero" << endl;
                cout << "5. Calcular el porcentaje de ocupación del avión" << endl;
                cout << "6. Consultar el valor total de ventas por concepto de sillas ocupadas en el avión" << endl;
                cout << "7. Consultar el valor promedio de venta por concepto de sillas ocupadas / pasajero en el avión" << endl;
                cout << "8. Salir" << endl;
                cout << "Ingrese una opción: ";
                cin >> opcion;
                switch (opcion) {
                    case 1:
                        asignarSilla();
                        break;
                    case 2:
                        consultarReserva();
                        break;
                    case 3:
                        eliminarReserva();
                        break;
                    case 4:
                        buscarPasajero();
                        break;
                    case 5:
                        calcularPorcentajeOcupacion();
                        break;
                    case 6:
                        consultarValorVentas();
                        break;
                    case 7:
                        consultarValorPromedio();
                        break;
                    case 8:
                        cout << "Saliendo del programa..." << endl;
                        break;
                    default:
                        cout << "Opción inválida. Intente de nuevo." << endl;
                        break;
                }
            }
            return 0;
        }

## 3. RESULTADO:

<p align="center">
<img src="https://user-images.githubusercontent.com/114120562/236732332-6326d83b-d426-46f1-9d3b-a09540808236.jpg">
</p>


