#include <iostream>
#inlude <iomanip>
#include <string>

using namespace std;

struct Student {

int id;
string firstName;
string lastName;
string course;
float gpa;
};

const int MAX_STUDENTS = 100;
Student students[MAX_STUDENTS];
int studentCount = 0;

void addStudent() {
    if (studentCount >= MAX_STUDENTS) return;
    int id;
    cout << "Enter Student ID: ";
    cin >> id;
    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == id) {
            cout << "Duplicate ID found.\n";
            return;
        }
    }
    students[studentCount].id = id;
    cout << "Enter First Name: ";
    cin >> students[studentCount].firstName;
    cout << "Enter Last Name: ";
    cin >> students[studentCount].lastName;
    cout << "Enter Course: ";
    cin >> students[studentCount].course;
    cout << "Enter GPA: ";
    cin >> students[studentCount].gpa;
    studentCount++;
    cout << "Student added successfully.\n";
}

void editStudent() {
    if (studentCount == 0) {
        cout << "No records found.\n";
        return;
    }
    int id;
    cout << "Enter Student ID to edit: ";
    cin >> id;
    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == id) {
            cout << "Enter New First Name: ";
            cin >> students[i].firstName;
            cout << "Enter New Last Name: ";
            cin >> students[i].lastName;
            cout << "Enter New Course: ";
            cin >> students[i].course;
            cout << "Enter New GPA: ";
            cin >> students[i].gpa;
            cout << "Student record updated.\n";
            return;
        }
    }
    cout << "Student not found.\n";
}

void deleteStudent() {
    if (studentCount == 0) {
        cout << "No records found.\n";
        return;
    }
    int id;
    cout << "Enter Student ID to delete: ";
    cin >> id;
    for (int i = 0; i < studentCount; i++) {
        if (students[i].id == id) {
            for (int j = i; j < studentCount - 1; j++) {
                students[j] = students[j + 1];
            }
            studentCount--;
            cout << "Student deleted successfully.\n";
            return;
        }
    }
    cout << "Student not found.\n";
}

void viewStudents() {
    if (studentCount == 0) {
        cout << "No records found.\n";
        return;
    }
    int option;
    cout << "View options:\n1. Alphabetically\n2. GPA (Ascending)\nSelect: ";
    cin >> option;
    if (option == 1) {
        for (int i = 0; i < studentCount - 1; i++) {
            for (int j = i + 1; j < studentCount; j++) {
                if (students[i].lastName > students[j].lastName) {
                    swap(students[i], students[j]);
                }
            }
        }
    } else if (option == 2) {
        for (int i = 0; i < studentCount - 1; i++) {
            for (int j = i + 1; j < studentCount; j++) {
                if (students[i].gpa > students[j].gpa) {
                    swap(students[i], students[j]);
                }
            }
        }
    } else {
        cout << "Invalid option.\n";
        return;
    }
    cout << "ID\tName\t\tCourse\tGPA\n";
    for (int i = 0; i < studentCount; i++) {
        cout << students[i].id << "\t" << students[i].lastName << ", " << students[i].firstName
             << "\t" << students[i].course << "\t" << fixed << setprecision(2) << students[i].gpa << endl;
    }
}

int main() {
    int choice;
    bool running = true;
    while (running) {
        cout << "\nMenu:\n1. Add Student\n2. Edit Student\n3. Delete Student\n4. View Students\n5. Exit\nSelect: ";
        cin >> choice;
        switch (choice) {
            case 1: addStudent(); break;
            case 2: editStudent(); break;
            case 3: deleteStudent(); break;
            case 4: viewStudents(); break;
            case 5: running = false; break;
            default: cout << "Invalid choice.\n";
        }
    }
    return 0;
}
