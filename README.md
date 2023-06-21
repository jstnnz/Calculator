#include <iostream> 

#include <limits>

using namespace std;

struct Calculation {

    int num1;

    int num2;

    char operatorSymbol;

    int result;

};

int sum(int n1, int n2, int& result) {

    result = n1 + n2;

    return result;

}

int dif(int n1, int n2, int& result) {

    result = n1 - n2;

    return result;

}

int prod(int n1, int n2, int& result) {

    result = n1 * n2;

    return result;

}

int quo(int n1, int n2, int& result) {

    if (n2 == 0) {

        cout << "Undefined";

        return 0;

    }

    result = n1 / n2;

    return result;

}

int main() {

    int n1, n2, result;

    char opt, back; 

    const int limit = 5; 

    Calculation history[limit]; 

    int history_size = 0; 

    do {

        

        cout << " ======================================" << endl;

        cout << "               CALCULATOR              " << endl;

        cout << " ======================================" << endl;

        cout << endl;

        cout << "Enter the numbers you'd like to calculate: \n\n";

        cout << "--> ";

        cin >> n1 >> opt >> n2;

        /* handle invalid input by checking if the input stream ('cin') has failed;

        If the input is invalid, an error message is displayed and the user is prompted to enter valid input again */

        while (cin.fail()) {

            cout << endl << "Invalid input. Please try again (ex. 5+5): ";

            cin.clear();

            cin.ignore(numeric_limits<streamsize>::max(), '\n');

            cin >> n1 >> opt >> n2;

        }

        cout << endl;

        switch (opt) {

            case '+':

                cout << "Answer: " << sum(n1, n2, result);

                break;

            case '-':

                cout << "Answer: " << dif(n1, n2, result);

                break;

            case '*':

                cout << "Answer: " << prod(n1, n2, result);

                break;

            case '/':

                cout << "Answer: " << quo(n1, n2, result);

                break;

            default:

                cout << "Answer: ";

        }

        Calculation calc; // 'calc'= new 'calculation' struct

        calc.num1 = n1;

        calc.num2 = n2;

        calc.operatorSymbol = opt;

        calc.result = result;

        history[history_size] = calc;

        history_size++;

        if (history_size > 0) { // If there are calculations in the history (i.e., history_size > 0), the code enters a loop to display the calculation history.

           

            cout << endl << endl << " ======================================" << endl;

            cout << "                HISTORY            " << endl;

            cout << " ======================================" << endl;

           

           

            for (int i = 0; i < history_size; i++) {

                cout << endl <<" [ " << history[i].num1 << history[i].operatorSymbol << history[i].num2 << "=" << history[i].result <<" ]"<< endl;

                cout << endl << "Addresses: " << endl;

                cout << history[i].num1 << "| Address = " << &history[i].num1 << endl;

                cout << history[i].num2 << "| Address = " << &history[i].num2 << endl;

                cout << history[i].result << "| Address = " << &history[i].result << endl;

            }

           

            cout << endl << endl << "Try again? [Y/N]: ";

            cin >> back;

            cout << endl << endl;

        }

    } while (back == 'y' || back == 'Y');

    return 0;

}
