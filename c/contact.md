contact.h

~~~c
#define _CRT_SECURE_NO_WARNINGS

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<errno.h>

#define MAX_NAME 20
#define MAX_SEX 5
#define MAX_TELE 12
#define MAX_ADDR 30

//人物信息类型
typedef struct PeoInfo
{
	char name[MAX_NAME];
	int age;
	char sex[MAX_SEX];
	char tele[MAX_TELE];
	char addr[MAX_ADDR];
}PeoInfo;

//通讯录类型
typedef struct Contact
{
	PeoInfo* data;//人物信息数组
	int size;//现有空间大小
	int capacity;//总容量
}Contact;

enum Option
{
	EXIT,//0
	ADD,//1
	DEL,//2
	SEARCH,//3
	MODIFY,//4
	SHOW,//5
	SAVE//6
};

//声明函数
void InitContact(Contact* ps);
void AddContact(Contact* ps);
void ShowContact(const Contact* ps);
void DelContact(Contact* ps);
void SearchContact(const Contact* ps);
void ModifyContact(Contact* ps);
void SaveContact(Contact* ps);
~~~

contact.c

~~~c
#include"contact.h"

//检查所占空间大小是否大于总容量，并扩容
void CheckCapacity(Contact* ps)
{
	if (ps->size == ps->capacity)
	{
		PeoInfo* ptr = realloc(ps->data, (ps->capacity + 2) * sizeof(PeoInfo));
		if (!ptr)
		{
			printf("扩容失败\n");
		}
		else
		{
			ps->data = ptr;
			ps->capacity += 2;
		}
	}
}

//下载通讯录
void LoadContact(Contact* ps)
{
	PeoInfo tmp = { 0 };//接受老通讯录每个人物信息的指针
	FILE* pfread = fopen("contact.dat", "rb");
	if(!pfread)
	{
		printf("Load Contact:%s\n", strerror(errno));
		return;
	}
	while (fread(&tmp, sizeof(PeoInfo), 1, pfread))
		//fread的返回值是读取的次数
	{
		CheckCapacity(ps);
		ps ->data[ps->size] = tmp;
		ps->size++;
	}
	fclose(pfread);
	pfread = NULL;
}

//初始化通讯录
void InitContact(Contact* ps)
{
	ps->data = (PeoInfo*)malloc(3 * sizeof(PeoInfo));
	ps->size = 0;
	ps->capacity = 3;
	LoadContact(ps);
}

//收录人物信息
void EnterInfo(Contact* ps)
{
	CheckCapacity(ps);
	printf("请输入名字：");
	scanf("%s", ps->data[ps->size].name);
	printf("请输入年龄：");
	scanf("%d", ps->data[ps->size].age);
	printf("请输入性别：");
	scanf("%s", ps->data[ps->size].sex);
	printf("请输入电话：");
	scanf("%s", ps->data[ps->size].tele);
	printf("请输入地址：");
	scanf("%s", ps->data[ps->size].addr);
	ps->size++;
	printf("添加成功\n");
}

//添加人物信息
void AddContact(Contact* ps)
{
	EnterInfo(ps);
	ps->size++;
	printf("添加成功\n");
}

//排序通讯录
void SortContact(Contact* ps)
{
	int i = 0,
		j = 0;
	for (i = 0; i < ps->size; i++)
	{
		for (j = 0; j < ps->size - 1; j++)
		{
			if (strcmp(ps->data[j].name, ps->data[j + 1].name) > 0)
			{
				PeoInfo tmp = ps->data[j];
				ps->data[j] = ps->data[j + 1];
				ps->data[j + 1] = tmp;
			}
		}
	}
}

//展示通讯录
void ShowContact(const Contact* ps)
{
	if (!ps->size)
	{
		printf("通讯录为空\n");
	}
	else
	{
		SortContact(ps);
		int i = 0;
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-30s\n", "名字", "年龄", "性别", "电话", "地址");
		for (; i < ps->size; i++)
		{
			printf("%-20s\t%-4d\t%-5s\t%-12s\t%-30s\n", 
				ps->data[i].name, ps->data[i].age, ps->data[i].sex, ps->data[i].tele, ps->data[i].addr);
		}
	}
}

//寻找某人的信息在通讯录的位置
int FindByName(const Contact* ps, char name[MAX_NAME])
{
	int i = 0;
	for (; i < ps->size; i++)
	{
		if (0 == strcmp(ps->data[i].name, name))
		{
			return i;
		}
	}
	return -1;
}

//删除人物信息
void DelContact(Contact* ps)
{
	char name[MAX_NAME];
	printf("请输入要删除的人的信息：");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)//返回-1表示找不到
	{
		printf("要删除的人不存在\n");
	}
	else
	{
		int j = 0;
		for (j = pos; j < ps->size - 1; j++)
		{
			ps->data[j] = ps->data[j + 1];
		}
		ps->size--;
		printf("删除成功\n");
	}
}

//查找人的信息
void SearchContact(const Contact* ps)
{
	//和del差不多
	char name[MAX_NAME];
	printf("请输入要查找的人的信息：");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要查找的人不存在\n");
	}
	else
	{
		printf("%-20s\t%-4s\t%-5s\t%-12s\t%-30s\n", "名字", "年龄", "性别", "电话", "地址");
		printf("%-20s\t%-4d\t%-5s\t%-12s\t%-30s\n",
			ps->data[pos].name, ps->data[pos].age, ps->data[pos].sex, ps->data[pos].tele, ps->data[pos].addr);
	}
}

//修改信息
void ModifyContact(Contact* ps)
{
	char name[MAX_NAME];
	printf("请输入要修改的人的信息：");
	scanf("%s", name);
	int pos = FindByName(ps, name);
	if (pos == -1)
	{
		printf("要修改的人不存在\n");
	}
	else
	{
		EnterInfo(ps);
		printf("修改成功\n");
	}
}

//保存通讯录
void SaveContact(Contact* ps)
{
	FILE* pfwrite = fopen("contact.dat", "wb");
	if (!pfwrite)
	{
		printf("Save Contact:%s\n", strerror(errno));
		return;
	}
	int i = 0;
	for (; i < ps->size; i++)
	{
		fwrite(&(ps->data[i]), sizeof(PeoInfo), 1, pfwrite);
	}
	fclose(pfwrite);
	pfwrite = NULL;
}

void DestroyContact(Contact* ps)
{
	free(ps->data);
	ps->data = NULL;
}
~~~

test.c

~~~c
#include"contact.h"

//打印菜单
void menu()
{
	printf("*******************************************************\n");
	printf("************1.ADD                    2.DEL*************\n");
	printf("************3.SEARCH              4.MODIFY*************\n");
	printf("************5.SHOW                  6.SAVE*************\n");
	printf("************0.EXIST                       *************\n");
}

//程序总实现
int main()
{
	int input = 0;
	int a = 0;
	Contact con;
	//初始化
	InitContact(&con);
	do 
	{
		menu();
		printf("请选择：");
		scanf("%d", &input);
		switch (input)
		{
		case ADD://添加
			AddContact(&con);
			break;
		case DEL://删除
			DelContact(&con);
			break;
		case SEARCH://查找
			SearchContact(&con);
			break;
		case MODIFY://修改
			ModifyContact(&con);
			break;
		case SHOW://展示
			ShowContact(&con);
			break;
		case SAVE://保存
			SaveContact(&con);
			break;
		case EXIT://离开
			printf("是否保存通讯录：（1是0否）");
			scanf("%s", &a);
			if (a)
			{
				SaveContact(&con);
			}
			printf("退出通讯录\n");
			break;
		default://其他情况
			printf("选择错误\n");
			break;
		}
	} while (input);
	DestroyContact(&con);
	return 0;
}
~~~

