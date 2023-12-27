#include <iostream>
#include <vector>
#include <sstream>
#include <windows.h>
#include <cmath> 
using namespace std; 

int main() {
    SetConsoleCP(1251);
    SetConsoleOutputCP(1251);
    int minimum = 1000; // задал большой минимум
    int intotal; // все дома
    string intotalstr;
    cout << "введите общее количество домов: ";
    cin >> intotalstr;
    try {
        intotal = stoi(intotalstr);
    }
    catch (const invalid_argument&) {
        cout << "введите целое число";
        return 1;
    }
    catch (const out_of_range&) {
        cout << "можно поменьше число";
        return 1;
    }
    if (intotal <= 0) {
        cout << "число должно быть положительным";
        return 1;
    }
    vector<int> a;
    while (true) {
        int i;
        string istr;
        cout << "введите дома в которые необходимо провести провода ( ноль как разделитель) ";
        cin >> istr; 
        try {
            i = stoi(istr);
        }
        catch (const invalid_argument&) {
            cout << "введите целое число";
            return 1;
        }
        catch (const out_of_range&) {
            cout << "можно поменьше число";
            return 1;
        }
        if (i > 0) {
            a.push_back(i);
        }
        else {
            break;
        }
    }
    for (int home = 1; home <= intotal; home++) {
        int cnt = 0;
        for (int i : a) {
            int a = abs(home - i);
            cnt += a;
        }
        if (cnt < minimum) {
            minimum = cnt;
        }
    }
    cout << minimum << " минимальная длина " << endl;
    for (int home = 1; home <= intotal; home++) {
        int cnt = 0;
        for (int i : a) {
            int a = abs(home - i);
            cnt += a;
        }
        if (cnt == minimum) {
            cout << "ставьте на " << home << " дом" << endl;
        }
    }
    return 0;
}
