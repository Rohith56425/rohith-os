#include <stdio.h>

void scan(int arr[], int size, int head, int direction) {
    int seek_sequence[size + 1];
    int index = 0;
    int distance, total_head_movement = 0;

    // Sort the request array
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }

    // Add head to the seek sequence
    seek_sequence[index++] = head;

    // Move towards the direction
    for (int i = 0; i < size; i++) {
        if (arr[i] >= head) {
            seek_sequence[index++] = arr[i];
        }
    }

    // Reverse direction
    if (direction == 1) {
        for (int i = size - 1; i >= 0; i--) {
            if (arr[i] < head) {
                seek_sequence[index++] = arr[i];
            }
        }
    } else {
        for (int i = 0; i < size; i++) {
            if (arr[i] < head) {
                seek_sequence[index++] = arr[i];
            }
        }
    }

    // Calculate total head movement
    for (int i = 0; i < index - 1; i++) {
        distance = seek_sequence[i + 1] - seek_sequence[i];
        total_head_movement += (distance < 0) ? -distance : distance;
    }

    printf("Seek Sequence: ");
    for (int i = 0; i < index; i++) {
        printf("%d ", seek_sequence[i]);
    }
    printf("\nTotal Head Movement: %d\n", total_head_movement);
}

int main() {
    int arr[] = { 98, 183, 37, 122, 14, 124, 65, 67 };
    int size = sizeof(arr) / sizeof(arr[0]);
    int head = 53; // Initial head position
    int direction = 1; // 1 for right, 0 for left

    scan(arr, size, head, direction);
    return 0;
}
