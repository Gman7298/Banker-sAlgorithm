#include <iostream>
#include <fstream>
#include <vector>

using namespace std;

const int P = 5;
const int R = 3;

int main() {
    ifstream infile("input.txt");
    if (!infile) {
        cerr << "Failed to open input.txt" << endl;
        return 1;
    }

    int available[R];
    int max[P][R], alloc[P][R], need[P][R];

    for (int i = 0; i < R; ++i) {
        infile >> available[i];
    }

    for (int i = 0; i < P; ++i)
        for (int j = 0; j < R; ++j)
            infile >> alloc[i][j];

    // Read Max matrix
    for (int i = 0; i < P; ++i)
        for (int j = 0; j < R; ++j)
            infile >> max[i][j];

    infile.close();

    for (int i = 0; i < P; ++i)
        for (int j = 0; j < R; ++j)
            need[i][j] = max[i][j] - alloc[i][j];

    vector<bool> finished(P, false);
    vector<int> safeSequence;

    int work[R];
    for (int i = 0; i < R; ++i)
        work[i] = available[i];

    int count = 0;
    while (count < P) {
        bool found = false;
        for (int i = 0; i < P; ++i) {
            if (!finished[i]) {
                bool canProceed = true;
                for (int j = 0; j < R; ++j) {
                    if (need[i][j] > work[j]) {
                        canProceed = false;
                        break;
                    }
                }

                if (canProceed) {
                    for (int j = 0; j < R; ++j)
                        work[j] += alloc[i][j];

                    safeSequence.push_back(i);
                    finished[i] = true;
                    found = true;
                    count++;
                }
            }
        }

        if (!found) {
            cout << "The system is NOT in a safe state." << endl;
            return 1;
        }
    }

    cout << "The system is in a SAFE state." << endl;
    cout << "Safe sequence: ";
    for (int i = 0; i < safeSequence.size(); ++i) {
        cout << "P" << safeSequence[i];
        if (i != safeSequence.size() - 1)
            cout << " -> ";
    }
    cout << endl;

    return 0;
}
