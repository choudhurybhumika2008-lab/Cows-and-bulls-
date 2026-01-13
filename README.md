#include <iostream>
#include <cstdlib>
#include <ctime>
#include <string>
#include <cctype>

using namespace std;

// Check if all characters are digits and unique
bool isValidGuess(const string& s) {
    if (s.length() != 4)
        return false;

    for (int i = 0; i < 4; i++) {
        if (!isdigit(s[i]))
            return false;

        for (int j = i + 1; j < 4; j++) {
            if (s[i] == s[j])
                return false;
        }
    }
    return true;
}

// Generate 4-digit secret number with unique digits
string generateSecret() {
    string secret = "";

    while (secret.length() < 4) {
        char digit = '0' + rand() % 10;
        if (secret.find(digit) == string::npos)
            secret += digit;
    }
    return secret;
}

int main() {
    srand(time(0));

    string secret = generateSecret();
    string guess;
    int cows = 0, bulls = 0, attempts = 0;

    cout << "🐄🐂 Cows and Bulls Game\n";
    cout << "Rules:\n";
    cout << "- Guess a 4-digit number\n";
    cout << "- All digits must be unique\n";

    do {
        cout << "\nEnter your guess: ";
        cin >> guess;

        if (!isValidGuess(guess)) {
            cout << "Invalid input! Enter 4 unique digits only.\n";
            continue;
        }

        cows = bulls = 0;
        attempts++;

        for (int i = 0; i < 4; i++) {
            if (guess[i] == secret[i])
                bulls++;
            else if (secret.find(guess[i]) != string::npos)
                cows++;
        }

        cout << "Cows: " << cows << " | Bulls: " << bulls << endl;

    } while (guess != secret);

    cout << "\n🎉 Congratulations! You guessed the number.\n";
    cout << "Secret Number: " << secret << endl;
    cout << "Total Attempts: " << attempts << endl;

    return 0;
}
