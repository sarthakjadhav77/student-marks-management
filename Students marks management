#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define M 100
#define N 50

typedef struct student {
    int id;
    char name[N];
    float math;
    float coa;
    float physics;
    float ds;
    float oop;
    float total;
    float average;
    struct student *next;
}student;

typedef struct studentlist {
    student *start;
    int count;
}studentlist;

int isDuplicateID(studentlist *list, int id) {
    student *temp = list->start;
    while (temp != NULL) {
        if (temp->id == id) {
            return 1;
        }
        temp = temp->next;
    }
    return 0;
}

void addstudent(studentlist *list) {
    student *s = (student *)malloc(sizeof(student));

    while(getchar() != '\n');

    printf("Enter Student name: ");
    gets(s->name);
    do {
        printf("Enter Student ID: ");
        scanf("%d", &s->id);
        if (isDuplicateID(list, s->id)) {
            printf("id %d already exists. please enter a unique ID.\n", s->id);
        }
    } while (isDuplicateID(list, s->id));
    printf("Enter math marks: ");
    scanf("%f", &s->math);
    printf("Enter coa marks: ");
    scanf("%f", &s->coa);
    printf("Enter physics marks: ");
    scanf("%f", &s->physics);
    printf("Enter ds marks: ");
    scanf("%f", &s->ds);
    printf("Enter oop marks: ");
    scanf("%f", &s->oop);
    
    s->total = s->math+s->coa+s->physics+s->ds+s->oop;
    s->average = s->total/5;
    
    s->next = list->start;
    list->start = s;
    list->count++;
}

void displaystudents(studentlist *list) {
    if (list->start == NULL) {
        printf("No student records found\n");
        return;
    }

    printf("\n%-5s %-20s %-7s %-7s %-10s %-7s %-7s %-8s %-7s\n", "id", "name", "math", "coa", "physics", "ds", "oop", "total", "avg");
    printf("-------------------------------------------------------------------------------------\n");

    student *s = list->start;
    for (int i = 0; i < list->count; i++) {
        printf("%-5d %-20s %-7.1f %-7.1f %-10.1f %-7.1f %-7.1f %-8.1f %-7.1f\n", s->id, s->name, s->math, s->coa, s->physics, s->ds, s->oop, s->total, s->average);
        s = s->next;
    }
    printf("-------------------------------------------------------------------------------------\n");
}

void sortstudents(studentlist *list, int mode) {
    if (list->start == NULL || list->start->next == NULL) {
        return;
    }

    int swapped;
    int n = list->count;

    for (int i = 0; i < n - 1; i++) {
        student *prev = NULL;
        student *current = list->start;
        swapped = 0;

        for (int j = 0; j < n - i - 1; j++) {
            student *a = current;
            student *b = a->next;

            int condition = 0;
            if (mode == 1) {
                condition = (a->id > b->id);
            } else if (mode == 2) {
                condition = (a->total < b->total);
            }

            if (condition) {
                a->next = b->next;
                b->next = a;

                if (prev == NULL) {
                    list->start = b;
                } else {
                    prev->next = b;
                }
                prev = b;
                swapped = 1;
            } else {
                prev = a;
                current = a->next;
            }
        }

        if (!swapped) 
            break;
    }
    printf("List sorted successfully.\n");
}

void deletestudent(studentlist *list) {
    if (list->start == NULL) 
        return;

    int targetID;
    printf("Enter ID to delete: ");
    scanf("%d", &targetID);

    student *temp = list->start, *prev = NULL;

    if (temp != NULL && temp->id == targetID) {
        list->start = temp->next;
        free(temp);
        list->count--;
        printf("Record deleted.\n");
        return;
    }
    while (temp != NULL && temp->id != targetID) {
        prev = temp;
        temp = temp->next;
    }
    if (temp == NULL) {
        printf("ID not found.\n");
        return;
    }
    prev->next = temp->next;
    free(temp);
    list->count--;
    printf("Record deleted.\n");
}

void updateMarks(studentlist *list) {
    int targetID;
    printf("Enter ID to update: ");
    scanf("%d", &targetID);

    student *s = list->start;
    while (s != NULL) {
        if (s->id == targetID) {
            printf("Updating marks for %s\n", s->name);
            printf("Enter new math marks(prev: %.1f): ", s->math); 
            scanf("%f", &s->math);
            printf("Enter new coa marks(prev: %.1f): ", s->coa); 
            scanf("%f", &s->coa);
            printf("Enter new physics marks(prev: %.1f): ", s->physics); 
            scanf("%f", &s->physics);
            printf("Enter new ds marks(prev: %.1f): ", s->ds); 
            scanf("%f", &s->ds);
            printf("Enter new oop marks(prev: %.1f): ", s->oop); 
            scanf("%f", &s->oop);
            
            
            s->total = s->math + s->coa + s->physics + s->ds + s->oop;
            s->average = s->total / 5;
            printf("Update successful\n");
            return;
        }
        s = s->next;
    }
    printf("id not found.\n");
}

void search(studentlist *list) {
    int targetID;
    printf("Enter ID to search: ");
    scanf("%d", &targetID);

    student *s = list->start;
    while (s != NULL) {
        if (s->id == targetID) {
            printf("\nRecord Found:\nName: %s\nAverage: %.1f\nTotal: %.1f\n", s->name, s->average,s->total);
            printf("math: %.1f | coa: %.1f | physics: %.1f | ds: %.1f | oop: %.1f\n", s->math, s->coa,s->physics, s->ds, s->oop);
            return;
        }
        s = s->next;
    }
    printf("Student not found.\n");
}

int main() {
    studentlist slist;
    slist.start = NULL;
    slist.count = 0;

    int choice;
    do {
        printf("\n1-Add student\n2-Display all\n3-Sort\n4-Delete student\n5-Search\n6-Update marks\n0-Exit\nEnter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: addstudent(&slist); 
                    break;
            case 2: displaystudents(&slist); 
                    break;
            case 3: if (slist.count < 2) {
                        printf("Not enough students to sort.\n");
                        break;
                    }
                    printf("\nSort by:\n1. Roll Number (ID)\n2. Total Marks\nEnter choice: ");
                    int sortChoice;
                    scanf("%d", &sortChoice);
                    if (sortChoice == 1 || sortChoice == 2)
                        sortstudents(&slist, sortChoice);
                    else
                        printf("Invalid choice. Please select 1 or 2.\n");
                    break;
            case 4: if (slist.count == 0)
                        printf("No records found.\n");
                    else
                        deletestudent(&slist);
                    break;
            case 5: if (slist.count == 0)
                        printf("No records found.\n");
                    else
                        search(&slist);
                    break;
            case 6: if (slist.count == 0)
                        printf("No records found.\n");
                    else
                        updateMarks(&slist);
                    break;
            case 0: printf("Exiting...\n"); 
                    break;
            default: printf("Invalid choice.\n");
        }
    } while (choice != 0);

    return 0;
}
