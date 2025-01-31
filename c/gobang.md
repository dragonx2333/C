gobang.h

~~~c
#define _CRT_SECURE_NO_WARNINGS

#include<stdio.h>
#include<stdlib.h>
#include<string.h>

#define ROW 15
#define COL 15

void InitBoard(char board[ROW][COL], int row, int col);
void DisplayBoard(char board[ROW][COL], int row, int col);
void PlayerMove(char board[ROW][COL], int row, int col, int flag);
void ComputerMove(char board[ROW][COL], int row, int col);
char IsWin(char board[ROW][COL], int row, int col);
~~~

gobang.c

~~~c
#include"gobang.h"

//初始化棋盘
void InitBoard(char board[ROW][COL], int row, int col)
{
	int i = 0,
		j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			board[i][j] = ' ';
			//将棋盘每个位置设为空格
		}
	}
}

//打印棋盘
void DisplayBoard(char board[ROW][COL], int row, int col)
{
	int i = 0, 
		j = 0;
	for (i = 0; i < row; i++)
	{
		//打印"   |   |   |   |   ..."
		for (j = 0; j < col; j++)
		{
			printf(" %c ", board[i][j]);
			if (j < col - 1)
			{
				printf("|");
			}
		}
		//换行
		printf("\n");
		//打印"---|---|---|---..."
		if (i < row - 1)
		{
			for(j = 0; j < col; j++)
			{
				printf("---");
				if (j < col - 1)
				{
					printf("|");
				}
			}
		}
		//换行
		printf("\n");
	}
}

//玩家落子
void PlayerMove(char board[ROW][COL], int row, int col,int flag)
{
	int x = 0,
		y = 0;
	printf("玩家走\n");
	while (1)
	{
		if (flag)
		{
			printf("请输入您要下的坐标：（如第五行第二个：5 2）");
		}
		else 
		{
			printf("请输入您要下的坐标：");
		}
		scanf("%d %d", &x, &y);
		//查看输入是否正确
		if (x >= 1 && x <= row && y >= 1 && y <= col)
		{
			//查看是位置否被占用
			if (board[x - 1][y - 1] == ' ')
			{
				board[x - 1][y - 1] = '*';
				DisplayBoard(board, row, col);
				break;
			}
			else
			{
				printf("该坐标被占用，请重新输入\n");
			}
		}
		else
		{
			printf("坐标非法，请重新输入\n");
		}
	}
}

//入机落子
void ComputerMove(char board[ROW][COL], int row, int col)
{
	int x = 0,
		y = 0;
	printf("电脑走\n");
	while (1)
	{
		x = rand() % row;
		y = rand() % col;
		//查看是位置否被占用
		if (board[x - 1][y - 1] == ' ')
		{
			board[x - 1][y - 1] = '#';
			DisplayBoard(board, row, col);
			break;
		}
	}
}


//检查键盘是否被下满
//返回1表示满了，0表示没满
int IsFull(char board[ROW][COL], int row, int col)
{
	int i = 0,
		j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			board[i][j] = ' ';
			return 0;//没满
		}
	}
	return 1;//满了
}

//检测是否有某方获胜
//告诉我们游戏的四种状态：1玩家赢'*'   2电脑赢'#'   3平局'Q'   4继续‘C’
char IsWin(char board[ROW][COL], int row, int col)
{
	int i = 0;
	int j = 0;
	for (i = 0; i < row; i++)//横行5个
	{
		for (j = 0; j < col - 4; j++)
		{
			if (board[i][j] == board[i][j + 1] && board[i][j + 1] == board[i][j + 2] &&
				board[i][j + 2] == board[i][j + 3] && board[i][j + 3] == board[i][j + 4] && board[i][j] != ' ')
			{
				return board[i][j];
			}
		}
	}
	for (j = 0; j < col; j++)//竖列5个
	{
		for (i = 0; i < row - 4; i++)
		{

			if (board[i][j] == board[i + 1][j] && board[i + 1][j] == board[i + 2][j] &&
				board[i + 2][j] == board[i + 3][j] && board[i + 3][j] == board[i + 4][j] && board[i][j] != ' ')
			{
				return board[i][j];
			}
		}
	}
	for (i = 0; i < row - 4; i++)//右下斜5个
	{
		for (j = 0; j < col - 4; j++)
		{
			if (board[i][j] == board[i + 1][j + 1] && board[i + 1][j + 1] == board[i + 2][j + 2] &&
				board[i + 2][j + 2] == board[i + 3][j + 3] && board[i + 3][j + 3] == board[i + 4][j + 4] && board[i][j] != ' ')
			{
				return board[i][j];
			}
		}
	}
	for (i = 0; i < row - 4; i++)//左下斜5个
	{
		for (j = 4; j < col; j++)
		{
			if (board[i][j] == board[i + 1][j - 1] && board[i + 1][j - 1] == board[i + 2][j - 2] &&
				board[i + 2][j - 2] == board[i + 3][j - 3] && board[i + 3][j - 3] == board[i + 4][j - 4] && board[i][j] != ' ')
			{
				return board[i][j];
			}
		}
	}
	if (IsFull(board, row, col))
	{
		return 'Q';
	}
	return 'C';
}
~~~

test.c

~~~c
#include"gobang.h"

void menu()
{
	printf("*********************************************\n");
	printf("************1.play        0.exit*************\n");
	printf("*********************************************\n");
}

void game()
{
	char board[ROW][COL] = { 0 };
	InitBoard(board, ROW, COL);
	int ret = 0;
	DisplayBoard(board, ROW, COL);
	int flag = 1;
	while (1)
	{
		PlayerMove(board, ROW, COL, flag);//玩家下棋
		flag = 0;
		ret = IsWin(board, ROW, COL);
		if (ret != 'C')
		{
			break;
		}
		ComputerMove(board, ROW, COL);//电脑下棋
		ret = IsWin(board, ROW, COL);
		if (ret != 'C')
		{
			break;
		}
	}
	if (ret == '*')
	{
		printf("玩家胜利\n");
	}
	else if (ret == '#')
	{
		printf("电脑胜利\n");
	}
	else
	{
		printf("平局\n");
	}
}

int main()
{
	int input = 0;
	do
	{
		menu();
		printf("请选择：");
		scanf("%d", &input);
		switch (input)
		{
		case 1:
			game();
			break;
		case 0:
			printf("退出游戏\n");
			break;
		default:
			printf("输入错误，请重新输入！\n");
			break;
		}
	} while (input);
	return 0;
}
~~~

