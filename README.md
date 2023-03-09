#include <stdio.h>

int main() {
    int x = 0;
    int y = 3;
    int direction = 0;
    int roomWidth = 15;
    int roomHeight = 15;
    int stepCount = 0;
    int maxSteps = (roomWidth + roomHeight) * 2;
    int throughDoor = 0;
    int isOutside = 0;
    int jumpOverBox = 0;

    // Schritte machen, bis der Roboter an der Ausgangsposition ist
    while (x != 0 || y != 3 || direction != 0) {
        switch (direction) {
            case 0:
                y++;
                break;
            case 1:
                x--;
                break;
            case 2:
                y--;
                break;
            case 3:
                x++;
                break;
        }
        
        if (x == 0 || y == 0 || x == roomWidth - 1 || y == roomHeight - 1) {
            direction = (direction + 1) % 4;
        }

        stepCount++;

        // Überprüfung, ob der Roboter draußen ist
        if (x == 2 && y == 0) {
            isOutside = 1;
            break;
        }
    }

    // Roboter dreht sich im Kreis, wenn er draußen ist
    if (isOutside) {
        printf("Ich bin draußen. ");
        printf("Soll ich mich im Kreis drehen? (0 - Nein, 1 - Ja): ");
        scanf("%d", &jumpOverBox);
        if (jumpOverBox) {
            printf("Ich drehe mich im Kreis...\n");
            for (int i = 0; i < 4; i++) {
                printf("Drehung %d\n", i+1);
                direction = (direction + 1) % 4;
            }
        }
    }

    // Roboter geht zurück ins Haus und dreht sich bei Bedarf
    while (x != 0 || y != 3 || direction != 0) {
        switch (direction) {
            case 0:
                y++;
                break;
            case 1:
                x--;
                break;
            case 2:
                y--;
                break;
            case 3:
                x++;
                break;
        }
        
        if (x == 0 || y == 0 || x == roomWidth - 1 || y == roomHeight - 1) {
            if (isOutside) {
                // Wenn der Roboter draußen ist, fragen, ob er sich drehen soll
                printf("Soll ich mich drehen, bevor ich reingehe? (0 - Nein, 1 - Ja): ");
                scanf("%d", &jumpOverBox);
                if (jumpOverBox) {
                    printf("Ich drehe mich...\n");
                    direction = (direction + 1) % 4;
                }
            } else {
                // Wenn der Roboter im Haus ist, einfach drehen
                direction = (direction + 1) % 4;
            }
        }
        
        stepCount++;
    }

    // Roboter sagt Auf Wiedersehen
    printf("Ich bin zurück am Startpunkt. ");
    printf("Auf Wiedersehen, Herr Baumann!\n");

    printf("Ich habe %d Schritte gemacht.\n", stepCount);

    printf("Ich schalte mich jetzt aus.\
