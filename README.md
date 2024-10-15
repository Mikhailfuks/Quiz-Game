#include <iostream>
#include <string>
#include <vector>
#include <map>
#include <random>
#include <ctime>

using namespace std;

// Question Structure
struct Question {
    string questionText;
    map<char, string> options;
    char correctAnswer;
};

// Quiz Class
class Quiz {
private:
    vector<Question> questions;
    int currentQuestionIndex;
    int score;
    int numQuestions;

public:
    // Constructor
    Quiz(const vector<Question>& questions) : questions(questions), currentQuestionIndex(0), score(0), numQuestions(questions.size()) {}

    // Ask a question
    void askQuestion() {
        const Question& currentQuestion = questions[currentQuestionIndex];
        cout << "\nQuestion " << currentQuestionIndex + 1 << ":" << endl;
        cout << currentQuestion.questionText << endl;
        for (auto const& [key, value] : currentQuestion.options) {
            cout << key << ". " << value << endl;
        }

        char answer;
        cout << "Enter your answer: ";
        cin >> answer;

        if (answer == currentQuestion.correctAnswer) {
            cout << "Correct!" << endl;
            score++;
        } else {
            cout << "Incorrect. The correct answer is " << currentQuestion.correctAnswer << "." << endl;
        }

        currentQuestionIndex++;
    }

    // Check if the quiz is finished
    bool isFinished() {
        return currentQuestionIndex >= numQuestions;
    }

    // Display the final score
    void displayScore() {
        cout << "\nQuiz finished!" << endl;
        cout << "Your final score is " << score << " out of " << numQuestions << endl;
    }
};

int main() {
    // Define quiz questions (replace with your own!)
    vector<Question> quizQuestions = {
        {
            "What is the capital of France?",
            {{'a', "London"}, {'b', "Paris"}, {'c', "Rome"}, {'d', "Berlin"}},
            'b'
        },
        {
            "Who painted the Mona Lisa?",
            {{'a', "Michelangelo"}, {'b', "Leonardo da Vinci"}, {'c', "Raphael"}, {'d', "Vincent van Gogh"}},
            'b'
        },
        {
            "What is the highest mountain in the world?",
            {{'a', "Mount Everest"}, {'b', "K2"}, {'c', "Kangchenjunga"}, {'d', "Lhotse"}},
            'a'
        }
    };

    // Create a Quiz object
    Quiz quiz(quizQuestions);

    // Start the quiz
    cout << "Welcome to the Quiz Game!" << endl;
    while (!quiz.isFinished()) {
        quiz.askQuestion();
    }

    // Display the final score
    quiz.displayScore();

    return 0;
}
