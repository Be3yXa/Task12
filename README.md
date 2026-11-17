~~~
#define _CRT_SECURE_NO_WARNINGS
#include <stdlib.h>
#include <stdio.h>
#include <locale.h>
#include <math.h>
#include <time.h>
#include <string.h>

int task1(void) {
	setlocale(LC_CTYPE, "RUS");
	char fname[20] = "number.txt"; //ИМЯ ФАЙЛА
	FILE* out; // файл чисел
	puts("Создание файла");
	if ((out = fopen(fname, "a")) == NULL) {
		printf("Ошибка открытия файла для записи");
		return 0;
	}
	/********начало работы с файлом********/
	fprintf(out, "\n%.2f", 12.56); //ввод числа в файл
	/********конец работы с файлом ********/
	fclose(out); //закрыть файл
	return 1;
}

double f(double x) {
    return pow(x, 3) + 3.0 * pow(x, 2) - 3.0 * sin(x);
}

int main() {
    setlocale(LC_CTYPE, "RUS");
    char fname[20] = "temp.txt"; // ИМЯ ФАЙЛА
    FILE* out;                   // файл результатов

    double a = 0.0, b = 2.0;     
    double h;                    
    int n_points;                // число точек табулирования
    int mode;                    // режим работы с файлом
    printf("Табулирование функции y = x^3 + 3x^2 - 3sin(x) на интервале [0; 2]\n");
    printf("Введите число точек табулирования (больше 1): ");
    scanf("%d", &n_points);
    h = (b - a) / (n_points - 1);
    printf("Выберите действие:\n");
    printf("1 - запись в новый файл\n");
    printf("2 - дозапись в существующий\n");
    printf("Ваш выбор: ");
    scanf("%d", &mode);
    puts("Открытие файла...");
    if (mode == 1) {
        out = fopen(fname, "w");
    }
    else if (mode == 2) {
        out = fopen(fname, "a");
    }
    else {
        printf("Ошибка: неверный выбор действия\n");
        return 0;
    }

    if (out == NULL) {
        printf("Ошибка открытия файла для записи\n");
        return 0;
    }
    /******** начало работы с файлом ********/
    printf("\n       x              y\n");
    printf("---------------------------\n");
    fprintf(out, "\n        y\n");
    fprintf(out, "------------\n");
    double x, y;
    for (int i = 0; i < n_points; i++) {
        x = a + i * h;
        y = f(x);
        printf("%8.2f       %10.4f\n", x, y);
        fprintf(out, "%10.4f\n", y);
    }
    /******** конец работы с файлом ********/
    fclose(out); // закрыть файл
    puts("Данные успешно записаны в temp.txt");
    return 1;
}

int writefile(char* fname, Devices* Device, int size) {
    FILE* out;
    if ((out = fopen(fname, "wt")) == NULL) {
        printf("Ошибка открытия файла для записи");
        return 0;
    }

    for (int i = 0; i < size;i++) //цикл по всем записям
        fprintf(out, "Название:%20s ; Производитель:%20s ; Тип устройства:%20s ; Год выпуска:%4d ; Цена:%4d ; Гарантия:%2d\n",
            Device[i].name, Device[i].brand, Device[i].type, Device[i].year, Device[i].price, Device[i].warranty); //запись полей структуры

    fclose(out);
    return 1;
}
~~~
