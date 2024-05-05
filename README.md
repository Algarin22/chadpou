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
time_t tiempoDormido = 0;
bool durmiendo = false;
bool estaDormido = false;

void dormido()
{
    string text;
    ifstream archivo("Muñecodormido.txt");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
    if (!durmiendo)
    {
        time(&tiempoDormido);
        durmiendo = true;
        cout << nombre << " se ha ido a dormir." << endl;
    }
    else
    {
        time_t ahora;
        time(&ahora);
        double tiempo_transcurrido = difftime(ahora, tiempoDormido);
        if (tiempo_transcurrido < 60)
        {
            cout << nombre << " sigue durmiendo. Tiempo restante: " << 60 - static_cast<int>(tiempo_transcurrido) << " segundos." << endl;
        }
        else
        {
            cout << nombre << " ha despertado." << endl;
            durmiendo = false;
        }
    }
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
    const char* comida[5] = { "Arroz", "Guineo", "Manzana", "Habichuela", "Agua"};
    int precios[5] = { 20, 12, 15, 5, 3 };
    cout << "Cantidad de monedas que tiene: " << monedas << endl;
    cout << "Lista de alimentos:" << endl;
    for (int i = 0; i < 5; i++)
    {
        cout << i + 1 << ". " << comida[i] << " - " << precios[i] << " monedas" << endl;
    }

    int opcion;
    cout << "Seleccione el alimento que desea comprar, si no lo quiere alimentar precione 5: ";
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

    srand(time(NULL));
    int monedasGanadas = rand() % 3 + 1;
    monedas += monedasGanadas;
    cout << "Has limpiado las necesidades de " << nombre << ". Has ganado " << monedasGanadas << " monedas." << endl;

    necesitaLimpiar = false;
    cout << "Has limpiado las necesidades de " << nombre << "." << endl;
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
    system("CLS");
    cout << "Bienvenido a Piedra, Papel o Tijeras del gran chadpou!" << endl;
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
        cout << "Empate!" << endl;
    }
    else if ((opcionJugador == 1 && opChadpou == 3) || (opcionJugador == 2 && opChadpou == 1) || (opcionJugador == 3 && opChadpou == 2))
    {
        int monedasGanadas = rand() % 20 + 1;
        cout << "Ganaste! Ganaste " << monedasGanadas << " monedas." << endl;
        monedas += monedasGanadas;
        enojado();
        cout << "******************************************************************************************************\n";
    }
    else
    {
        cout << "QUE PENA!! Gano " << nombre << " intentelo de nuevo." << endl;

    }
}

void jugarAdivinanza()
{
    system("CLS");
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
    triste();
    cout << "******************************************************************************************************\n";
}
void banco()
{
    cout << "Estas son la cantidad de monedas que tiene: " << monedas << endl;
}

void juegoMemoria()
{
    system("CLS");
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

        
        for (int i = 0; i < nivel; ++i)
        {
            numeros[i] = rand() % 10; 
        }

        
        for (int i = 0; i < nivel; ++i)
        {
            cout << numeros[i] << " ";
        }
        cout << endl;

        
        cout << "Memoriza los numeros... (5 segundos)" << endl;
       
        for (int i = 0; i < 5; ++i)
        {
            cout << 5 - i << "... ";
            cout.flush(); 
            Sleep(1000); // Windows
        }
        cout << endl;

        
        system("CLS");

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
            monedas += monedasGanadas;
            cout << "Gano estas monedas: " << monedasGanadas << endl;
            ++nivel;
        }
        else
        {
            cout << "¡Incorrecto! Fin del juego." << endl;
            juegoTerminado = true;
            triste();
            cout << "******************************************************************************************************\n";
        }
    }
}

void verificarNecesidades()
{
    time_t ahora;
    time(&ahora);

    if (ahora - ultimaComida >= 300 && ahora >= tiempoNecesidades && !necesitaLimpiar)
    {
        cout << "¡" << nombre << " ha hecho sus necesidades! Deberias limpiarlo." << endl;
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
        if (!estaDormido)
        {
            Feliz();
            verificarNecesidades();
        }
        else
        {
            dormido();
        }
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
            cout << "g. Banco" << endl;
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
                
            }
            else if (opcion2 == 'b')
            {
                if (!estaDormido) // Solo se puede dormir si no está ya dormido
                {
                    dormido();
                    cout << endl;
                    cout << nombre << " Se a ido a dormir\n";
                    estaDormido = true;
                    cout << "Para volver al inicio coloque 'a': ";
                    cin >> opcion;
                    cout << endl;
                }
                else
                {
                    cout << nombre << " ya está dormido." << endl;
                }
            }
            else if (opcion2 == 'c')
            {
                if (!estaDormido) // Solo se puede jugar si no está dormido
                {
                    jugarPiedraPapelTijeras();
                }
                else
                {
                    cout << nombre << " está dormido. Espere a que se despierte." << endl;
                }
            }
            else if (opcion2 == 'd')
            {
                if (!estaDormido) // Solo se puede jugar si no está dormido
                {
                    jugarAdivinanza();
                }
                else
                {
                    cout << nombre << " está dormido. Espere a que se despierte." << endl;
                }
            }
            else if (opcion2 == 'e')
            {
                if (!estaDormido) // Solo se puede jugar si no está dormido
                {
                    juegoMemoria();
                }
                else
                {
                    cout << nombre << " está dormido. Espere a que se despierte." << endl;
                }
            }
            else if (opcion2 == 'f' && necesitaLimpiar)
            {
                limpiarNecesidades();
            }
            else if (opcion2 == 'g')
            {
                banco();
            }

            break;
        }
    } while (opcion != 'd');

    cout << "Gracias por jugar. Hasta luego!" << endl;

    return 0;
}
