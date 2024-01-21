#include <stdio.h>
#include <stdlib.h>

#define MAX_ROWS 5
#define MAX_COLUMNS 10

// Structure to represent a seat
struct Seat {
    int row;
    int column;
    int isBooked;
};

// Function prototypes
void displaySeats(struct Seat seats[MAX_ROWS][MAX_COLUMNS]);
void bookSeat(struct Seat seats[MAX_ROWS][MAX_COLUMNS]);
int isValidSeat(int row, int column);

int main() {
    struct Seat seats[MAX_ROWS][MAX_COLUMNS];

    // Initialize seats
    for (int i = 0; i < MAX_ROWS; i++) {
        for (int j = 0; j < MAX_COLUMNS; j++) {
            seats[i][j].row = i + 1;
            seats[i][j].column = j + 1;
            seats[i][j].isBooked = 0;
        }
    }

    int option;

    do {
        printf("\nOnline Seat Booking System Menu:\n");
        printf("1. Display Available Seats\n");
        printf("2. Book a Seat\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &option);

        switch (option) {
            case 1:
                displaySeats(seats);
                break;
            case 2:
                bookSeat(seats);
                break;
            case 3:
                printf("Exiting the Online Seat Booking System. Goodbye!\n");
                break;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    } while (option != 3);

    return 0;
}

void displaySeats(struct Seat seats[MAX_ROWS][MAX_COLUMNS]) {
    printf("\nAvailable Seats:\n");

    for (int i = 0; i < MAX_ROWS; i++) {
        for (int j = 0; j < MAX_COLUMNS; j++) {
            if (seats[i][j].isBooked == 0) {
                printf("[ ] "); // Unbooked seat
            } else {
                printf("[X] "); // Booked seat
            }
        }
        printf("\n");
    }
}

void bookSeat(struct Seat seats[MAX_ROWS][MAX_COLUMNS]) {
    int row, column;

    printf("Enter the row number: ");
    scanf("%d", &row);

    printf("Enter the column number: ");
    scanf("%d", &column);

    if (isValidSeat(row, column) && seats[row - 1][column - 1].isBooked == 0) {
        seats[row - 1][column - 1].isBooked = 1;
        printf("Seat booked successfully!\n");
    } else {
        printf("Invalid seat or seat already booked. Please try again.\n");
    }
}

int isValidSeat(int row, int column) {
    return row >= 1 && row <= MAX_ROWS && column >= 1 && column <= MAX_COLUMNS;
}


