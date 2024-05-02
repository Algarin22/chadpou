#include <iostream>
#include <stdlib.h>
#include <string>
#include <fstream>
#include <time.h>
#include <Windows.h>

using namespace std;

int monedas = 0;
time_t ultimaComida;
time_t ultimaJugada;
time_t tiempoNecesidades;
bool necesitaLimpiar = false;
string nombre;

void dormido()
{
    string text;
    ifstream archivo("MuñecoDormido.txt");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
}

void Feliz()
{
    string text;
    ifstream archivo("muñecofeliz.txt");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
}

void comida()
{
    const char* comida[5] = { "Arroz", "Guineo", "Manzana", "Habichuela", "Agua" };
    int precios[5] = { 20, 12, 15, 5, 3 };
    cout << "Cantidad de monedas que tiene: " << monedas << endl;
    cout << "Lista de alimentos:" << endl;
    for (int i = 0; i < 5; i++)
    {
        cout << i + 1 << ". " << comida[i] << " - " << precios[i] << " monedas" << endl;
    }

    int opcion;
    cout << "Seleccione el alimento que desea comprar: ";
    cin >> opcion;
    opcion--;

    if (opcion >= 0 && opcion < 5)
    {
        if (monedas >= precios[opcion])
        {
            monedas -= precios[opcion];
            cout << "Has comprado " << comida[opcion] << ". Ahora tienes " << monedas << " monedas restantes." << endl;
            cout << "Tu chadpou ya no tiene hambre." << endl;
            time(&ultimaComida);

            int tiempoAleatorio = rand() % 240 + 60;
            tiempoNecesidades = ultimaComida + tiempoAleatorio;
            necesitaLimpiar = true;
        }
        else
        {
            cout << "No tienes suficientes monedas para comprar este alimento." << endl;
        }
    }
    else
    {
        cout << "Opción inválida." << endl;
    }
}

void limpiarNecesidades()
{
    necesitaLimpiar = false;
    cout << "Has limpiado las necesidades de " << nombre << "." << endl;
}

void serio()
{
    string text;
    ifstream archivo("muñecoserio.txt");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
}

void enojado()
{
    string text;
    ifstream archivo("muñeco enojado.txt");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
}

void triste()
{
    string text;
    ifstream archivo("muñecotriste.txt");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
}

void jugarPiedraPapelTijeras()
{
    cout << "Bienvenido a Piedra, Papel o Tijeras!" << endl;
    cout << "Elige tu opcion: " << endl;
    cout << "1. Piedra" << endl;
    cout << "2. Papel" << endl;
    cout << "3. Tijeras" << endl;

    int opcionJugador;
    cout << "Ingresa tu opcion: ";
    cin >> opcionJugador;

    srand(time(NULL));
    int opChadpou = rand() % 3 + 1;

    cout << "La computadora eligio: ";
    switch (opChadpou)
    {
    case 1:
        cout << "Piedra" << endl;
        break;
    case 2:
        cout << "Papel" << endl;
        break;
    case 3:
        cout << "Tijeras" << endl;
        break;
    }

    if (opcionJugador == opChadpou)
    {
        cout << "¡Empate!" << endl;
    }
    else if ((opcionJugador == 1 && opChadpou == 3) || (opcionJugador == 2 && opChadpou == 1) || (opcionJugador == 3 && opChadpou == 2))
    {
        int monedasGanadas = rand() % 20 + 1;
        cout << "¡Ganaste! Ganaste " << monedasGanadas << " monedas." << endl;
        monedas += monedasGanadas;
        enojado();
        cout << "******************************************************************************************************\n";
    }
    else
    {
        cout << "¡Perdiste! Inténtalo de nuevo." << endl;

    }
}

void jugarAdivinanza()
{
    srand(time(NULL));
    int numeroSecreto = rand() % 100 + 1;
    int intentos = 10;
    int intento;

    cout << "Bienvenido al juego de adivinanza. Tienes que adivinar un numero entre 1 y 100." << endl;

    while (intentos > 0)
    {
        cout << "Estos son tus intentos (" << intentos << " intentos restantes): ";
        cin >> intento;

        if (intento == numeroSecreto)
        {
            int monedasGanadas = rand() % 50 + 1;
            cout << "¡Felicidades! Has adivinado el numero secreto. Ganaste " << monedasGanadas << " monedas." << endl;
            monedas += monedasGanadas;
            return;
        }
        else if (intento < numeroSecreto)
        {
            cout << "El numero secreto es mayor." << endl;
        }
        else
        {
            cout << "El numero secreto es menor." << endl;
        }

        intentos--;
    }

    cout << "Lo siento, has agotado todos tus intentos. El numero secreto era: " << numeroSecreto << endl;
}

void juegoMemoria()
{
    cout << "¡Bienvenido al juego de memoria!" << endl;
    cout << "Se te mostraran una serie de numeros. Memorízalos y luego intenta repetirlos." << endl;

    srand(time(NULL));
#define MAX_NUMEROS 10
    bool juegoTerminado = false;
    int nivel = 1;

    while (!juegoTerminado)
    {
        cout << "Nivel " << nivel << endl;

        int numeros[MAX_NUMEROS];
        int numerosUsuario[MAX_NUMEROS];

        // Generar números aleatorios
        for (int i = 0; i < nivel; ++i)
        {
            numeros[i] = rand() % 10; // Números aleatorios del 0 al 9
        }

        // Mostrar números al jugador
        for (int i = 0; i < nivel; ++i)
        {
            cout << numeros[i] << " ";
        }
        cout << endl;

        // Esperar unos segundos para que el jugador memorice los números
        cout << "Memoriza los numeros... (5 segundos)" << endl;
        // Pausa de 5 segundos
        for (int i = 0; i < 5; ++i)
        {
            cout << 5 - i << "... ";
            cout.flush(); // Limpiar el buffer de salida para mostrar los números en orden
            Sleep(1000); // Windows
        }
        cout << endl;

        // Limpiar la pantalla
        system("CLS||clear");

        // Pedir al jugador que repita los números
        cout << "Ingresa los numeros que memorizaste, separados por espacios:" << endl;
        for (int i = 0; i < nivel; ++i)
        {
            cin >> numerosUsuario[i];
        }

        // Comparar números
        bool correcto = true;
        for (int i = 0; i < nivel; ++i)
        {
            if (numeros[i] != numerosUsuario[i])
            {
                correcto = false;

                break;
            }
        }

        if (correcto)
        {
            cout << "¡Correcto! Pasas al siguiente nivel." << endl;
            int monedasGanadas = rand() % 5 + 1;
            cout << "Gano estas monedas: " << monedasGanadas << endl;
            ++nivel;
        }
        else
        {
            cout << "¡Incorrecto! Fin del juego." << endl;
            juegoTerminado = true;
        }
    }
}

void verificarNecesidades()
{
    time_t ahora;
    time(&ahora);

    if (ahora - ultimaComida >= 300 && ahora >= tiempoNecesidades && !necesitaLimpiar)
    {
        cout << "¡" << nombre << " ha hecho sus necesidades! Deberías limpiarlo." << endl;
        necesitaLimpiar = true;
    }
}

int main()
{
    char opcion;

    srand(time(NULL));
    time(&ultimaComida);
    time(&tiempoNecesidades);

    cout << "Bienvenido a chadpou. " << endl;
    cout << "Pongale un nombre a chadpou: ";
    cin >> nombre;

    cout << "Tiene que elegir las opciones que se le va a dar de dar de comer, mandarlo a dormir o cosas asi\n\n";

    do
    {
        Feliz();
        verificarNecesidades();
       
        cout << "Elige una de las siguientes opciones: " << endl;
        cout << "a. Inicio" << endl;
        cout << "b. Reglas" << endl;
        cout << "c. Opciones para la mascota" << endl;
        cout << "d. Salir del programa" << endl;
        cout << "Opcion: ";
        cin >> opcion;
        cout << endl;

        switch (opcion)
        {
        case 'a':
            system("CLS");
            break;
        case 'b':
            cout << "Reglas: " << endl;
            cout << "Tiene que alimentar a su mascota para que este no muera de hambre." << endl;
            cout << "Tiene que jugar para conseguir dinero y que asi puedas conseguir alimento para tu mascota\n";
            cout << "Para volver al inicio coloque 'a': ";
            cin >> opcion;
            cout << endl;
            break;
        case 'c':
            char opcion2;
            cout << "Elija una de las siguientes opciones para la mascota: " << endl;
            cout << "a. Alimentar" << endl;
            cout << "b. Dormir" << endl;
            cout << "c. Jugar Piedra, Papel o Tijeras" << endl;
            cout << "d. Jugar Adivinanza" << endl;
            cout << "e. Juego de Memoria" << endl;
            if (necesitaLimpiar)
            {
                cout << "f. Limpiar" << endl;
            }
            cout << "Opcion: ";
            cin >> opcion2;
            cout << endl;

            if (opcion2 == 'a')
            {
                comida();
                cout << "Para volver al inicio coloque 'a': ";
                cin >> opcion;
                cout << endl;
                system("CLS");
            }
            else if (opcion2 == 'b')
            {
                dormido();
                cout << endl;
                cout << nombre << " Se a ido a dormir\n";
                cout << "Para volver al inicio coloque 'a': ";
                cin >> opcion;
                cout << endl;
            }
            else if (opcion2 == 'c')
            {
                jugarPiedraPapelTijeras();
            }
            else if (opcion2 == 'd')
            {
                jugarAdivinanza();
            }
            else if (opcion2 == 'e')
            {
                juegoMemoria();
            }
            else if (opcion2 == 'f' && necesitaLimpiar)
            {
                limpiarNecesidades();
            }

            break;
        }
    } while (opcion != 'd');

    cout << "Gracias por jugar. ¡Hasta luego!" << endl;

    return 0;
}
