# information-theory
\#include \<iostream>

\#include \<vector>
 
using namespace std;
 
void PrintReversed(vector<int> vector)

{

        for (int i = 0; i<vector.size(); i++) {
                cout << vector[vector.size() - 1 - i] << " ";
        }
        cout << endl;
}
 
void ClearZeros(vector<int> &vector)

{

        vector.erase(vector.end() - 1);
}
 
void CalculateModulo(vector<int> &poly1, vector<int> &poly2, vector<int> &modulo,vector<int> &result)
{

        reverse(poly1.begin(), poly1.end());
        reverse(poly2.begin(), poly2.end());
        modulo = poly1;
       
        while (modulo.size() >= poly2.size())
        {
                int offset = modulo.size() - poly2.size();
                result.push_back(modulo[modulo.size() - 1]);
                if (modulo[modulo.size()-1]!=0)
                for (int i = offset++, j = 0; i < modulo.size(); i++, j++)
                        modulo[i]=(modulo[i] ^ poly2[j]);
                ClearZeros(modulo);
        }
        reverse(result.begin(), result.end());
}
 
int main(void)
{
 
        vector<int> poly1 = { 1, 0, 0, 0, 1 };
        vector<int> poly2 = { 1, 1, 0, 1 };
        vector<int> modulo, result;
        //Делимое
        cout << "Dividend:" << endl;
        //Делитель
        PrintReversed(poly1);
        cout << "Divider:" << endl;
        PrintReversed(poly2);
 
        CalculateModulo(poly1, poly2, modulo, result);
 
        cout <<endl<< "Result:" << endl;
        PrintReversed(result);
        cout << "Modulo:" << endl;
        PrintReversed(modulo);
        system("pause");
        return 0;
}
