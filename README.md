/* 
PROJECT NAME: Pathfinding (using backtracking)
CREATOR NAME: Hong Quang Cung
DESCRIPTION: 
 - The program solve the pathfinding problem by using backtracking algorithm (stack)
 - The purpose of the problem is help the mouse (trapped in the maze) to find the path to get out of the maze
 - The Mouse can only move to the allowable cell (value = 1) and can't move if hit the wall (value = 0)
*/

#include <cstring>
#include <iostream>
#include <stack>
#include <bits/stdc++.h>

#define N 4
#define M 5

using namespace std;

class node{
public:
	int x, y;
	node(int i, int j){
		x = i;
		y = j;
	}
};

bool isReachable(int maze[N][M], int fx, int fy){
	stack <node> s; 	//stack of node to go through

	//Initially starting at (0,0):
	s.push(node(0,0));

	//Complete this function below:
	/*
	Create the matrix to track number of visit to the specific node:
	0 - not yet travel
	1 - travel 1 times
	2 - travel 2 times
	...
	*/

	int vis[N][M];							//matrix to track if visit or not
	memset(vis,0,sizeof(vis));				//set all element of array to 0

	//go check each node:
	while(!s.empty()){
		node curr = s.top();				//get the top or newest element in the stack
		int cx = curr.x, cy = curr.y;		//coordinate of the element
		vis[cx][cy]++;						//set the current position to not visit
		
		//Print the searching step
		//cout << "[" << cx << "]" << "[" << cy << "]" <<'\n';
		for(int i=0; i<N; i++){
			for(int j=0; j<M; j++){
				
				if(i == cx && j == cy){
					cout << "Mou" << " ";
				}else{
					cout << maze[i][j] << " ";
				}
			}
			cout << endl;
		}
		cout << endl;
		
		//Check if reach the destination:
		if(cx == fx and cy == fy){
			return true;
		}

		//Chek the up direction:
		if(cx - 1 >= 0 and maze[cx-1][cy] != 0 and vis[cx-1][cy] < 1){
			node surr(cx-1,cy);				//get surrounding nodes
			s.push(surr);					//push the new feasible node to the stack
		}

		//Check the down direction:
		else if(cx + 1 < N and maze[cx+1][cy] != 0 and vis[cx+1][cy] < 1){
			node surr(cx+1,cy);
			s.push(surr);
		}

		//check the left direction:
		else if(cy - 1 >= 0 and maze[cx][cy-1] != 0 and vis[cx][cy-1] < 1){
			node surr(cx,cy-1);
			s.push(surr);
		}

		//check the right direction: 
		else if(cy + 1 < M and maze[cx][cy+1] != 0 and vis[cx][cy+1] < 1){
			node surr(cx,cy+1);
			s.push(surr);
		}
		else{
			s.pop();						//if there is no direction to go -> pop out of stack
		}
	}

	return false;		//No element in the stack -> no path
}

//Drive code
int main(){

	//Maze matrix 1:
	int maze[N][M] = {
		{1,0,1,1,1},
		{1,1,1,0,1},
		{0,0,0,0,1},
		{1,1,1,0,1}
	};

	//food coordinate:
	int fx = 3;
	int fy = 4;

	//Maze matrix 2:
	
/*	int maze[N][M] = {
		{1,0,1,1,0},
		{1,1,1,0,1},
		{0,1,0,0,1},
		{1,1,1,0,1}
	};

	//food coordinate:
	int fx = 2;
	int fy = 3;
*/

	//Find the feasible path:
	if (isReachable(maze, fx,fy)){
		cout << "Path Found!" << '\n';
	}else{
		cout << "No Path Found!" << '\n';
	}

	return 0;
}
