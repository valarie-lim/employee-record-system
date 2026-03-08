#include <iostream>
#include <fstream> // For file input and output
#include <string>
#include <sstream> // For stringstream
#include <cstdlib> // For system()
#include <cstdio> // For remove() & rename() file
#include <cctype>  // For function check input (isdigit)
#include <limits>  // For cin.ignore()
#include <vector> // For dynamic array
#include <windows.h> // WinApi header (display line color in console)
#include <regex> // To check valid input

using namespace std;

HANDLE h = GetStdHandle(STD_OUTPUT_HANDLE); //display line color in console

// structure list
struct Employee {
	string identityNo;
	string firstName;
	string middleName;
	string lastName;
	string age;
	string gender;
	string birthday;
	string contact;
	string email;
	string department;
	string position;
	string employmentDate;
};

//funtion prototype
void menu();
void generalMenu();
void login();
void registration();
void forgotPass();
void addRecord();
void displayRecord();
void searchRecord();
void updateRecord();
void deleteRecord();
void generalSearchRecord();
void navMenu();
void generalNavMenu();



//Global Variable Declaration
Employee record;
Employee updatedRecord;
int choice; //for use in switch case choice
char action; //for use in question Yes or No
string option; //for use in searching confirmation
fstream file;
 
//Main
int main()
{
	//login page
	while (true) {
		system("cls");
		cout << "\n\n";
		SetConsoleTextAttribute(h, 6);
		cout << " ----------------------------------------------------------" << endl;
		cout << "|================  Employee Record System  ================|" << endl;
		cout << "|                                                          |" << endl;
		cout << "|================== = XYZ SUPERMARKET = ===================|" << endl;
		cout << " ----------------------------------------------------------" << endl;
		cout << "\n\n";
		SetConsoleTextAttribute(h, 2);
		cout << "   WELCOME TO XYZ SUPERMARKET EMPLOYEE DATABASE VER 1.0\n" << endl;

		SetConsoleTextAttribute(h, 7);
		cout << "\t 1. Login as administrator" << endl;
		cout << "\t 2. Register as administrator" << endl;
		cout << "\t 3. Search record as general user" << endl;
		cout << "\n\t 0. Exit" << endl;

		SetConsoleTextAttribute(h, 3);
		cout << "\n\t Please select an option: ";
		cin >> choice;
		cin.ignore(); //ignore any leftover newline character

		SetConsoleTextAttribute(h, 7);
		switch (choice) {
			// CASE 1. Login
		case 1: {
			system("cls");
			login(); // call login function
			break;
		} //end CASE 1. Login

		// CASE 2. Register		
		case 2: {
			registration(); //call register function
			break;
		} //end CASE 2. Register

		// CASE 3. general user
		case 3: {
			system("cls");
			generalMenu(); // call general menu function
			break;
		} // end CASE 3. general user

		// CASE 0. Exit	
		case 0: {
			SetConsoleTextAttribute(h, 14);
			cout << "\n\n Thank you for using XYZ Supermarket Employee Record System. \n\n";
			exit(0);
			break;
		} //end CASE 0. Exit

		// DEFAULT
		default:
			cout << " " << endl;
			SetConsoleTextAttribute(h, 12);
			cout << "\n\n\t Invalid input. Press any key to continue... \n";
			cin.get();
			break;
		} //end switch
	} //end while
	return 0;
} // end main


/*FUNCTION - MAIN MENU*/
//Menu
void menu() {
	system("cls");

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                        MAIN MENU                        |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	SetConsoleTextAttribute(h, 7);
	cout << "\t What do you want to do? (choose 0 - 6)" << endl;
	cout << "\t 1. Add new employee record" << endl;
	cout << "\t 2. Search employee record" << endl;
	cout << "\t 3. Update employee record" << endl;
	cout << "\t 4. Delete employee record" << endl;
	cout << "\t 5. Display all employee records" << endl;
	cout << "\t 6. Logout" << endl;
	cout << "\n\t 0. Exit " << endl;

	SetConsoleTextAttribute(h, 3);
	cout << "\n\t Please select an option: ";
	cin >> choice;
	cin.ignore();

	SetConsoleTextAttribute(h, 7);
	switch (choice)
	{
		// 1. Add Record (admin)
	case 1: {
		system("cls");
		addRecord(); // Call function add record
		break;
	}
		  // 2. Search Record (admin)							
	case 2: {
		system("cls");
		searchRecord(); // Call function search record
		break;
	}
		  //3. Update Record (admin)						
	case 3: {
		system("cls");
		updateRecord(); // Call function update record
		break;
	}
		  // 4. Delete Record (admin)							
	case 4: {
		system("cls");
		deleteRecord(); // Call function delete record
		break;
	}
		  // 5. Display Record (admin)							
	case 5: {
		system("cls");
		displayRecord(); // call function display record
		break;
	}
		  //6. Logout (admin)	
	case 6: {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\t Continue to logout [Y/N]?  ";
		cin >> action;
		cin.ignore();
		if (action == 'Y' || action == 'y')
		{
			SetConsoleTextAttribute(h, 10);
			cout << "\n\n You have successfully logout. Press any key to continue...";
			cin.get();
			main();
		}
		else if (action == 'N' || action == 'n')
		{
			SetConsoleTextAttribute(h, 7);
			menu();
		}
		else
			SetConsoleTextAttribute(h, 12);
		cout << "\n\n\t Invalid input. Press any key to continue... \n";
		cin.get();

		SetConsoleTextAttribute(h, 7);
		menu();
		break;
	} // end case 6. logout (admin)

	//0. Exit Program (admin)	
	case 0: {
		SetConsoleTextAttribute(h, 14);
		cout << "\n\n Thank you for using XYZ Supermarket Employee Record System. \n\n";
		exit(0);
		break;
	}
		  //Default
	default:
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\t Invalid input. Press any key to continue... \n";
		cin.get();

		SetConsoleTextAttribute(h, 7);
		menu();
	} //end switch
}//end menu

//General User Menu
void generalMenu() {
	system("cls");

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                       WELCOME USER                      |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";
	SetConsoleTextAttribute(h, 7);
	cout << "\t What do you want to do? (choose 0 - 2)" << endl;
	cout << "\t 1. Search employee record" << endl;
	cout << "\t 2. Return to login page" << endl;
	cout << "\n\t 0. Exit " << endl;

	SetConsoleTextAttribute(h, 3);
	cout << "\n\t Please select an option: ";
	cin >> choice;
	cin.ignore();

	SetConsoleTextAttribute(h, 7);
	switch (choice)
	{
		// case 1. search record (general)
	case 1: {
		generalSearchRecord(); //call function search record (general user)
		break;
	} //end case 1. search record (general) 

	// case 2. return login page (general)
	case 2: {
		main();
		break;
	} // end case 2. return login page (general)

	// case 0. exit program (general)
	case 0: {
		SetConsoleTextAttribute(h, 14);
		cout << "\n\n Thank you for using XYZ Supermarket Employee Record System. \n\n";
		exit(0);
		break;
	} // case 0. exit program (general)

	default:
		SetConsoleTextAttribute(h, 12);
		cout << "\n\t Invalid input. Press any key to continue.... \n" << endl;
		cin.get();
		system("cls");
		break;
	}
	SetConsoleTextAttribute(h, 7);
	generalMenu();

}//end general menu



/*FUNCTION - CHECK INPUT*/
//Function Check Input IC
bool isValidIC(const string& ic) {
	// Regular expression for the format DD-MM-YYYY
	regex icPattern(R"((\d{6})-(\d{2})-(\d{4}))");
	return regex_match(ic, icPattern);
}

//Function Check Input Age
bool isValidAge(const string& age) {
	// Regular expression for the format DD-MM-YYYY
	regex agePattern(R"((\d{2}))");
	return regex_match(age, agePattern);
}

//Function Check Input Contact
bool isValidContact(const string& contact) {
	// Regular expression for the format DD-MM-YYYY
	regex contactPattern(R"(0\d{2,3}-\d{7})");
	return regex_match(contact, contactPattern);
}

//Function Check Input Email
bool isValidEmail(const string& email) {
	// Regular expression for the format DD-MM-YYYY
	regex emailPattern(R"((\w+)(\.\w+)*@(\w+)(\.\w+)+)");
	return regex_match(email, emailPattern);
}

//Function Check Input Date
bool isValidDate(const string& date) {
	// Regular expression for the format DD-MM-YYYY
	regex datePattern(R"((\d{2})-(\d{2})-(\d{4}))");
	return regex_match(date, datePattern);
}

//Function Check Input isdigit
bool isNumber(const string& input) {
	for (char c : input) {
		if (!isdigit(c)) {
			return false;
		}
	}
	return true;
}//end bool

//Function Check Input isstring
bool isString(const string& input) {
	for (char c : input) {
		if (!isalpha(c)) {
			return false;
		}
	}
	return true;
}


/*FUNCTION - ACCOUNT LOGIN, REGISTER, FORGOT PASSWORD*/
//Function Login (DONE)
void login() {
	system("cls");

	string userId, id;
	string password, pass;

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                       ADMIN LOGIN                       |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	SetConsoleTextAttribute(h, 7);
	cout << "\t\t Username : ";
	cin >> userId;
	cout << "\t\t Password : ";
	cin >> password;

	ifstream input("Login_Records.txt");

	int count = 0;
	while (input >> id >> pass) {
		if (id == userId && pass == password)
			count = 1;
	} //end while
	input.close();

	if (count == 1) {
		SetConsoleTextAttribute(h, 10);
		cout << "\n\n\t Welcome " << userId << ", you have successfully log in." << endl;
		cout << "\t Press any key to continue... ";
		cin.ignore();
		cin.get();
		SetConsoleTextAttribute(h, 7);
		menu();
	} //end if
	else {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\t Your login attempt was unsuccessful.\n" << endl;
		cout << "\t Please check your username and password!";

		SetConsoleTextAttribute(h, 3);
		cout << "\n\n forgot password? [Y: reset password /N: proceed as user] ";
		cin >> action;
		cin.ignore();

		if (action == 'Y' || action == 'y') {
			forgotPass();
		}//end if
		else if (action == 'N' || action == 'n') {
			SetConsoleTextAttribute(h, 7);
			generalNavMenu();
		}//end else if
		else {
			SetConsoleTextAttribute(h, 12);
			cout << "\n\n\t Invalid input. Press any key to continue... \n";
			cin.get();
			SetConsoleTextAttribute(h, 7);
			menu();
		}//end else
	} //end else
} //end Function Login

//Function Register Account (DONE)
void registration() {
	system("cls");

	string registerUserId;
	string registerPass;

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                     CREATE ACCOUNT                      |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	SetConsoleTextAttribute(h, 7);
	cout << "\t\t Username : ";
	cin >> registerUserId;
	cout << "\t\t Password : ";
	cin >> registerPass;

	ofstream loginFile("Login_Records.txt", ios::app); //open file 
	loginFile << registerUserId << ' ' << registerPass << endl; //write input into file

	loginFile.close();
	SetConsoleTextAttribute(h, 10);
	cout << "\n\t Account created. Press any key to continue... \n";
	cin.ignore();
	cin.get();

	SetConsoleTextAttribute(h, 7);
	main(); //return to main function
} //end Function Register Account

//Function Reset Password
void forgotPass() {
	system("cls");

	//open file for username and password
	file.open("Login_Records.txt");

	if (!file) { //check if file open successful
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	} //end if

	//read the file and search for the record
	vector<string> loginRecords;
	string userPass;

	//read the file into the vector
	while (getline(file, userPass)) {
		loginRecords.push_back(userPass);
	}//end while

	//close input file after reading
	file.close();

	string forgotPassId;

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|            RESET PASSWORD WITH YOUR USERNAME            |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	SetConsoleTextAttribute(h, 7);
	cout << "\t Enter last username you remember: ";
	cin >> forgotPassId;

	//read the record into stringstream and formatted each line
	string username, password;
	bool found = false;
	bool checkUsername = false;

	//read the record into stringstream and formatted each line
	for (size_t i = 0; i < loginRecords.size(); ++i) {
		if (loginRecords[i].find(forgotPassId) != string::npos) {
			stringstream sts(loginRecords[i]); //create a string stream from the read line
			sts >> username >> password;
			found = true;
			if (username == forgotPassId) {
				checkUsername = true;
				SetConsoleTextAttribute(h, 10);
				cout << "\n\t Username Found ! " << username << endl;
				cout << "\n";
				SetConsoleTextAttribute(h, 7);
				break;
			}//end if
		}//end if
	} //end for

	//if no username was found after the loop
	if (!checkUsername) {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\n\t No records found matching: " << forgotPassId << endl;
		SetConsoleTextAttribute(h, 12);
		cout << "\n\t Press any key to continue..." << endl;
		cin.ignore();
		cin.get();
		SetConsoleTextAttribute(h, 7);
		main();
	}//end if

	//open temp file for writing
	ofstream tempLoginFile("temp_login.txt");

	if (!tempLoginFile) { //check if found open successfully
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	}//end if

	//prompt user to update a new password
	string newPass;
	string confirmPass;
	do {
		SetConsoleTextAttribute(h, 7);
		cout << "\t Enter new password: ";
		cin >> newPass;
		cin.ignore();
		cout << "\t Confirm your new password: ";
		cin >> confirmPass;
		cin.ignore();
		if (newPass != confirmPass) { //check if new password are same with confirm password
			SetConsoleTextAttribute(h, 12);
			cout << "\n\t Your password do not match. Please try again!\n\n" << endl;
		}//end of
	} while (newPass != confirmPass); //end do-while loop

	//create the modify line into new string
	string newLoginRecord = forgotPassId + " " + newPass + "\n";

	//output new data to temp file
	bool updatedWritten = false; //flag to prevent duplicate updates
	for (size_t i = 0; i < loginRecords.size(); ++i) {
		if (loginRecords[i].find(forgotPassId) != string::npos) {
			tempLoginFile << newLoginRecord;
		}//end if
		else {
			tempLoginFile << loginRecords[i] << endl; //write other record to file not contain the search id
		}//end else
	}//end for

	//close output file after writing
	tempLoginFile.close();

	//replace original file with temp file
	remove("Login_Records.txt");
	rename("temp_login.txt", "Login_Records.txt");

	//clear the remaining data in vector
	loginRecords.clear();

	system("cls");
	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|            RESET PASSWORD WITH YOUR USERNAME            |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";
	SetConsoleTextAttribute(h, 10);
	cout << "\n\n\n\t Your password has been successfully reset.\n" << endl;
	cout << "\t Press any key to continue to login...\n" << endl;
	cin.get();
	SetConsoleTextAttribute(h, 7);
	login();

}//end Function Reset Password


/*MAIN MENU FUNCTION - ADD, DISPLAY ALL, SEARCH, UPDATE, DELETE */
//Function Add Record (DONE)
void addRecord() {
	system("cls");

	Employee record;

	//open file to edit
	file.open("Employee_Records.txt", ios::out | ios::app); //read file


	if (!file) { //check if file open successful
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\n\t\t Error: Could not create file! " << endl;
		menu();
	} // end if

	//prompt user to input record detail
	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                   ADD NEW EMPLOYEE RECORD               |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";
	SetConsoleTextAttribute(h, 3);
	cout << "\t\t Complete the Detail Below." << endl;
	cout << "----------------------------------------------------------" << endl;

IC:
	SetConsoleTextAttribute(h, 7);
	cout << "\n   Malaysia IC No. \n";
	cout << "  [XXXXXX-XX-XXXX]) \t\t: ";
	getline(cin, record.identityNo);
	if (isValidIC(record.identityNo)) { //check if IC input valid

		cout << "  First Name \t\t\t: ";
		getline(cin, record.firstName);
		cout << "  Middle Name \t\t\t: ";
		getline(cin, record.middleName);
		cout << "  Last Name (Surname) \t\t: ";
		getline(cin, record.lastName);
	Age:
		cout << "  Age \t\t\t\t: ";
		getline(cin, record.age);
		if (isValidAge(record.age)) { //check if age input valid

		Gender:
			cout << "  Gender [1.Male/2.Female]\t: ";
			cin >> choice;
			cin.ignore();
			switch (choice) { //display gender base on user choice
			case 1:
				cout << "\t\t\t\t Male" << endl;
				record.gender = "Male";
				break;
			case 2:
				cout << "\t\t\t\t Female" << endl;
				record.gender = "Female";
				break;
			default:
				cout << "\n Invalid input. Please choose 1. for male / 2. for female.";
				goto Gender;
				break;
			}//end switch gender

		Birthday:
			cout << "  Birthday [DD-MM-YYYY] \t: ";
			getline(cin, record.birthday);
			if (isValidDate(record.birthday)) {

			Contact:
				cout << "  Contact no. [XXX-XXXXXXX]\t: ";
				getline(cin, record.contact);
				if (isValidContact(record.contact)) {

				Email:
					cout << "  Email \t\t\t: ";
					getline(cin, record.email);
					if (isValidEmail(record.email)) {

					Department:
						cout << "  Department \t\t\t: ";
						getline(cin, record.department);

					Position:
						cout << "  Job Position \t\t\t: ";
						getline(cin, record.position);

					EmploymentDate:
						cout << "  Employment Date [DD-MM-YYYY]  : ";
						getline(cin, record.employmentDate);
						if (isValidDate(record.employmentDate)) {
							goto PrintRecord;
						}//end if employment date

						else {
							SetConsoleTextAttribute(h, 12);
							cout << "\n\t Invalid input. Please input a valid date.\n";
							SetConsoleTextAttribute(h, 7);
							goto EmploymentDate;
						}//end else employment date
					}//end if email
					else {
						SetConsoleTextAttribute(h, 12);
						cout << "\n\t Invalid input. Please input a valid email.\n";
						SetConsoleTextAttribute(h, 7);
						goto Email;
					}//end else email
				}//end if contact
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please follow the format.\n";
					SetConsoleTextAttribute(h, 7);
					goto Contact;
				}//end else contact
			}//end if birthday
			else {
				SetConsoleTextAttribute(h, 12);
				cout << "\n\t Invalid input. Please follow the format.\n";
				SetConsoleTextAttribute(h, 7);
				goto Birthday;
			}//end else birthday
		}//end if age
		else {
			SetConsoleTextAttribute(h, 12);
			cout << "\n\t Invalid input. Please input a valid number for age.\n";
			SetConsoleTextAttribute(h, 7);
			goto Age;
		}//end else age
	}// end if IC
	else {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\t Invalid input. Please follow the format.\n";
		SetConsoleTextAttribute(h, 7);
		goto IC;
	}//end else IC

PrintRecord:
	//print employee details to file
	file << record.identityNo
		<< "\t" << record.firstName
		<< "\t" << record.middleName
		<< "\t" << record.lastName
		<< "\t" << record.age
		<< "\t" << record.gender
		<< "\t" << record.birthday
		<< "\t" << record.contact
		<< "\t" << record.email
		<< "\t" << record.department
		<< "\t" << record.position
		<< "\t" << record.employmentDate
		<< "\t" << "\n";

	SetConsoleTextAttribute(h, 10);
	cout << "\n\n\t The new employee details has been added. \n\n" << endl;

	//close file
	file.close();

	SetConsoleTextAttribute(h, 7);
	navMenu(); //call function navigation menu
}; //end Function Add Record

//Function Display Record (DONE)
void displayRecord() {
	system("cls");

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                  ALL EMPLOYEES' RECORD                  |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	//open file and read record
	file.open("employee_records.txt", ios::in);

	if (!file) { // check if file open successful
		SetConsoleTextAttribute(h, 3);
		cout << "\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
	} //end if

	//read record into a vector
	vector<string> searchDisplay;
	string line;
	while (getline(file, line)) { //read line by line
		searchDisplay.push_back(line);
	}//end while

	//display result with field labels
	for (const auto& line : searchDisplay) {
		stringstream sts(line);
		string formatted;
		int formattedIndex = 0;

		SetConsoleTextAttribute(h, 7);
		while (getline(sts, formatted, '\t')) {
			switch (formattedIndex) {
			case 0: cout << "\t" << "Malaysia IC \t: "; break;
			case 1: cout << "\t" << "First Name \t: "; break;
			case 2: cout << "\t" << "Middle Name \t: "; break;
			case 3: cout << "\t" << "Last Name \t: "; break;
			case 4: cout << "\t" << "Age \t\t: "; break;
			case 5: cout << "\t" << "Gender \t\t: "; break;
			case 6: cout << "\t" << "Birth Date \t: "; break;
			case 7: cout << "\t" << "Contact No.\t: "; break;
			case 8: cout << "\t" << "Email \t\t: "; break;
			case 9: cout << "\t" << "Department   \t: "; break;
			case 10: cout << "\t" << "Job Position \t: "; break;
			case 11: cout << "\t" << "Employment Date : "; break;
			}//end switch
			cout << formatted << endl;
			formattedIndex++;
		}//end while
		cout << "\n\n";
	}//end for

	//close file
	file.close();
	//clear the remaining data in vector
	searchDisplay.clear();

	navMenu(); //call function navigation menu
};

//Function Search Record (DONE)
void searchRecord() {
	system("cls");

	//open file and read record
	file.open("employee_records.txt", ios::in); //read file

	if (!file) { //check if file open successful
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	} //end if

	//prompt user for search keyword

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                 SEARCH EMPLOYEE RECORD                  |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	bool validInput = false;

	do {
		SetConsoleTextAttribute(h, 3);
		cout << "\t Enter Employee IC Number: ";
		getline(cin, option);
		cout << "\n\n";

		if (!isValidIC(option)) { //check if search input valid
			SetConsoleTextAttribute(h, 12);
			cout << "\t Invalid input. Please enter a valid IC Number.\n" << endl;
		}//end if check search input
		else {
			validInput = true;
		}
	} while (!validInput); //end do-while loop

	//search the keyword line by line
	vector<string> searchRec;
	string line;
	bool found = false;
	int lineCount = 0;

	while (getline(file, line)) {
		if (line.find(option) != string::npos) { //check if search term is found
			found = true;
			stringstream ss(line); //create a string stream from the read line
			string formatted;
			int lineIndex = 0;

			SetConsoleTextAttribute(h, 7);
			while (getline(ss, formatted, '\t')) { //split the line by tab delimiter \t and print each line
				switch (lineIndex) {
				case 0: cout << "\t" << "Malaysia IC \t: "; break;
				case 1: cout << "\t" << "First Name \t: "; break;
				case 2: cout << "\t" << "Middle Name \t: "; break;
				case 3: cout << "\t" << "Last Name \t: "; break;
				case 4: cout << "\t" << "Age \t\t: "; break;
				case 5: cout << "\t" << "Gender \t\t: "; break;
				case 6: cout << "\t" << "Birth Date \t: "; break;
				case 7: cout << "\t" << "Contact No.\t: "; break;
				case 8: cout << "\t" << "Email \t\t: "; break;
				case 9: cout << "\t" << "Department   \t: "; break;
				case 10: cout << "\t" << "Job Position \t: "; break;
				case 11: cout << "\t" << "Employment Date : "; break;
				}//end switch

				cout << formatted << endl;
				lineIndex++;
			}//end while
			cout << "\n\n";
			break; //exit loop after record found
		} //end if
	} //end while

	//print if search not found
	if (!found) {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\n\t No records found matching: " << option << endl;
	} //end if

	//close file
	file.close();

	//clear the remaining data in vector
	searchRec.clear();

	SetConsoleTextAttribute(h, 7);
	navMenu(); //call function navigation menu	
} //end Function Search Record

//Function Update Record ()
void updateRecord() {
	system("cls");

	//open and read file
	file.open("employee_records.txt", ios::in);

	if (!file) { //check if found open successfully
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	}//end if

	//prompt user to search for an ID
	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                 UPDATE EMPLOYEE RECORD                  |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	bool validInput = false;

	do {
		SetConsoleTextAttribute(h, 3);
		cout << "\t Enter Employee IC Number: ";
		getline(cin, option);
		cout << "\n\n";

		if (!isValidIC(option)) { //check if search input valid
			SetConsoleTextAttribute(h, 12);
			cout << "\t Invalid input. Please enter a valid IC Number.\n" << endl;
		}//end if check search input
		else {
			validInput = true;
		}//end else
	} while (!validInput); //end do-while loop

	//read the file and search for the record
	vector<string> modifyRecord;
	string line;
	string searchTerm = option; // Replace with the actual search term

	//read the file into the vector
	while (getline(file, line)) {
		modifyRecord.push_back(line);
	}//end while

	//close input file after reading
	file.close();

	//iterate through the vector and search for the term
	bool found = false;
	for (size_t i = 0; i < modifyRecord.size(); ++i) {
		if (modifyRecord[i].find(searchTerm) != string::npos) {
			// If the search term is found, modify the line
			SetConsoleTextAttribute(h, 10);
			cout << "\tEmployee Found: \n" << endl;

			stringstream ss(modifyRecord[i]); //create a string stream from the read line
			string formatted;
			int lineIndex = 0;

			SetConsoleTextAttribute(h, 7);
			while (getline(ss, formatted, '\t')) { //split the line by tab delimiter \t and print each line
				switch (lineIndex) {
				case 0: cout << "\t (A)  Malaysia IC \t: "; break;
				case 1: cout << "\t (B)  First Name \t: "; break;
				case 2: cout << "\t (C)  Middle Name \t: "; break;
				case 3: cout << "\t (D)  Last Name \t: "; break;
				case 4: cout << "\t (E)  Age \t\t: "; break;
				case 5: cout << "\t (F)  Gender \t\t: "; break;
				case 6: cout << "\t (G)  Birth Date \t: "; break;
				case 7: cout << "\t (H)  Contact No.\t: "; break;
				case 8: cout << "\t (I)  Email \t\t: "; break;
				case 9: cout << "\t (J)  Department   \t: "; break;
				case 10: cout << "\t (K)  Job Position \t: "; break;
				case 11: cout << "\t (L)  Employment Date   : "; break;
				}//end switch

				cout << formatted << endl;
				lineIndex++;
			}//end while
			cout << "\n";
			break; // Stop the loop after finding the first match
		}//end if
	} //end for

	//read the record into stringstream and formatted each line
	for (size_t i = 0; i < modifyRecord.size(); ++i) {
		if (modifyRecord[i].find(searchTerm) != string::npos) {
			stringstream sts(modifyRecord[i]); //create a string stream from the read line
			getline(sts, record.identityNo, '\t');
			getline(sts, record.firstName, '\t');
			getline(sts, record.middleName, '\t');
			getline(sts, record.lastName, '\t');
			getline(sts, record.age, '\t');
			getline(sts, record.gender, '\t');
			getline(sts, record.birthday, '\t');
			getline(sts, record.contact, '\t');
			getline(sts, record.email, '\t');
			getline(sts, record.department, '\t');
			getline(sts, record.position, '\t');
			getline(sts, record.employmentDate, '\t');
		}//end if
	} //end for

	//open temp file for writing
	ofstream tempFile("temp.txt"); //open in trunc mode to clear previous content

	if (!tempFile) { //check if found open successfully
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	}//end if

	//prompt user for update action
UpdateRecord:
	cout << endl;
	cout << " ----------------------------------------------------------" << endl;
	SetConsoleTextAttribute(h, 6);
	cout << "\n Enter (1) to edit a line, enter (0) to return to menu: ";
	cin >> choice;

	if (choice == 0) {
		SetConsoleTextAttribute(h, 6);
		cout << "\n\t Edit request has been cancelled.\n\n";
		SetConsoleTextAttribute(h, 7);
		menu();
	}//end if

	else if (choice == 1) {
		// Prompt user to choose the line to edit
		SetConsoleTextAttribute(h, 6);
		cout << "\n Choose the assigned alphabet (A - L) to that line: ";
		char editChoice;
		cin >> editChoice;
		cin.ignore();

		switch (editChoice) {
		case 'A': //Malaysia IC
		case 'a':
		{
			bool validICInput = false;

			while (!validICInput) {
				SetConsoleTextAttribute(h, 6);
				cout << "\n\t   Malaysia IC No.\n";
				cout << "\t  [XXXXXX-XX-XXXX]) \t\t: ";
				getline(cin, record.identityNo);
				cin.ignore();

				if (isValidIC(record.identityNo)) {
					validICInput = true; //check if input is true, break loop
				}//end if
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please follow the format.\n";
				}//end else
			}//end while
			goto StoreRecord;

			break;
		}// end case A

		case 'B': //First Name
		case 'b':
		{
			SetConsoleTextAttribute(h, 6);
			cout << "\t  First Name : ";
			cin >> record.firstName;
			cin.ignore();
			goto StoreRecord;
			break;
		}// end case B
		break;

		case 'C': //Middle Name
		case 'c':
		{
			SetConsoleTextAttribute(h, 6);
			cout << "\t  Middle Name : ";
			cin.ignore();
			goto StoreRecord;
			break;
		}// end case C
		break;

		case 'D': //Last Name
		case 'd':
		{
			SetConsoleTextAttribute(h, 6);
			cout << "\t  Last Name : ";
			cin >> record.lastName;
			cin.ignore();
			goto StoreRecord;
			break;
		}// end case D

		case 'E': //Age
		case 'e':
		{
			bool validAgeInput = false;

			while (!validAgeInput) {
				SetConsoleTextAttribute(h, 6);
				cout << "\t  Age : ";
				cin >> record.age;
				cin.ignore();

				if (isValidAge(record.age)) {
					validAgeInput = true; //check if input is true, break loop
				}//end if
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please input numeral only.\n";
				}//end else
			}//end while
			goto StoreRecord;
			break;
		}// end case E

		case 'F': //Gender
		case 'f':
		{
		Gender:
			SetConsoleTextAttribute(h, 6);
			cout << "\t  Gender [1.Male/2.Female] : ";
			cin >> choice;
			cin.ignore();

			switch (choice) { //display gender base on user choice
			case 1:
				cout << "\t\t\t Male" << endl;
				record.gender = "Male";
				break;
			case 2:
				cout << "\t\t Female" << endl;
				record.gender = "Female";
				break;
			default:
				SetConsoleTextAttribute(h, 12);
				cout << "\n Invalid input. Please choose 1. for male / 2. for female.";
				goto Gender;
				break;
			}//end switch gender
			goto StoreRecord;
			break;
		}// end case F

		case 'G': //Birthday
		case 'g':
		{
			bool validDateInput = false;

			while (!validDateInput) {
				SetConsoleTextAttribute(h, 6);
				cout << "\t  Birth Date [DD-MM-YYYY] : ";
				cin >> record.birthday;
				cin.ignore();

				if (isValidDate(record.birthday)) {
					validDateInput = true; //check if input is true, break loop
				}//end if
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please enter a valid date.\n";
				}//end else
			}//end while
			goto StoreRecord;
			break;
		}// end case G

		case 'H': //Contact
		case 'h':
		{
			bool validContactInput = false;

			while (!validContactInput) {
				SetConsoleTextAttribute(h, 6);
				cout << "\t  Contact No. [XXX-XXXXXXX] : ";
				cin >> record.contact;
				cin.ignore();

				if (isValidContact(record.contact)) {
					validContactInput = true; //check if input is true, break loop
				}//end if
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please enter a valid contact number.\n";
				}//end else
			}//end while
			goto StoreRecord;
			break;
		}// end case H

		case 'I': //Email
		case 'i':
		{
			bool validEmailInput = false;

			while (!validEmailInput) {
				SetConsoleTextAttribute(h, 6);
				cout << "\t  Email : ";
				cin >> record.email;
				cin.ignore();

				if (isValidEmail(record.email)) {
					validEmailInput = true; //check if input is true, break loop
				}//end if
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please enter a valid email.\n";
				}//end else
			}//end while
			goto StoreRecord;
			break;
		}// end case I

		case 'J': //Department
		case 'j':
		{
			SetConsoleTextAttribute(h, 6);
			cout << "\t  Department : ";
			cin >> record.department;
			cin.ignore();
			goto StoreRecord;
			break;
		}// end case J

		case 'K': //Job Position
		case 'k':
		{
			SetConsoleTextAttribute(h, 6);
			cout << "\t  Job Position : ";
			getline(cin, record.position);
			goto StoreRecord;
			break;
		}// end case K

		case 'L': //Deployment Date
		case 'l':
		{
			bool validDateInput = false;

			while (!validDateInput) {
				SetConsoleTextAttribute(h, 6);
				cout << "\t  Employment Date [DD-MM-YYYY] : ";
				cin >> record.employmentDate;
				cin.ignore();

				if (isValidDate(record.employmentDate)) {
					validDateInput = true; //check if input is true, break loop
				}//end if
				else {
					SetConsoleTextAttribute(h, 12);
					cout << "\n\t Invalid input. Please enter a valid date.\n";
				}//end else
			}//end while
			goto StoreRecord;
			break;
		}// end case L

		default:
		{
			SetConsoleTextAttribute(h, 12);
			cout << "Invalid input. Press any key to continue...";
			cin.get();
			menu();
			break;
		}//end default
		}//end inner switch

		//output updated record as string
	StoreRecord:
		string updatedRecord = record.identityNo + "\t" +
			record.firstName + "\t" +
			record.middleName + "\t" +
			record.lastName + "\t" +
			record.age + "\t" +
			record.gender + "\t" +
			record.birthday + "\t" +
			record.contact + "\t" +
			record.email + "\t" +
			record.department + "\t" +
			record.position + "\t" +
			record.employmentDate + "\n";

		//output data to temp file
		bool updatedWritten = false; //flag to prevent duplicate updates
		for (size_t i = 0; i < modifyRecord.size(); ++i) {
			if (modifyRecord[i].find(searchTerm) != string::npos) {
				//Write the updated record
				tempFile << updatedRecord;
			}//end if
			else {
				tempFile << modifyRecord[i] << endl;
			}//end else
		}//end for

		//close output file after writing
		tempFile.close();

		//replace original file with temp file
		remove("employee_records.txt");
		rename("temp.txt", "employee_records.txt");

		//clear the remaining data in vector
		modifyRecord.clear();

		system("cls");
		cout << "\n\n";
		SetConsoleTextAttribute(h, 6);
		cout << " ---------------------------------------------------------" << endl;
		cout << "|                 UPDATE EMPLOYEE RECORD                  |" << endl;
		cout << " ---------------------------------------------------------" << endl;
		cout << "\n\n";
		SetConsoleTextAttribute(h, 10);
		cout << "\n\n\n\t Record has been successfully update.\n" << endl;
		SetConsoleTextAttribute(h, 7);
		navMenu();
	}//end else if


	else {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\t Invalid input. Please choose 1 or 0." << endl;
		cin.get();
		SetConsoleTextAttribute(h, 7);
		goto UpdateRecord;
	}//end else

} //end Function Update Record

//Function Delete Record (DONE)
void deleteRecord() {
	system("cls");

	//open and read file
	file.open("employee_records.txt", ios::in);

	if (!file) { //check if found open successfully
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	}//end if

	//prompt user to search for an ID
	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                 DELETE EMPLOYEE RECORD                  |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	bool validInput = false;

	do {
		SetConsoleTextAttribute(h, 3);
		cout << "\t Enter Employee IC Number: ";
		getline(cin, option);
		cout << "\n\n";

		if (!isValidIC(option)) { //check if search input valid
			SetConsoleTextAttribute(h, 12);
			cout << "\t Invalid input. Please enter a valid IC Number.\n" << endl;
		}//end if check search input
		else {
			validInput = true;
		}
	} while (!validInput); //end do-while loop

	//read the file into a vector for searching and deletion
	vector<string> contents;
	string line;
	bool found = false;

	while (getline(file, line)) {
		contents.push_back(line); //store lines for later processing
		if (line.find(option) != string::npos) {
			found = true;
		}//end if
	}//end while

	//close input file
	file.close();

	//print if search not found
	if (!found) {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\n\t No records found matching: " << option << endl;
		navMenu(); // Return to the navigation menu
		return; // Exit the function
	}//end if

	//display search result
	for (const auto& searchDelete : contents) {
		if (searchDelete.find(option) != string::npos) {
			found = true;
			stringstream ss(searchDelete); //create a string stream from the read line
			string formatted;
			int lineIndex = 0;

			SetConsoleTextAttribute(h, 7);
			while (getline(ss, formatted, '\t')) { //split the line by tab delimiter \t and print each line
				switch (lineIndex) {
				case 0: cout << "\t" << "Malaysia IC \t: "; break;
				case 1: cout << "\t" << "First Name \t: "; break;
				case 2: cout << "\t" << "Middle Name \t: "; break;
				case 3: cout << "\t" << "Last Name \t: "; break;
				case 4: cout << "\t" << "Age \t\t: "; break;
				case 5: cout << "\t" << "Gender \t\t: "; break;
				case 6: cout << "\t" << "Birth Date \t: "; break;
				case 7: cout << "\t" << "Contact No.\t: "; break;
				case 8: cout << "\t" << "Email \t\t: "; break;
				case 9: cout << "\t" << "Department   \t: "; break;
				case 10: cout << "\t" << "Job Position \t: "; break;
				case 11: cout << "\t" << "Employment Date : "; break;
				}//end switch

				cout << formatted << endl;
				lineIndex++;
			}//end while

			break; //exit loop after record found
		}//end if
	}//end for


	//prompt user for delete confirmation
ConfirmDelete:
	cout << endl;
	cout << "\n ----------------------------------------------------------" << endl;
	SetConsoleTextAttribute(h, 3);
	cout << "\n Do you want to delete this employee records [Y/N] ? ";
	cin >> action;

	if (action == 'N' || action == 'n') {
		SetConsoleTextAttribute(h, 10);
		cout << "\n\t Record deletion has been cancelled.\n\n";
		SetConsoleTextAttribute(h, 7);
		navMenu();
	}//end if

	else if (action == 'Y' || action == 'y') {

		//create a temporarily file
		ofstream tempFile("temp.txt");

		if (!tempFile) { //check if file open successful 
			SetConsoleTextAttribute(h, 3);
			cout << "\n\n\n\t Error: File not found! " << endl;
			cout << "\t Please try again." << endl;
			SetConsoleTextAttribute(h, 7);
			menu();
		}//end if

			//delete the employee record in the vector
		for (const auto& rec : contents) {
			if (rec.find(option) == string::npos) {
				tempFile << rec << endl;
			}//end if
		}//end for

	//close temp file
		tempFile.close();

		// Remove original file and rename temp file to replace original file
		remove("employee_records.txt");
		rename("temp.txt", "employee_records.txt");

		//clear the remaining data in vector
		contents.clear();

		//print record delete successful message
		system("cls");
		cout << "\n\n";
		SetConsoleTextAttribute(h, 6);
		cout << " ---------------------------------------------------------" << endl;
		cout << "|                 DELETE EMPLOYEE RECORD                  |" << endl;
		cout << " ---------------------------------------------------------" << endl;
		cout << "\n\n";
		SetConsoleTextAttribute(h, 10);
		cout << "\n\n\n\t Record has been succesfully deleted.\n\n" << endl;
		SetConsoleTextAttribute(h, 7);
		navMenu(); //call function navigation menu
	}//end else if

	else {
		SetConsoleTextAttribute(h, 12);
		cout << "Input invalid. Press any key to continue...";
		cin.get();
		SetConsoleTextAttribute(h, 7);
		goto ConfirmDelete;
	}//end else
}//end Function Delete Record

//Function Search Record (general user)
void generalSearchRecord() {
	system("cls");

	//open file and read record
	file.open("employee_records.txt", ios::in); //read file

	if (!file) { //check if file open successful
		SetConsoleTextAttribute(h, 3);
		cout << "\n\n\n\t Error: File not found! " << endl;
		cout << "\t Please try again." << endl;
		menu();
	} //end if

	//prompt user for search keyword

	cout << "\n\n";
	SetConsoleTextAttribute(h, 6);
	cout << " ---------------------------------------------------------" << endl;
	cout << "|                 SEARCH EMPLOYEE RECORD                  |" << endl;
	cout << " ---------------------------------------------------------" << endl;
	cout << "\n\n";

	bool validInput = false;

	do {
		SetConsoleTextAttribute(h, 3);
		cout << "\t Enter Employee IC Number: ";
		getline(cin, option);
		cout << "\n\n";

		if (!isValidIC(option)) { //check if search input valid
			SetConsoleTextAttribute(h, 12);
			cout << "\t Invalid input. Please enter a valid IC Number.\n" << endl;
		}//end if check search input
		else {
			validInput = true;
		}
	} while (!validInput); //end do-while loop

	//search the keyword line by line
	string line;
	bool found = false;
	int lineCount = 0;

	while (getline(file, line)) {
		if (line.find(option) != string::npos) { //check if search term is found
			found = true;
			stringstream ss(line); //create a string stream from the read line
			string formatted;
			int lineIndex = 0;

			SetConsoleTextAttribute(h, 7);
			while (getline(ss, formatted, '\t')) { //split the line by tab delimiter \t and print each line
				switch (lineIndex) {
				case 0: cout << "\t" << "Malaysia IC \t: "; break;
				case 1:	cout << "\t" << "First Name \t: "; break;
				case 2:	cout << "\t" << "Middle Name \t: "; break;
				case 3:	cout << "\t" << "Last Name \t: "; break;
				case 4:	cout << "\t" << "Age \t\t: "; break;
				case 5:	cout << "\t" << "Gender \t\t: "; break;
				case 6: cout << "\t" << "Birth Date \t: "; break;
				case 7:	cout << "\t" << "Contact No.\t: "; break;
				case 8:	cout << "\t" << "Email \t\t: "; break;
				case 9:	cout << "\t" << "Department   \t: "; break;
				case 10:cout << "\t" << "Job Position \t: "; break;
				case 11:cout << "\t" << "Employment Date : "; break;
				}//end switch

				cout << formatted << endl;
				lineIndex++;
			}//end while
			cout << "\n";
			break; //exit loop after record found
		} //end if
	} //end while

	//print if search not found
	if (!found) {
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\n\t No records found matching: " << option << endl;
	} //end if

	//close file
	file.close();

	SetConsoleTextAttribute(h, 7);
	generalNavMenu(); //call general navigation menu function
} //end Function Search Record (general user)



/*FUNCTION - NAVIGATION MENU */
//Function Navigation Menu (DONE)
void navMenu() {

	//prompt user for choice
	SetConsoleTextAttribute(h, 6);
	cout << "---------------------------------------------------------" << endl;
	cout << endl;
	cout << "\t What do you want to do?" << endl;
	cout << "\t (1) Add a new employee record" << endl;
	cout << "\t (2) Search and update record" << endl;
	cout << "\t (3) Search and delete record" << endl;
	cout << "\t (4) Search for another employee" << endl;
	cout << "\n\t (0) Return to menu" << endl;
	SetConsoleTextAttribute(h, 3);
	cout << "\n\t Please select an option: ";
	cin >> choice;
	cin.ignore();

	SetConsoleTextAttribute(h, 7);
	switch (choice)
	{
	case 1:
		addRecord(); // Call function add record
		break;
	case 2:
		updateRecord(); // Call function update record
		break;
	case 3:
		deleteRecord(); // Call function delete record
		break;
	case 4:
		searchRecord(); // Call function search record
		break;
	case 0:
		menu();
		break;
	default:
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\t Invalid input. Press any key to continue... \n";
		cin.get();
		menu();
	}
}//end Function Navigation Menu

//Function Navigation Menu (general user)
void generalNavMenu() {

	//prompt user for choice
	SetConsoleTextAttribute(h, 6);
	cout << "\n\n\n----------------------------------------------------------" << endl;
	cout << "\n\n\t What do you want to do?" << endl;
	cout << "\t (1) Login as administrator to modify record" << endl;
	cout << "\t (2) Continue searching as general user" << endl;
	cout << "\n\t (0) Return to main page" << endl;
	SetConsoleTextAttribute(h, 3);
	cout << "\n\t Please select an option: ";
	cin >> choice;
	cin.ignore();

	SetConsoleTextAttribute(h, 7);
	switch (choice)
	{
	case 1:
		login();
		break;
	case 2:
		generalSearchRecord();
		break;
	case 0:
		main();
		break;
	default:
		SetConsoleTextAttribute(h, 12);
		cout << "\n\n\t Invalid input. Press any key to continue... \n";
		cin.get();
		break;
	} //end switch	
} //end Function Navigation Menu (general user)
