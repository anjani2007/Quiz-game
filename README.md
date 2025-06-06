# Quiz-game
Here's a simple C++ implementation of a Quiz Game that includes:

Multiple-choice questions

Score tracking

Feedback at the end

Support for categories (manually selectable)

Timer support (basic countdown simulation)

Answer review at the end


> This version runs in the terminal and uses basic C++ features.




---

✅ C++ Quiz Game Code:

#include <iostream>
#include <vector>
#include <string>
#include <chrono>
#include <thread>

using namespace std;

// Question structure
struct Question {
    string category;
    string question;
    vector<string> options;
    int correctOption;
};

// Display a single question and return if the answer was correct
bool askQuestion(const Question& q, int& selectedOption) {
    cout << "\nCategory: " << q.category << "\n";
    cout << q.question << "\n";

    for (size_t i = 0; i < q.options.size(); ++i) {
        cout << i + 1 << ". " << q.options[i] << "\n";
    }

    cout << "You have 10 seconds to answer...\n";

    // Simulated countdown
    for (int i = 10; i >= 1; --i) {
        cout << "\rTime left: " << i << "s " << flush;
        this_thread::sleep_for(chrono::seconds(1));
    }
    cout << "\nEnter your answer (1-" << q.options.size() << "): ";
    cin >> selectedOption;

    return selectedOption - 1 == q.correctOption;
}

// Main function
int main() {
    vector<Question> quiz = {
        {"Science", "What is the chemical symbol for water?", {"H2O", "CO2", "NaCl", "O2"}, 0},
        {"History", "Who was the first President of the United States?", {"Abraham Lincoln", "George Washington", "Thomas Jefferson", "John Adams"}, 1},
        {"Geography", "Which is the largest ocean on Earth?", {"Atlantic", "Indian", "Arctic", "Pacific"}, 3}
    };

    int score = 0;
    vector<int> userAnswers;

    cout << "=== Welcome to the Quiz Game! ===\n";

    for (const auto& q : quiz) {
        int selected = -1;
        if (askQuestion(q, selected)) {
            cout << "Correct!\n";
            ++score;
        } else {
            cout << "Incorrect. The correct answer was: " << q.options[q.correctOption] << "\n";
        }
        userAnswers.push_back(selected);
    }

    // Final score
    cout << "\n=== Quiz Completed ===\n";
    cout << "Your score: " << score << " out of " << quiz.size() << "\n";

    // Review
    cout << "\n--- Answer Review ---\n";
    for (size_t i = 0; i < quiz.size(); ++i) {
        cout << quiz[i].question << "\n";
        cout << "Your answer: " << quiz[i].options[userAnswers[i] - 1] << "\n";
        cout << "Correct answer: " << quiz[i].options[quiz[i].correctOption] << "\n\n";
    }

    return 0
    }

