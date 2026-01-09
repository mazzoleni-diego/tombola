#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    
    srand(time(0));

    //variabile per salvare le cartelle fuori dal ciclo
    int cartelle[2][3][9];

    //stampa del tabellone 
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

    //creazione cartelle
    for (int z = 1 ; z < 3; z++)
    {
        int n[15]; 
        int decine[9] = {0};
        for (int i = 0; i < 15; )
        {
            int numero = rand() % 90 + 1;
            int colonna = (numero) / 10;
            
            if (decine[colonna] >= 3)
                continue;
                
            int j;
            for ( j = 0; j < 15; j++)
                if (n[j] == numero)
                    break;
                    
            if (j < i)
                
                {
                i--;
                continue;
                }
            n[i] = numero;
                
            decine[colonna]++;
            i++;
        }
        
        int cartella[3][9] = {0};
        int nriga[3] = {0};
        int inseriti = 0;
        cout << "cartella " << z << " :\n";
        
        while (inseriti < 15)
        {
            for (int i = 0; i < 15 && inseriti < 15; i++)
            {
                int colonna = (n[i]) / 10;
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
        
        //salvo le cartelle fuori dal ciclo 
        for (int r = 0; r < 3; r++)
            for (int c = 0; c < 9; c++)
                cartelle[z-1][r][c] = cartella[r][c];
                
        //stampa della cartella
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
    }

    //estrazione dei numeri
    int estratti[91] = {0};
    int controllo[2][3][9] = {0};

    while (1)
    {
        
        int numero;
        do 
        {
            numero = rand() % 90 + 1;
        } while (estratti[numero] == 1);
        
        estratti[numero] = 1;
        cout << "il numero estratto e' " << numero << endl;
        
        //aggiorna le cartelle 
        for (int z = 0; z < 2; z++)
        {
            int cont = 0;
            
            cout << "cartella " << z + 1 << ":\n";
            cout << "---------------------------------------------\n";
            
            for (int r = 0; r < 3; r++)
            {
                cout << "| ";
                for (int c = 0; c < 9; c++)
                {
                    if (cartelle[z][r][c] == numero)
                        controllo[z][r][c] = 1;
                        
                    if (controllo[z][r][c] == 1)
                        cont++;
                        
                    if (cartelle[z][r][c] == 0)
                        cout << "   | ";
                    else
                    {
                        if (controllo[z][r][c] == 1)
                            cout << " X | ";
                        else
                        {
                            if (cartelle[z][r][c] < 10) cout << " ";
                            cout << cartelle[z][r][c] << " | ";
                        }
                    }
                }
                cout << "\n---------------------------------------------\n";
            }
            
            if (cont == 15)
            {
                cout << "tombola\n";
                cout << "la cartella " << z + 1 << " ha vinto\n";
                return 0;
            }
        }
    }

    return 0;
}
