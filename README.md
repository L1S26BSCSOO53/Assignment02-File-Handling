# Assignment02-File-Handling
File Handling
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


