#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <math.h>

#define MILLION 1000000
#define BILLION 1000000000

#define WEAK 1
#define MODERATE 2
#define STRONG 3

void printColor(const char *message, const char *color) {
    printf("%s%s\033[0m", color, message);
}

int evaluatePassword(const char *password) {
    int hasUpper = 0, hasLower = 0, hasDigit = 0, hasSpecial = 0;
    const char *specialChars = "!@#$%^&*()-_=+[]{};:,.<>?";
    int length = strlen(password);

    for (int i = 0; i < length; i++) {
        if (isupper(password[i])) hasUpper = 1;
        if (islower(password[i])) hasLower = 1;
        if (isdigit(password[i])) hasDigit = 1;
        if (strchr(specialChars, password[i])) hasSpecial = 1;
    }

    if ((hasUpper && hasLower && hasDigit && hasSpecial) && length >= 12) {
        return STRONG;
    } else if ((hasUpper && hasLower && hasDigit) && length >= 8) {
        return MODERATE;
    } else {
        return WEAK;
    }
}

double calculateEntropy(const char *password) {
    int length = strlen(password);
    int poolSize = 0;

    if (strpbrk(password, "abcdefghijklmnopqrstuvwxyz")) poolSize += 26;
    if (strpbrk(password, "ABCDEFGHIJKLMNOPQRSTUVWXYZ")) poolSize += 26;
    if (strpbrk(password, "0123456789")) poolSize += 10;
    if (strpbrk(password, "!@#$%^&*()-_=+[]{};:,.<>?")) poolSize += 32;

    return length * log2(poolSize);
}

void bruteForceTimeEstimate(int length, int poolSize, double guessesPerSecond) {
    double totalCombinations = pow(poolSize, length);
    double timeToCrack = totalCombinations / guessesPerSecond;

    printf("Estimated brute-force time: %.2f seconds\n", timeToCrack);
    printf("Equivalent time in years: %.2f years\n", timeToCrack / (60 * 60 * 24 * 365));
}

void suggestImprovements(int strength) {
    if (strength == WEAK) {
        printColor("Suggestions: Use a longer password with mixed case, numbers, and special characters.\n", "\033[1;31m"); // Red
    } else if (strength == MODERATE) {
        printColor("Suggestions: Increase the password length and add more special characters for better security.\n", "\033[1;33m"); // Yellow
    } else {
        printColor("Your password is strong! Great job!\n", "\033[1;32m"); // Green
    }
}

int main() {
    char password[100];
    printf("Enter your password: ");
    scanf("%s", password);

    int strength = evaluatePassword(password);
    double entropy = calculateEntropy(password);

    printf("\nPassword Strength: ");
    if (strength == STRONG) {
        printColor("Strong\n", "\033[1;32m"); // Green
    } else if (strength == MODERATE) {
        printColor("Moderate\n", "\033[1;33m"); // Yellow
    } else {
        printColor("Weak\n", "\033[1;31m"); // Red
    }

    printf("Password Entropy: %.2f bits\n", entropy);

    int poolSize = 0;
    if (strpbrk(password, "abcdefghijklmnopqrstuvwxyz")) poolSize += 26;
    if (strpbrk(password, "ABCDEFGHIJKLMNOPQRSTUVWXYZ")) poolSize += 26;
    if (strpbrk(password, "0123456789")) poolSize += 10;
    if (strpbrk(password, "!@#$%^&*()-_=+[]{};:,.<>?")) poolSize += 32;

    bruteForceTimeEstimate(strlen(password), poolSize, BILLION); // Assumes 1 billion guesses per second
    suggestImprovements(strength);

    return 0;
}
