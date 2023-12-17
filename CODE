#include <stdlib.h>
#include <iostream>
#include <conio.h>
#include <sstream>
#include <string>
#include <time.h>
#include <ctime>
#include <dos.h>
#include <windows.h>
#include <fstream>



#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>

#pragma comment(lib, "crypt32")
#pragma comment(lib, "ws2_32.lib")
#pragma warning(disable : 4996)  

using namespace std;

const string server = "localhost";
const string username = "root";
const string password = "shelter*1";

sql::Driver* driver;
sql::Connection* con;
sql::Statement* stmt;
sql::PreparedStatement* pstmt;
sql::ResultSet* result;

// Functions
void ReserveSeat();
void UserTicket();
void FlightSchedule();
void DisplayPassenger();
void FlightDetails();
void AddNewFlight();
void EditFlight();
void DeleteFlight();
void FlightLeaveArrive();
// Functions End

void DBConnection()               //Established the connection to db
{

    driver = get_driver_instance();

    try
    {
        driver = get_driver_instance();
        con = driver->connect(server, username, password);
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to server. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    //please create database "quickstartdb" ahead of time
    con->setSchema("airline");
}

void callHTML(void)
{
    const char* fn= "passenger.html";
    ShellExecute(NULL, "open", fn, NULL, NULL, SW_SHOWNORMAL);
    //writeHTML();  
}

void ScreenColor()
{
    system("color 6");
    /*  0 = Black
        1 = Blue
        2 = Green
        3 = Aqua
        4 = Red
        5 = Purple
        6 = Yellow
        7 = White
        8 = Gray
        9 = Light Blue
        A = Light Green
        B = Light Aqua
        C = Light Red
        D = Light Purple
        E = Light Yellow
        F = Bright White*/

}

int main()
{
    system("cls");
    system("color 09");


    DBConnection();

    int chooseOneFromMenu = 0;
    char exitSurity;

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Airlines Reservation System Menu" << endl;
    cout << "1. Book Your Ticket" << endl;
    cout << "2. User Ticket" << endl;
    cout << "3. Show Flights Schedule" << endl;
    cout << "4. Display Passenger Details" << endl;
    cout << "5. Managing Flight Details" << endl;
    system("color 04");
    cout << "6. Exit Program." << endl;
    system("color 0b");
    cout << "Choose One: ";
    cin >> chooseOneFromMenu;

    switch (chooseOneFromMenu)
    {
    case 1:
        ReserveSeat();
        break;
    case 2:
        UserTicket();
        break;
    case 3:
        FlightSchedule();
        break;
    case 4:
        DisplayPassenger();
        break;
    case 5:
        FlightDetails();
        break;
    case 6:
    ExitProgram:
        cout << "Program terminating. Are you sure? (y/N): ";
        cin >> exitSurity;
        if (exitSurity == 'y' || exitSurity == 'Y') {
            return 0;
        }
        else if (exitSurity == 'n' || exitSurity == 'N') {
            system("cls");
            main();
        }
        else {
            cout << "Invalid Entry" << endl;
            goto ExitProgram;
        }
        break;
    default:
        cout << "Please choose between The Given Numbers. Press Enter To Continue...";
        //getch();
        system("cls");
        main();
        break;
    }
}

void ReserveSeat()
{
    // Get the current time
        time_t current_time = time(NULL);

    // Convert the time to a string using the desired format
    char date_string[20];
    strftime(date_string, 20, "%d-%b-%y", localtime(&current_time));

    // Print the date string
    //printf("The current date is: %s\n", date_string);
        
    // Variables

    string userName = "";
    string userPhone = "";
    string userAddress = "";
    string userTicket = "";
    string userFlightNo = "";
    string userBookdate = date_string;
    string userTraveldate;
    char choose;
    // Variables End

    cin.ignore(1, '\n');
    cout << "Enter Name:\n ";
    getline(cin, userName);
    cout << "Enter Phone No:\n ";
    getline(cin, userPhone);
    cout << "Enter Address:\n ";
    getline(cin, userAddress);
    cout << "Enter PNR No: \n";
    getline(cin, userTicket);
    cout << "Enter Travel Date:\n ";
    getline(cin, userTraveldate);

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Book Your Seat" << endl << endl;


    pstmt = con->prepareStatement("select * from flight_master where f_available = 'A'");
    result = pstmt->executeQuery();

    printf("--------------------------------------------------------------------------------------------------------------------\n");
    printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", "Flight No", "Flight Name", "From", "To", "Dep. Time", "Arr. Time", "Rate");

    while ((result->next()))
    {
        printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", result->getString(2), result->getString(3), result->getString(4), result->getString(5), result->getString(6), result->getString(7), result->getString(8));
    }
    printf("--------------------------------------------------------------------------------------------------------------------\n");

    cout << "Enter Flight No: ";
    getline(cin, userFlightNo);

    pstmt = con->prepareStatement("insert into user_data (u_name, u_phone, u_address, u_ticket, u_flightno, u_bookdate,u_traveldate) values(?,?,?,?,?,?,?)");
    pstmt->setString(1, userName);
    pstmt->setString(2, userPhone);
    pstmt->setString(3, userAddress);
    pstmt->setString(4, userTicket);
    pstmt->setString(5, userFlightNo);
    pstmt->setString(6, userBookdate);
    pstmt->setString(7, userTraveldate);
    pstmt->execute();

    cout << endl << "Successfully added in database." << endl;

    // Exit Code
    cout << "Press 'm' to Menu and 'a' to Reserve Again Or Any Other key to exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        main();
    }
    else if (choose == 'a' || choose == 'A')
    {
        ReserveSeat();
    }
    else
    {
        exit(0);
    }
}

void DisplayPassenger()
{
    // Initial Load
    system("cls");
    // Initial Load End
    system("color 0a");

    // Variables
    char choose;
    // Variables End

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Display Passenger details" << endl << endl;

    string findbyname_query = "select * from user_data";
    const char* qn = findbyname_query.c_str();
    pstmt = con->prepareStatement(qn);
    result = pstmt->executeQuery();

    printf("------------------------------------------------------------------------------------------------------------------\n");
    printf("| %-20s | %-15s | %-15s | %-15s | %-15s | %-15s |\n", "User Name", "Phone No.", "Address", "PNR No.", "Flight No.", "Travel Date");
    while (result->next())
    {
        printf("| %-20s | %-15s | %-15s | %-15s | %-15s | %-15s |\n", result->getString(2), result->getString(3), result->getString(4), result->getString(5), result->getString(6), result->getString(8));
    }
    printf("------------------------------------------------------------------------------------------------------------------\n");

    //callHTML();
 
    // Exit Code
ExitMenu:
    cout << "Press 'm' to Menu and any other key to Exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        main();
    }
    else
    {
        exit(0);
    }
}

void UserTicket()
{
    // Initial Load
    system("cls");
    // Initial Load End
    system("color 0b");

    // Variables
    string input = "";
    char choose;
    // Variables End

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "User Ticket Details" << endl << endl;

    cin.ignore(1, '\n');
    cout << "Enter User Name: ";
    getline(cin, input);

    string findbyname_query = "select * from user_data where u_name like '%" + input + "%'";
    const char* qn = findbyname_query.c_str();
    pstmt = con->prepareStatement(qn);
    result = pstmt->executeQuery();
    int rcount = result->rowsCount();
    
    if (rcount == 0)
    {
        cout << "\n\n NO SUCH USER \n\n";
        return;
    }
    cout << endl;
    cout << "Showing Ticket of " << input << endl << endl;
    while ((result->next()))
    {
        cout << "Ticket No.: " << result->getString(5) << "\nUser Name: " << result->getString(2) << "\nUser Phone No.: " << result->getString(3) << "\nUser Address: " << result->getString(4) << "\nFlight No.: " << result->getString(6) << "\nUser Travel Date: " << result->getString(8) << endl << endl;
    }


    // Exit Code
ExitMenu:
    cout << "Press 'm' to Menu, 'a' to Search again and any other key to Exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        main();
    }
    else if (choose == 'a' || choose == 'A')
    {
        UserTicket();
    }
    else
    {
        exit(0);
    }
}

void FlightSchedule()
{
    system("cls");
    system("color 0a");

    // Variables
    char choose;
    // Variables End

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Flight Schedule" << endl << endl;

    string findbyname_query = "select * from flight_master";
    const char* qn = findbyname_query.c_str();
    pstmt = con->prepareStatement(qn);
    result = pstmt->executeQuery();

    printf("-----------------------------------------------------------------------------------------------------------------\n");
    printf("| %-12s | %-12s | %-12s | %-12s | %-12s | %-12s | %-12s | \n", "Flight No.", "Flight Name", "From", "To", "Dept.Time", "Arr.Time", "Rate");
    while (result->next())
    {
        printf("| %-12s | %-12s | %-12s | %-12s | %-12s | %-12s | %-12s |\n", result->getString(2), result->getString(3), result->getString(4), result->getString(5), result->getString(6), result->getString(7), result->getString(8));

    }
    printf("------------------------------------------------------------------------------------------------------------------\n");

    // Exit Code
ExitMenu:
    cout << "Press 'm' to Menu and any other key to Exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        main();
    }
    else
    {
        exit(0);
    }
}


void FlightDetails()
{   ScreenColor();
    // Initial Load
    system("cls");
    system("Airlines Reservation System Program");

    // Initial Load End

    // Variables
    int chooseOneFromMenu = 0;
    // Variables End

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Airlines Reservation System Menu" << endl;
    cout << "1. Add Flight." << endl;
    cout << "2. Edit Flight." << endl;
    cout << "3. Delete Flight." << endl;
    cout << "4. Back To Menu." << endl;
    cout << "Choose One: ";
    cin >> chooseOneFromMenu;

    switch (chooseOneFromMenu)
    {
    case 1:
        AddNewFlight();
        break;
    case 2:
        EditFlight();
        break;
    case 3:
        DeleteFlight();
        break;
    case 4:
        main();
        break;
    default:
        cout << "Please choose between The Given Numbers. Press Enter To Continue...";
        //getch();
        system("cls");
        FlightDetails();
        break;
    }
}

void AddNewFlight()
{
    // Initial Load
    system("cls");
    // Initial Load End

    // Variables
    string flightNo = "";
    string flightName = "";
    string flightFrom = "";
    string flightTo = "";
    string flightDeptime = "";
    string flightArrtime = "";
    string flightRate = "";
    string flightAvailability = "";
    char choose;
    // Variables End

    // Store Variables
    // Store Variables End

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Add New Flight Menu" << endl << endl;

    cin.ignore(1, '\n');
    cout << "Enter Flight No: ";
    getline(cin, flightNo);
    cout << "Enter Flight Name: ";
    getline(cin, flightName);
    cout << "Enter Flight From: ";
    getline(cin, flightFrom);
    cout << "Enter Flight To: ";
    getline(cin, flightTo);
    cout << "Enter Departure Time: ";
    getline(cin, flightDeptime);
    cout << "Enter Arrival Time: ";
    getline(cin, flightArrtime);
    cout << "Enter Ticket Rate: ";
    getline(cin, flightRate);
    cout << "Enter Flight Availability (A (Available) / N (Not Available)): ";
    getline(cin, flightAvailability);

    /*string insert_query = "insert into flight_master (f_no, f_name, f_from, f_to, f_deptime, f_arrtime, f_rate, f_availability) values ('" + flightNo + "','" + flightName + "','" + flightFrom + "','" + flightTo + "','" + flightDeptime + "','" + flightArrtime + "','" + flightRate + "','" + flightAvailability + "')";
    const char* q = insert_query.c_str();
    puts(q);
    return;*/

    pstmt = con->prepareStatement("insert into flight_master(f_no, f_name, f_from, f_to, f_deptime, f_arrtime, f_rate, f_available) values(? , ? , ? , ? , ? , ? ,?, ?)");
    pstmt->setString(1, flightNo);
    pstmt->setString(2, flightName);
    pstmt->setString(3, flightFrom);
    pstmt->setString(4, flightTo);
    pstmt->setString(5, flightDeptime);
    pstmt->setString(6, flightArrtime);
    pstmt->setString(7, flightRate);
    pstmt->setString(8, flightAvailability);
    int status = pstmt->execute();


    if (status)
    {
        cout << endl << "Successfully added flight details." << endl;
    }
    else
    {
        //cout << "Query Execution Problem!" << mysql_errno(conn) << endl;
    }

    // Exit Code
    cout << "Press 'm' to Flight Details Menu and 'a' to Insert Again Or Any Other key to exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        FlightDetails();
    }
    else if (choose == 'a' || choose == 'A')
    {
        AddNewFlight();
    }
    else
    {
        exit(0);
    }
}


void EditFlight()
{
    system("cls");
    
    // Variables
    string flightNo = "";
    string flightName = "";
    string flightFrom = "";
    string flightTo = "";
    string flightDepTime = "";
    string flightArrTime = "";
    string flightRate = "";
    int choose;

    // Store Variables
    string storeColumnId = "";
    string storeFlightNo = "";
    string storeFlightName = "";
    string storeFlightFrom = "";
    string storeFlightTo = "";
    string storeFlightDepTime = "";
    string storeFlightArrTime = "";
    string storeFlightRate = "";

    // Variables End
    
    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Edit Flight Record" << endl;

    pstmt = con->prepareStatement("select * from flight_master where f_available = 'A'");
    result = pstmt->executeQuery();

    printf("--------------------------------------------------------------------------------------------------------------------\n");
    printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", "Flight No", "Flight Name", "From", "To", "Dep. Time", "Arr. Time", "Rate");

    while ((result->next()))
    {
        printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", result->getString(2), result->getString(3), result->getString(4), result->getString(5), result->getString(6), result->getString(7), result->getString(8));
    }
    printf("--------------------------------------------------------------------------------------------------------------------\n");
    
    cin.ignore(1, '\n');
    cout << "Enter Flight No. to be changed ";
    getline(cin, flightNo);

    pstmt = con->prepareStatement("select * from flight_master where f_no = '" + flightNo + "'");
    result = pstmt->executeQuery();

   while ((result->next()))
    {
        printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", result->getString(2), result->getString(3), result->getString(4), result->getString(5), result->getString(6), result->getString(7), result->getString(8));
        flightName = result->getString(3);
        flightFrom = result->getString(4);
        flightTo = result->getString(5);
        flightDepTime = result->getString(6);
        flightArrTime = result->getString(7);
        flightRate = result->getString(8);
   }
    printf("%s", flightFrom);

    cout << "Enter Flight Name (X to not change): ";
    getline(cin, storeFlightName);
    if (storeFlightName != "X" && storeFlightName != "x")
    {
        flightName = storeFlightName;
    }
    cout << "Enter From (X to not change): ";
    getline(cin, storeFlightFrom);
    if (storeFlightFrom != "X" && storeFlightFrom != "x")
    {
        flightFrom = storeFlightFrom;
    }
    cout << "Enter To (X to not change): ";
    getline(cin, storeFlightTo);
    if (storeFlightTo != "X" && storeFlightTo != "x")
    {
        flightTo = storeFlightTo;
    }
    cout << "Enter Departure Time (X to not change): ";
    cin >> storeFlightDepTime;
    if (storeFlightDepTime != "X" && storeFlightDepTime != "x")
    {
        flightDepTime = storeFlightDepTime;
    }
    cout << "Enter Arrival Time (X to not change): ";
    cin >> storeFlightArrTime;
    if (storeFlightArrTime != "X" && storeFlightArrTime != "x")
    {
        flightArrTime = storeFlightArrTime;
    }
    cout << "Enter Rate (X to not change): ";
    cin >> storeFlightRate;
    if (storeFlightRate != "X" && storeFlightRate != "x")
    {
        flightRate = storeFlightRate;
    }

    string update_query = "update flight_master set f_no = '" + flightNo + "', f_name = '" + flightName + "', f_from = '" + flightFrom + "', f_to = '" + flightTo + "', f_Deptime = '" + flightDepTime + "', f_ArrTime = '" + flightDepTime + "',f_rate='" + flightRate + "' where f_no = '" + flightNo + "'";
    const char* qu = update_query.c_str();

    pstmt = con->prepareStatement(qu);
    result = pstmt->executeQuery();
    printf("Flight details Updated\n");

    // Exit Code
ExitMenu:
    cout << "Press 'm' to Menu, 'e' to edit another item and any other key to Exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        FlightDetails();
    }
    else if (choose == 'e' || choose == 'E')
    {
        EditFlight();
    }
    else
    {
        exit(0);
    }
}

void DeleteFlight()
{
    system("cls");

    // Variables
    char choose;
    string flightno;
    string items[5000];
    int indexForId = 0;
    bool HaveException = false, NotInDatabase = false;
    // Variables End

    cout << "Welcome To Airlines Reservation System" << endl << endl;
    cout << "Delete Flight Menu" << endl << endl;


    pstmt = con->prepareStatement("select * from flight_master where f_available = 'A'");
    result = pstmt->executeQuery();

    printf("--------------------------------------------------------------------------------------------------------------------\n");
    printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", "Flight No", "Flight Name", "From", "To", "Dep. Time", "Arr. Time", "Rate");

    while ((result->next()))
    {
        printf("| %-10s | %-20s | %-10s | %-10s | %-10s | %-10s | %-10s |\n", result->getString(2), result->getString(3), result->getString(4), result->getString(5), result->getString(6), result->getString(7), result->getString(8));
    }
    printf("--------------------------------------------------------------------------------------------------------------------\n");

        cout << endl;
        cout << "Enter Flight No: ";
        cin >> flightno;
        cout << endl;
             
        pstmt = con->prepareStatement("Select * from flight_master where f_no = '" + flightno + "'");
        result = pstmt->executeQuery();
        if (!result->next())
        {
            printf("No such flight\n\n");
            return;
        }

            pstmt = con->prepareStatement("delete from flight_master where f_no = '" + flightno + "'");
            result = pstmt->executeQuery();
            printf("Flight details deleted\n");

    // Exit Code
ExitMenu:
    cout << "Press 'm' to Flight Details Menu, 'd' to delete another record and any other key to Exit: ";
    cin >> choose;
    if (choose == 'm' || choose == 'M')
    {
        FlightDetails();
    }
    else if (choose == 'd' || choose == 'D')
    {
        DeleteFlight();
    }
    else
    {
        exit(0);
    }
}
       
