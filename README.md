#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    srand(time(0));

    //stampa tabellone
    cout << "tabellone:\n";
    cout << "-----------------------------------\n";
    for (int i = 1; i <= 90; i++)
    {
        if (i % 10 == 1)
            cout << "| ";
        
        if (i < 10)
            cout << " ";

        cout << i << " ";
        
        if (i % 10 == 5)
            cout << "| ";

        if (i % 10 == 0)
        {
            cout << "|\n";
            if (i == 30 || i == 60)
                cout << "-----------------------------------\n";
        }
    }
    cout << "-----------------------------------\n";

    // generare numeri estratti
    int n[15]; 
    int decine[9] = {0};

    for (int i = 0; i < 15; )
    {
        int numero = rand() % 90 + 1;
        int colonna = (numero - 1) / 10;

        //controllo per avere 3 numeri per colonna tutti diversi 
        if (decine[colonna] >= 3)
            continue;
            
        int j;
        for ( j = 0; j < i; j++)
            if (n[j] == numero)
                break;
                
        if (j < i)
            continue; 
            
        n[i] = numero;
        decine[colonna]++;
        i++;
    }

/*
    // Stampa numeri estratti
    for (int i = 0; i < 15; i++)
        cout << n[i] << " ";
        
    cout << "\n";
*/

    //creazione cartella
    int cartella[3][9] = {0};
    int nriga[3] = {0};
    int inseriti = 0;

    while (inseriti < 15)
    {
        for (int i = 0; i < 15 && inseriti < 15; i++)
        {
            int colonna = (n[i] - 1) / 10;
            
            //controllo per inserire max 3 numemri per colonna
            int cont = 0;
            for (int r = 0; r < 3; r++)
                if (cartella[r][colonna] != 0)
                    cont++;
            if (cont >= 3)
                continue;
                
            for (int r = 0; r < 3; r++)
            {
                if (nriga[r] < 5 && cartella[r][colonna] == 0)
                {
                    cartella[r][colonna] = n[i];
                    nriga[r]++;
                    inseriti++;
                    break;
                }
            }
        }
    }

   
    // Stampa cartella
    cout << "cartella:\n";
    cout << "---------------------------------------------\n";
    for (int r = 0; r < 3; r++)
    {
        cout << "| ";
        for (int c = 0; c < 9; c++)
        {
            if (cartella[r][c] == 0)
                cout << "   | ";
            else
            {
                if (cartella[r][c] < 10) cout << " ";
                cout << cartella[r][c] << " | ";
            }
        }
        cout << "\n---------------------------------------------\n";
    }

    return 0;
}
