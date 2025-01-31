mine.h

~~~c
#define _CRT_SECURE_NO_WARNINGS

#include<stdio.h>
#include<stdlib.h>
#include<string.h>

#define ROW 9
#define COL 9
#define ROWS ROW + 2
#define COLS COL + 2
#define COUNT 10//雷的数量

//声明函数
void InitBoard1(int board[ROWS][COLS], int row, int col, int set);//初始化
void InitBoard2(char board[ROWS][COLS], int row, int col, char set);
void DisplayBoard(char board[ROWS][COLS], int row, int col);//打印
void SetMine(int board[ROWS][COLS], int row, int col);//布雷
int FindMine(int mine[ROWS][COLS], char show[ROWS][COLS], int row, int col);
//排雷
~~~

mine.c

~~~c
#include"mine.h"

//整型初始化
void InitBoard1(int board[ROWS][COLS], int row, int col, int set)
{
	int i = 0,
		j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			board[i][j] = set;
		}
	}
}

//字符初始化
void InitBoard2(char board[ROWS][COLS], int row, int col, char set)
{
	int i = 0,
		j = 0;
	for (i = 0; i < row; i++)
	{
		for (j = 0; j < col; j++)
		{
			board[i][j] = set;
		}
	}
}

//打印棋盘
void DisplayBoard(char board[ROWS][COLS], int row, int col)
{
	int i = 0,
		j = 0;
	for (i = 0; i <= row; i++)
	{
		printf("%d ", i);
	}
	printf("\n");
	for (i = 1; i <= row; i++)
	{
		printf("%d ", i);
		for (j = 1; j <= row; j++)
		{
			printf("%c ", board[i][j]);
		}
		printf("\n");
	}
}

//布下雷（mine的0 -> 1）
void SetMine(int board[ROWS][COLS], int row, int col)
{
	int count = COUNT;
	while (count)
	{
		int x = rand() % row + 1;
		int y = rand() % col + 1;
		if (board[x][y] == 0)
		{
			board[x][y] = 1;//布雷
			count--;
		}
	}
}

//计算附近的雷的数量，由于是整型数组，可以直接返回棋盘周围数字之和
int get_mine_count(int board[ROWS][COLS], int x, int y)
{
	return board[x - 1][y - 1] + board[x - 1][y] + board[x - 1][y + 1] + board[x][y - 1]
		+ board[x][y + 1] + board[x + 1][y - 1] + board[x + 1][y] + board[x + 1][y + 1];
}



//进行排雷，查看是否排到雷，并返回附近雷的数量
int FindMine(int mine[ROWS][COLS], char show[ROWS][COLS], int row, int col)
{
	int x = 0,
		y = 0,
		flag = 1,
		win = 0;
	while(1)
	{
		if (flag)
		{
			printf("请输入排查雷的坐标：（如5行3排：5 3）");
		}
		else
		{
			printf("请输入排查雷的坐标：");
		}
		flag = 0;
		scanf("%d %d", &x, &y);
		//输入是否合法
		if (x >= 1 && x <= row && y >= 1 && y <= col)
		{
			//是否排到雷
			if (mine[x][y] == 1)
			{
				DisplayBoard(mine, col, row);
				printf("很遗憾，您排查到雷了\n");
				break;
			}
			else
			{
				int Count = get_mine_count(mine, x, y);
				char count = Count + '0';
				show[x][y] = count;
				DisplayBoard(show, col, row);
				win++;
			}
		}
		else
		{
			printf("输入坐标违法，请重新输入\n");
		}
		//当排了(总位置数 - 雷数)次，结束游戏
		if (win == row * col - COUNT)
		{
			printf("恭喜你，排雷成功\n");
			break;
		}
	}
}
~~~

test.c

~~~c
#include"mine.h"

void menu()
{
	printf("*********************************************\n");
	printf("************1.play        0.exit*************\n");
	printf("*********************************************\n");
}

void game()
{
	int mine[ROWS][COLS] = { 0 };//布置好雷的信息，
	//由于后面需要计算附近雷的数量，使用整型数组
	char show[ROWS][COLS] = { 0 };//排查出的雷的信息
	InitBoard1(mine, ROWS, COLS, 0);
	InitBoard2(show, ROWS, COLS, '*');
	DisplayBoard(show, ROW, COL);
	SetMine(mine, ROW, COL);
	FindMine(mine, show, ROW, COL);
}

int main()
{
	int input = 0;
	do
	{
		menu();
		printf("请输入：");
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
			printf("输入错误，请重新输入\n");
			break;
		}
	} while (input);
	return 0;
 }
~~~



~~~c
	int Count = get_mine_count(mine, x, y);
	char count = Count + '0';
	char tmp = count;
	int a = x;
	int b = y;
	show[x][y] = count;
	while(count == '0')
	{
		if (x <= row)
		{
			x++;
			int Count = get_mine_count(mine, x, y);
			char count = Count + '0';
			show[x][y] = count;
		}
	}
	count = tmp;
	x = a;
	y = b;
	while (count == '0')
	{
		if (x >= 1)
		{
			x--;
			int Count = get_mine_count(mine, x, y);
			char count = Count + '0';
			show[x][y] = count;
		}
	}
	count = tmp;
	x = a;
	y = b;
	while (count == '0')
	{
		if (y >= 1)
		{
			y--;
			int Count = get_mine_count(mine, x, y);
			char count = Count + '0';
			show[x][y] = count;
		}
	}
	count = tmp;
	x = a;
	y = b;
	while (count == '0')
	{
		if (y <= col)
		{
			y++;
			int Count = get_mine_count(mine, x, y);
			char count = Count + '0';
			show[x][y] = count;
		}
	}
	DisplayBoard(show, col, row);
	win++;
~~~

这为一代改良版本，尝试以(x,y)为中心进行寻找，以失败告终，同时想到可以以雷为对象，根据雷周围八个各自来围成一个我们需要的可清除的范围