# SudokuSolver

#include<bits/stdc++.h>
using namespace std;
#define UNASSIGNED 0
#define N 9

bool findunassignedlocation(int grid[N][N], int &row, int &col);
bool isSafe(int grid[N][N], int row, int col, int num);


bool SolveSudoku(int grid[N][N])
{
	int row,column;
	if(!findunassignedlocation(grid,row,column))
	return true;

	for(int num=1;num<=9;num++)
	{ 
	    if(isSafe(grid,row,column,num))
	    {
	    	grid[row][column]=num;
	    	if(SolveSudoku(grid))
	    	return true;
	    	grid[row][column]=UNASSIGNED;
		}

	}
	return false;
}
bool findunassignedlocation(int grid[N][N],int &row , int &col)
{
	 for (row = 0; row < N; row++)
        for (col = 0; col < N; col++)
            if (grid[row][col] == UNASSIGNED)
                return true;
    return false;
}
bool UsedInRow(int grid[N][N],int row , int num)
{
	for(int col=0;col<N;col++)
	if (grid[row][col] == num)
            return true;

	return false;

}
bool UsedInColumn(int grid[N][N] ,int col , int num)
{
	for(int row=0;row<N;row++)
	{
	    if(grid[row][col]==num)
	    return true;
	}
	return false;
}
bool UsedInBox(int grid[N][N], int boxStartRow, int boxStartCol, int num)
{
     for(int row=0;row<3;row++)
     {
     	for (int col = 0; col < 3; col++)
            if (grid[row+boxStartRow][col+boxStartCol] == num)
                return true;

	 }
	 return false;
}
bool isSafe(int grid[N][N],int row,int column,int num)
{
	return !UsedInRow(grid,row,num) and !UsedInColumn(grid,column,num) and !UsedInBox(grid, row - row % 3 , column - column % 3, num);
}

void print(int grid[N][N])
{
    for (int row = 0; row < N; row++)
    {
        for (int col = 0; col < N; col++)
            cout<<grid[row][col]<<"  ";
        cout<<endl;
    }
}



int main()
{

int grid[N][N] = {{3, 0, 6, 5, 0, 8, 4, 0, 0},
                      {5, 2, 0, 0, 0, 0, 0, 0, 0},
                      {0, 8, 7, 0, 0, 0, 0, 3, 1},
                      {0, 0, 3, 0, 1, 0, 0, 8, 0},
                      {9, 0, 0, 8, 6, 3, 0, 0, 5},
                      {0, 5, 0, 0, 9, 0, 6, 0, 0},
                      {1, 3, 0, 0, 0, 0, 2, 5, 0},
                      {0, 0, 0, 0, 0, 0, 0, 7, 4},
                      {0, 0, 5, 2, 0, 6, 3, 0, 0}};

	if(SolveSudoku(grid)==true)
	   print(grid);
	else
	cout<<"NO Solution Exists";
}
