// Own OS called MDQ - by MDQDev

#include <iostream>
#include <thread>
#include <chrono>

std::string user = "\0";

void Clear();
void Asking(void self());
void Calculator();
void Textbook();
void Terminal();
void OS();
void ShowTime();
void ShowOS();
void Timer();
void Games();
void Guessing();
void RPS();

int main()
{
    Clear();
    std::cout << "\033[0mWelcome to MDQ!\n";
    std::cout << "-------------------------\n";
    std::cout << "Exit (exit)\n";
    std::cout << "Calculator (calc)\n";
    std::cout << "Textbook (book)\n";
    std::cout << "Terminal (terminal)\n";
    std::cout << "OS Terminal (os)\n";
    std::cout << "Show Time (show-time)\n";
    std::cout << "Show OS (show-os)\n";
    std::cout << "Timer (timer)\n";
    std::cout << "Games Section (games)\n";
    std::cout << "-------------------------\n";
    std::cout << "Option: ";
    std::cin >> user;
    if (user == "exit")
        exit(0);
    else if (user == "calc")
        Calculator();
    else if (user == "book")
        Textbook();
    else if (user == "book")
        Terminal();
    else if (user == "terminal")
        Terminal();
    else if (user == "os")
        OS();
    else if (user == "show-time")
        ShowTime();
    else if (user == "show-os")
        ShowOS();
    else if (user == "timer")
        Timer();
    else if (user == "games")
        Games();
    else
        main();
    return 0;
}

void Clear()
{
#ifdef _WIN32
    system("cls");
#else
    system("clear");
#endif
}

void Asking(void self())
{
    std::cout << "Again (again)\n";
    std::cout << "Back (back)\n";
    std::cout << "-------------------------\n";
    std::cout << "Option: ";
    std::cin >> user;
    if (user == "again")
        self();
    else
        main();
}

void Calculator()
{
    Clear();
    char op = '\0';
    bool isvalid = 1;
    int a = 0, b = 0, c = 0;
    std::cout << "Calculator\n";
    std::cout << "-------------------------\n\n";
    std::cout << "-------------------------\n\033[2A";
    std::cout << "Number One: ";
    std::cin >> a;
    Clear();
    std::cout << "-------------------------\n\n";
    std::cout << "-------------------------\n\033[2A";
    std::cout << "Enter +, -, * or /: ";
    std::cin >> op;
    Clear();
    std::cout << "-------------------------\n\n";
    std::cout << "-------------------------\n\033[2A";
    std::cout << "Number Two: ";
    std::cin >> b;
    Clear();
    switch (op)
    {
    case '+':
        c = a + b;
        break;
    case '-':
        c = a - b;
        break;
    case '*':
        c = a * b;
        break;
    case '/':
        c = a / b;
        break;

    default:
        isvalid = 0;
        break;
    }
    std::cout << "-------------------------\n";
    if (isvalid)
        std::cout << a << " " << op << " " << b << " = " << c << '\n';
    else
        std::cout << "\033[33mInvalid Operator!\033[0m\n";
    std::cout << "-------------------------\n\n";
    Asking(Calculator);
}

void Textbook()
{
    Clear();
    std::cout << "Textbook\n";
    std::cout << "-------------------------\n";
    while (true)
    {
        std::cin >> user;
        if (user == "exit")
            break;
        else if (user == "clear")
            Clear();
    }
    main();
}

void Terminal()
{
    Clear();
    std::cout << "Terminal\n";
    std::cout << "-------------------------\n";
    while (true)
    {
        std::cout << "Command: ";
        std::cin >> user;
        if (user == "exit")
            break;
        else if (user == "clear")
            Clear();
        else if (user == "white")
            std::cout << "\033[0m";
        else if (user == "black")
            std::cout << "\033[30m";
        else if (user == "red")
            std::cout << "\033[31m";
        else if (user == "green")
            std::cout << "\033[32m";
        else if (user == "yellow")
            std::cout << "\033[33m";
        else if (user == "blue")
            std::cout << "\033[34m";
        else if (user == "magenta")
            std::cout << "\033[35m";
        else if (user == "cyan")
            std::cout << "\033[36m";
        else
            std::cout << "\n\033[33mThe command '" << user << "' was not found.\033[0m\n\n";
    }
    main();
}

void OS()
{
    Clear();
    std::cout << "This is the Terminal of your OS.\n";
    std::cout << "-------------------------\n";
    while (true)
    {
        std::cout << "Command: ";
        std::cin >> user;
        if (user == "exit")
            break;
        else
            system(user.c_str());
    }
    main();
}

void ShowTime()
{
    Clear();
    time_t timestamp;
    time(&timestamp);
    std::cout << "Time\n";
    std::cout << "-------------------------\n";
    std::cout << ctime(&timestamp);
    std::cout << "-------------------------\n";
    Asking(ShowTime);
}

void ShowOS()
{
    Clear();
    std::cout << "Your OS is: ";
#ifdef _WIN32
    std::cout << "Windows.\n";
#elif __linux__
    std::cout << "Linux.\n";
#elif __APPLE__
    std::cout << "MacOS.\n";
#else
    std::cout << "Unknown OS.\n"
#endif
    std::cout << "-------------------------\n\n";
    Asking(ShowOS);
}

void Timer()
{
    Clear();
    int sec = 0;
    std::cout << "Timer\n";
    std::cout << "-------------------------\n\n";
    std::cout << "-------------------------\n";
    std::cout << "\033[2AHow long: ";
    std::cin >> sec;
    Clear();
    for (int i = 0; i <= sec; i++)
    {
        std::cout << "\rSeconds: " << i;
        std::this_thread::sleep_for(std::chrono::seconds(1));
    }
    Clear();
    Asking(Timer);
}

void Games()
{
    Clear();
    std::cout << "Game Section\n";
    std::cout << "-------------------------\n";
    std::cout << "Exit (exit)\n";
    std::cout << "Number Guessing (guessing)\n";
    std::cout << "Rock Paper Scissors (rps)\n";
    std::cout << "-------------------------\n";
    std::cout << "Option: ";
    std::cin >> user;
    if (user == "exit")
        main();
    else if (user == "guessing")
        Guessing();
    else if (user == "rps")
        RPS();
    else
        Games();
}

void Guessing()
{
    Clear();
    srand(time(0));
    int num = rand() % 100 + 1;
    int guess = 0;
    int tries = 0;
    std::cout << "Number Guessing\n";
    std::cout << "Guess a number between 1 - 100\n";
    std::cout << "-------------------------\n";
    while (true)
    {
        tries++;
        std::cout << "Your Guess: ";
        std::cin >> guess;
        if (guess == num)
            break;
        else if (guess < num)
            std::cout << "\n\033[31mToo Low!\033[0m\n\n";
        else if (guess > num)
            std::cout << "\n\033[31mToo High!\033[0m\n\n";
    }
    std::cout << "\033[32m\nCorrect! You guessed the number " << num << " in " << tries << " tries.\033[0m\n\n";

    std::cout << "Again (again)\n";
    std::cout << "Back (back)\n\n";
    std::cout << "Option: ";
    std::cin >> user;
    if (user == "again")
        Guessing();
    else
        Games();
}

void RPS()
{
    Clear();
    srand(time(0));
    char player = '\0';
    int ai = 0;
    std::cout << "Rock-Paper-Scissors\nRock(r), Paper(p), Scissors(s), Exit(e)\n";
    std::cout << "-------------------------\n";
    while (true)
    {
        ai = rand() % 3;
        std::cout << "Your Try: ";
        std::cin >> player;
        if (player == 'e')
            break;
        else if (player == 'r' && ai == 0)
            std::cout << "\n\033[33mI have Rock too. Tie!\033[0m\n\n";
        else if (player == 'p' && ai == 1)
            std::cout << "\n\033[33mI have Paper too. Tie!\033[0m\n\n";
        else if (player == 's' && ai == 2)
            std::cout << "\n\033[33mI have Scissors too. Tie!\033[0m\n\n";
        else if (player == 'r' && ai == 1)
            std::cout << "\n\033[31mI have Paper. You Lost!\033[0m\n\n";
        else if (player == 'p' && ai == 2)
            std::cout << "\n\033[31mI have Scissors. You Lost!\033[0m\n\n";
        else if (player == 's' && ai == 0)
            std::cout << "\n\033[31mI have Rock. You Lost!\033[0m\n\n";
        else if (player == 'r' && ai == 2)
            std::cout << "\n\033[32mI have Scissors. You Won!\033[0m\n\n";
        else if (player == 'p' && ai == 0)
            std::cout << "\n\033[32mI have Rock. You Won!\033[0m\n\n";
        else if (player == 's' && ai == 1)
            std::cout << "\n\033[32mI have Paper. You Won!\033[0m\n\n";
        else
            std::cout << "\n\033[33mInvalid Try!\033[0m\n\n";
    }
    Games();
}
