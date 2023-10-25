# DigitalProject
#include <iostream>
#include <string>
#include <regex>
#include <cmath>
#include <unordered_set>

using namespace std;

bool validateBooleanExpression(const string& expression) {
    // Check for valid characters
    if (!regex_match(expression, regex("^[a-z()+*\\s']+"))) {
        return false;
    }

    // Check for balanced parentheses
    int openParentheses = 0;
    int closeParentheses = 0;
    for (char c : expression) {
        if (c == '(') {
            openParentheses++;
        } else if (c == ')') {
            closeParentheses++;
        }
    }
    if (openParentheses != closeParentheses) {
        return false;
    }

    // Check for valid operator usage
    if (expression.find("**") != string::npos || expression.find("++") != string::npos) {
        return false;
    }

    return true;
}

bool Sop(string expression) {
     // Remove spaces and make the expression lowercase for uniform matching
    expression.erase(remove_if(expression.begin(), expression.end(), ::isspace), expression.end());
    transform(expression.begin(), expression.end(), expression.begin(), ::tolower);

    // Check for valid SOP format
    if (expression.empty()) {
        return false;  // Expression should not be empty
    }

    // Check for valid characters
    if (!regex_match(expression, regex("^[a-z'+*()]+$"))) {
        return false;
    }

    // Check for valid operator usage
    if (expression.find("**") != string::npos || expression.find("++") != string::npos) {
        return false;
    }

    // Implement additional checks for SOP format (e.g., presence of variables and operators)

    return true;
}

bool Pos(string expression) {
   // Remove spaces and make the expression lowercase for uniform matching
    expression.erase(remove_if(expression.begin(), expression.end(), ::isspace), expression.end());
    transform(expression.begin(), expression.end(), expression.begin(), ::tolower);

    // Check for valid POS format
    if (expression.empty()) {
        return false;  // Expression should not be empty
    }

    // Check for valid characters
    if (!regex_match(expression, regex("^[a-z'+*()]+$"))) {
        return false;
    }

    // Check for valid operator usage
    if (expression.find("**") != string::npos || expression.find("++") != string::npos) {
        return false;
    }

    // Implement additional checks for POS format (e.g., presence of variables and operators)

    return true;
}

int cntDistinct(string str) {
    unordered_set<char> s;
    for (int i = 0; i < str.size(); i++) {
        s.insert(str[i]);
    }
    return s.size();
}

void trutht(string sopExpression) {
    int n = cntDistinct(sopExpression); // number of variables
    int outputs = pow(2, n);            // number of outputs in the truth table
    // Implement the logic for generating the truth table
}

int main() {
    string sopExpression;
    cin >> sopExpression;
    string posExpression;
    cin>>posExpression;

    for (auto& x : sopExpression) {
        x = tolower(x);
    }
    for (auto& x : posExpression) {
        x = tolower(x);
    }

    if (validateBooleanExpression(sopExpression)) {
        if (Sop(sopExpression)) {
            cout << "'" << sopExpression << "' is a valid SoP expression." << endl;
        } else {
            cout << "'" << sopExpression << "' is not a valid SoP expression." << endl;
        }
    } else {
        cout << "Invalid Format" << endl;
    }

    if (validateBooleanExpression(posExpression)) {
        if (Pos(posExpression)) {
            cout << "'" << posExpression << "' is a valid PoS expression." << endl;
        } else {
            cout << "'" << posExpression << "' is not a valid PoS expression." << endl;
        }
    } else {
        cout << "Invalid Format" << endl;
    }

    return 0;
}
