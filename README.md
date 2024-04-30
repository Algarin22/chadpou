#include <iostream>
#include <stdlib.h>
#include <string>
#include <fstream>
#include<time.h>
#include<Windows.h>

using namespace std;

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

const string& nombreMascota()
{
    static string nombre;

    cout << "Introduzca el nombre de su chadpou: ";
    cin >> nombre;
    cout << endl;

    return nombre;
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
    const char* comida[5] = { "Arroz","Guineo","Manzana","Habichuela","Agua" };
    for (int i = 0;i < 5;i++)
    {
        cout << comida[i] << "\n";
    }
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
}
void triste()
{
}



int main()
{
    char opcion;

    cout << "Bienvenido a chadpou. " << endl;

    const string& nombre = nombreMascota();

    cout << "Tiene que elegir las opciones que se le va a dar de dar de comer, mandarlo a dormir o cosas asi\n\n";

    do
    {
        Feliz();
        cout << "Elige una de las siguientes opciones: " << endl;
        cout << "a. Inicio" << endl;
        cout << "b. Reglas" << endl;
        cout << "c. Opciones para la mascota" << endl;
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
            cout << endl;
            cout << "Para volver al inicio coloque 'a': ";
            cin >> opcion;
            cout << endl;
            break;
        case 'c':
            char opcion2;
            cout << "Elija una de las siguientes opciones para la mascota: " << endl;
            cout << "a. Alimentar" << endl;
            cout << "b. Dormir" << endl;
            cout << "Opcion: ";
            cin >> opcion2;
            cout << endl;

            if (opcion2 == 'a')
            {
                comida();
                cout << "Tu chadpou ya no tiene hambre." << endl;
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

            break;
        }
    } while (opcion == 'a');

    return 0;
}
