# task4
#include <iostream> 
#include <sstream>

using namespace std ;

class compiler{
    public:
        compiler(const string& ex) : input(ex) , pos(0){}

        double parseExpression(){
            double result = parseTerm();
            while (peek() == '+' || peek() == '-'){
              char op = get() ;
              if(op == '+'){
                result += parseTerm();
              }  
            else result -= parseTerm();
            }
            return result ;
        }

    private:
        string input; 
        size_t pos ;

        char peek(){
            while(pos < input.size() && input[pos] == ' ')
                ++pos ;
            return pos < input.size() ? input[pos] : '\0' ;
        }
        char get() {
            return pos < input.size() ? input[pos++] : '\0';
        }
    double parseNumber(){
        stringstream ss;
            while(isdigit(peek()) || peek() == '-')
                ss << get() ;
                double num ;
                ss >> num ;
                return num ;
    }
    double parseFactor(){
        if(peek() == '('){
            get();
        double result = parseExpression() ;
        get() ;
        return result ;
        }
    return parseNumber();
    }
    double parseTerm() {
        double result = parseFactor();
        while (peek() == '*' || peek() == '/') {
            char op = get();
            if (op == '*') result *= parseFactor();
            else result /= parseFactor();
        }
        return result;
    } 
};

int main(){
    string expression ;
    cout << "ENTER AN EXPRESSION : " ;

    while(getline(cin , expression) && !expression.empty()){
        compiler compiler(expression) ;
        cout << " RESULT : " << compiler.parseExpression() << endl;
    }
    return 0 ;
}
