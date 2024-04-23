#include <iostream>
#include<stdlib.h>
#include<string>
#include<fstream>
using namespace std;
char eleccion;
int main()
{
    do
    {
        inicio();
        reglas();
        opciones();

    } while ();

}
void inicio()
{
    cout << "Bienvenido a chadpou\n";
}
void reglas()
{
    cout << "Tiene que elegir las opciones que se le va a dar de dar de comer, mandarlo a dormir o cosas asi\n";

}
void opciones()
{
    cout << "Estas son las opciones\n";
    cout << "D para que vaya a dormir\n";
    cout << "D para que vaya a dormir\n";
    cout << "D para que vaya a dormir\n";
    cout << "D para que vaya a dormir\n";
    cout << "D para que vaya a dormir\n";
    cout << "D para que vaya a dormir\n";
    cout << "D para que vaya a dormir\n"; 
    cin >> eleccion;

}
void dormido()
{
    string text;
    ifstream archivo("MuñecoDormido");

    while (getline(archivo, text))
    {
        cout << text << "\n";
    }
    archivo.close();
  
}
void serio()
{}
void Feliz()
{}
void enojado()
{}
void triste()
{}
