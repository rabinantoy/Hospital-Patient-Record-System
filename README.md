#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// --- Patient Structure ---
typedef struct {
    int patientId;
    char name[100];
    int age;
    char disease[200];
} Patient;

// --- Function Prototypes ---
void addPatient(FILE *fp);
void displayAllPatients(FILE *fp);
// ... other functions ...

void displayMenu() {
    printf("\n--- Hospital Patient Record System ---\n");
    printf("1. Add New Patient\n");
    printf("2. View All Patients\n");
    // ... other options ...
    printf("0. Exit\n");
    printf("Enter choice: ");
}

// --- Main Function ---
int main() {
    FILE *fp;
    int choice;
    // Open file in append binary mode (ab+)
    fp = fopen("patients.dat", "ab+");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return 1;
    }

    do {
        displayMenu();
        scanf("%d", &choice);
        // Clear input buffer after scanf
        getchar(); 

        switch (choice) {
            case 1:
                addPatient(fp);
                break;
            case 2:
                displayAllPatients(fp);
                break;
            // ... other cases ...
            case 0:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice!\n");
        }
    } while (choice != 0);

    fclose(fp);
    return 0;
}

// --- addPatient Function (Example) ---
void addPatient(FILE *fp) {
    Patient newPatient;
    printf("\nEnter Patient ID: ");
    scanf("%d", &newPatient.patientId);
    getchar(); // Clear buffer

    printf("Enter Name: ");
    fgets(newPatient.name, 100, stdin);
    newPatient.name[strcspn(newPatient.name, "\n")] = 0; // Remove newline

    printf("Enter Age: ");
    scanf("%d", &newPatient.age);
    getchar();

    printf("Enter Disease: ");
    fgets(newPatient.disease, 200, stdin);
    newPatient.disease[strcspn(newPatient
