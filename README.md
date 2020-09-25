#include <iostream>

using namespace std;

int** grabMemory(int ROWS, int COLS);
void delteMemory(int** arr, int ROWS);
void enterArray(int** arr, int ROWS, int COLS);
void showElementsOfArray(int** arr, int ROWS, int COLS);
void findMinElements(int** arr, int ROWS, int COLS, int& ROW_index, int& COL_index, int& minElement);

int main() {
	int ROWS, COLS, ROW_index, COL_index, minElement;

	cout << "Enter amount of ROWS in array: ";
	cin >> ROWS;

	cout << "Enter amount of COLS in array: ";
	cin >> COLS;

	int** arr = grabMemory(ROWS, COLS);

	enterArray(arr, ROWS, COLS);
	cout << "Your array: " << endl;
	showElementsOfArray(arr, ROWS, COLS);

	findMinElements(arr, ROWS, COLS, ROW_index, COL_index, minElement);
	cout << "Min element of array is " << minElement << " and his coords: " << ROW_index + 1 << " row " << COL_index + 1 << " column." << endl;

	delteMemory(arr, ROWS);
}

int** grabMemory(int ROWS, int COLS) { // захват памяти
	int** newArray = new int* [ROWS];

	for (int i = 0; i < ROWS; i++) {
		newArray[i] = new int[COLS];
	}

	return newArray;
}

void delteMemory(int** arr, int ROWS) { // удаление захваченной памяти
	for (int i = 0; i < ROWS; i++) {
		delete[] arr[i];
	}

	delete[] arr;
}

void enterArray(int** arr, int ROWS, int COLS) { // ввести массив
	cout << "Enter elements of array:" << endl;

	for (int i = 0; i < ROWS; i++) {
		cout << "Row " << i + 1 << ":" << endl;
		for (int j = 0; j < COLS; j++) {
			cin >> arr[i][j];
		}
	}
}

void showElementsOfArray(int** arr, int ROWS, int COLS) { // показать массив в консоли
	for (int i = 0; i < ROWS; i++) {
		for (int j = 0; j < COLS; j++) {
			cout << arr[i][j] << "\t";
		}
		cout << endl;
	}
}

void findMinElements(int** arr, int ROWS, int COLS, int& ROW_index, int& COL_index, int& minElement) {

	if (COLS > 1) {
		ROW_index = 0;
		COL_index = 1;
	}
	else {
		ROW_index = 1;
		COL_index = 0;
	}

	minElement = arr[ROW_index][COL_index];

	if (COLS % 2 == 0) {
		for (int i = 0; i < ROWS; i++) {
			for (int j = 1; j < COLS; j +=2) {
				if (arr[i][j] < minElement) {
					minElement = arr[i][j];
					ROW_index = i;
					COL_index = j;
				}
			}
		}
	}
	else {
		for (int i = 0, g = 1; i < ROWS; i++, g++) {
			if (g % 2 == 0) {
				for (int j = 0; j < COLS; j += 2) {
					if (arr[i][j] < minElement) {
						minElement = arr[i][j];
						ROW_index = i;
						COL_index = j;
					}
				}
			}
			else if (COLS > 1) {
				for (int j = 1; j < COLS; j += 2) {
					if (arr[i][j] < minElement) {
						minElement = arr[i][j];
						ROW_index = i;
						COL_index = j;
					}
				}
			}
		}
	}
}
