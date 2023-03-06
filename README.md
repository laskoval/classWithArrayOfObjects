# classWithArrayOfObjects
The appliction includes the interactive menu with 4 options - displaying, selling, reporting, and quiting. Records stored in the class. There is an array of objects.  3 files -  header, implementation and main -are dipslayed with different actions.
cat tickets.h
#include <iostream>

class tickets{
 private:
  int artistsCircle;
  int mainFloor;
  int balcony;

  public:
  void displayInventory();
  int getArtistSeats()const;
  int getFloorSeats()const;
  int getBalconySeats()const;
  tickets();
  void update(char pLetter, int numTicket);
};
#include "ticketsImp.cpp"

bash-4.2$ cat ticketsImp.cpp
#include <iostream> 

using namespace std;

tickets::tickets(){
 artistsCircle = 25;
 mainFloor = 400;
 balcony = 200;
}

int tickets::getArtistSeats()const
{
  return artistsCircle;
}

int tickets::getFloorSeats() const
{
  return mainFloor;
}

int tickets::getBalconySeats() const
{
  return balcony;
}

void tickets::displayInventory()
{
cout << "Artist's Circle: "<< getArtistSeats()  << endl;
cout << "Main Floor: " << getFloorSeats() << endl;
cout << "Balcony: " << getBalconySeats() << endl;
}
void tickets::update(char pLetter, int numTickets)
{ 
 switch(pLetter){
 case 'A':
 case 'a':
 artistsCircle -= numTickets;
 break;

 case 'M':
 case 'm':
 mainFloor -= numTickets;
 break;

 case 'B':
 case 'b':
balcony -= numTickets;
 break;
}
}
bash-4.2$ cat tickets.cpp
//Title:    Faculty Overload Reports
////Name:     Lidia Laskova
////Course:   CSCI241
////Instructor: Professor Gunnett
////Due date:   February 23, 2023
//
////This program stores 3 types of concert tickets
////The program shows a menu with 4 options:
//// D - display the number of available tickets on a certain day
//// S - sell tickets of a certain type for a particular day
//// R - show the report of all available tickets for each of 21 days
//// Q - quit the program


#include <iostream>
#include "tickets.h"


using namespace std;

void showSelection();
int whichDay(); //Validate the number of the day
char typeLetter(); 
const int NUMBER_DAYS=21; // Maximum number of days
int main(){

tickets days[NUMBER_DAYS+1]; 

char choice; // variable to hold the selection
showSelection();
cin >> choice; //read the choice

//depending on which letter the user puts, do different actions
while((choice != 'Q') && (choice !='q'))
{
 switch(choice)
{
//Dsiplay avaiable tickets for certain day
  case 'D':
  case 'd':
 int number;//variable to hold the number of the day
number = whichDay();//validate the day
days[number].displayInventory();
    break;
//Sell tickets for certain day
  case 'S':
  case 's':
  int numOfTicket; // desirable number of tickets to buy
 number = whichDay();
  cout << "Enter A for Artist Circle Seats "<< endl;
  cout << "Enter M for Main Floor Seats " << endl;
  cout << "Enter B for Balcone Seats " << endl; 
  char letter;//variable to hold the letter for the type ticket
 letter = typeLetter(); //validate the letter
  cout << "Enter number of tickets to be sold ";
  cin >> numOfTicket;
     if(letter == 'A'|| letter =='a')
        if(numOfTicket <=days[number].getArtistSeats())
          days[number].update(letter, numOfTicket);
            else 
               cout << "There are not enough sets, please try again." << endl;
  
     else if(letter == 'M' || letter =='m')
        if(numOfTicket <= days[number].getFloorSeats())
          days[number].update(letter, numOfTicket);
             else
               cout << "There are not enough sets, please try again." << endl;
     
     else if(letter == 'B' || letter =='b')
        if(numOfTicket <= days[number].getBalconySeats())
          days[number].update(letter, numOfTicket);
             else
               cout << "There are not enough sets, choose another type of seats" << endl; 
 break;
//Report of all days and available tickets
  case 'R':
  case 'r':
for(int i=1; i < NUMBER_DAYS+1; i++)
{ cout << "Day " <<i << endl;
  days[i].displayInventory();
}
    break;
  default:
    cout << "Invalid selection." << endl;
} //end of switch
showSelection();
cin >> choice;
} //end of while
return 0;
}




void showSelection()
{ //Display the menu with 4 options:
 //Display the number of available ticktes for certain day
 //Sell tickets 
 //Report all avaiable tickets for all days
 //Quit the program
    cout << endl;
    cout << "*** Welcome to Concert Ticket Inventory ***" << endl;
    cout << "To select a transaction, enter " << endl;
    cout << "D for Display Inventory" << endl;
    cout << "S for Sell Tickets " << endl;
    cout << "R for Report" << endl;
    cout << "Q for quit the program" << endl;
}


char typeLetter(){
// Validate the letter for the type of the ticket
// The letter should be A,a or M,m or B,b

char letter;
do{
cout << "Please enter A, M, or B for the type ticket" << endl;
cin >> letter;
}while (letter !='A' && letter !='a' && letter !='M' && letter !='m' && letter !='B' && letter !='b' );
return letter;
}
int whichDay(){
// Validate the number that has been entered by user
// The number should between 1 and 21, if not, display the message
int day;
do {
cout <<"Please enter the number of the day 1-21" << endl;
cin >> day;
} while ( day < 1 || day > NUMBER_DAYS);
return day;
}
bash-4.2$ c++ tickets.cpp
bash-4.2$ ./a.out

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
S
Please enter the number of the day 1-21
1
Enter A for Artist Circle Seats 
Enter M for Main Floor Seats 
Enter B for Balcone Seats 
Please enter A, M, or B for the type ticket
M
Enter number of tickets to be sold 12

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
S
Please enter the number of the day 1-21
21
Enter A for Artist Circle Seats 
Enter M for Main Floor Seats 
Enter B for Balcone Seats 
Please enter A, M, or B for the type ticket
B
Enter number of tickets to be sold 8

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
S
Please enter the number of the day 1-21
11
Enter A for Artist Circle Seats 
Enter M for Main Floor Seats 
Enter B for Balcone Seats 
Please enter A, M, or B for the type ticket
A
Enter number of tickets to be sold 3

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
S
Please enter the number of the day 1-21
11
Enter A for Artist Circle Seats 
Enter M for Main Floor Seats 
Enter B for Balcone Seats 
Please enter A, M, or B for the type ticket
B
Enter number of tickets to be sold 5

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
D
Please enter the number of the day 1-21
1
Artist's Circle: 25
Main Floor: 388
Balcony: 200

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
D
Please enter the number of the day 1-21
11
Artist's Circle: 22
Main Floor: 400
Balcony: 195

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
S
Please enter the number of the day 1-21
222
Please enter the number of the day 1-21
22
Please enter the number of the day 1-21
21
Enter A for Artist Circle Seats 
Enter M for Main Floor Seats 
Enter B for Balcone Seats 
Please enter A, M, or B for the type ticket
Y
Please enter A, M, or B for the type ticket
X
Please enter A, M, or B for the type ticket
A
Enter number of tickets to be sold 2

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
S
Please enter the number of the day 1-21
11
Enter A for Artist Circle Seats 
Enter M for Main Floor Seats 
Enter B for Balcone Seats 
Please enter A, M, or B for the type ticket
A
Enter number of tickets to be sold 23
There are not enough sets, please try again.

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
R
Day 1
Artist's Circle: 25
Main Floor: 388
Balcony: 200
Day 2
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 3
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 4
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 5
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 6
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 7
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 8
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 9
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 10
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 11
Artist's Circle: 22
Main Floor: 400
Balcony: 195
Day 12
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 13
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 14
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 15
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 16
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 17
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 18
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 19
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 20
Artist's Circle: 25
Main Floor: 400
Balcony: 200
Day 21
Artist's Circle: 23
Main Floor: 400
Balcony: 192

*** Welcome to Concert Ticket Inventory ***
To select a transaction, enter 
D for Display Inventory
S for Sell Tickets 
R for Report
Q for quit the program
q
bash-4.2$ exit
exit

Script done on Fri 24 Feb 2023 09:44:46 PM EST
