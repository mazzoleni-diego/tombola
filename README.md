#include <iostream>
#include <cstdlib>
#include <ctime>

using namespace std;

int main() {
    srand(time(0));

//stampa tabellone
cout<<"-----------------------------------\n";

for(int i = 1; i <= 90; i++)
{
    if(i % 10 == 1)
       cout<<"| ";
        
    if(i < 10)
        cout<<" ";

     cout<<i<<" ";
        
    if(i%10== 5)
        cout<<"| ";

    if(i %10== 0)
    {
        cout<<"|\n";
        if(i == 30 || i == 60)
            cout<<"-----------------------------------\n";
    }
}
cout<<"-----------------------------------\n";

//generare numeri estratti
int n[15];

for(int i = 0; i < 15; i++)
{
    n[i]=rand()%89+1;
        
    for(int j = 0; j < i; j++)
    {  //controllo per far uscire i numeri solo 1 volta
        if(n[i] == n[j])
        {
            i--;
            break;
        }
    }
}

//stampa numeri estratti
for(int i = 0; i < 15; i++) 
{
    cout<<n[i]<<" ";
}
    
    
    return 0;
}
