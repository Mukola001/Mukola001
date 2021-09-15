#include <iostream>
#include <windows.h>
#include <ctime>
#include <fstream>
#include <cmath>
#include <string>
#include <cstring>
#include <iomanip>

using namespace std;

struct Car {
    char sname[20];
    char mark[20];
    int num;
    char color[20];
}cars[5];

void StructTask(Car *cars) {
    cout << "Створити структуру даних про автомобілі (прізвище власника, марка, номер, колір автомобіля)." << endl;
    cout << "Вивести на екран дані про автомобілі марки Volvo.  \n\n" << endl;
    ifstream f;
    f.open("file1.txt");
    for (int i = 0; !f.eof(); i++) {
        f >> cars[i].sname;
        f >> cars[i].mark;
        f >> cars[i].num;
        f >> cars[i].color;
        if (strstr(cars[i].mark, "Volvo"))
        {
            cout << cars[i].sname << " " << cars[i].mark << " " << cars[i].num << " " << cars[i].color << endl;
        }
    }
    f.close();
}

void gotoxy(int x, int y) {
    COORD coord;
    coord.X = x;
    coord.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}
void ArrayTask() {
    cout << "Нехай а0=1; ак=как-1+1/к, к=1,2,... Задано натуральне число n. Отримати аn." << endl;
    int n;
    double a[100];
    cout << "enter n:";
    cin >> n;
    a[0] = 1;
    for (int k = 1; k <= n; k++) {
        a[k] = k * a[k - 1] + 1 / k;
    }
    cout << "an = " << a[n] << endl;
}


void MatrixTask() {
    cout << "Дано дійсна квадратна матриця порядку n." << endl;
    cout << "Знайти найбільше із значень елементів, які розташовані в заштрихованій частині матриці. \n\n" << endl;
    int n;
    cout << "Введіть порядок матриці - n ";
    cin >> n;
    double** myMatrix = new double* [n];
    cout << "Матриця: " << endl;
    for (int i = 0; i < n; i++) {
        myMatrix[i] = new double[n];
        for (int j = 0; j < n; j++) {
            myMatrix[i][j] = rand() % 200;
            cout << setw(4) << myMatrix[i][j];
        }
        cout << endl;
    }
    int max = myMatrix[0][0];
    cout << "Елементи, серед яких вiдбуватиметься пошук найбiльшого елемента: " << endl;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (i >= n / 2 && j + i >= n - 1 && j <= n - (n - i)) {
                cout << setw(4) << myMatrix[i][j];
                if (max < myMatrix[i][j])
                    max = myMatrix[i][j];
            }
            else
                cout << setw(4) << "  ";
        }
        cout << endl;
    }
    cout << "Найбiльший елемент матрицi у цiй зонi пошуку = " << max << endl;
    for (int i = 0; i < n; i++) {
        delete[]myMatrix[i];
    }
    delete[] myMatrix;
}

int main() {
    SetConsoleOutputCP(1251);
    srand(time(0));
    string str;
    ifstream f_1;
    f_1.open("file2.txt");
    for (int i = 0; !f_1.eof(); i++) {
        gotoxy(20, 4 + i);
        getline(f_1, str);
        cout << str << endl;
    }
    f_1.close();
    cin >> str;
    system("cls");
    char NumberMenu[4][30] = { "1. Робота з масивами", "2. Робота з матрицями","3. Робота зі структурами" ,"4. Close" };
    while (true) {
        system("cls");
        gotoxy(20, 4);
        cout << "----------------" << endl;
        gotoxy(20, 5);
        cout << "| Головне меню |" << endl;
        gotoxy(20, 6);
        cout << "----------------" << endl;
        for (int j = 0; j < 4; ++j) {
            gotoxy(20, 8 + j);
            cout << NumberMenu[j];
        }
        gotoxy(20, 15);
        int k;
        cout << "Виберiть номер завдання ";
        cin >> k;
        switch (k) {
        case 1: ArrayTask();
            system("pause");
            break;
        case 2: MatrixTask();
            system("pause");
            break;
        case 3: StructTask(cars);
            system("pause");
            break;
        case 4:
            exit(0);
            break;
        default: {
            gotoxy(20, 17);
            cout << "Невiрно вибраний номер завдання";
            cout << endl;
            system("pause");
        }
        }
    }
    system("pause");
    return 0;
}
