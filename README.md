# Library--Management--System
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <math.h>
#include <time.h>
#include <windows.h>
#define NUM 4
time_t t;
struct tm* lt;
//书籍信息
typedef struct book_info{
	char book_name[21];
	char book_num[9];
	char book_author[15];
	char book_publisher[21];
	int book_index;
	int book_index2;
	book_info* next;
	long lend_time[6];
	long return_time[6];
	bool flag;
	double stu_penalty;
}info_book,*book;
//学生数据
typedef struct stu_table{
	char stu_name[21];    //最后一个单元放'\0'
	char stu_num[13];
	char stu_mm[13];
	stu_table* next;
	info_book* stu_book;
	int stu_already_len;
	int stu_can_len;
}table_stu,*stu;
//管理员数据
typedef struct man_table{
	char man_name[10];
	long man_num;
	long man_mm;
	man_table* next;
}table_man,*man;

//登录界面选项
void Select_Options(){
    system("cls");
	system("color 0f");
    Sleep(200);
    puts("\t\t                                                               "                            );
    Sleep(200);
    puts("\t\t                        ♀ ♀ ♀  ♀ ♀ ♀  ♀  欢迎使用图书馆管理系统  ♀ ♀ ♀  ♀ ♀ ♀  ♀   "        );
    Sleep(200);
    puts("\t\t                                                                                          " );
    Sleep(200);
    puts("\t\t                          ♀ ♀ ♀     ☉ ☉ ☉ ☉         菜单     ☉ ☉ ☉ ☉      ♀ ♀ ♀    "       );
    Sleep(200);
    puts("\t\t                                                                                       "  );
    Sleep(200);
    puts("\t\t                           ★ ℡ (^-^)                1.注册新用户              (^-^) ℡ ★"  );
    Sleep(200);
    puts("\t\t                           ★ ℡ (^-^)                2.学生登录                (^-^) ℡ ★"  );
    Sleep(200);
    puts("\t\t                           ★ ℡ (^-^)                3.管理员登陆              (^-^) ℡ ★"  );
    Sleep(200);
    puts("\t\t                           ★ ℡ (^-^)                4.退出                    (^-^) ℡ ★"  );
    Sleep(200);
    puts("\t\t                                                                                         ");
    Sleep(200);
    puts("\t\t                       ♀ ♀ ♀  ♀ ♀ ♀  ♀ ♀ ♀ ♀ ♀ ♀  ♀ ♀ ♀  ♀ ♀ ♀ ♀ ♀ ♀  ♀          ");
}


//学生用户选项
void Select_Stu(){
    system("cls");
    Sleep(200);
    printf("                                  ◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇\n");
    Sleep(200);
	printf("                                  ◇                 请选择操作                 ◇\n");
    Sleep(200);
    printf("                                  ◇                 1.借阅书籍                 ◇\n");
    Sleep(200);
	printf("                                  ◇                 2.查看已借书籍             ◇\n");
	Sleep(200);
	printf("                                  ◇                 3.归还书籍                 ◇\n");
	Sleep(200);
	printf("                                  ◇                 4.查看所有书籍             ◇\n");
	Sleep(200);
	printf("                                  ◇                 5.返回登录界面             ◇\n");
	Sleep(200);
	printf("                                  ◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇");
}
//管理员选项
void Select_Man()
{    system("cls");
     Sleep(200);
    printf("                                  ◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇\n");
    Sleep(200);
	printf("                                  ◇                  请选择操作                    ◇\n");
	Sleep(200);
	printf("                                  ◇                  1.添加书籍                    ◇\n");
	Sleep(200);
	printf("                                  ◇                  2.删除书籍                    ◇\n");
	Sleep(200);
	printf("                                  ◇                  3.书籍信息更改                ◇\n");
	Sleep(200);
	printf("                                  ◇                  4.查看所有书籍                ◇\n");
	Sleep(200);
	printf("                                  ◇                  5.查看已注册用户列表          ◇\n");
	Sleep(200);
	printf("                                  ◇                  6.返回登录界面                ◇\n");
	Sleep(200);
    printf("                                  ◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇◇");
}
/**************** 初始化 ****************/
//初始化书籍链表
info_book* Init_Book(book Lb){
	Lb = (book_info*)malloc(sizeof(book_info));
	book f = (book_info*)malloc(sizeof(book_info));
	book b = (book_info*)malloc(sizeof(book_info));
	if( Lb == NULL || b == NULL || f == NULL){
		printf("error!\n");
		return NULL;
	}
	b->next = NULL;
	Lb->next = b;
	f = b;
	strcpy(b->book_name,"数据结构(c语言版)");
	strcpy(b->book_num,"1001");
	strcpy(b->book_author,"耿国华");
	strcpy(b->book_publisher,"陕西出版社");
	b->book_index = 10;
	b->book_index2 = 0;

	b = (book_info*)malloc(sizeof(book_info));
	if(b == NULL){
		printf("error!\n");
		return NULL;
	}
	b->next = NULL;
	f->next = b;
	f = b;                  //顺序建立书籍链表
	strcpy(b->book_name,"全新版大学英语4");
	strcpy(b->book_num,"1002");
	strcpy(b->book_author,"王丹");
	strcpy(b->book_publisher,"北京出版社");
	b->book_index = 10;
	b->book_index2 = 0;

	b = (book_info*)malloc(sizeof(book_info));
	if(b == NULL){
		printf("error!\n");
		return NULL;
	}
	b->next = NULL;
	f->next = b;
	f = b;
	strcpy(b->book_name,"高等数学");
	strcpy(b->book_num,"1003");
	strcpy(b->book_author,"张建中");
	strcpy(b->book_publisher,"华北出版社");
	b->book_index = 10;
	b->book_index2 = 0;
	return Lb;
}
//初始化学生表
table_stu* Stu_Table(stu Ls){
	Ls = (table_stu*)malloc(sizeof(stu_table));
	book b = (book_info*)malloc(sizeof(book_info));
	stu p = (table_stu*)malloc(sizeof(stu_table));
	if(Ls == NULL||b == NULL||p == NULL){
		printf("initial error!");
		return NULL;
	}
	Ls->next = NULL;      //这句必不可少，否则下面的遍历将进入死循环
	p->next = Ls->next;
	Ls->next = p;
	strcpy(p->stu_name,"张三");  //这里必须使用strcpy()函数进行串传送
	strcpy(p->stu_num,"201707014212");
	strcpy(p->stu_mm,"201707014212");
	p->stu_already_len = 0;
	p->stu_can_len = 10;
	b->next = NULL;
	b->stu_penalty = 0;
	p->stu_book = b;
	return Ls;
}
//初始化管理员表
table_man* Man_Table(man Lm){
	Lm = (table_man*)malloc(sizeof(man_table));
	man q = (table_man*)malloc(sizeof(man_table));
	if(Lm == NULL || q == NULL)
	{
		printf("initial error!\n");
		return NULL;
	}
	Lm->next = NULL;
	q->next = Lm->next;
	Lm->next = q;
	strcpy(q->man_name,"管理员");
	q->man_num = 666666;
	q->man_mm = 123456;
	return Lm;
}
/**************** 学生登录、新用户注册 ****************/
//学生登录
table_stu* Stu_Login(stu Ls){
	char a[13],b[13];
	printf("用户名：");
	scanf("%s",a);
	printf("密码：");
	scanf("%s",b);
	stu q = Ls->next;
	while(q != NULL){
		if(strcmp(q->stu_num,a) == 0 && strcmp(q->stu_mm,b) == 0){
			return q;
		}
		q = q->next;
	}
	return q;
}
//注册新用户
table_stu* Guidein(stu Ls){
	stu p = (table_stu*)malloc(sizeof(stu_table));
	book b = (book_info*)malloc(sizeof(book_info));
	if(p == NULL||b == NULL){
		printf("error!");
		return Ls;
	}
	while(true){
		printf("请输入姓名：");
		scanf("%s",p->stu_name);
		if(strlen(p->stu_name) > 20){
			printf("注意不可以超过最大长度!\n");
		}else  break;
	}
	while(true){
		printf("请输入用户名：");
		scanf("%s",p->stu_num);
		if(strlen(p->stu_num) > 12) printf("注意不可以超过最大长度! \n");
		else break;
	}
	char ch1[13],ch2[13];
	while(true){
		printf("请设置密码：");
		scanf("%s",ch1);
		printf("请再次确认密码：");
		scanf("%s",ch2);
		if(strcmp(ch1,ch2) != 0) printf("两次输入的密码不一致!\n");
		else {
			strcpy(p->stu_mm,ch1);
			break;
		}
	}
	stu q = Ls->next;
	while(q != NULL){
		if(strcmp(p->stu_name,q->stu_name) == 0||strcmp(p->stu_num,q->stu_num) == 0){
			printf("注册失败，用户已经存在!\n");
			return Ls;
		}
		q = q->next;
	}
	p->next = Ls->next;
	Ls->next = p;
	p->stu_already_len = 0;
	p->stu_can_len = 10;
	b->next = NULL;
	b->stu_penalty = 0;
	p->stu_book = b;
	printf("\n注册成功！\n\n");
	return Ls;
}
/**************** 管理员登录 ****************/
//管理员登录
table_man* Man_Login(man Lm){
	int a,b;
	printf("请输入管理员账号：");
	scanf("%ld",&a);
	printf("请输入密码：");
	scanf("%ld",&b);
	man p = Lm->next;
	while(p != NULL){
		if(p->man_num == a && p->man_mm == b){
			return p;
		}
		p = p->next;
	}
	return p;
}
/**************** 管理员界面操作 ****************/

//添加书籍
book_info* Insert_Book(book Lb){
	book p = (book_info*)malloc(sizeof(book_info));//p为新添加的结点
	book q = Lb->next;//q为链表中某一结点
	book r = Lb->next;
	char ch1[9],ch2[21];
	while(r->next != NULL) r = r->next;//q为最后一个结点
	if(p == NULL){
		printf("initial error!\n");
		return NULL;
	}
	printf("请录入添加书籍的编号：");
	while(true){
		scanf("%s",ch1);
		if(strlen(ch1) > 8){
			printf("编号长度不可以超过8个字符长度，请重新录入!\n");
		}else {
			strcpy(p->book_num,ch1);
			break;
		}
	}
	//如果编号相同，则将原书籍本数+1
	while(q != NULL){
		if(strcmp(p->book_num,q->book_num) == 0){
			q->book_index++;
			printf("添加书籍成功！\n");
			printf("添加结果：原书籍本数增加\n");
			return Lb;
		}
		q = q->next;
	}
	//如果书籍编号不重复，则录入书籍名称
	if(q == NULL){
		printf("请录入添加书籍的名称:");
		while(true){
			scanf("%s",ch2);
			if(strlen(ch2) > 20){
				printf("名称长度不可以超过20个字符长度，请重新录入!\n");
			}else {
				strcpy(p->book_name,ch2);
				break;
			}
		}
		q = Lb->next;
		//如果名称相同，原书籍本数+1
		while(q != NULL){
			if(strcmp(p->book_name,q->book_name) == 0){
				q->book_index++;
				printf("添加书籍成功！\n");
				printf("添加结果：原书籍本数增加\n");
				return Lb;
			}
			q = q->next;
		}
		//如果书籍名称不重复，则输入本数，然后添加
		if(q == NULL){
			printf("请输入本数：");
			int i;
			while(true){
				scanf("%d",&i);
				if(i>0 && i<1000){
					p->book_index = i;
					p->book_index2 = 0;
					p->next = NULL;  //尾插法
					r->next = p;
					break;
				}else	printf("您输入的本书有误，请重新输入!");
			}
        printf("请输入作者名：");
        scanf("%s",p->book_author);
        printf("请输入出版社：");
        scanf("%s",p->book_publisher);

        printf("添加结果：增添了新书籍\n");
		}
	}
	return Lb;
}
//删除书籍
book_info* Delete_Book(book Lb){
	book p = Lb;
	book q = Lb->next;
	if(q == NULL){
		printf("列表是空的\n");
		return Lb;
	}
	printf("请输入要删除书籍的名称或编号：");
	char ch[20];
	scanf("%s",ch);
	while(q != NULL){
		if(strcmp(ch,q->book_name) == 0||strcmp(ch,q->book_num) == 0){
			if(q->book_index2 != 0){
				printf("这本书已经借出去了，请等待全部归还后再进行操作\n");
				return Lb;
			}
			printf("\n找到书籍！\n\n");
			printf("该书籍编号为：%s\n",q->book_num);
			printf("该书籍名称为：%s\n",q->book_name);
			printf("1.删除本书所有信息  2.删除指定本数\n");
			int z;
			while(true){
				scanf("%d",&z);
				if(z == 2){
					printf("请输入删除本数（放弃删除请输入-1）：");
					int i;
					while(true){
						scanf("%d",&i);
						if(i > q->book_index){
							printf("根本没有这么多书!\n");
							return Lb;
						}
						if(i > 0){
							q->book_index = q->book_index-i;
							printf("已成功删除%d本，剩余%d本!\n",i,q->book_index);
							return Lb;
						}
						if(i == -1){
							printf("您已放弃删除！\n");
							return Lb;
						}
						else printf("您的输入有误，请重新输入！\n");
					}
				}
				if(z == 1){
					printf("真的要删除这本书吗？ 1.是  2.否\n");
					int i;
					while(true){
						scanf("%d",&i);
						if(i == 1){
							p->next = p->next->next;
							free(q);
							printf("该书籍已被删除！\n");
							return Lb;
						}
						if(i == 2){
							printf("您已放弃删除！\n");
							return Lb;
						}
						else printf("您的输入有误哦，请重新输入！\n");
					}
				}
				else printf("您的输入有误哦，请重新输入！\n");
			}
		}
		p = p->next;
		q = q->next;
	}
	if(q == NULL) printf("列表中似乎没有这本书！\n");
	return Lb;
}
//修改书籍信息
book_info* Alter_Book(book Lb){
	book b = Lb->next;
	if(b == NULL){
		printf("列表已经是空表！\n");
		return Lb;
	}
	printf("请输入您要修改书籍的编号或名称：\n");
	char ch[20];
	scanf("%s",ch);
	while(b != NULL){
		if(strcmp(ch,b->book_name) == 0||strcmp(ch,b->book_num) == 0){
			if(b->book_index2 != 0){
				printf("这本书已经借出去啦，请等待全部归还后再操作！\n");
				return Lb;
			}
			printf("\n找到书籍!\n\n");
			printf("该书籍编号为：%s\n",b->book_num);
			printf("该书籍名称为：%s\n",b->book_name);
			printf("请选择您想修改的信息： 1.编号  2.名称  3.本数  4.放弃修改\n");
			int z;
			char ch1[9],ch2[21];
			while(true){
				scanf("%d",&z);
				if(z == 1){
					printf("请输入新的编号：");
					while(true){
						scanf("%s",ch1);
						if(strlen(ch1) > 8){
							printf("编号长度不得超过8个字符长度，请重新输入！\n");
						}else break;
					}
					book p = Lb->next;
					while(p != NULL){
						if(strcmp(ch1,p->book_num) == 0){
							printf("真遗憾，修改失败，编号不能重复或列表中已存在此编号!\n");
							break;
						}
						p = p->next;
					}
					if(p == NULL){
						strcpy(b->book_num,ch1);
						printf("书籍信息已更新!/\n");
					}
					break;
				}
				if(z == 2){
					printf("请输入新的名称：");
					while(true){
						scanf("%s",ch2);
						if(strlen(ch2) > 20){
							printf("名称长度不得超过20个字符长度，请重新输入！\n");
						}else break;
					}
					book p = Lb->next;
					while(p != NULL){
						if(strcmp(ch2,p->book_name) == 0){
							printf("真遗憾，修改失败，名称不能重复或列表中已有该书籍!\n");
							break;
						}
						p = p->next;
					}
					if(p == NULL){
						strcpy(b->book_name,ch2);
						printf("书籍信息已更新!\n");
					}
					break;
				}
				if(z == 3){
					printf("请输入新的本数：");
					int i;
					while(true){
						scanf("%d",&i);
						if(i>0 && i<1000){
							b->book_index = i;
							printf("书籍信息已更新！\n");
							break;
						}else printf("您输入的本数有误，请重新输入！\n");
					}
				}
					break;
				if(z == 4){
					printf("您已放弃修改!\n");
					break;
				}else printf("您的输入有误，请重新输入!\n");
			}
			break;
		}
		b = b->next;
	}
	if(b == NULL) printf("列表中没有这本书！\n");
		return Lb;
}
//显示所有已注册用户
void All_Stu(stu Ls){
	stu s = Ls->next;
	printf("学号\t\t姓名\t\t密码\n");
	printf("----------------------------------------------\n");
	while(s != NULL){
		printf("%-16s%-16s%s\n",s->stu_num,s->stu_name,s->stu_mm);
		s = s->next;
	}
	printf("----------------------------------------------\n");
}
//计算超时时间
double Over_Time(long times[]){
	time(&t);
	lt = localtime(&t);
	double t1,t2,t3,t4,t5,t6,t8;
	if(lt->tm_sec >= times[5]){//秒大于，那么分正常减
				t2 = (lt->tm_sec)-(times[5]); //超出几秒
				if(lt->tm_min >= times[4]){//分大于，那么时正常减
					t3 = (lt->tm_min)-(times[4]);  //超出几分
					if(lt->tm_hour >= times[3]){ //时大于，日正常减
						t4 = (lt->tm_hour)-(times[3]);//超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2]); //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mday)-(times[2]);
								t1 = (lt->tm_year+1900)-(times[0])-1;
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2]); //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}else{//时小于，日减一
						t4 = 24+(lt->tm_hour)-(times[3]); //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2])-1; //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2])-1; //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}
				}else{//分小于，那么时减一
					t3 = 60+(lt->tm_min)-(times[4]);  //超出几分
					if(lt->tm_hour >= times[3]){//时大于，日正常减
						t4 = (lt->tm_hour)-(times[3])-1;  //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2]);  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2]);  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}else{//时小于，日减一
						t4 = 24+(lt->tm_hour)-(times[3])-1;  //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2])-1;  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2])-1;  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}
				}//分小于完成
			}else{//秒小于，那么分减一
				t2 = 60+(lt->tm_sec)-(times[5]); //超出几秒
				if(lt->tm_min >= times[4]){//分大于，时正常减
					t3 = (lt->tm_min)-(times[4])-1; //超出几分
					if(lt->tm_hour >= times[3]){//时大于，日正常减
						t4 = (lt->tm_hour)-(times[3]);  //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2]);  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2]);  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}else{//时小于，日减一
						t4 = 24+(lt->tm_hour)-(times[3]);  //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2])-1;  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2])-1;  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}
				}else{//分小于，时减一
					t3 = 60+(lt->tm_min)-(times[4])-1; //超出几分
					if(lt->tm_hour >= times[3]){//时大于，日正常减
						t4 = (lt->tm_hour)-(times[3])-1;  //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2]);  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2]);  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}else{//时小于，日减一
						t4 = 24+(lt->tm_hour)-(times[3])-1;  //超出几时
						if(lt->tm_mday >= times[2]){//日大于，月正常减
							t5 = (lt->tm_mday)-(times[2])-1;  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1]); //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}else{//日小于，月减一
							t5 = 30+(lt->tm_mday)-(times[2])-1;  //超出几日
							if(lt->tm_mon+1 >= times[1]){//月大于，年正常减
								t6 = (lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0]);  //超出几年
							}else{//月小于，年减一
								t6 = 12+(lt->tm_mon+1)-(times[1])-1; //超出几月
								t1 = (lt->tm_year+1900)-(times[0])-1;  //超出几年
							}
						}
					}
				}
			}//秒小于完成
			t8 = t1*31536000+t6*2592000+t5*86400+t4*3600+t3*60+t2;
			return t8;
}
/**************** 学生界面操作 ****************/
//已借书籍列表
void Stu_Lend(stu s){
	book b = s->stu_book;
	time(&t);
	lt = localtime(&t);
	printf("书籍编号    书籍名称\t\t借书日期\t     应还日期\t\t 超期状态\n");
	while(b->next != NULL){
		if(s->stu_already_len != 0){
			printf("  %-10s%-20s",b->book_num,b->book_name);
			printf("%ld-%ld-%ld %ld:%ld:%-4ld",b->lend_time[0],b->lend_time[1],
				b->lend_time[2],b->lend_time[3],b->lend_time[4],b->lend_time[5]);
			printf(" %ld-%ld-%ld %ld:%ld:%-5ld",b->return_time[0],b->return_time[1],
				b->return_time[2],b->return_time[3],b->return_time[4],b->return_time[5]);
			if(b->flag == true){
				printf("已超期  ");
			}else {
				printf("未超期  ");
			}
			if(b->flag == true){
				double t8 = Over_Time(b->return_time);
				b->stu_penalty = t8*0.000001;
			}
			if(b->stu_penalty != 0){
				//超期罚款金额(每秒罚款0.000001元)：
				//printf("已罚款%.2lf元",b->stu_penalty);
			}
		    printf("\n");
		}
		b = b->next;
	}
	//计算总罚款金额
	b = s->stu_book;
	double sum=0;
	while(b->next != NULL){
		if(b->stu_penalty != 0){
			sum = sum+b->stu_penalty;
		}
		b = b->next;
	}
	printf("----------------------------------------------------------------------------------------------\n");
	printf("可借册数:%d\t已借册数:%d\t当前时间：%ld年%ld月%ld日  ",s->stu_can_len,s->stu_already_len,
		lt->tm_year+1900,lt->tm_mon+1,lt->tm_mday);
	if(lt->tm_wday == 0) printf("星期日");
	if(lt->tm_wday == 1) printf("星期一");
	if(lt->tm_wday == 2) printf("星期二");
	if(lt->tm_wday == 3) printf("星期三");
	if(lt->tm_wday == 4) printf("星期四");
	if(lt->tm_wday == 5) printf("星期五");
	if(lt->tm_wday == 6) printf("星期六");
	printf("   %ld:%ld:%ld\n",lt->tm_hour,lt->tm_min,lt->tm_sec);
}
//借书
void Lend_Book(book Lb,stu s){
	char ch[20];
	book k,b = Lb->next;
	book h = s->stu_book;
	book g = h;
	while(g->next != NULL){
		if(g->flag == true){
			printf("有书籍逾期未还哦，请先归还书籍，有借有还，再借不难！\n");
			return;
		}
		g = g->next;
	}
	if(s->stu_already_len == 10){
		printf("已经借满10本咯，做人不能贪得无厌！\n");
		return;
	}
	while(h->next != NULL) h = h->next;  //重要操作，h指向最后一个结点
	printf("您好，请输入要借书的书名或编号：");
	scanf("%s",ch);
	while(b != NULL){
		if(strcmp(ch,b->book_name)==0 || strcmp(ch,b->book_num)==0){
			if(b->book_index == 0){
				printf("这本书已经借完啦！\n");
				return;
			}
			printf("借书成功!\n");
			b->book_index--;
			b->book_index2++;
			s->stu_already_len++;
			s->stu_can_len--;
			time(&t);
			lt = localtime(&t);
			strcpy(h->book_name,b->book_name);
			strcpy(h->book_num,b->book_num);
			h->lend_time[0] = lt->tm_year+1900;
			h->lend_time[1] = lt->tm_mon+1;
			h->lend_time[2] = lt->tm_mday;
			h->lend_time[3] = lt->tm_hour;
			h->lend_time[4] = lt->tm_min;
			h->lend_time[5] = lt->tm_sec;

			h->return_time[0] = h->lend_time[0];
			h->return_time[1] = h->lend_time[1];
			h->return_time[2] = h->lend_time[2]+3;
			h->return_time[3] = h->lend_time[3];
			h->return_time[4] = h->lend_time[4];
			h->return_time[5] = h->lend_time[5]+60;
			if(h->return_time[5] >= 60){
				h->return_time[5] = h->return_time[5]-60;
				h->return_time[4]++;
			}
			if(h->return_time[4] >= 60){
				h->return_time[4] = h->return_time[4]-60;
				h->return_time[3]++;
			}
			if(h->return_time[3] >= 24){
				h->return_time[4] = h->return_time[4]-24;
				h->return_time[2]++;
			}

			k = (book_info*)malloc(sizeof(book_info));
			k->next = NULL;
			h->stu_penalty = 0;
			h->next = k;
			printf("借书时间：%ld-%ld-%ld %ld:%ld:%ld\n",h->lend_time[0],h->lend_time[1],
				h->lend_time[2],h->lend_time[3],h->lend_time[4],h->lend_time[5]);
			printf("归还时间：%ld-%ld-%ld %ld:%ld:%ld\n",h->return_time[0],h->return_time[1],
				h->return_time[2],h->return_time[3],h->return_time[4],h->return_time[5]);
			break;
		}
		b = b->next;
	}
	if(b == NULL) printf("列表中好像没有这本书！\n");
}
//还书
void Return_Book(book Lb,stu s){
	char ch[20];
	book h = s->stu_book;
	book g = h->next;
	if(g == NULL){
		printf("您目前无需待还书籍!\n");
		return;
	}
	book b = Lb->next;
	printf("您好，请输入待还书籍的名称或编号：");
	scanf("%s",ch);
	while(b != NULL){
		if(strcmp(ch,b->book_name)==0 || strcmp(ch,b->book_num)==0){
			//第一种：只有一本书的情况
			if(strcmp(ch,h->book_name) == 0 || strcmp(ch,h->book_num) == 0){
				if(h->stu_penalty != 0){
					printf("啊哦，该书欠款未还清，不能自助归还，请咨询管理员！\n");
					return;
				}
				s->stu_already_len--;
				s->stu_can_len++;
				s->stu_book = g;
				free(h);
				b->book_index++;
				b->book_index2--;
				printf("归还成功！\n");
				return;
			}
			//第二种：有多本书
			while(g->next != NULL){
				if(strcmp(ch,g->book_name) == 0 || strcmp(ch,g->book_num) == 0){
					if(g->stu_penalty != 0){
						printf("啊哦，该书欠款未还清，不能自助归还，请咨询管理员！\n");
						return;
					}
					s->stu_already_len--;
					s->stu_can_len++;
					h->next = h->next->next;
					free(g);
					b->book_index++;
					b->book_index2--;
					printf("归还成功！\n");
					return;
				}
				h = h->next;//h记得跟上
				g = g->next;
			}
			break;
		}
		b = b->next;
	}
	if(b == NULL)	printf("列表中没有这本书哦！\n");
	else printf("这本书你应该没借吧？\n");
	return;
}
//显示所有书籍列表
void All_Book(book Lb){
	book b = (info_book*)malloc(sizeof(book_info));
	if(b == NULL){
		printf("分配失败!\n");
		return;
	}
	b = Lb->next;
	printf("-------------------------------------------------------------------\n");
	printf("编号\t\t名称\t\t\t作者\t\t出版社\t\t\t借阅状态\n");
	while(b != NULL){
		printf("%-16s%-24s",b->book_num,b->book_name);
		printf("%-16s%-24s",b->book_author,b->book_publisher);
		printf("已借出：%d本\t\t可借阅：%d本\n",b->book_index2,b->book_index);
		b = b->next;
	}
	printf("-------------------------------------------------------------------\n");
}

/**************** 登录界面显示函数 ****************/
//用户登录界面
void Stu_Menu(book Lb,stu Ls,stu a){
	printf("\n");
	printf("\n  您好,%s,欢迎使用!\n",a->stu_name);
	char i;
	double tt;
	book b;
	stu p;
	Select_Stu();
	scanf("%c",&i);
	while(i != '5'){
		p = Ls->next;
		b = p->stu_book;
		time(&t);
		lt = localtime(&t);
		while(b->next != NULL){
			if((lt->tm_year+1900) > b->return_time[0]){
					b->flag = true;
				}else if((lt->tm_year+1900) == b->return_time[0]&&(lt->tm_mon+1) > b->return_time[1]){
					b->flag = true;
				}else if((lt->tm_mon+1) == b->return_time[1]&&lt->tm_mday > b->return_time[2]){
					b->flag = true;
				}else if(lt->tm_mday == b->return_time[2]&&lt->tm_hour > b->return_time[3]){
					b->flag = true;
				}else if(lt->tm_hour == b->return_time[3]&&lt->tm_min > b->return_time[4]){
					b->flag = true;
				}else if(lt->tm_min == b->return_time[4]&&lt->tm_sec > b->return_time[5]){
					b->flag = true;
				}else {
					b->flag = false;
				}
				if(b->flag == true){
					double t8 = Over_Time(b->return_time);
					b->stu_penalty = t8*0.5;
				}
				b = b->next;
		}

		switch(i){
			case '1':Lend_Book(Lb,a);break;
			case '2':Stu_Lend(a);break;
			case '3':Return_Book(Lb,a);break;
			case '4':All_Book(Lb);break;
			case 10:break;
			default:printf("input error!\n");
		}
		scanf("%c",&i);
	}
}
//管理员登录界面
void Man_Menu(book Lb,man a,stu Ls){
	printf("您好，%s！\n",a->man_name);
	char i;
	Select_Man();
	scanf("%c",&i);
	while(i != '6'){
		time(&t);
		lt = localtime(&t);
		stu s = Ls->next;
		book b = s->stu_book;
		while(b->next != NULL){
		if((lt->tm_year+1900) > b->return_time[0]){
				b->flag = true;
			}else if((lt->tm_year+1900) == b->return_time[0]&&(lt->tm_mon+1) > b->return_time[1]){
				b->flag = true;
			}else if((lt->tm_mon+1) == b->return_time[1]&&lt->tm_mday > b->return_time[2]){
				b->flag = true;
			}else if(lt->tm_mday == b->return_time[2]&&lt->tm_hour > b->return_time[3]){
				b->flag = true;
			}else if(lt->tm_hour == b->return_time[3]&&lt->tm_min > b->return_time[4]){
				b->flag = true;
			}else if(lt->tm_min == b->return_time[4]&&lt->tm_sec > b->return_time[5]){
				b->flag = true;
			}else {
				b->flag = false;
			}
			if(b->flag == true){
				double t8 = Over_Time(b->return_time);
				b->stu_penalty = t8*0.5;
			}
			b = b->next;
		}
		switch(i){
			case '1':Lb = Insert_Book(Lb);break;
			case '2':Lb = Delete_Book(Lb);break;
			case '3':Lb = Alter_Book(Lb);break;
			case '4':All_Book(Lb);break;
			case '5':All_Stu(Ls);break;

			case 10:break;
			default:printf("input error!\n");
		}
		scanf("%c",&i);
	}
}

/**************** main函数 ****************/
int main(){
	char a;
	book Lb;
	stu Ls,s;
	man Lm,m;
	Lb = Init_Book(Lb);
	Ls = Stu_Table(Ls);  //初始化学生链表
	Lm = Man_Table(Lm);  //初始化管理员链表
	Select_Options();
	scanf("%c",&a);   //使用char类型，这样输入字母不会死循环
	while(a != '4'){
		switch(a){
		    			//注册新用户
			case '1':Ls = Guidein(Ls);break;
			//学生登录
			case '2':s = Stu_Login(Ls);
				if(s == NULL){
					printf("用户名或密码错误！\n");
					printf("是否注册新用户？（1.是   2.否）\n");
					int z;
					while(true){
						scanf("%d",&z);
						if(z == 1) {
							Ls = Guidein(Ls);
							break;
						}
						if(z == 2) break;
						else printf("您的输入有误，请重新输入!\n");
					}
				}else{
					Stu_Menu(Lb,Ls,s);
				}
			break;
			//管理员登录
			case '3':m = Man_Login(Lm);
				if(m == NULL){
					printf("帐号或密码错误!\n\n");
				}else{
					Man_Menu(Lb,m,Ls);
				}
				break;
			case 10:break;
			default:printf("input error!\n");
		}
		if(a == 10) scanf("%c",&a);  //如果是回车，就继续录入，不显示菜单
		else{
			Select_Options();
			scanf("%c",&a);
		}
	}
}
