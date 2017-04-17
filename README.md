# schoolproject
/*
 * Sudoku game
 * the player has three 4 choice
 * show, swap, verify and quit
 *
 *
 */
//Sudoku game
//
#include<algorithm>
#include<vector>
#include <iostream>
#include<cstdlib>
#include<iomanip>
using namespace std;
void INCON(vector<vector<short> >&);
bool Check(vector<vector<short> >&);
void Swap(vector<vector<short> >&);
void Show(vector<vector<short> >&);
void Board(vector<vector<short> >&board)
{
	 for(int i=0;i<9;++i){
		     	vector<short>row;
		     	for(int j=0,pos=0;j<9;++j) {
		     		if(i == 0)pos=j+1;
		     		if(i > 0 && i != 3 && i != 6) pos=board[i-1][3] +j;
		     		if(i == 3 || i == 6) pos = board [i-1][3] + j + 4;
		     		if(pos > 9) pos -=9;
		     		row.push_back(pos);
		     	}
		     	board.push_back(row);
	 	 }
}

int main()
{
	string input;
srand(time(0));

	 vector< vector<short> >board;
	 Board(board);
	cout<<" Welcome Sudoku Initializer!"<<endl;
while(true){
	bool w=false;
		cout<<'>'; cin>>input;

	 if(input == "show"){Show(board);w=true;}
	 if(input=="swap"){Swap(board);w=true;}
	 if(input=="quit")break;
	 if(input=="verify"){w=true;
		bool verify= Check(board);
	     INCON(board);
	     if(verify==true)cout<<"- All columns, rows, and components are OK..."<<endl;
	 }
	 if(input=="erase"){w=true;
	 for(int i=0;i<2;++i){
     int r= rand()% 9; int c= rand()% 9;
 	cout<<"Erasing row "<<char('P'+r)<<" column "<<char('A'+c)<<endl;
	 board[r][c]=-1; r=0,c=0;
	 	 }
	 }

	if(!w)cout<<"Invalid input enter \"show\", \"swap\", \"verify\", \"erase\", or \"quit\""<<endl;
	}
cout<<"Bye";

return 0;
}

void Show(vector<vector<short> >&board){
    cout<<"   ";
          for(int col=0;col<9; ++col)cout<<setw(2)<<char('A'+col);
          cout<<endl;
          for(int row=0; row<9; ++row){
             cout<<setw(3)<<char('P'+row);
              for(int col=0;col<9;++col) {
            	  if(board[row][col]==-1)cout<<" -";
            	  else
            	  cout<<setw(2)<<board[row][col];

              }
              cout<<endl;
          }
}
void Swap(vector<vector<short> >&board){
	int rc=rand() %2;
	/*
	 * Trying to swap rows Q and S...
       - Rows P and S were swapped...
	 */
	if(rc==0){
	 for(int i=0;i<4;++i){
	     	int s1= rand() %9 ;
		    int s2= rand() %9;
		    if(s1!=s2){
		    	if(i==0){
		    	cout<<"Trying to swap rows "<<char('P'+s1)<<" and "<<char('P'+s2)<<"..."<<endl;
		    	}
		    	if(i>0){cout<<setw(3)<<"-Rows  "<<char('P'+s1)<<" and "<<char('P'+s2)<<" were swapped..."<<endl;
		    	}
		    	for(int i=0;i<9; ++i){
		    		swap(board[s1][i], board[s2][i]);//swap row by different rows
		    	}
		    }
	 	 }
	}
	else{
		 for(int i=0;i<4;++i){
		     	int s1= rand() %9 ;int s2= rand() %9;
			    if(s1!=s2){
			    	if(i==0){
			    	cout<<"Trying to swap columns "<<char('A'+s1)<<" and "<<char('A'+s2)<<"..."<<endl;
			        }
			    	if(i>0){cout<<setw(3)<<"- Columns "<<char('P'+s1)<<" and "<<char('P'+s2)<<" were swapped..."<<endl;
			    	}
			    	for(int i=0;i<9; ++i){
			    		swap(board[i][s1], board[i][s2]);//swap row by different cols
			    	}
			    }
		 	 }
		}
}
bool Check(vector<vector<short> >&B){
	bool t=true;
	          for(int row=0; row<9; ++row){
	              for(int col=0;col<9;++col){
	            	  if(!(B[row][col]>=1&&B[row][col]<=9)){ t=false;
	                  cout<<"- Found inconsistency in row "<<char('P'+row)<<"... "<<endl;
	                  }
	              }
	          }
	          for(int row=0; row<9; ++row){
	              for(int col=0;col<9;++col){
	            	  if(!(B[row][col]>=1&&B[row][col]<=9)){t=false;
	                  cout<<"- Found inconsistency in column "<<char('A'+col)<<"... "<<endl;
	                 }
	            }
	        }
	          return t;
}

void INCON(vector<vector<short> >&b){
    for(int row=0; row<3; ++row){
        for(int col=0;col<3;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
            cout<<"- Found inconsistency in component starting at row P and column\nA... "<<endl;
            }
        }
    }
    for(int row=0; row<3; ++row){
        for(int col=3;col<6;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
      	  //- Found inconsistency in row P...
            cout<<"- Found inconsistency component starting at row P and column\nD... "<<endl;
            }
        }
    }
    for(int row=0; row<3; ++row){
        for(int col=6;col<9;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
      	  //- Found inconsistency in row P...
            cout<<"- Found inconsistency component starting at row P and column\nG... "<<endl;
            }
        }
    }
//Row  3<r<6
    for(int row=3; row<6; ++row){
        for(int col=0;col<3;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
      	  //- Found inconsistency in row P...
            cout<<"- Found inconsistency component starting at row S and column\nA... "<<endl;
            }
        }
    }
    for(int row=3; row<6; ++row){
        for(int col=3;col<6;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
      	  //- Found inconsistency in row P...
            cout<<"- Found inconsistency component starting at row S and column\nD... "<<endl;
            }
        }
    }
    for(int row=3; row<6; ++row){
        for(int col=6;col<9;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
      	  //- Found inconsistency in row P...
            cout<<"- Found inconsistency component starting at row S and column\nG... "<<endl;
            }
        }
    }
  // 6<row<9
    for(int row=6; row<9; ++row){
        for(int col=0;col<3;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
            cout<<"- Found inconsistency component starting at row X and column\nA... "<<endl;
            }
        }
    }
    for(int row=6; row<9; ++row){
        for(int col=3;col<6;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
            cout<<"- Found inconsistency component starting at row X and column\nD... "<<endl;
            }
        }
    }
    for(int row=6; row<9; ++row){
        for(int col=6;col<9;++col){
      	  if(!(b[row][col]>=1&&b[row][col]<=9)){
            cout<<"- Found inconsistency component starting at row X and column\nG... "<<endl;
            }
        }
    }
}
