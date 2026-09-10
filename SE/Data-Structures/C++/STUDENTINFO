#include <iostream>
#include <cstdlib>
#include <cstring>
#include <iomanip>
#include <chrono>

using namespace std;

struct Student
{
    int id;
    char name[50];
    float cgpa;
};

Student *students = NULL;
int n = 0;

// Function to display students
void displayStudents()
{
    if (n == 0)
    {
        cout << "\nNo student records available.\n";
        return;
    }

    cout << "\n--------------------------------------------------\n";
    cout << left << setw(10) << "ID"
         << setw(25) << "Name"
         << setw(10) << "CGPA" << endl;
    cout << "--------------------------------------------------\n";

    for (int i = 0; i < n; i++)
    {
        cout << left << setw(10) << students[i].id
             << setw(25) << students[i].name
             << setw(10) << students[i].cgpa << endl;
    }

    cout << "--------------------------------------------------\n";
}

// Add student using realloc()
void addStudent()
{
    Student *temp;

    temp = (Student *)realloc(students, (n + 1) * sizeof(Student));

    if (temp == NULL)
    {
        cout << "\nMemory allocation failed!\n";
        return;
    }

    students = temp;

    cout << "\nEnter Student ID: ";
    cin >> students[n].id;

    cout << "Enter Student Name: ";
    cin.ignore();
    cin.getline(students[n].name, 50);

    cout << "Enter CGPA: ";
    cin >> students[n].cgpa;

    n++;

    cout << "\nStudent record added successfully!\n";
}

// Linear Search
int linearSearch(int id)
{
    for (int i = 0; i < n; i++)
    {
        if (students[i].id == id)
            return i;
    }

    return -1;
}

// Binary Search
// Works only when records are sorted by ID
int binarySearch(int id)
{
    int low = 0;
    int high = n - 1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        if (students[mid].id == id)
            return mid;

        else if (students[mid].id < id)
            low = mid + 1;

        else
            high = mid - 1;
    }

    return -1;
}

// Sort by ID for Binary Search
void sortByID()
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (students[j].id > students[j + 1].id)
            {
                Student temp = students[j];
                students[j] = students[j + 1];
                students[j + 1] = temp;
            }
        }
    }

    cout << "\nStudents sorted by ID successfully!\n";
}

// Bubble Sort by Name
void bubbleSortByName()
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (strcmp(students[j].name, students[j + 1].name) > 0)
            {
                Student temp = students[j];
                students[j] = students[j + 1];
                students[j + 1] = temp;
            }
        }
    }

    cout << "\nStudents sorted by Name alphabetically!\n";
}

// Selection Sort by CGPA
void selectionSortByCGPA()
{
    for (int i = 0; i < n - 1; i++)
    {
        int minIndex = i;

        for (int j = i + 1; j < n; j++)
        {
            if (students[j].cgpa < students[minIndex].cgpa)
            {
                minIndex = j;
            }
        }

        Student temp = students[i];
        students[i] = students[minIndex];
        students[minIndex] = temp;
    }

    cout << "\nStudents sorted by CGPA in ascending order!\n";
}

// Search student and display record
void displaySearchResult(int index)
{
    if (index == -1)
    {
        cout << "\nStudent not found!\n";
        return;
    }

    cout << "\nStudent Found!\n";
    cout << "ID   : " << students[index].id << endl;
    cout << "Name : " << students[index].name << endl;
    cout << "CGPA : " << students[index].cgpa << endl;
}

// Compare Linear and Binary Search
void compareSearch()
{
    if (n == 0)
    {
        cout << "\nNo records available.\n";
        return;
    }

    int id;

    cout << "\nEnter Student ID to search: ";
    cin >> id;

    // Linear Search
    auto start1 = chrono::high_resolution_clock::now();

    int linearResult = linearSearch(id);

    auto end1 = chrono::high_resolution_clock::now();

    // Binary Search requires ID sorting
    sortByID();

    auto start2 = chrono::high_resolution_clock::now();

    int binaryResult = binarySearch(id);

    auto end2 = chrono::high_resolution_clock::now();

    auto linearTime =
        chrono::duration_cast<chrono::nanoseconds>(end1 - start1).count();

    auto binaryTime =
        chrono::duration_cast<chrono::nanoseconds>(end2 - start2).count();

    cout << "\n========== SEARCH RESULT ==========\n";

    cout << "\nLinear Search:";
    displaySearchResult(linearResult);

    cout << "\nBinary Search:";
    displaySearchResult(binaryResult);

    cout << "\n========== PERFORMANCE ==========\n";
    cout << "Linear Search Time : " << linearTime << " nanoseconds\n";
    cout << "Binary Search Time : " << binaryTime << " nanoseconds\n";

    cout << "\nTime Complexity:\n";
    cout << "Linear Search : O(n)\n";
    cout << "Binary Search : O(log n)\n";
}

// Main Function
int main()
{
    int choice;
    int id;

    do
    {
        cout << "\n\n========== STUDENT DATABASE ==========\n";
        cout << "1. Add Student\n";
        cout << "2. Display Students\n";
        cout << "3. Linear Search by ID\n";
        cout << "4. Sort by ID\n";
        cout << "5. Binary Search by ID\n";
        cout << "6. Sort by Name (Bubble Sort)\n";
        cout << "7. Sort by CGPA (Selection Sort)\n";
        cout << "8. Compare Search Performance\n";
        cout << "9. Exit\n";

        cout << "\nEnter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            addStudent();
            break;

        case 2:
            displayStudents();
            break;

        case 3:
            cout << "\nEnter Student ID: ";
            cin >> id;
            displaySearchResult(linearSearch(id));
            break;

        case 4:
            sortByID();
            displayStudents();
            break;

        case 5:
            cout << "\nFirst sorting records by ID...\n";
            sortByID();

            cout << "Enter Student ID: ";
            cin >> id;

            displaySearchResult(binarySearch(id));
            break;

        case 6:
            bubbleSortByName();
            displayStudents();
            break;

        case 7:
            selectionSortByCGPA();
            displayStudents();
            break;

        case 8:
            compareSearch();
            break;

        case 9:
            cout << "\nProgram terminated.\n";
            break;

        default:
            cout << "\nInvalid choice! Try again.\n";
        }

    } while (choice != 9);

    free(students);

    return 0;
}
