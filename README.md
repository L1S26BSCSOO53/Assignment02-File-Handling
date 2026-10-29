# Assignment02-File-Handling
File Handling

Name: Zainab Shakoor
Reg Number:L1S26BSCS0053
##Programs
- Q1_stock_debugging.cpp
- Q2_parking_report.cpp
- Q3_scholarship_list.cpp
- Q4_heart_rate.cpp
- Q5_expense_tracker.cpp
/*
 * Name       : Zainab Shakoor
 * Reg No     : L1S26BSCS0053
 * Assignment : 02 - File Handling
 * Question   : Q1 - Stock Report (Debugging)
 */
 
#include <iostream>
#include <fstream>                                              /*Fix 1: we have to include fstream in header to do file handling and 
                                                                         to use ifstream and ofstream which would be otherwise an error
                                                                         as there  would be no meaning of ifstream and ofstream without
                                                                         including fstream in the header file.*/
using namespace std;

int main() {
    ifstream inFile("stock.txt");
    if (!inFile)                                                /* Fix 2: we have to check if the file is opened successfully or not, and
                                                                         to assure that we should be getting the message "stock.txt not found!" if
                                                                          the file is not opened successfully.here without !it would not show that
                                                                         file is not opened infact it will allow you to give output on console and
                                                                           definetly would not be reading the data from the file.*/
    {
        cout << "stock.txt not found!" << endl;
        return 1;
    }

    ofstream reorder("reorder.txt", ios::app);                   /*Fix 3: So far as we are writing the data in the file when
                                                                          we use only ofstream it will overwrite the data in
                                                                          the file and the previous data will be lost to avoid
                                                                          this as we want the previous data to be be there we
                                                                          will use append mode as we k now that with the help o
                                                                          f ios::app we can add our data one by one as we will be
                                                                          writing it on console  and then closing console so that
                                                                          the data is save there than in our file where we are
                                                                          wriiting we have to poress enter there so that the dat
                                                                          a is saved there and by pressing the enter key to the file
                                                                          without losing the previous data */



    char code[10];
    int qty, count = 0, low = 0;
    double price;
    double total = 0;                                         /*Fix 4: Now we know that with the help of int we will be getting our output
                                                                       total which we want which will be integer acording to the previous
                                                                       code but in this case there will be loss of data which will go to
                                                                       garbage but this is not our requirement  infact we want the whole
                                                                       value with the decimal points in our output so for the sake of that
                                                                       we will use double datatype instead of int  */




    inFile.ignore(100, '\n');                                  /*Fix 5: according to the data given to us we are asked not to read the header
                                                                        line when we press for output we will see that our program  is failed
                                                                        now why it hapened? we know that whwn the cursor will read the word
                                                                        one by one which is code with  datatye char  with variable code  would
                                                                        read the word code and due astractions it will skip the space moving to
                                                                        the new word which is qty whgen the cursor will reach q it would crash
                                                                        which is because of the datatype qty which would not let it read to which
                                                                         we can read with the help of datatype char but this is not our requirement
                                                                         so according to requirement to skip the header line we have to use the
                                                                        ignore  by randomly giving it the limit and then using  /n it so which
                                                                        means tha while reading the header the cursor should move to the next line
                                                                        ignoring the first line*/

    while (count < 50 && inFile >> code >> qty >> price) {
        count++;
        total = total + qty * price;
        if (qty < 10) {
            reorder << code << " " << qty;                   /* Fix 6: Now here we have to use endl so that after printing one data
                                                                      in the file it may move to the next line after to print he next
                                                                      data and so on if we will not use endl it would print he data in
                                                                      file but it will be written in one line which is not easy to read*/
            low++;
        }
    }
    inFile.close();
    reorder.close();

    cout << "Items: " << count << endl;
    cout << "Total stock value: " << total << endl;
    cout << "Low stock items: " << low << endl;
    return 0;
}
/*
 * Name       : Zainab Shakoor
 * Reg No     : L1S26BSCS0053
 * Assignment : 02 - File Handling
 * Question   : Q2 - Parking Report
 */
#define _CRT_SECURE_NO_WARNINGS	
#include<iostream>
#include<fstream>
#include<cstring>

using namespace std;
int main()
{
	ifstream fin("parking.txt");
	if (!fin)
	{
		cout << "parking.txt not found!" << endl;
		return 1;
	}
	ofstream fout("receipt.txt");
	if(!fout)
	{
		cout << "receipt.txt not found!" << endl;
		return 1;
	}
	int d;
	int m;
	int y;
	char slash;
	cout << "Parking report for";
	fin >> d >> slash >> m >> slash >> y;
	fout << "Receipt for";
	fout<< " " << d << slash << m << slash << y << endl;
	cout << " " << d << slash << m << slash << y << endl;
	char junk[100];
	fin >> junk;
	fin.ignore(100,'\n');
	fin.clear();
	string platename;
	int platenum;
	int h;
	int min;
	char vehicle;
	char colon;
	int inth;
	int intmin;
	int outh;
	int outmin;
	int totalh;
	int totalmin;
	int fee;
	int timeparked;
	int intotal;
	int outtotal;
	int cars=0;
	int bikes=0;
	int totalfee=0;
	char longestplatename[100];
	int longesth=0;
	int longestmin = 0;
	while (fin>>platename)
	{


		
		cout << platename;
		fin >> vehicle;
		if (vehicle == 'C')
		{
			cout << " Car ";
		}
		else
		{
			cout << " Bike ";
		}
		fin >> inth >> colon >> intmin;
		fin >> outh >> colon >> outmin;
		//	cout << " " << inth << colon << intmin << " " << outh << colon << outmin;
		intotal = inth * 60 + intmin;
		outtotal = outh * 60 + outmin;
		timeparked = outtotal - intotal;
		totalh = timeparked / 60;
		totalmin = timeparked % 60;
		cout << " " << totalh << " h " << totalmin << " min ";
		int hourscharge = (totalh * 60 + totalmin + 59) / 60;
		if (vehicle == 'C')
		{
			fee = hourscharge * 100;
		}
		else
		{
			fee = hourscharge * 40;
		}
		cout << " Fee: " << fee << endl;
		
		if (vehicle == 'C')
		{
			cars++;
		}
		else
		{
			bikes++;
		}
		if (timeparked > longesth * 60 + longestmin)
		{
			longesth = totalh;
			longestmin = totalmin;
			strcpy(longestplatename, platename.c_str());
		}
		fout << platename << " " << fee << endl;

		totalfee += fee;
     
	}
	fin.close();
	fout.close();
	
	
	cout << "Total fee: " << totalfee << endl;
	cout << "Total cars: " << cars << endl;
	cout << "Total bikes: " << bikes << endl;
	cout << "Total vehicles: " << cars + bikes << endl;
    cout << "Longest time spent in the parking lot: " << longestplatename << " " << longesth << " h " << longestmin << " min" << endl;
	



	return 0;


	

    


	

}
/*
 *  Student Name : Zainab Shakoor
 *  Reg No     : L1S26BSCS0053
 * Assignment : 02 - File Handling
 * Question :  Scholarship_list
*/
#define _CRT_SECURE_NO_WARNINGS
#include<iostream>
#include<fstream>
using namespace std;
int main()
{
	char filename[30];
	cout << "Enter the name of the file: ";
	cin.getline(filename, 30);
	ifstream fin(filename);
	if (!fin.is_open())
	{
		cout << "file" << " " << filename << " cannot be opened" << endl;
		return 1;
	}
	
	ofstream fout("scholarship.txt");
	if(!fout)
	{
		cout << "Could not open file scholarship.txt";
		return 1;
	}
	int n;
	char name[30];
	double cgpa;
	int count=0;
	double sum=0;
	int scholarship = 0;
	double maxcgpa = 0;
	char topname[30] = " ";
	if (filename)
	{
		
		{
			fin >> n;
			fin.ignore(100, '\n');
			if (n > 30)
			{
				cout << "too many students" << endl;
				return 1;
				
			}

			for(int i=0;i<n;i++)
			{
				
				fin.getline(name, 30, ',');
				fin >> cgpa;
				if (!fin)
				{
					break;
				}
				fin.ignore(100,'\n');
				cout <<  "[" << name << "]"<< " " << "CGPA:" << " " << cgpa << endl;
				count++;
				sum+= cgpa;
				if (count&& cgpa >= 3.5)
				{
					scholarship++;
					fout << name << " " << "," << cgpa << endl;
				}
				if (cgpa > maxcgpa)
				{
					maxcgpa = cgpa;
					strcpy(topname, name);
				}
			}
			if (count < n)
			{
				cout << "Warning: only "<< count <<" of" << n << "records found." << endl;
			}
			cout << "Students=" << count << endl;
			double average = sum / count;
			cout << "Average=" << average << endl;
			cout << "Scholarship=" << scholarship++ << endl;
			cout << "TOP Student=" << topname << "[" << maxcgpa << "]" << endl;

		}
		fin.close();
		fout.close();
		
		
		
	}
	return 0;
}
/*
 * Name       : Zainab Shakoor
 * Reg No     : L1S26BSCS0053
 * Assignment : 02 - File Handling
 * Question   : Q4 - Heart Rate Cleaner
 */

#include <iostream>
#include <fstream>
using namespace std;

int main() {
    ifstream inFile("heart_rate.txt");
    if (!inFile) {
        cout << "heart_rate.txt not found!" << endl;
        return 1;
    }

    int rate[100];
    int count = 0;      // number of valid readings stored in rate[]
    int bad = 0;        // number of junk words skipped
    int x;
    char junk[50];
    int reason = 0;     // 1 = sentinel found, 2 = end of file, 3 = array full

    while (true) {
        if (count == 100) {                 // (1) the array is full
            reason = 3;
            break;
        }
        if (inFile >> x) {                  // a number was read
            if (x == -1) {                  // (2) the sentinel value
                reason = 1;
                break;
            }
            rate[count] = x;
            count++;                        // (3)
        }
        else if (inFile.eof()) {            // (4) nothing left in the file
            reason = 2;
            break;
        }
        else {                              // a junk word
            inFile.clear();                 // (5)
            inFile >> junk;
            bad++;
        }
    }
    inFile.close();

    // TODO 1: write every valid reading to clean_heart_rate.txt
    ofstream outFile("clean_heart_rate.txt");
    for (int i = 0; i < count; i++) {
        outFile << rate[i] << endl;
    }
    outFile.close();

    // TODO 2: Display "Valid readings: " and "Junk skipped: ".
    cout << "Valid readings: " << count << endl;
    cout << "Junk skipped: " << bad << endl;

    // TODO 3: If count is 0, display "No valid readings!".
    //         Otherwise display the Average, Highest, Above average
    //         and Alerts (above 100) lines.
    if (count == 0) {
        cout << "No valid readings!" << endl;
    }
    else {
        int total = 0;
        int highest = rate[0];
        for (int i = 0; i < count; i++) {
            total += rate[i];
            if (rate[i] > highest)
                highest = rate[i];
        }
        double average = (double)total / count;

        int above = 0;
        int alerts = 0;
        for (int i = 0; i < count; i++) {
            if (rate[i] > average) above++;
            if (rate[i] > 100) alerts++;
        }

        cout << "Average: " << average << endl;
        cout << "Highest: " << highest << endl;
        cout << "Above average: " << above << endl;
        cout << "Alerts (above 100): " << alerts << endl;
    }

    // TODO 4: Display "Stopped because: " followed by
    //         sentinel found, end of file or array full.
    cout << "Stopped because: ";
    if (reason == 1)
        cout << "sentinel found" << endl;
    else if (reason == 2)
        cout << "end of file" << endl;
    else
        cout << "array full" << endl;

    return 0;
}
/*
* Student Name: Zainab Shakoor
* Reg No: L1S26BSCS0053
* Assignmnet:02-File Handling
* Question: Q5_expense_tracker
*/
#include<iostream>
#include<fstream>
using namespace std;
int main()

{
	int choice;
	do
	{
		cout << "=======Expense Tracker========" << endl;
		cout << "1. Add an expense" << endl;
		cout << "2. Show all expenses" << endl;
		cout << "3. Show total of a category" << endl;
		cout << "4. Clear all expenses" << endl;
		cout << "5. Exit" << endl;
		cout << "Enter your choice:";
		cin >> choice;
		if (choice == 1)
		{
			char category[20];
			int amount;
			cout << "Enter Category";
			cin >> category;
			cout << endl;
			cout << "Enter amount";
			cin >> amount;

			if (amount <= 0)
			{
				cout << "Invalid Amount!" << endl;
			}
			else
			{
				ofstream fout("expenses.txt", ios::app);

				fout << category << " " << amount << endl;
				fout.close();
				cout << "Expense Saved" << endl;
			}

		}else if (choice == 2)
		{
			char categories[100][20];
			int amounts[100];
			int n = 0;
			ifstream fin("expenses.txt");
			while (n < 100 && fin >> categories[n] >> amounts[n])
			{
				n++;
			}
			fin.close();

			if (n == 0)
			{
				cout << "No expenses yet." << endl;
			}
			else
			{
				int total = 0;
				int largest = 0;
				for (int i = 0; i < n; i++)
				{
					cout << (i + 1) << "." << categories[i] << " " << amounts[i] << endl;
					total += amounts[i];
					if (amounts[i] > amounts[largest])
					{
						largest = i;
					}
						
				}
				cout << "Total spent:" << total << endl;
				cout << "Largest expense:" << categories[largest] << "(" << amounts[largest] << "(" << endl;
			}
		}
		else if (choice == 3)
		{
			char wanted[20];
			char category[20];
			int amount;
			int count = 0;
			int total = 0;
			cout << "Enter category:";
			cin >> wanted;
			ifstream fin("expenses.txt");
			while (fin >> category >> amount)
			{
				if (strcmp(category, wanted) == 0)
				{
					count++;
					total += amount;
				}
			}
			fin.close();
			if (count == 0)
			{
				cout << "No expenses found for" << wanted << endl;
			}
			else
			{
				cout << "Expenses in" << wanted << ":" << count << endl;
				cout << "Total for" << wanted << ":" << total << endl;
			}

		}
		else if (choice == 4)
		{
			ofstream fout("expesnses,txt");
			fout.close();
			cout << "All expenses cleared." << endl;
		}
		else if (choice == 5) 
		{
			cout << "Goodbye!" << endl;
		}
		else
		{
			cout << "Invalid choice!" << endl;
		}
			
	} while (choice != 5);
	return 0;
}

	













