#include <iostream>
#include <cmath>
#include <vector>
#include <chrono>

using namespace std;
using namespace chrono;

// Funkcja pomocnicza do sprawdzania, czy liczba jest pierwsza - używana w metodach naiwnych
bool czyPierwsza(int liczba) {
    if (liczba < 2) return false;
    for (int i = 2; i <= sqrt(liczba); i++) {
        if (liczba % i == 0) return false;
    }
    return true;
}

// a) Naiwna metoda sprawdzająca wszystkie liczby od 2 do k-1
int liczbPierwszychMetodaA(int n) {
    int licznik = 0;
    for (int k = 2; k <= n; k++) {
        bool jestPierwsza = true;
        for (int i = 2; i < k; i++) {
            if (k % i == 0) {
                jestPierwsza = false;
                break;
            }
        }
        if (jestPierwsza) licznik++;
    }
    return licznik;
}

// b) Naiwna metoda z wykluczeniem liczb parzystych większych od 2
int liczbPierwszychMetodaB(int n) {
    int licznik = (n >= 2) ? 1 : 0; // 2 jest liczbą pierwszą
    for (int k = 3; k <= n; k += 2) { // Sprawdzamy tylko liczby nieparzyste
        bool jestPierwsza = true;
        for (int i = 3; i < k; i += 2) { // Sprawdzamy tylko nieparzyste dzielniki
            if (k % i == 0) {
                jestPierwsza = false;
                break;
            }
        }
        if (jestPierwsza) licznik++;
    }
    return licznik;
}

// c) Naiwna metoda sprawdzająca tylko do sqrt(k)
int liczbPierwszychMetodaC(int n) {
    int licznik = (n >= 2) ? 1 : 0; // 2 jest liczbą pierwszą
    for (int k = 3; k <= n; k += 2) { // Sprawdzamy tylko liczby nieparzyste
        if (czyPierwsza(k)) licznik++;
    }
    return licznik;
}

// d) Metoda Sita Eratostenesa
int liczbPierwszychSitoEratostenesa(int n) {
    vector<bool> czyPierwsza(n + 1, true);
    czyPierwsza[0] = czyPierwsza[1] = false;
    for (int i = 2; i * i <= n; i++) {
        if (czyPierwsza[i]) {
            for (int j = i * i; j <= n; j += i) {
                czyPierwsza[j] = false;
            }
        }
    }
    int licznik = 0;
    for (int i = 2; i <= n; i++) {
        if (czyPierwsza[i]) licznik++;
    }
    return licznik;
}

// e) Metoda Sita Atkina
int liczbPierwszychSitoAtkina(int limit) {
    if (limit < 2) return 0;

    vector<bool> czyPierwsza(limit + 1, false);
    int sqrtLimit = sqrt(limit);
    for (int x = 1; x <= sqrtLimit; x++) {
        for (int y = 1; y <= sqrtLimit; y++) {
            int n = (4 * x * x) + (y * y);
            if (n <= limit && (n % 12 == 1 || n % 12 == 5)) czyPierwsza[n] = !czyPierwsza[n];
            n = (3 * x * x) + (y * y);
            if (n <= limit && n % 12 == 7) czyPierwsza[n] = !czyPierwsza[n];
            n = (3 * x * x) - (y * y);
            if (x > y && n <= limit && n % 12 == 11) czyPierwsza[n] = !czyPierwsza[n];
        }
    }
    for (int i = 5; i <= sqrtLimit; i++) {
        if (czyPierwsza[i]) {
            for (int j = i * i; j <= limit; j += i * i) czyPierwsza[j] = false;
        }
    }
    int licznik = 2; // Liczymy 2 i 3 jako pierwsze
    for (int i = 5; i <= limit; i++) {
        if (czyPierwsza[i]) licznik++;
    }
    return licznik;
}

int main() {
    int n_values[] = {1000, 10000, 100000, 1000000};

    for (int n : n_values) {
        cout << "Dla n = " << n << ":\n";

        // Metoda a
        auto start = high_resolution_clock::now();
        int wynikA = liczbPierwszychMetodaA(n);
        auto end = high_resolution_clock::now();
        cout << "Metoda a): " << wynikA << " liczb pierwszych, czas: " 
             << duration_cast<milliseconds>(end - start).count() << " ms\n";

        // Metoda b
        start = high_resolution_clock::now();
        int wynikB = liczbPierwszychMetodaB(n);
        end = high_resolution_clock::now();
        cout << "Metoda b): " << wynikB << " liczb pierwszych, czas: " 
             << duration_cast<milliseconds>(end - start).count() << " ms\n";

        // Metoda c
        start = high_resolution_clock::now();
        int wynikC = liczbPierwszychMetodaC(n);
        end = high_resolution_clock::now();
        cout << "Metoda c): " << wynikC << " liczb pierwszych, czas: " 
             << duration_cast<milliseconds>(end - start).count() << " ms\n";

        // Sito Eratostenesa
        start = high_resolution_clock::now();
        int wynikD = liczbPierwszychSitoEratostenesa(n);
        end = high_resolution_clock::now();
        cout << "Sito Eratostenesa: " << wynikD << " liczb pierwszych, czas: " 
             << duration_cast<milliseconds>(end - start).count() << " ms\n";

        // Sito Atkina
        start = high_resolution_clock::now();
        int wynikE = liczbPierwszychSitoAtkina(n);
        end = high_resolution_clock::now();
        cout << "Sito Atkina: " << wynikE << " liczb pierwszych, czas: " 
             << duration_cast<milliseconds>(end - start).count() << " ms\n";

        cout << "--------------------------------------\n";
    }

    return 0;
}
