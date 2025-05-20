# laba6-number6
# 6 Уменьшающееся число
Над целым числом можно производить следующие операции: 
* 1 Если число делится на 3, то делить его на 3; 
* 2 Если число делится на 2, то делить его на 2;
* 3 Вычитать 1
По заданному натуральному числу n найти наименьшее количество операций, после выполнения которых получится 1

# Реализация
*   **Функция `solve(int start)`:**  Основная функция, реализующая алгоритм BFS. Она принимает начальное число `start` и возвращает минимальное количество шагов до 1.
*   **Очередь `queue<pair<int, int>> q`:** Используется для хранения состояний (число и количество шагов) в процессе поиска.
*   **Вектор `vector<int> visited`:** Используется для отслеживания посещенных чисел, чтобы избежать зацикливания. Если `visited[i] == 1`, это означает, что число `i` уже было посещено.

# Код
```
cpp
#include <iostream>
#include <queue>
#include <vector>

using namespace std;

int solve(int start) {
    queue<pair<int, int>> q; // {number, steps}
    q.push({ start, 0 });

    vector<int> visited(start + 1, 0); // Отслеживаем посещенные числа
    visited[start] = 1;

    while (!q.empty()) {
        int num = q.front().first;
        int steps = q.front().second;
        q.pop();

        if (num == 1) {
            return steps;
        }

        //  Все возможные переходы (если они допустимы):

        // Вычитание 1
        if (num - 1 >= 1 && visited[num - 1] == 0) {
            int next_num = num - 1;
            q.push({ next_num, steps + 1 });
            visited[next_num] = 1;
        }


        // Деление на 2
        if (num % 2 == 0 && visited[num / 2] == 0) {
            int next_num = num / 2;
            q.push({ next_num, steps + 1 });
            visited[next_num] = 1;

        }


        // Деление на 3
        if (num % 3 == 0 && visited[num / 3] == 0) {
            int next_num = num / 3;
            q.push({ next_num, steps + 1 });
            visited[next_num] = 1;
        }


    }

    return -1; // Если не нашли путь (чего не должно произойти)
}

int main() {
    int n;
    while (cin >> n) {
        cout << solve(n) << endl;
    }
    return 0;
}
```
