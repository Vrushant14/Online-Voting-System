#include <iostream>
#include <ios>
#include <vector>
#include <string>
#include <iomanip>
#include <unistd.h>
#include <windows.h>
using namespace std;

int canvote = 0;

void clr();
void regvotes(int cv);

class candidates {
    private:
        int votes;
        friend class admin;

    public:
        int id;
        string name;
        int age;
        string party;

        candidates(int i, string n, int a, string p) {
            id = i;
            age = a;
            name = n;
            party = p;
            votes = 0;
        }
};

class users {
    string name;
    int age;
    int voterid;
    int castvote;
    bool v;

    public:
        void vote() {
            if (age < 18) {
                cout << "User not old enough to Vote!" << endl;
                return;
            }
            if (!v) {
                cout << "Enter Candidate's ID to vote: ";
                cin >> castvote;
                v = 1;
                regvotes(castvote);
            }
            else {
                cout << "User has already cast their vote!" << endl;
                return;
            }
        }

        void details() {
            cout << "Name: " << name << endl;
            cout << "Age: " << age << endl;
            cout << "Registered VoterID: " << voterid << endl;
        }

        int hasvoted(int vid) {
            if (vid == voterid) {
                if (!v) {
                    cout << "User has already cast their vote!" << endl;
                    return 1;
                } else {
                    return 0;
                }
            } else {
                return 0;
            }
        }

        users() {
            name = "";
            age = 0;
            voterid = -1;
        }

        users(string n, int a, int vid) {
            name = n;
            age = a;
            voterid = vid;
        }
};

void userpage(users u);

class admin {
    private:
        vector<candidates> cand;
        vector<users> userlist;

    protected:
        void addcand() {
        	clr();
            int id, age;
            string name, party;
            cout << "Enter valid ID: ";
            cin >> id;
            for (int i = 0; i < cand.size(); i++) {
                candidates c = cand[i];
                if (id == c.id) {
                    cout << "This ID is not valid!" << endl;
                    clr();
                    return;
                }
            }
            cout << "Enter Name: ";
            cin >> name;
            cout << "Enter Age: ";
            cin >> age;
            cout << "Enter Party Name: ";
            cin >> party;
            candidates c(id, name, age, party);
            cand.push_back(c);
            cout<<"\nCandidate Details Successfully saved!"<<endl;
            Sleep(500);
            clr();
        }

        void remcand() {
            // Remove candidates if needed
            cout<<"To remove a candidate"<<endl;
            cout<<"Enter Candidate ID:";
            int cid;
            cin>>cid;
            int i,d=-1;
            for(i=0;i<cand.size();i++)
            {
            	if(cand[i].id=cid)
            	{
            		d=1;
            		break;
				}
				
			}
			if(d==-1)
			{
				cout<<"Candidate Not Found!"<<endl;
			}
			else
			{
				candidates c=cand[i];
				cout<<"Name: "<<cand[i].name<<endl;
				cout<<"ID: "<<cand[i].id<<endl;
				cout<<"Candidate Disqualified!"<<endl;
				cand.erase(cand.begin() + i);
				Sleep(500);
			}
			clr();
        }

    public:
        void displaycand() {
        	if(cand.size()==0)
        	{
        		cout<<"No Candidates available to show!"<<endl;
        		Sleep(300);
        		clr();
        		return;
			}
            cout << "\n\t\tCandidate Details: " << endl;
            cout << setw(5) << "SNo." << setw(10) << "ID" << setw(20) << "Name" << setw(10) << "Age" << setw(15) << "Party" << endl;
            for (int i = 0; i < cand.size(); i++) {
                candidates c = cand[i];
                cout << setw(5) << i + 1 << setw(10) << c.id << setw(20) << c.name << setw(10) << c.age << setw(15) << c.party << endl;
            }
            cout<<"\n\n";
        }

        void newuser() {
            string name;
            int age, vid;
            cout << "Enter your voterID: ";
            cin >> vid;
            for (int i = 0; i < userlist.size(); i++) {
                users u = userlist[i];
                int x = u.hasvoted(vid);
                if (x == 1) {
                    cout << "User has already cast their vote!" << endl;
                    return;
                }
            }
            cout << "Enter your Name: ";
            cin >> name;
            cout << "Enter your age: ";
            cin >> age;
            users u(name, age, vid);
            userlist.push_back(u);
            userpage(u);
        }
        
        bool canstart()
        {
        	if(cand.size()==0)
        	{
        		cout<<"No Candidates Available to Start the Elections!"<<endl;
        		Sleep(350);
        		clr();
        		return false;
			}
			else
			{
				if (!canvote) {
                canvote = 1;
                return true;
            }
            else {
            	cout << "Elections already Started!!" << endl;
            	clr();
			}
			}
		}

        void regvote(int cv) {
            for (int i = 0; i < cand.size(); i++) {
                candidates &c = cand[i];
                if (c.id == cv) {
                    c.votes++;
                    break;
                }
            }
        }

        void viewscore() {
        	
        	if(cand.size()==0)
        	{
        		cout << "No candidates available to view score!" << endl;
        		return;
			}
            cout << "\t\t\tCandidate Details and Votes" << endl;
            cout << setw(5) << "SNo." << setw(10) << "ID" << setw(20) << "Name" << setw(15) << "Party" << setw(10) << "Votes" << endl;
            for (int i = 0; i < cand.size(); i++) {
                candidates c = cand[i];
                cout << setw(5) << i + 1 << setw(10) << c.id << setw(20) << c.name << setw(15) << c.party << setw(10) << c.votes << endl;
            }           
        }
        
        void declare() {
        	if(!canvote) {
        		cout << "Elections not yet started!" << endl;
        		return;
			}
        	candidates max = cand[0];
        	for(int i = 0; i < cand.size(); i++) {
        		candidates c = cand[i];
        		int v = c.votes;
        		if(v > max.votes) {
        			max = c;
				}
			}
			cout << "\t\t\tElection Results" << endl;
			cout << "Winning Candidate: " << setw(25) << right << max.name << endl;
			cout << setw(19) << left << "ID: " << setw(25) << right << max.id << endl;
			cout << setw(19) << left << "Party: " << setw(25) << right << max.party << endl;
			exit(0);
		}
};

class adminaccess : public admin {
    public:
        void add() {
            if (canvote) {
                cout << "Elections Started, Cannot Add Candidates Now!" << endl;
                clr();
                return;
            }
            addcand();
        }

        void rem() {
            if (canvote) {
                cout << "Elections Started, Cannot Remove Candidates Now!" << endl;
                clr();
                return;
            }
            remcand();
        }

};

admin a;
adminaccess aa;
void regvotes(int cv) {
	aa.regvote(cv);
}

void clr() {
	sleep(1);
    system("CLS");
}

void adminpage() {
    int o;
    while (true) {
    	ios init(NULL);
    	init.copyfmt(cout);
    	cout << "\t\t\tAdmin Page" << endl;
        cout << "1. "<<setw(20)<<right<<setfill('-')<<"Add Candidate"<<endl;
		cout<<"2. "<<setw(20)<<right<<setfill('-')<<"Remove Candidate"<<endl;
		cout<<"3. "<<setw(20)<<right<<setfill('-')<<"Display Candidates"<<endl;
		cout<<"4. "<<setw(20)<<right<<setfill('-')<<"Start Election"<<endl;
		cout<<"5. "<<setw(20)<<right<<setfill('-')<<"View Score"<<endl;
		cout<<"6. "<<setw(20)<<right<<setfill('-')<<"Declare Results"<<endl;
		cout<<"7. "<<setw(20)<<right<<setfill('-')<<"Logout"<<endl;
		cout<<"Choose an Option: ";
        cin >> o;
        cout.copyfmt(init);
        char cha[100];
        switch (o) {
            case 1:
                aa.add();
                break;
            case 2:
                aa.rem();
                break;
            case 3:
                aa.displaycand();
                break;
            case 4:
                if(aa.canstart()){
                	cout<<"Elections have Started!"<<endl;
                	strcpy(cha,"Voters can login from the home page to vote!");
                	//cout<<"Voters can login from the home page to vote!"<<endl;
	                for(int i=0;i<44;i++)
	                {
	                	cout<<cha[i];
	                	Sleep(60);
					}
					cout<<endl;
					Sleep(100);
					clr();
	                
	            }
	            break;
			case 5:
				if(!canvote) {
					cout << "Elections not yet started!" << endl;
					clr();
					break;
				}
				aa.viewscore();
				break;
			case 6:
				if(canvote){
				
				cout << "Declaring Results" << endl;
				cout << "Calculating Scores";
				for(int i = 0; i < 6; i++) {
					Sleep(750);
					cout << ".";
				}
				cout << endl;
				aa.declare();
				}
				else
				{
					cout<<"Elections not yet Started!!";
					clr();
				}
				break;
            case 7:
                clr();
                return;
            default:
                cout << "Error!";
                clr();
                return;
        }
    }
}

void userpage(users u) {
    int o;
    while (true) {
    	cout << "\t\t\tUser Page" << endl;
        cout << "1. "<<setw(20)<<right<<setfill('-')<<"Display Candidates"<<endl;
		cout<<"2. "<<setw(20)<<right<<setfill('-')<<"Vote Candidate"<<endl;
		cout<<"3. "<<setw(20)<<right<<setfill('-')<<"Details"<<endl;
		cout<<"4. "<<setw(20)<<right<<setfill('-')<<"Logout"<<endl;
		cout<<"Choose an Option: ";
        cin >> o;
        switch (o) {
            case 1:
            	clr();
                aa.displaycand();
                break;
            case 2:
                clr();
                aa.displaycand();
                u.vote();
                break;
            case 3:
                u.details();
                break;
            case 4:
                return;
            default:
                cout << "Error!";
                clr();
                return;
        }
    }
}

int main() {
    int o;
    while (true) {
    	ios init(NULL);
    	init.copyfmt(cout);
        cout << "\t\t\tONLINE VOTING SYSTEM" << endl;
        cout << "1. "<<setw(20)<<right<<setfill('-')<<"Admin Login"<<endl;
		cout<<"2. "<<setw(20)<<right<<setfill('-')<<"Voter Login"<<endl;
		cout<<"3. "<<setw(20)<<right<<setfill('-')<<"Exit"<<endl;
		cout<<"Choose an Option: ";
        cin >> o;
        cout.copyfmt(init);
        switch (o) {
            case 1:
                int aid, apin;
                cout << "Enter admin id: ";
                cin >> aid;
                cout << "Enter admin pin: ";
                cin >> apin;
                
                if (aid == 1234 && apin == 1234) {
                    cout << "Welcome Admin!" << endl;
                    clr();
                    adminpage();
                }
                else
                {
                	cout<<"Incorrect Login ID for Admin!"<<endl;
                	clr();
				}
                break;
            case 2:
                if (!canvote) {
                    
                    cout << "Elections not started yet!" << endl;
                    clr();
                    break;
                }
                a.newuser();
                break;
            case 3:
                return 0;
            default:
                cout << "Error Logging in!";
                
        }
    }
}
