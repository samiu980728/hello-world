```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <conio.h>
#define BACKSPACE 8
//学生节点
typedef struct _STU
{
	char arrStuNum[10];
	char arrStuName[10];
	int  iStuScore;
	int  CScore;
    int  SumScore;
	struct _STU* pNext;
} STUNODE;
int JudgeIfRFight();
//判断指令输入的是否正确？是否需要重新输入

//声明链表的头和尾
STUNODE* g_pHead = NULL;  //O
STUNODE* g_pEnd = NULL;
//通过姓名查找指定学生的信息
STUNODE * FindMSGByName(char* arrStuName);
//统计成绩低于60分学生的数量
void AddUpNumOfScoreLower60();
//查询成绩高于60分的学生并输出
void AddUpScoreHigher60();
//降序排序学生
void RankStuBymaxNum();
//升序排序学生
void RankStuByminNum();
//添加一个学生的信息
void AddStuMSG(char *arrStuNum, char arrStuName[10], char iStuScore[], char CScore[100], int SumScore);


//清空链表
void FreeLinkData();

//打印数据
void ShowStuData();

//显示指令
void ShowOrder();

//查找制定学生
STUNODE* FindStuByNum(char* arrStuNum); //【】

//指定位置插入节点
void InsertNode(STUNODE* pTemp, char *arrStuNum, char arrStuName[10], char iStuScore[100], char CScore[100], int SumScore);

//删除指定学生
void DeleteStuNode(STUNODE* pNode);

//保存信息进文件
void SaveStuToFile();

//读取文件中学生信息
void ReadStuFromFile();
//学生端读取信息
void STUReadStuFromFile();
int j,k,i,nCount;

int main(void)
{
    system("color 0A");
	FILE * fp = NULL;
	FILE * pFile = NULL;
	char strStuNum[10] = {0};//检测是否重复
  //  int FindMsg = 0;//查找学号用到

    char password[100] = {"s123456"};
    char vippassword[100] = {"t123456"};
    char vipaccount[100] = {"tcaihong"};
    char account[100] = {"scaihong"};
    char userpassword[100] = {0};
    char useraccount[100] = {0};
    char Print1Or2[100] = {0};
    char VipFirstAcount[100] = {0};
     //先将VIP的账号和密码保存在文件中
/*    fp = fopen("NewCount","ab+");
    strcpy(VipFirstAcount, vipaccount);
    strcat(VipFirstAcount, ".");
    strcat(VipFirstAcount, vippassword);
    strcat(VipFirstAcount, ".");
    fwrite(VipFirstAcount, 1, strlen(VipFirstAcount), fp);
    fwrite("\r\n", 1, strlen("\r\n"), fp);
    fclose(fp);
    fp = NULL;
    */

    printf("\t\t*******************欢迎您进入学生信息管理系统*********************\n");
    printf("\t\t************1.登陆 2.注册新账户(教师端) 其他.程序结束*************\n");
    printf("\t\t请输入指令\n\t\t再次提示，这一步请仔细输入指令，一旦输入错误，您将还有三次输入机会\n");
    printf("\t\t");
    scanf("%s",Print1Or2);
    getchar();
    if ( (Print1Or2[0] != '1' && Print1Or2[0] != '2') || strlen(Print1Or2) != 1){
 //           printf("\t\tPrint1Or2[0] = %c,strlen(Print1Or2) = %d\n",Print1Or2[0],strlen(Print1Or2));
        printf("\t\t您输入的指令不正确，您还有两次输入机会\n\t\t请重新输入\n");
        printf("\t\t");
        scanf("%s",Print1Or2);
        getchar();

    if ( (Print1Or2[0] != '1' && Print1Or2[0] != '2') || strlen(Print1Or2) != 1){
  //      printf("\t\tPrint1Or2[0] = %c,strlen(Print1Or2) = %d\n",Print1Or2[0],strlen(Print1Or2));
        printf("\t\t您输入的指令不正确，您还有一次输入机会\n\t\t警告，本次输入若再出现错误，将退出系统！\n\t\t请重新输入\n");
        printf("\t\t");
        scanf("%s",Print1Or2);
        getchar();
               }
    }

if ( strlen(Print1Or2) == 1 && Print1Or2[0] == '2' ){
	pFile = fopen("NewCount","rb+");
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
    char AppalyCount[100] = {0};
    char AppalyPassWord[100] = {0};
    char TeacherNewAcount[100] = {0};
    char TeacherOldAcount[100] = {0};
    char TeacherNewPassWord[100] = {0};
    char TeacherOldPsaaWord[100] = {0};
    char TeacherOld[100] = {0};
    char TeacherNew[100] = {0};
    int m = 0;
 //   FILE * pFile = NULL;

 //   pFile = fopen("NewCount","wb+");
    //先将VIP的账号和密码保存在文件中


    puts("\t\t请输入教师端新账户的账号：");
    printf("\t\t");
    scanf("%s",AppalyCount);//新账号
    getchar();
    puts("\t\t请输入教师端新账户的密码：");
    printf("\t\t");
  //  scanf("%s",AppalyPassWord);//新密码
  //  getchar();


    char ch;
  int sum = 0;//计数光标退格几次
  i = 0;
    while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			sum++;
			i--;

		}else{
		putchar('*');
		AppalyPassWord[i] = ch;
		i++;
	}
	}
	AppalyPassWord[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",AppalyPassWord);








    //判断是否和已有账户重复
    k = 0;
    //判断与源文件中的账号密码是否重复。
//    现在问题是 比较之后明明新账号与之前账号相同，系统却显示不同，进入下一步。。。。
    while ( fgets(TeacherOld, 100, pFile) != NULL && k == 0 && m != 1){
            nCount = 0;
        j = 0;
        for ( i = 0; TeacherOld[i] != '\r'; i++ ){
        if ( nCount == 0 ){
            TeacherNewAcount[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewAcount[j-1] = '\0';
                nCount++;
                j = 0;
                //这个break break掉while吗？？？
            }
            }
        else if ( nCount == 1 ){
            TeacherNewPassWord[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewPassWord[j-1] = '\0';
                nCount++;
                j = 0;
            }

        }
        }
 //       printf("%s %s\n",TeacherNewAcount, TeacherNewPassWord);
 //       printf("%s %s\n",AppalyCount, AppalyPassWord);
        //这样的话 一个密码就读取完毕
     //   这里有问题，应该让新账户和文件中的所有账户比较完之后 再下结论。
        if ( strcmp(TeacherNewAcount, AppalyCount) == 0 && strcmp(TeacherNewPassWord, AppalyPassWord) == 0 ){
        	printf("\t\t您输入的新账户的账号或密码与已有账户信息重复\n\t\t您还有一次机会，请重新输入您想要注册的账号信息\n");
        	m = 1;
        	puts("\t\t请输入教师端新账户的账号：");
        	printf("\t\t");
    scanf("%s",AppalyCount);//新账号
    getchar();
    puts("\t\t请输入教师端新账户的密码：");
    printf("\t\t");
    scanf("%s",AppalyPassWord);//新密码
    getchar();
    //判断是否和已有账户重复
    k = 0;
    //判断与源文件中的账号密码是否重复。
//    现在问题是 比较之后明明新账号与之前账号相同，系统却显示不同，进入下一步。。。。
    fclose(pFile);
    pFile = NULL;
    pFile = fopen("NewCount","rb+");
    while ( fgets(TeacherOld, 100, pFile) != NULL && k == 0 ){
            nCount = 0;
        j = 0;
        for ( i = 0; TeacherOld[i] != '\r'; i++ ){
        if ( nCount == 0 ){
            TeacherNewAcount[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewAcount[j-1] = '\0';
                nCount++;
                j = 0;
                //这个break break掉while吗？？？
            }
            }
        else if ( nCount == 1 ){
            TeacherNewPassWord[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewPassWord[j-1] = '\0';
                nCount++;
                j = 0;
            }

        }
        }
  //      printf("%s %s\n",TeacherNewAcount, TeacherNewPassWord);
 //       printf("%s %s\n",AppalyCount, AppalyPassWord);
        if ( strcmp(TeacherNewAcount, AppalyCount) == 0 && strcmp(TeacherNewPassWord, AppalyPassWord) == 0 ){
		printf("\t\t您又一次输入了已有的账户信息，系统将自动退出\n\t\t下次输入请认真对待，谢谢！\n");



        	return 0;
        }
		}
    }
	}//不用加任何，只要不return 0 就说明新账户不与原账户重复！
    fclose(pFile);
    pFile = NULL;






//问题在这
//char TeacherNew[100] = {0};
    //    if ( strcmp(TeacherNewAcount, AppalyCount) != 0 && strcmp(TeacherNewPassWord, AppalyPassWord) != 0 ){//文件中的一个密码与你输入的新密码比较，看是否相同
//    问题：新注册的账号在这里 但是没有保存进去文件，是不是strcpy的问题？
            k = 1;
            printf("\t\t恭喜，您申请的教师端新账户可用\n\t\t系统将进入登陆界面\n");//然后把账户啥的信息写进文件中去
            pFile = fopen("NewCount","ab+");
            if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
            strcpy(TeacherNew, AppalyCount);
            strcat(TeacherNew, ".");
            strcat(TeacherNew, AppalyPassWord);
            strcat(TeacherNew, ".");
       //     fwrite("\r\n", 1, strlen("\r\n"), pFile);
            fwrite(TeacherNew, 1, strlen(TeacherNew), pFile);
            fwrite("\r\n", 1, strlen("\r\n"), pFile);//**********将新账号信息保存到文件中去
            fclose(pFile);
            pFile = NULL;
            //然后直接自动进入即可
        //    k = 1;
  //      }
     //   if ( strcmp(TeacherNewAcount, AppalyCount) == 0 && strcmp(TeacherNewPassWord, AppalyPassWord) == 0 ){
    //    	printf("您输入的新账户的账号或密码与已有账户信息重复\n退出系统\n");
    //    	return 0;
	//	}
    }//写入完毕，下来就是输入密码了，

//}
  //  fclose(pFile);
 //   pFile = NULL;






  //  printf("k = %d\n",k);

   if ( (strlen(Print1Or2) == 1 && Print1Or2[0] == '1' ) || k == 1 ){

	char AllUserMSG[100] = {0};
	int MSG = 0;
    printf("\t\t************  系统已进入登录界面，请您输入账号和密码  **************\n");

    printf("\t\t-------------------------------------------------------------------\n");

    printf("\t\t账号：\n");
    printf("\t\t");
    scanf("%s",useraccount);
    getchar();
 //   printf("\t\t");
    printf("\t\t密码：\n");
 //  scanf("%s",userpassword);
 //  getchar();
  //使用 * 号输入：
  //这里有问题 怎么输入密码
  char ch;
  int sum = 0;//计数光标退格几次
  i = 0;

  printf("\t\t");

    while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			sum++;
			i--;

		}else{
		putchar('*');
		userpassword[i] = ch;
		i++;
	}
	}
	userpassword[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",userpassword);

	if (strcmp(useraccount, account) == 0 && strcmp(userpassword, password) == 0){




        puts("\t\t您已作为学生端用户登录学生管理系统,您只能行使查看学生信息的权限。\n");
        puts("\t\t以下为系统中所有学生的信息：\n");
        STUReadStuFromFile();
        return 0;
    }






    //下面检验当前输入的账号和密码与保存在文件中的任一除了系统初始设定的普通账号和密码不同的一组账号和密码，简单，在文件中只保存VIP的账号和密码
    pFile = fopen("NewCount","rb+");
    if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
//    fwrite("zhanghao.mima.", 1, strlen("zhanghao.mima."), pFile);
    //读入文件中每一行的账号和密码，每读入一次，把把账号和密码分别赋值给两个新创建的数组储存，再用strcmp函数作比较，只要有一次符合要求，就进入教师端
    MSG = 0;
//这里有问题，UserTextPassword无法保存
    while ( fgets(AllUserMSG, 100, pFile) != NULL && MSG == 0){//把文件中的所有账号和密码都遍历一遍，与你现在输入的账号和密码做比较
    char UserTextCount[100] = {0};
	char UserTextPassword[100] = {0};
	//这下面写 把每一行的账号和密码转化出来赋值给 UserTextCount 和 UserTextPassword
    nCount = 0;
    j = 0;
    for ( i = 0; AllUserMSG[i] != '\r'; i++ ){

    	if ( nCount == 0 ){
    		UserTextCount[j] = AllUserMSG[i];
    		j++;
    		if ( AllUserMSG[i] == '.' ){
    			UserTextCount[j-1] = '\0';
    			j = 0;
    			nCount++;
    	//		printf("nCount = %d\n",nCount);
			}
		}
	//	printf("j = %d\n",j);
		else if ( nCount == 1 ){
			UserTextPassword[j] = AllUserMSG[i];
			j++;
			if ( AllUserMSG[i] == '.' ){
				UserTextPassword[j-1] = '\0';
				j = 0;
				nCount++;
			//	printf("nCount = %d\n",nCount);
			}
		}
//		printf("AllUserMSG = %s\n",AllUserMSG);
	//	printf("111\n");
	}
//	printf("\t\tUserTextCount = %s, UserTextPassword = %s\n",UserTextCount, UserTextPassword);
//	printf("\t\tuseraccount = %s, userpassword = %s\n",useraccount, userpassword);
	if ( strcmp(useraccount, UserTextCount) == 0 && strcmp(userpassword, UserTextPassword) == 0 ){
        printf("\t\t您输入的账户信息正确\n");
        MSG = 1;
     //   printf("111\n");

	}
    }
    fclose(pFile);
    pFile = NULL;
    if ( MSG == 0 ){
            printf("\t\t您输入的账号或密码不正确，您还有两次输入机会，请重新输入\n");
             printf("\t\t账号：\n\t\t");
       //      printf("\t\t");
    scanf("%s",useraccount);
    getchar();

    printf("\t\t密码：\n");
 //  scanf("%s",userpassword);
 //  getchar();
  //使用 * 号输入：
  //这里有问题 怎么输入密码
  char ch;
  i = 0;
  printf("\t\t");

    while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			i--;

		}else{
		putchar('*');
		userpassword[i] = ch;
		i++;
	}
	}
	userpassword[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",userpassword);






    //下面检验当前输入的账号和密码与保存在文件中的任一除了系统初始设定的普通账号和密码不同的一组账号和密码，简单，在文件中只保存VIP的账号和密码
    pFile = fopen("NewCount","rb+");
    if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
//    fwrite("zhanghao.mima.", 1, strlen("zhanghao.mima."), pFile);
    //读入文件中每一行的账号和密码，每读入一次，把把账号和密码分别赋值给两个新创建的数组储存，再用strcmp函数作比较，只要有一次符合要求，就进入教师端
    MSG = 0;
//这里有问题，UserTextPassword无法保存
    while ( fgets(AllUserMSG, 100, pFile) != NULL && MSG == 0){//把文件中的所有账号和密码都遍历一遍，与你现在输入的账号和密码做比较
    char UserTextCount[100] = {0};
	char UserTextPassword[100] = {0};
	//这下面写 把每一行的账号和密码转化出来赋值给 UserTextCount 和 UserTextPassword
    nCount = 0;
    j = 0;
    for ( i = 0; AllUserMSG[i] != '\r'; i++ ){

    	if ( nCount == 0 ){
    		UserTextCount[j] = AllUserMSG[i];
    		j++;
    		if ( AllUserMSG[i] == '.' ){
    			UserTextCount[j-1] = '\0';
    			j = 0;
    			nCount++;
    	//		printf("nCount = %d\n",nCount);
			}
		}
	//	printf("j = %d\n",j);
		else if ( nCount == 1 ){
			UserTextPassword[j] = AllUserMSG[i];
			j++;
			if ( AllUserMSG[i] == '.' ){
				UserTextPassword[j-1] = '\0';
				j = 0;
				nCount++;
			//	printf("nCount = %d\n",nCount);
			}
		}
//		printf("AllUserMSG = %s\n",AllUserMSG);
	//	printf("111\n");
	}
//	printf("UserTextCount = %s, UserTextPassword = %s\n",UserTextCount, UserTextPassword);
//	printf("useraccount = %s, userpassword = %s\n",useraccount, userpassword);
	if ( strcmp(useraccount, UserTextCount) == 0 && strcmp(userpassword, UserTextPassword) == 0 ){
        printf("\t\t您输入的账户信息正确\n");
        MSG = 1;
     //   printf("111\n");

	}
    }
    fclose(pFile);
        pFile = NULL;



        if ( MSG == 0 ){
            printf("\t\t您输入的账号或密码不正确，您还有一次输入机会\n\t\t警告，如果再次输入不正确，将退出程序！\n\t\t请重新输入:\n");
             printf("\t\t账号：\n");
        //     printf("\t\t");
    scanf("%s",useraccount);
    getchar();

    printf("\t\t密码：\n");
 //  scanf("%s",userpassword);
 //  getchar();
  //使用 * 号输入：
  //这里有问题 怎么输入密码
  char ch;
  i = 0;
  printf("\t\t");
/*
    while ( (ch = getch()) != '\r' && i < 100 ){

			userpassword[i] = ch;
			i++;
			printf("*");
	}*/
	while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			i--;

		}else{
		putchar('*');
		userpassword[i] = ch;
		i++;
	}
	}
	userpassword[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",userpassword);





    //下面检验当前输入的账号和密码与保存在文件中的任一除了系统初始设定的普通账号和密码不同的一组账号和密码，简单，在文件中只保存VIP的账号和密码
    pFile = fopen("NewCount","rb+");
    if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
//    fwrite("zhanghao.mima.", 1, strlen("zhanghao.mima."), pFile);
    //读入文件中每一行的账号和密码，每读入一次，把把账号和密码分别赋值给两个新创建的数组储存，再用strcmp函数作比较，只要有一次符合要求，就进入教师端
    MSG = 0;
//这里有问题，UserTextPassword无法保存
    while ( fgets(AllUserMSG, 100, pFile) != NULL && MSG == 0){//把文件中的所有账号和密码都遍历一遍，与你现在输入的账号和密码做比较
    char UserTextCount[100] = {0};
	char UserTextPassword[100] = {0};
	//这下面写 把每一行的账号和密码转化出来赋值给 UserTextCount 和 UserTextPassword
    nCount = 0;
    j = 0;
    for ( i = 0; AllUserMSG[i] != '\r'; i++ ){

    	if ( nCount == 0 ){
    		UserTextCount[j] = AllUserMSG[i];
    		j++;
    		if ( AllUserMSG[i] == '.' ){
    			UserTextCount[j-1] = '\0';
    			j = 0;
    			nCount++;
    	//		printf("nCount = %d\n",nCount);
			}
		}
	//	printf("j = %d\n",j);
		else if ( nCount == 1 ){
			UserTextPassword[j] = AllUserMSG[i];
			j++;
			if ( AllUserMSG[i] == '.' ){
				UserTextPassword[j-1] = '\0';
				j = 0;
				nCount++;
			//	printf("nCount = %d\n",nCount);
			}
		}
//		printf("AllUserMSG = %s\n",AllUserMSG);
	//	printf("111\n");
	}
//	printf("UserTextCount = %s, UserTextPassword = %s\n",UserTextCount, UserTextPassword);
	//printf("useraccount = %s, userpassword = %s\n",useraccount, userpassword);
	if ( strcmp(useraccount, UserTextCount) == 0 && strcmp(userpassword, UserTextPassword) == 0 ){
        printf("\t\t您输入的账户信息正确\n");
        MSG = 1;
     //   printf("111\n");

	}
    }
    fclose(pFile);
        pFile = NULL;
        }




    }



 //   后面那个while的大括号记得去掉


    if ( MSG == 1 ){//只要成立，自动认为是教师端账户
   // 	MSG = 1;
    	printf("\t\t您的账号密码输入均正确\n\t\t您已成功进入教师端学生成绩管理系统\n");
//	int nOrder = -1; //nOrder iOrder  s db arr p
	                 //初始化
	char arrStuNum[10] = {'\0'};
	char arrStuName[10] = {'\0'};
//	int  iStuScore = -1;
    int Select;
	int nFlag = 1;
    int RankSelect;//这也得改成char雷迪奥迪
  //  int AgainCarryOut;//回到选择命令行，重新输入指令

    int RealSelectBy;//用于打印信息的case
  //  int InterSelectByOneAndTwo[100] = {0};




  //  getchar();
	STUNODE* pTemp = NULL;
	ShowOrder();
    //取其一选择
	//读取文件中学生信息
	ReadStuFromFile();
  //  char nOrder[100] = {0};
//    int i;
 //   int InterNOrder[100] = {0};
	while(nFlag)
	{
	    int AgainCarryOut;
	    int kNum = 1;
	    int Score1 = 0;
	    int Score2 = 0;
	    int RealSelectByOneAndTwo = 0;
	    char SelectByOneAndTwo[100] = {0};
        char FindMsg[100] = {0};
	    char iStuScore[100] = {0};
	    char CScore[100] = {0};
//	    char SumScore[100] = {0};
	    int SumScore = 0;
        int InteriStuScore[100] = {0};
        int NumiStuScore = 0;
        int kScore = 1;
	    int InterSelectByOneAndTwo[100] = {0};
	    char nOrder[100] = {0};
	    k = 1;
	    int SwitchNumber = 0;
	    int InterNOrder[100] = {0};
		printf ("\t\t请输入指令(10、查看指令):\n");
	//	getchar();//必须加gechar()要不然前面有%s
	printf("\t\t");
		scanf("%s",nOrder);
//		printf("strlen(nOrder) = %d\n",strlen(nOrder));
		for ( i = 0; i < strlen(nOrder); i++ ){
            InterNOrder[i] = nOrder[i] - 48;
  //          printf("%d\n",InterNOrder[i]);
		}
		for ( i = strlen(nOrder)-1; i >= 0; i-- ){
            SwitchNumber += k * InterNOrder[i];
            k *= 10;
		}
	//	getchar();
//        int i;
        int Flag1;
        int Num1;
        int Num2;
        int Num3;
        int Num4;
        char strBuf[200] = {0};
        char strStuNum[10] = {0};
	    int nCount;
//	    int j;
	    int MarkOrLogo;
	    int LogoIfTextHaveReapper;
  //      atoi(nOrder);


   //     printf("SwitchNumber= %d\n",SwitchNumber);
        if ( SwitchNumber < 1 || SwitchNumber > 14 ){
            printf("\t\t您输入的指令有误，请重新输入！\n");
            printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
        }
        else {
             //   getchar();
		switch (SwitchNumber)//两种可能 输入错误的话还得加一种 选择退出或者是继续输入。
		{
		case 1:
      //      int InterSelectByOneAndTwo[100] = {0};
            nCount = 0;
            LogoIfTextHaveReapper = 0;
            j = 0;
            MarkOrLogo = 0;
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
		    system("cls");
		    //尾添加
		    //把他们也写到一个函数中去
		//    JudgeIfRFight();
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		    }else {
			//添加一个学生的信息
			printf ("\t\t请输入8位学号:\n");
			printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			fp = NULL;


			fp = fopen("dat.dat", "rb+");

	if (NULL == fp)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, fp) && LogoIfTextHaveReapper == 0 )  //EOF  feof   3部分
	{

		i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
		}
		if ( strcmp(arrStuNum, strStuNum) == 0 ){
		    printf("\t\t您输入的学号和之前系统中保存的学号相同\n\t\t请仔细检查您的学号输入是否有误！\n");
		    MarkOrLogo = 1;
		    LogoIfTextHaveReapper = 1;
		}
		if ( MarkOrLogo == 1 ){
		    printf ("\t\tPS:这次不要再输入重复学号啦！\n\t\t请输入8位学号:\n");
		    printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
				if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
          //      printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }





        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
    //    if ( AgainCarryOut != 1 && Num2 != 2)

        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}




		}
	}
	fclose(fp);



		if ( MarkOrLogo == 0 ){

			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
        //        printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( AgainCarryOut != 1 && Num2 != 2 ){

        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
		}

             /*   printf("您输入的学号不够8位，您还有一次输入机会，如果您再次因粗心输入错误，将退出程序！\n请认真核对后重新输入学号:\n");
                Num2 = 1;
			}else{
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("您输入的学号不正确，可能是您输入了字母或键入学号不够8位，您还有一次输入机会，如果您再次因粗心输入错误，将退出程序！\n请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }
			if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                scanf ("%s", arrStuNum);
			}*/
			printf ("\t\t请输入姓名:\n");
			printf("\t\t");
			scanf ("%s", arrStuName);

			getchar();
	//		printf("strlen(arrStuName) = %d\n",strlen(arrStuName));
			for ( i = 0; i < strlen(arrStuName); i++ ){
        //            printf("arrStuName[i] = %d\n",arrStuName[i]);
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t您输入的姓名格式不正确，可能是您输入了数字\n\t\t因为您已经成功输入了正确的学号,系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生姓名:\n");
                    Num3 = 1;
                    break;
                }
			}
                if (Num3 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}
			//下面这些函数声明 写到上面去 最后
		//	char iStuScore[100] = {0};
		//	int InteriStuScore[100] = {0};
		//	int NumiStuScore = 0;
		//	int kScore = 1;
			printf ("\t\t请输入托福分数:\n");
		//	scanf ("%d", &iStuScore);
		printf("\t\t");
		scanf("%s",iStuScore);
		getchar();
		for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;



			if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还有极大可能您输入了字母\n\t\t因为您已经成功输入了正确的学号和姓名,系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", iStuScore);
                getchar();
                kScore = 1;
                NumiStuScore = 0;

                for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;


                for ( i = 0; i < strlen(iStuScore); i++ ){
                    if ( iStuScore[i] < 48 || iStuScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			NumiStuScore = 0;
			kScore = 1;
			Num4 = 0;




			printf ("\t\t输入雅思分数:\n");
		//	scanf ("%d", &iStuScore);
		printf("\t\t");
		scanf("%s",CScore);
		getchar();
		for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;



			if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还有极大可能您输入了字母\n\t\t因为您已经成功输入了正确的学号和姓名,系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", CScore);
                getchar();
                kScore = 1;
                NumiStuScore = 0;

                for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;



                for ( i = 0; i < strlen(CScore); i++ ){
                    if ( CScore[i] < 48 || CScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			SumScore = (Score1 + Score2) / 2;










			AddStuMSG(arrStuNum, arrStuName, iStuScore, CScore, SumScore);
		}
	}

		printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();


			break;

		case 11:  //中间插入添加
		    NumiStuScore = 0;
		    nCount = 0;
            LogoIfTextHaveReapper = 0;
            j = 0;
            MarkOrLogo = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
		    system("cls");
		    //尾添加
		    //把他们也写到一个函数中去
		//    JudgeIfRFight();
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
		        printf ("\t\t以下为已有学生信息\n\t\t请输入8位学号(已有学生的学号)，来选择将新学生插入到哪个学生的后面去:\n");//输入已添加学号
		        ShowStuData();
		        printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			//判断是否重复


			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
            //    printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);
                ;
            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }


        if ( Num2 == 2 ){
            break;
        }
        printf("\t\tstrlen(arrStuNum) = %d\n",strlen(arrStuNum));
        if ( strlen(arrStuNum) == 8 ){
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
         if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;

			pTemp = FindStuByNum(arrStuNum);
			if (NULL != pTemp)  //200501013  1254
			{
				//TODO：插入
				printf ("\t\t请输入新添加学生的8位学号:\n");
				printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			fp = NULL;


			fp = fopen("dat.dat", "rb+");

	if (NULL == fp)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, fp) && LogoIfTextHaveReapper == 0 )  //EOF  feof   3部分
	{

		i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}



		}
		if ( strcmp(arrStuNum, strStuNum) == 0 ){
		    printf("\t\t您输入的学号和之前系统中保存的学号相同\n\t\t请仔细检查您的学号输入是否有误！\n");
		    MarkOrLogo = 1;
		    LogoIfTextHaveReapper = 1;
		}
		if ( MarkOrLogo == 1 ){
		    printf ("\t\tPS:这次不要再输入重复学号啦！\n\t\t请输入8位学号:\n");
		    printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
				if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
       //         printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}




		}
	}
	fclose(fp);



		if ( MarkOrLogo == 0 ){





			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
			}
			if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
            if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
         if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
		}




			printf ("\t\t请输入新添加的学生的姓名:\n");
			printf("\t\t");
			scanf ("%s", arrStuName);
			getchar();
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t您输入的姓名格式不正确，可能是您输入了数字。\n\t\t因为您已经将新添加的学生学号输入正确，系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生姓名:\n");
                    Num3 = 1;
                    break;
                }
			}
                if (Num3 == 1){//输入的学号格式不正确,重新输入printf("\t\t");
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}







			printf ("\t\t请输入新添加的学生的托福分数:\n");
			printf("\t\t");
			scanf ("%s", iStuScore);
			getchar();


				for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;
		NumiStuScore = 0;
		kScore = 1;



			if (Score1 < 0 || Score1 > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分，还可能是您输入了字母。\n\t\t因为您已经将新添加的学生学号和姓名输入正确，系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", iStuScore);
                getchar();
                NumiStuScore = 0;
		        kScore = 1;

				for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;



                for ( i = 0; i < strlen(iStuScore); i++ ){
                    if ( iStuScore[i] < 48 || iStuScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }


			}
			NumiStuScore = 0;
			kScore = 1;
			Num4 = 0;
			printf ("\t\t请输入新添加的学生的雅思分数:\n");
			printf("\t\t");
			scanf ("%s", CScore);
			getchar();


				for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;



			if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分，还可能是您输入了字母。\n\t\t因为您已经将新添加的学生学号和姓名输入正确，系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", CScore);
                getchar();
                NumiStuScore = 0;
                kScore = 1;


                for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;


                for ( i = 0; i < strlen(CScore); i++ ){
                    if ( CScore[i] < 48 || CScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }


			}
			SumScore = ( Score2 + Score1) / 2;










				InsertNode(pTemp, arrStuNum, arrStuName, iStuScore, CScore, SumScore);
        //111}
			}
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
			break;
		case 2: //查找\打印指定学生的信息
			//输入一个学号
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			printf("\t\t想通过什么方式查找信息？\n\t\t键入1.通过学号查找 键入2.通过姓名查找\n");
			printf("\t\t");
			scanf("%s",FindMsg);
			getchar();
			for ( i = 0; i < strlen(FindMsg); i++ ){
			    InterSelectByOneAndTwo[i] = FindMsg[i] - 48;
			}
			for ( i = strlen(FindMsg)-1; i >= 0; i-- ){
			    RealSelectBy += InterSelectByOneAndTwo[i] * kNum;
			    kNum *= 10;
			}
			printf("RealSelectBy = %d\n",RealSelectBy);

			if ( RealSelectBy == 1 ){//通过学号查找
                printf ("\t\t请输入8位指定学号，以便于查找学生信息:\n");
                printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			//判断
			kNum = 1;

			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
			//查找
			pTemp = FindStuByNum(arrStuNum);

			//打印
			if (NULL != pTemp)  //200501013  1254
			{
				printf("\t\t以下为该学生信息：\n学号:%-10s, 姓名:%-12s, 托福分数:%-4d， 托福分数:%-4d， 平均分数:%-4d\n ", pTemp->arrStuNum, pTemp->arrStuName, pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
			}else{
			    printf("\t\t您输入的学号有误！\n");
            }
			}
			else if ( RealSelectBy == 2 ){//通过姓名查找
			NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
                printf("\t\t请输入学生姓名,以便于查找学生信息：\n");
                printf("\t\t");
            scanf("%s", arrStuName);
            getchar();
            for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t由于您输入的姓名的格式输入有误，可能是您输入了数字。系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
                    printf("\t\t");
                   scanf("%s",SelectByOneAndTwo);
                   getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的姓名的格式输入有误，可能是您输入了数字。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入姓名:\n");
                Num3 = 1;
                break;
            default:
                Num3 = 2;
                printf("\t\t您输入的不符合任何，将重新返回选择命令行\n");
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                break;
            }

                }
                break;
			}
			if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
            if ( Num3 == 2 ){
                break;
            }

                if (Num3 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}
            pTemp = FindMSGByName(arrStuName);
            if ( pTemp ){
                printf("\t\t以下为该学生信息：\n");
                printf("\t\t学号：%-10s 姓名：%-12s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
            }else{
                printf("\t\t系统中没有您要查找的学生信息,系统将重新返回选择命令行\n");
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
            }
			}
			else {//NUM不等于1也不等于2时
			    printf("\t\t您输入的指令错误，系统重回命令选择界面\n");
			    printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
			    break;
			}
			}
				printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();

			break;
		case 3:  //修改指定学生的信息
		    nCount = 0;
            LogoIfTextHaveReapper = 0;
            j = 0;
            MarkOrLogo = 0;
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            //判断指令是否输入正确
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else{
			//输入一个学号
			printf ("\t\t以下为已有学生信息：\n");
			ShowStuData();
			printf("\t\t请输入8位指定学号(已有学生)，用于修改已有学生信息:\n");
			printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }

        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();

			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
                }
			pTemp = FindStuByNum(arrStuNum);


			//查找
			NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;

			//打印
			if (NULL != pTemp)  //200501013  1254
			{
				//修改学好
				printf ("\t\t请输入修改后的学号:\n");
				printf("\t\t");
				scanf("%s", arrStuNum);
				getchar();




				/*if (strlen(arrStuNum) != 8){
                printf("\t\t您输入的学号不够8位。\n\t\t因为您已经成功输入了要修改学生的学号,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生学号:\n");
                Num2 = 1;
			    }else{
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母。\n\t\t因为您已经成功输入了要修改学生的学号,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }
            if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                    printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}*/

			fp = NULL;


			fp = fopen("dat.dat", "rb+");

	if (NULL == fp)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, fp) && LogoIfTextHaveReapper == 0 )  //EOF  feof   3部分
	{

		i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}



		}
		if ( strcmp(arrStuNum, strStuNum) == 0 ){
		    printf("\t\t您输入的学号和之前系统中保存的学号相同\n\t\t请仔细检查您的学号输入是否有误！\n");
		    MarkOrLogo = 1;
		    LogoIfTextHaveReapper = 1;
		}
		if ( MarkOrLogo == 1 ){
		    printf ("\t\tPS:这次不要再输入重复学号啦！\n\t\t请输入8位学号:\n");
		    printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
				if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
       //         printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}




		}
	}
	fclose(fp);



		if ( MarkOrLogo == 0 ){





			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
			}
			if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
            if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
         if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
		}

				strcpy(pTemp->arrStuNum, arrStuNum);

				//修改名字、
				printf ("\t\t请输入修改后的名字:\n");
				printf("\t\t");
				scanf("%s", arrStuName);
				getchar();
				for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t您输入的姓名格式不正确，可能是您输入了数字。\n\t\t因为您已经成功输入了修改后学生的学号,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生姓名:\n");
                    Num3 = 1;
                    break;
                }
			}
                if (Num3 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}

				strcpy(pTemp->arrStuName, arrStuName);

				//修改分数
				printf ("\t\t请输入修改后的托福分数:\n");
	//			printf("\t\t");
				scanf("%s", iStuScore);
				getchar();
				for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;

				if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还可能您输入了字母。\n\t\t因为您已经成功输入了修改后学生的学号和姓名,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生成绩:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", iStuScore);
    //            printf("\t\t");
                getchar();

                for ( i = 0; i < strlen(iStuScore); i++ ){
                    if ( iStuScore[i] < 48 || iStuScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			NumiStuScore = 0;
			kScore = 1;
			for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }
            }
			for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;

				pTemp->iStuScore = NumiStuScore;

				NumiStuScore = 0;
				kScore = 1;
				Num4 = 0;


				printf ("\t\t请输入修改后的雅思分数:\n");
	//			printf("\t\t");
				scanf("%s", CScore);
				getchar();
				for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;

				if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还可能您输入了字母。\n\t\t因为您已经成功输入了修改后学生的学号和姓名,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生成绩:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", CScore);
          //      printf("\t\t");
                getchar();

                for ( i = 0; i < strlen(CScore); i++ ){
                    if ( CScore[i] < 48 || CScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			NumiStuScore = 0;
			kScore = 1;
			for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }
            }
			for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;

				pTemp->CScore = NumiStuScore;

				SumScore = (Score2 + Score1) / 2;

				pTemp->SumScore = SumScore;







			}
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
		case 4://保存信息
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。

		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//保存学生信息
			SaveStuToFile();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
/*        case 5:
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		    }else {
            RankStuByminNum();//升序排序学生
		    }
		    	printf("该指令已经执行完毕\n下面为您显示选择命令行，方便进行下一个指令的输入\n");
		ShowOrder();
            break;*/
		case 6://删除学生信息
			//输入一个学号
			  NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
            printf("\t\t以下为您显示已有学生信息：\n");
            ShowStuData();
			printf ("\t\t输入要删除的学生的8位学号:\n");
			printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
         //       printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t您输入的不符合任何，将重新返回选择命令行\n");
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}

			//查找
			pTemp = FindStuByNum(arrStuNum);

			//删除这个节点
			if (NULL != pTemp)  //200501013  1254
			{
				//调用删除学生的函数
				DeleteStuNode(pTemp);
			}
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
		case 7:
			//,释放
			system("cls");
			if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			FreeLinkData();
			g_pHead = NULL;
			g_pEnd = NULL;
			//回复 添加节点
			ReadStuFromFile();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();

			break;
 /*       case 8://按成绩由高到低对学生进行排序
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		    }else {
            RankStuBymaxNum();
		    }
		    	printf("该指令已经执行完毕\n下面为您显示选择命令行，方便进行下一个指令的输入\n");
		ShowOrder();
            break;*/
		case 8://显示所有学生信息
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//显示链表内容
			ShowStuData();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
		case 10://查看指令
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//查看指令
			ShowOrder();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
   /*     case 12:
            //统计成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
        case 13:
            //统计成绩低于60分学生的数量
            AddUpNumOfScoreLower60();
            break;
            /*
        /*case 14://通过姓名查找学生信息
            printf("请输入学生姓名：");
            scanf("%s", arrStuName);

            pTemp = FindMSGByName(arrStuName);
            if ( pTemp ){
                printf("以下为该学生信息：\n");
                printf("学号：%s 姓名：%s 成绩：%d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore);
            }
            break;
            */
		case 13://结束程序
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//退出
			nFlag = 0;
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，系统将自动退出\n");
		    	getchar();
			break;
        case 14://统计成绩
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {

            printf("\t\t键入1：统计托福成绩低于600分学生的数量 \n\t\t键入2：统计托福成绩高于600分的学生并输出\n\t\t键入其他错误指令，您还有一次输入机会\n");
            printf("\t\t");
            scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
      //          printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);
            switch(RealSelectByOneAndTwo)
            {
                case 1://统计成绩低于60分学生的数量
            AddUpNumOfScoreLower60();
            break;
                case 2://统计成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
                default:
                    kNum = 1;
                    Num2 = 2;
                    RealSelectByOneAndTwo = 0;
                printf("\t\t您输入的不符合任何，您还有一次输入机会，如果再次输入错误指令，将返回选择命令行\n\t\t请输入指令：\n");
                printf("\t\t键入1：统计托福成绩低于600分学生的数量 \n\t\t键入2：统计托福成绩高于600分的学生并输出\n\t\t键入其他，返回选择命令行\n");
                printf("\t\t");
            scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                switch(RealSelectByOneAndTwo)
            {
                case 1://统计托福成绩低于60分学生的数量并输出
            AddUpNumOfScoreLower60();
            break;
                case 2://统计托福成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
                default:
                	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                    printf("\t\t第二次您又输入了错误的指令，请您细心一些，粗心不成事！\n\t\t系统将返回选择命令行\n");
                break;

            }
            break;
		    }
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
            break;
        case 12://排序集合
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
		        printf("\t\t键入1：按托福成绩由低到高对学生进行排序\n\t\t键入2：按托福成绩由高到低对学生进行排序\n\t\t键入其他错误指令，您还有一次输入机会\n");
		        printf("\t\t");
		        scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
            //    printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);
            switch(RealSelectByOneAndTwo)
            {
                 case 1:
                RankStuByminNum();//升序排序学生
                break;
              case 2:
                 RankStuBymaxNum();//降序排序学生
                 break;
                default:
                    kNum = 1;
                    Num2 = 2;
                    RealSelectByOneAndTwo = 0;
                printf("\t\t您输入的不符合任何，您还有一次输入机会，如果再次输入错误指令，将返回选择命令行\n\t\t请输入指令：\n");
                printf("\t\t键入1：按成绩由低到高对学生进行排序 \n\t\t键入2：按成绩由高到低对学生进行排序\n\t\t键入其他，返回选择命令行\n");
                printf("\t\t");
            scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                switch(RealSelectByOneAndTwo)
            {
                case 1://统计成绩低于60分学生的数量
            AddUpNumOfScoreLower60();
            break;
                case 2://统计成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
                default:
                	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                    printf("\t\t第二次您又输入了错误的指令，请您细心一些，粗心不成事！\n\t\t系统将返回选择命令行\n");
                break;

            }
            	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
            break;
        }
		    }
    }
	}



    }

	//保存
	SaveStuToFile();
	//释放链表
	FreeLinkData();
	//system("pause");

    system("pause");
    }
//},这是账户信息正确 那里 的 while循环的右括号



   if (strcmp(useraccount, account) == 0 && strcmp(userpassword, password) == 0){




        puts("\t\t您已作为学生端用户登录学生管理系统,您只能行使查看学生信息的权限。\n");
        puts("\t\t以下为系统中所有学生的信息：\n");
        STUReadStuFromFile();
        system("pause");
    }else{
        puts("\t\t您输入的账号或密码不正确\n");
    }
}
else{
	printf("\t\t您输入的指令不正确！程序结束\n");
}
	return 0;
}
int JudgeIfRFight()//判断是否输入错误？？？
{
    getchar();
    int k;
    char judge[20];
    printf("\t\t是否输入错误?如果输入指令有误，请输入'n'。\n");//如果输入错误，直接break;
    int num = 0;
    printf("\t\t");
    scanf("%s",judge);
    if ( strlen(judge) != 1){
        k = 0;
        printf("\t\t既然指令输入正确，那就请继续执行\n");
            getchar();
        return k;//输入指令正确,继续执行
    }
    if ( judge[0] == 'n' ){
            k = 1;//指令输入不正确
                getchar();
            return k;
    }else{//输入指令正确
        printf("\t\t既然指令输入正确，那就请继续执行\n");
        k = 0;
    }
    getchar();
    return k;
}

//添加一个学生的信息
void AddStuMSG(char *arrStuNum, char arrStuName[10], char  iStuScore[100], char CScore[100], int SumScore) //函数定义
{
	//逻辑
	//创建一个节点
	STUNODE* pTemp = (STUNODE *)malloc(sizeof (STUNODE));
    int ScoreReal[100] = {0};
    int i;
    int kScor = 1;
    int RealSc = 0;
    int RealCScore = 0;
    //转化成整数
	for ( i = 0; i < strlen(iStuScore); i++ ){
		if ( iStuScore[i] >= 48 && iStuScore[i] <= 57 ){
			ScoreReal[i] = iStuScore[i]-48;
		}
	}
	for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
		RealSc += ScoreReal[i] * kScor;
		kScor *= 10;
	}
	kScor = 1;

	for ( i = 0; i < strlen(CScore); i++ ){
		if ( CScore[i] >= 48 && CScore[i] <= 57 ){
			ScoreReal[i] = CScore[i]-48;
		}
	}
	for ( i = strlen(CScore)-1; i >= 0; i-- ){
		RealCScore += ScoreReal[i] * kScor;
		kScor *= 10;
	}




	//第一步，检验参数的合法性
	if (NULL == arrStuNum || NULL == arrStuName || iStuScore < 0)
	{
		printf ("\t\t学生信息输入错误!\n");
		return ;
	}
	//节点成员符初始值
	strcpy(pTemp->arrStuNum, arrStuNum);
	strcpy(pTemp->arrStuName, arrStuName);
//	把 iStuScorechar类型 先转化为 int类型在赋值给 pTemp->iStuScore  因为pTemp->iStuScore 是int类型的

	pTemp->iStuScore = RealSc;
	pTemp->CScore = RealCScore;
	pTemp->SumScore = SumScore;
	pTemp->pNext = NULL;

	//接在链表上
	if (NULL == g_pHead || NULL == g_pEnd)
	{
		g_pHead = pTemp;
		//g_pEnd = pTemp;
	}
	else
	{
		g_pEnd->pNext = pTemp;  //链接
		//g_pEnd = pTemp;         //向后移动
	}
	g_pEnd = pTemp;
}


//清空链表
void FreeLinkData()
{
	STUNODE* pTemp = g_pHead;
	STUNODE * q = NULL;
	while (pTemp)
	{
		//记录节点
		q = pTemp;

		//向后移动了一个
		pTemp = pTemp->pNext;

		//删除节点
		free(q);
	}
}

//打印数据
void ShowStuData()
{
	STUNODE* pTemp = g_pHead;
	while (pTemp != NULL)
	{
		printf("\t\t学号：%-8s 姓名：%-10s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
		//向下走一步
		pTemp = pTemp->pNext;
	}
}

//显示指令
void ShowOrder()
{
	printf("\t\t***********您已进入学生信息管理系统——教师端*************\n");
	printf("\t\t**********首先为您显示系统内保存的学生历史信息**********\n");
	printf("\t\t*******************您拥有以下操作权限*******************\n");
	printf("\t\t***             1、 增加一个学生信息(尾添加)         ***\n");
//	printf("***            111、 增加一个学生信息(头添加)         ***\n");
	printf("\t\t***           11、 增加一个学生信息(在指定位置添加)  ***\n");
	printf("\t\t***             2、 查找指定学生的信息（姓名/学号）  ***\n");
	printf("\t\t***             3、 修改指定学生的信息               ***\n");
	printf("\t\t***             4、 保存业主的信息到文件中           ***\n");
//	printf("***             5、 按成绩由低到高对学生进行排序     ***\n");
	printf("\t\t***             6、 删除指定学生的信息               ***\n");
	printf("\t\t***             7、 读取文件中学生信息               ***\n");
//	printf("***             8、 按成绩由高到低对学生进行排序     ***\n");
	printf("\t\t***             8、 显示所有学生的信息               ***\n");
//	printf("***             12、 统计成绩高于60分的学生并输出    ***\n");
	printf("\t\t***             10、 查看指令                        ***\n");
//	printf("***             9、 通过姓名查找指定学生信息        ***\n");
	printf("\t\t***             14、 统计学生信息集合                ***\n");
	printf("\t\t***            12、 对学生进行排序集合               ***\n");
	printf("\t\t***             13、 退出系统                         ***\n");
	printf("\t\t********************************************************\n");
}


//查找制定学生
STUNODE* FindStuByNum(char* arrStuNum)  //200501013  1254
{
	STUNODE* pTemp = g_pHead;
	//检测参数的合法性
	if (NULL == arrStuNum)
	{
		printf ("学号输入错误！\n");
		return NULL;
	}

	//判断链表是否是空
	if (NULL == g_pHead || NULL == g_pEnd)
	{
		printf ("\t\t链表为NULL！\n");
		return NULL;
	}

	//遍历链表
	while(pTemp != NULL)
	{
		if (0 == strcmp(pTemp->arrStuNum, arrStuNum))
		{
			return pTemp;
		}
		pTemp = pTemp->pNext;
	}

	printf ("\t\t查无此节点！\n");
	return NULL;
}

//指定位置插入节点
void InsertNode(STUNODE* pTemp, char *arrStuNum, char arrStuName[10], char iStuScore[100], char CScore[100], int SumScore)
{
	int ScoreReal[100] = {0};
    int i;
    int kScor = 1;
    int RealSc = 0;
    int RealCScore = 0;
	//创建节点
	STUNODE* pNewTemp = (STUNODE *)malloc(sizeof(STUNODE));
	//转化成整数
	for ( i = 0; i < strlen(iStuScore); i++ ){
		if ( iStuScore[i] >= 48 && iStuScore[i] <= 57 ){
			ScoreReal[i] = iStuScore[i] - 48;
		}
	}
	for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
		RealSc += ScoreReal[i] * kScor;
		kScor *= 10;
	}
	kScor = 1;
	for ( i = 0; i < strlen(CScore); i++ ){
		if ( CScore[i] >= 48 && CScore[i] <= 57 ){
			ScoreReal[i] = CScore[i] - 48;
		}
	}
	for ( i = strlen(CScore)-1; i >= 0; i-- ){
		RealCScore += ScoreReal[i] * kScor;
		kScor *= 10;
	}



	//成员赋值
	strcpy(pNewTemp->arrStuNum, arrStuNum);
	strcpy(pNewTemp->arrStuName, arrStuName);
	pNewTemp->iStuScore = RealSc;
	pNewTemp->CScore = RealCScore;
	pNewTemp->SumScore = SumScore;
	pNewTemp->pNext = NULL;    ///


	//插入
	if (pTemp == g_pEnd)  //是尾节点
	{
		g_pEnd->pNext = pNewTemp;
		g_pEnd = pNewTemp;
	}
	else
	{
		//
		pNewTemp->pNext = pTemp->pNext;
		pTemp->pNext = pNewTemp;
	}
}

//删除指定学生
void DeleteStuNode(STUNODE* pNode)
{
	//只有一个节点
	if (g_pHead == g_pEnd)
	{
		free(g_pHead);
		g_pHead = NULL;
		g_pEnd = NULL;
	}
	//只有两个节点
	else if (g_pHead->pNext == g_pEnd)
	{
		if (g_pHead == pNode)
		{
			free(g_pHead);
			g_pHead = g_pEnd;
		}
		else
		{
			free(g_pEnd);
			g_pEnd = g_pHead;
			g_pHead->pNext = NULL;
		}
	}
	else // >=3
	{
		STUNODE* pTemp = g_pHead;
		//判断头
		if(g_pHead == pNode)
		{
			//记住头
			pTemp = g_pHead;
			g_pHead = g_pHead->pNext;
			free(pTemp);
			pTemp = NULL;
			return ;  //结束
		}

		while(pTemp)
		{
			if(pTemp->pNext == pNode)
			{
				//删除
				if (pNode == g_pEnd)
				{
					free(pNode);
					pNode = NULL;
					g_pEnd = pTemp;
					g_pEnd->pNext = NULL;
					return ;
				}
				else
				{
					//记住要删除的节点
					STUNODE* p = pTemp->pNext;
					//链接
					pTemp->pNext = pTemp->pNext->pNext;
					//释放节点
					free(p);
					p = NULL;
					return ;
				}
			}

			pTemp = pTemp->pNext;
		}
	}
}

//保存信息进文件
void SaveStuToFile()
{
	//判断链表是否是NULL
	FILE* pFile = NULL;
	STUNODE* pTemp = g_pHead;
	char strBuf[100] = {0};
//	char strScore[20] = {0};
//    char CScore[10] = {0};
 //   char SumScore[10] = {0};
	if (NULL == g_pHead)
	{
		printf("\t\t没有学生\n");
		return ;
	}

	//打开文件
	pFile = fopen("dat.dat", "wb+");
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return ;
	}
	//操作文件指针
	while(pTemp)
	{
	    char strScore[20] = {0};
        char CScore[20] = {0};
        char SumScore[20] = {0};
		//学号赋值进去
		strcpy(strBuf, pTemp->arrStuNum);
		strcat(strBuf, ".");
		//姓名
		strcat(strBuf, pTemp->arrStuName);
		strcat(strBuf, ".");
		//分数
		itoa(pTemp->iStuScore, strScore, 10);
		strcat(strBuf, strScore);
		strcat(strBuf, ".");
      //  strcat(strBuf, ".");
        itoa(pTemp->CScore, CScore, 10);
		strcat(strBuf, CScore);
		strcat(strBuf, ".");

		itoa(pTemp->SumScore, SumScore, 10);
		strcat(strBuf, SumScore);
		strcat(strBuf, ".");

		fwrite(strBuf, 1, strlen(strBuf), pFile); //
		fwrite("\r\n", 1, strlen("\r\n"), pFile);

		pTemp = pTemp->pNext;
	}

	//关闭文件
	fclose(pFile);
}

//读取文件中学生信息
void ReadStuFromFile()
{
	FILE* pFile = fopen("dat.dat", "rb+"); //

	char strBuf[200] = {0};
//	char strStuNum[10] = {0};
//	char strStuName[10] = {0};
//	char strStuScore[20] = {0};
	int nCount = 0;
	int j;
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return ;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, pFile))  //EOF  feof   3部分
	{
	    char strStuNum[10] = {0};
	    char strStuName[10] = {0};
	    char strStuScore[20] = {0};
	    char CScore[10] = {0};
       char SumScore[10] = {0};
       int NumiStuScore = 0;
       char iStuScore[10] = {0};
       int kScore = 1;
       int  InteriStuScore[20] = {0};
       int Score1 = 0;
       int Score2 = 0;
       int Score3 = 0;

		int i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
			else if (1 == nCount) //第一个'.'
			{
				strStuName[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					strStuName[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}

			else if (2 == nCount) //第一个'.'
			{
				iStuScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					iStuScore[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}


			else if ( 3 == nCount )  //第二个'.' 2 == nCount
			{
				CScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					CScore[j-1] = '\0';
					nCount++;
					j = 0;
				}

			}
			else if ( 4 == nCount) {
                SumScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					SumScore[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
		}
		//这里存的有问题，SUnScore先转换为整数在存储！
		for ( i = 0; i < strlen(SumScore); i++ ){
                if ( 48 <=  SumScore[i] && SumScore[i] <= 57){
            InteriStuScore[i] = SumScore[i] - 48;
                }
		}
		for ( i = strlen(SumScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score3 = NumiStuScore;
		NumiStuScore = 0;
		kScore = 1;
		for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;

		NumiStuScore = 0;
		kScore = 1;
		for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;


		//插入到链表
		AddStuMSG(strStuNum, strStuName, iStuScore, CScore, Score3);
	//	printf("strlen(CScore) = %d strlen(strStuScore) = %d\n strlen(SumScore) = %d",strlen(CScore),strlen(iStuScore),strlen(SumScore));
		printf("\t\t学号:%-10s 姓名:%-12s 托福分数:%-4d 雅思分数:%-4d 平均分数:%-4d\n",strStuNum, strStuName, Score1, Score2, Score3);
	}

	fclose(pFile);
}
//通过学号升序排序学生
void RankStuByminNum()
{
    STUNODE * pTemp = g_pHead;
    STUNODE * tail = NULL;
  //  char temp1[20] = {0};
   // char temp2[20] = {0};
    int temp;
    int CScore = 0;
    int SumScore = 0;
    while ( pTemp != tail ){
            while ( pTemp->pNext != tail ){
                if ( pTemp->iStuScore > pTemp->pNext->iStuScore ){
                    char temp1[20] = {0};
                    char temp2[20] = {0};
                    temp = pTemp->pNext->iStuScore;
                    pTemp->pNext->iStuScore = pTemp->iStuScore;
                    pTemp->iStuScore = temp;

                    CScore = pTemp->pNext->CScore;
                    pTemp->pNext->CScore = pTemp->CScore;
                    pTemp->CScore = CScore;

                    SumScore = pTemp->pNext->SumScore;
                    pTemp->pNext->SumScore = pTemp->SumScore;
                    pTemp->SumScore = SumScore;

                strcpy(temp2, pTemp->pNext->arrStuNum);
                strcpy(pTemp->pNext->arrStuNum, pTemp->arrStuNum);
                strcpy(pTemp->arrStuNum, temp2);
                strcpy(temp1, pTemp->pNext->arrStuName);
                strcpy(pTemp->pNext->arrStuName, pTemp->arrStuName);
                strcpy(pTemp->arrStuName, temp1);
                }
                pTemp = pTemp->pNext;
            }
            tail = pTemp;
            pTemp = g_pHead;
    }
    ShowStuData();
}
void RankStuBymaxNum()
{
    STUNODE * pTemp = g_pHead;
    STUNODE * tail = NULL;
  //  char temp1[20] = {0};
   // char temp2[20] = {0};
    int temp;
    int CScore = 0;
    int SumScore = 0;
    while ( pTemp != tail ){
            while ( pTemp->pNext != tail ){
                if ( pTemp->iStuScore < pTemp->pNext->iStuScore ){
                    char temp1[20] = {0};
                    char temp2[20] = {0};
                    temp = pTemp->pNext->iStuScore;
                    pTemp->pNext->iStuScore = pTemp->iStuScore;
                    pTemp->iStuScore = temp;

                    CScore = pTemp->pNext->CScore;
                    pTemp->pNext->CScore = pTemp->CScore;
                    pTemp->CScore = CScore;

                    SumScore = pTemp->pNext->SumScore;
                    pTemp->pNext->SumScore = pTemp->SumScore;
                    pTemp->SumScore = SumScore;

                strcpy(temp2, pTemp->pNext->arrStuNum);
                strcpy(pTemp->pNext->arrStuNum, pTemp->arrStuNum);
                strcpy(pTemp->arrStuNum, temp2);
                strcpy(temp1, pTemp->pNext->arrStuName);
                strcpy(pTemp->pNext->arrStuName, pTemp->arrStuName);
                strcpy(pTemp->arrStuName, temp1);
                }
                pTemp = pTemp->pNext;
            }
            tail = pTemp;
            pTemp = g_pHead;
    }
    ShowStuData();
}
//统计托福成绩高于600分的学生并输出
void AddUpScoreHigher60()
{
    STUNODE * pTemp = g_pHead;
    while (pTemp){
        if ( pTemp->iStuScore > 600 ){
            printf("\t\t学号：%-8s 姓名：%-10s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
        }
        pTemp = pTemp->pNext;
    }
}
//统计成绩低于600分学生的数量并输出
void AddUpNumOfScoreLower60()
{
    STUNODE * pTemp = g_pHead;
    int num = 0;
    while (pTemp){
        if ( pTemp->iStuScore < 600 ){
                printf("\t\t学号：%-8s 姓名：%-10s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
            num++;
        }
        pTemp = pTemp->pNext;
    }
    printf("\t\t托福成绩低于600分的学生一共有：%d人\n",num);
}
//通过姓名查找学生信息
STUNODE * FindMSGByName(char* arrStuName)
{
    STUNODE * pTemp = g_pHead;
    while (pTemp){
        if ( strcmp(pTemp->arrStuName, arrStuName) == 0 ){
            return pTemp;
        }
        pTemp = pTemp->pNext;
    }
    return NULL;
}
void STUReadStuFromFile()
{
	FILE* pFile = fopen("dat.dat", "rb+"); //

	char strBuf[200] = {0};

	char strStuNum[10] = {0};
	char strStuName[10] = {0};
	char strStuScore[20] = {0};
	int nCount = 0;
	int j = 0;
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return ;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, pFile))  //EOF  feof   3部分
	{
	    char strStuNum[10] = {0};
	    char strStuName[10] = {0};
	    char strStuScore[20] = {0};
	    char CScore[10] = {0};
       char SumScore[10] = {0};
		int i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[i] = strBuf[i];
				if ('.' == strBuf[i])
				{
					strStuNum[i] = '\0';
					nCount++;
				}
			}
			else if (1 == nCount) //第一个'.'
			{#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <conio.h>
#define BACKSPACE 8
//学生节点
typedef struct _STU
{
	char arrStuNum[10];
	char arrStuName[10];
	int  iStuScore;
	int  CScore;
    int  SumScore;
	struct _STU* pNext;
} STUNODE;
int JudgeIfRFight();
//判断指令输入的是否正确？是否需要重新输入

//声明链表的头和尾
STUNODE* g_pHead = NULL;  //O
STUNODE* g_pEnd = NULL;
//通过姓名查找指定学生的信息
STUNODE * FindMSGByName(char* arrStuName);
//统计成绩低于60分学生的数量
void AddUpNumOfScoreLower60();
//查询成绩高于60分的学生并输出
void AddUpScoreHigher60();
//降序排序学生
void RankStuBymaxNum();
//升序排序学生
void RankStuByminNum();
//添加一个学生的信息
void AddStuMSG(char *arrStuNum, char arrStuName[10], char iStuScore[], char CScore[100], int SumScore);


//清空链表
void FreeLinkData();

//打印数据
void ShowStuData();

//显示指令
void ShowOrder();

//查找制定学生
STUNODE* FindStuByNum(char* arrStuNum); //【】

//指定位置插入节点
void InsertNode(STUNODE* pTemp, char *arrStuNum, char arrStuName[10], char iStuScore[100], char CScore[100], int SumScore);

//删除指定学生
void DeleteStuNode(STUNODE* pNode);

//保存信息进文件
void SaveStuToFile();

//读取文件中学生信息
void ReadStuFromFile();
//学生端读取信息
void STUReadStuFromFile();
int j,k,i,nCount;

int main(void)
{
    system("color 0A");
	FILE * fp = NULL;
	FILE * pFile = NULL;
	char strStuNum[10] = {0};//检测是否重复
  //  int FindMsg = 0;//查找学号用到

    char password[100] = {"s123456"};
    char vippassword[100] = {"t123456"};
    char vipaccount[100] = {"tcaihong"};
    char account[100] = {"scaihong"};
    char userpassword[100] = {0};
    char useraccount[100] = {0};
    char Print1Or2[100] = {0};
    char VipFirstAcount[100] = {0};
     //先将VIP的账号和密码保存在文件中
/*    fp = fopen("NewCount","ab+");
    strcpy(VipFirstAcount, vipaccount);
    strcat(VipFirstAcount, ".");
    strcat(VipFirstAcount, vippassword);
    strcat(VipFirstAcount, ".");
    fwrite(VipFirstAcount, 1, strlen(VipFirstAcount), fp);
    fwrite("\r\n", 1, strlen("\r\n"), fp);
    fclose(fp);
    fp = NULL;
    */

    printf("\t\t*******************欢迎您进入学生信息管理系统*********************\n");
    printf("\t\t************1.登陆 2.注册新账户(教师端) 其他.程序结束*************\n");
    printf("\t\t请输入指令\n\t\t再次提示，这一步请仔细输入指令，一旦输入错误，您将还有三次输入机会\n");
    printf("\t\t");
    scanf("%s",Print1Or2);
    getchar();
    if ( (Print1Or2[0] != '1' && Print1Or2[0] != '2') || strlen(Print1Or2) != 1){
 //           printf("\t\tPrint1Or2[0] = %c,strlen(Print1Or2) = %d\n",Print1Or2[0],strlen(Print1Or2));
        printf("\t\t您输入的指令不正确，您还有两次输入机会\n\t\t请重新输入\n");
        printf("\t\t");
        scanf("%s",Print1Or2);
        getchar();

    if ( (Print1Or2[0] != '1' && Print1Or2[0] != '2') || strlen(Print1Or2) != 1){
  //      printf("\t\tPrint1Or2[0] = %c,strlen(Print1Or2) = %d\n",Print1Or2[0],strlen(Print1Or2));
        printf("\t\t您输入的指令不正确，您还有一次输入机会\n\t\t警告，本次输入若再出现错误，将退出系统！\n\t\t请重新输入\n");
        printf("\t\t");
        scanf("%s",Print1Or2);
        getchar();
               }
    }

if ( strlen(Print1Or2) == 1 && Print1Or2[0] == '2' ){
	pFile = fopen("NewCount","rb+");
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
    char AppalyCount[100] = {0};
    char AppalyPassWord[100] = {0};
    char TeacherNewAcount[100] = {0};
    char TeacherOldAcount[100] = {0};
    char TeacherNewPassWord[100] = {0};
    char TeacherOldPsaaWord[100] = {0};
    char TeacherOld[100] = {0};
    char TeacherNew[100] = {0};
    int m = 0;
 //   FILE * pFile = NULL;

 //   pFile = fopen("NewCount","wb+");
    //先将VIP的账号和密码保存在文件中


    puts("\t\t请输入教师端新账户的账号：");
    printf("\t\t");
    scanf("%s",AppalyCount);//新账号
    getchar();
    puts("\t\t请输入教师端新账户的密码：");
    printf("\t\t");
  //  scanf("%s",AppalyPassWord);//新密码
  //  getchar();


    char ch;
  int sum = 0;//计数光标退格几次
  i = 0;
    while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			sum++;
			i--;

		}else{
		putchar('*');
		AppalyPassWord[i] = ch;
		i++;
	}
	}
	AppalyPassWord[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",AppalyPassWord);








    //判断是否和已有账户重复
    k = 0;
    //判断与源文件中的账号密码是否重复。
//    现在问题是 比较之后明明新账号与之前账号相同，系统却显示不同，进入下一步。。。。
    while ( fgets(TeacherOld, 100, pFile) != NULL && k == 0 && m != 1){
            nCount = 0;
        j = 0;
        for ( i = 0; TeacherOld[i] != '\r'; i++ ){
        if ( nCount == 0 ){
            TeacherNewAcount[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewAcount[j-1] = '\0';
                nCount++;
                j = 0;
                //这个break break掉while吗？？？
            }
            }
        else if ( nCount == 1 ){
            TeacherNewPassWord[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewPassWord[j-1] = '\0';
                nCount++;
                j = 0;
            }

        }
        }
 //       printf("%s %s\n",TeacherNewAcount, TeacherNewPassWord);
 //       printf("%s %s\n",AppalyCount, AppalyPassWord);
        //这样的话 一个密码就读取完毕
     //   这里有问题，应该让新账户和文件中的所有账户比较完之后 再下结论。
        if ( strcmp(TeacherNewAcount, AppalyCount) == 0 && strcmp(TeacherNewPassWord, AppalyPassWord) == 0 ){
        	printf("\t\t您输入的新账户的账号或密码与已有账户信息重复\n\t\t您还有一次机会，请重新输入您想要注册的账号信息\n");
        	m = 1;
        	puts("\t\t请输入教师端新账户的账号：");
        	printf("\t\t");
    scanf("%s",AppalyCount);//新账号
    getchar();
    puts("\t\t请输入教师端新账户的密码：");
    printf("\t\t");
    scanf("%s",AppalyPassWord);//新密码
    getchar();
    //判断是否和已有账户重复
    k = 0;
    //判断与源文件中的账号密码是否重复。
//    现在问题是 比较之后明明新账号与之前账号相同，系统却显示不同，进入下一步。。。。
    fclose(pFile);
    pFile = NULL;
    pFile = fopen("NewCount","rb+");
    while ( fgets(TeacherOld, 100, pFile) != NULL && k == 0 ){
            nCount = 0;
        j = 0;
        for ( i = 0; TeacherOld[i] != '\r'; i++ ){
        if ( nCount == 0 ){
            TeacherNewAcount[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewAcount[j-1] = '\0';
                nCount++;
                j = 0;
                //这个break break掉while吗？？？
            }
            }
        else if ( nCount == 1 ){
            TeacherNewPassWord[j] = TeacherOld[i];
            j++;
            if ( TeacherOld[i] == '.' ){
                TeacherNewPassWord[j-1] = '\0';
                nCount++;
                j = 0;
            }

        }
        }
  //      printf("%s %s\n",TeacherNewAcount, TeacherNewPassWord);
 //       printf("%s %s\n",AppalyCount, AppalyPassWord);
        if ( strcmp(TeacherNewAcount, AppalyCount) == 0 && strcmp(TeacherNewPassWord, AppalyPassWord) == 0 ){
		printf("\t\t您又一次输入了已有的账户信息，系统将自动退出\n\t\t下次输入请认真对待，谢谢！\n");



        	return 0;
        }
		}
    }
	}//不用加任何，只要不return 0 就说明新账户不与原账户重复！
    fclose(pFile);
    pFile = NULL;






//问题在这
//char TeacherNew[100] = {0};
    //    if ( strcmp(TeacherNewAcount, AppalyCount) != 0 && strcmp(TeacherNewPassWord, AppalyPassWord) != 0 ){//文件中的一个密码与你输入的新密码比较，看是否相同
//    问题：新注册的账号在这里 但是没有保存进去文件，是不是strcpy的问题？
            k = 1;
            printf("\t\t恭喜，您申请的教师端新账户可用\n\t\t系统将进入登陆界面\n");//然后把账户啥的信息写进文件中去
            pFile = fopen("NewCount","ab+");
            if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
            strcpy(TeacherNew, AppalyCount);
            strcat(TeacherNew, ".");
            strcat(TeacherNew, AppalyPassWord);
            strcat(TeacherNew, ".");
       //     fwrite("\r\n", 1, strlen("\r\n"), pFile);
            fwrite(TeacherNew, 1, strlen(TeacherNew), pFile);
            fwrite("\r\n", 1, strlen("\r\n"), pFile);//**********将新账号信息保存到文件中去
            fclose(pFile);
            pFile = NULL;
            //然后直接自动进入即可
        //    k = 1;
  //      }
     //   if ( strcmp(TeacherNewAcount, AppalyCount) == 0 && strcmp(TeacherNewPassWord, AppalyPassWord) == 0 ){
    //    	printf("您输入的新账户的账号或密码与已有账户信息重复\n退出系统\n");
    //    	return 0;
	//	}
    }//写入完毕，下来就是输入密码了，

//}
  //  fclose(pFile);
 //   pFile = NULL;






  //  printf("k = %d\n",k);

   if ( (strlen(Print1Or2) == 1 && Print1Or2[0] == '1' ) || k == 1 ){

	char AllUserMSG[100] = {0};
	int MSG = 0;
    printf("\t\t************  系统已进入登录界面，请您输入账号和密码  **************\n");

    printf("\t\t-------------------------------------------------------------------\n");

    printf("\t\t账号：\n");
    printf("\t\t");
    scanf("%s",useraccount);
    getchar();
 //   printf("\t\t");
    printf("\t\t密码：\n");
 //  scanf("%s",userpassword);
 //  getchar();
  //使用 * 号输入：
  //这里有问题 怎么输入密码
  char ch;
  int sum = 0;//计数光标退格几次
  i = 0;

  printf("\t\t");

    while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			sum++;
			i--;

		}else{
		putchar('*');
		userpassword[i] = ch;
		i++;
	}
	}
	userpassword[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",userpassword);

	if (strcmp(useraccount, account) == 0 && strcmp(userpassword, password) == 0){




        puts("\t\t您已作为学生端用户登录学生管理系统,您只能行使查看学生信息的权限。\n");
        puts("\t\t以下为系统中所有学生的信息：\n");
        STUReadStuFromFile();
        return 0;
    }






    //下面检验当前输入的账号和密码与保存在文件中的任一除了系统初始设定的普通账号和密码不同的一组账号和密码，简单，在文件中只保存VIP的账号和密码
    pFile = fopen("NewCount","rb+");
    if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
//    fwrite("zhanghao.mima.", 1, strlen("zhanghao.mima."), pFile);
    //读入文件中每一行的账号和密码，每读入一次，把把账号和密码分别赋值给两个新创建的数组储存，再用strcmp函数作比较，只要有一次符合要求，就进入教师端
    MSG = 0;
//这里有问题，UserTextPassword无法保存
    while ( fgets(AllUserMSG, 100, pFile) != NULL && MSG == 0){//把文件中的所有账号和密码都遍历一遍，与你现在输入的账号和密码做比较
    char UserTextCount[100] = {0};
	char UserTextPassword[100] = {0};
	//这下面写 把每一行的账号和密码转化出来赋值给 UserTextCount 和 UserTextPassword
    nCount = 0;
    j = 0;
    for ( i = 0; AllUserMSG[i] != '\r'; i++ ){

    	if ( nCount == 0 ){
    		UserTextCount[j] = AllUserMSG[i];
    		j++;
    		if ( AllUserMSG[i] == '.' ){
    			UserTextCount[j-1] = '\0';
    			j = 0;
    			nCount++;
    	//		printf("nCount = %d\n",nCount);
			}
		}
	//	printf("j = %d\n",j);
		else if ( nCount == 1 ){
			UserTextPassword[j] = AllUserMSG[i];
			j++;
			if ( AllUserMSG[i] == '.' ){
				UserTextPassword[j-1] = '\0';
				j = 0;
				nCount++;
			//	printf("nCount = %d\n",nCount);
			}
		}
//		printf("AllUserMSG = %s\n",AllUserMSG);
	//	printf("111\n");
	}
//	printf("\t\tUserTextCount = %s, UserTextPassword = %s\n",UserTextCount, UserTextPassword);
//	printf("\t\tuseraccount = %s, userpassword = %s\n",useraccount, userpassword);
	if ( strcmp(useraccount, UserTextCount) == 0 && strcmp(userpassword, UserTextPassword) == 0 ){
        printf("\t\t您输入的账户信息正确\n");
        MSG = 1;
     //   printf("111\n");

	}
    }
    fclose(pFile);
    pFile = NULL;
    if ( MSG == 0 ){
            printf("\t\t您输入的账号或密码不正确，您还有两次输入机会，请重新输入\n");
             printf("\t\t账号：\n\t\t");
       //      printf("\t\t");
    scanf("%s",useraccount);
    getchar();

    printf("\t\t密码：\n");
 //  scanf("%s",userpassword);
 //  getchar();
  //使用 * 号输入：
  //这里有问题 怎么输入密码
  char ch;
  i = 0;
  printf("\t\t");

    while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			i--;

		}else{
		putchar('*');
		userpassword[i] = ch;
		i++;
	}
	}
	userpassword[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",userpassword);






    //下面检验当前输入的账号和密码与保存在文件中的任一除了系统初始设定的普通账号和密码不同的一组账号和密码，简单，在文件中只保存VIP的账号和密码
    pFile = fopen("NewCount","rb+");
    if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
//    fwrite("zhanghao.mima.", 1, strlen("zhanghao.mima."), pFile);
    //读入文件中每一行的账号和密码，每读入一次，把把账号和密码分别赋值给两个新创建的数组储存，再用strcmp函数作比较，只要有一次符合要求，就进入教师端
    MSG = 0;
//这里有问题，UserTextPassword无法保存
    while ( fgets(AllUserMSG, 100, pFile) != NULL && MSG == 0){//把文件中的所有账号和密码都遍历一遍，与你现在输入的账号和密码做比较
    char UserTextCount[100] = {0};
	char UserTextPassword[100] = {0};
	//这下面写 把每一行的账号和密码转化出来赋值给 UserTextCount 和 UserTextPassword
    nCount = 0;
    j = 0;
    for ( i = 0; AllUserMSG[i] != '\r'; i++ ){

    	if ( nCount == 0 ){
    		UserTextCount[j] = AllUserMSG[i];
    		j++;
    		if ( AllUserMSG[i] == '.' ){
    			UserTextCount[j-1] = '\0';
    			j = 0;
    			nCount++;
    	//		printf("nCount = %d\n",nCount);
			}
		}
	//	printf("j = %d\n",j);
		else if ( nCount == 1 ){
			UserTextPassword[j] = AllUserMSG[i];
			j++;
			if ( AllUserMSG[i] == '.' ){
				UserTextPassword[j-1] = '\0';
				j = 0;
				nCount++;
			//	printf("nCount = %d\n",nCount);
			}
		}
//		printf("AllUserMSG = %s\n",AllUserMSG);
	//	printf("111\n");
	}
//	printf("UserTextCount = %s, UserTextPassword = %s\n",UserTextCount, UserTextPassword);
//	printf("useraccount = %s, userpassword = %s\n",useraccount, userpassword);
	if ( strcmp(useraccount, UserTextCount) == 0 && strcmp(userpassword, UserTextPassword) == 0 ){
        printf("\t\t您输入的账户信息正确\n");
        MSG = 1;
     //   printf("111\n");

	}
    }
    fclose(pFile);
        pFile = NULL;



        if ( MSG == 0 ){
            printf("\t\t您输入的账号或密码不正确，您还有一次输入机会\n\t\t警告，如果再次输入不正确，将退出程序！\n\t\t请重新输入:\n");
             printf("\t\t账号：\n");
        //     printf("\t\t");
    scanf("%s",useraccount);
    getchar();

    printf("\t\t密码：\n");
 //  scanf("%s",userpassword);
 //  getchar();
  //使用 * 号输入：
  //这里有问题 怎么输入密码
  char ch;
  i = 0;
  printf("\t\t");
/*
    while ( (ch = getch()) != '\r' && i < 100 ){

			userpassword[i] = ch;
			i++;
			printf("*");
	}*/
	while ( (ch = getch()) != '\r' ){
		if ( ch ==  8 ){
	//		return 0;
			putchar('\b');
            putchar(' ');
			putchar('\b');
			i--;

		}else{
		putchar('*');
		userpassword[i] = ch;
		i++;
	}
	}
	userpassword[i] = '\0';
	printf("\n");
	printf("\t\t%s\n",userpassword);





    //下面检验当前输入的账号和密码与保存在文件中的任一除了系统初始设定的普通账号和密码不同的一组账号和密码，简单，在文件中只保存VIP的账号和密码
    pFile = fopen("NewCount","rb+");
    if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}
//    fwrite("zhanghao.mima.", 1, strlen("zhanghao.mima."), pFile);
    //读入文件中每一行的账号和密码，每读入一次，把把账号和密码分别赋值给两个新创建的数组储存，再用strcmp函数作比较，只要有一次符合要求，就进入教师端
    MSG = 0;
//这里有问题，UserTextPassword无法保存
    while ( fgets(AllUserMSG, 100, pFile) != NULL && MSG == 0){//把文件中的所有账号和密码都遍历一遍，与你现在输入的账号和密码做比较
    char UserTextCount[100] = {0};
	char UserTextPassword[100] = {0};
	//这下面写 把每一行的账号和密码转化出来赋值给 UserTextCount 和 UserTextPassword
    nCount = 0;
    j = 0;
    for ( i = 0; AllUserMSG[i] != '\r'; i++ ){

    	if ( nCount == 0 ){
    		UserTextCount[j] = AllUserMSG[i];
    		j++;
    		if ( AllUserMSG[i] == '.' ){
    			UserTextCount[j-1] = '\0';
    			j = 0;
    			nCount++;
    	//		printf("nCount = %d\n",nCount);
			}
		}
	//	printf("j = %d\n",j);
		else if ( nCount == 1 ){
			UserTextPassword[j] = AllUserMSG[i];
			j++;
			if ( AllUserMSG[i] == '.' ){
				UserTextPassword[j-1] = '\0';
				j = 0;
				nCount++;
			//	printf("nCount = %d\n",nCount);
			}
		}
//		printf("AllUserMSG = %s\n",AllUserMSG);
	//	printf("111\n");
	}
//	printf("UserTextCount = %s, UserTextPassword = %s\n",UserTextCount, UserTextPassword);
	//printf("useraccount = %s, userpassword = %s\n",useraccount, userpassword);
	if ( strcmp(useraccount, UserTextCount) == 0 && strcmp(userpassword, UserTextPassword) == 0 ){
        printf("\t\t您输入的账户信息正确\n");
        MSG = 1;
     //   printf("111\n");

	}
    }
    fclose(pFile);
        pFile = NULL;
        }




    }



 //   后面那个while的大括号记得去掉


    if ( MSG == 1 ){//只要成立，自动认为是教师端账户
   // 	MSG = 1;
    	printf("\t\t您的账号密码输入均正确\n\t\t您已成功进入教师端学生成绩管理系统\n");
//	int nOrder = -1; //nOrder iOrder  s db arr p
	                 //初始化
	char arrStuNum[10] = {'\0'};
	char arrStuName[10] = {'\0'};
//	int  iStuScore = -1;
    int Select;
	int nFlag = 1;
    int RankSelect;//这也得改成char雷迪奥迪
  //  int AgainCarryOut;//回到选择命令行，重新输入指令

    int RealSelectBy;//用于打印信息的case
  //  int InterSelectByOneAndTwo[100] = {0};




  //  getchar();
	STUNODE* pTemp = NULL;
	ShowOrder();
    //取其一选择
	//读取文件中学生信息
	ReadStuFromFile();
  //  char nOrder[100] = {0};
//    int i;
 //   int InterNOrder[100] = {0};
	while(nFlag)
	{
	    int AgainCarryOut;
	    int kNum = 1;
	    int Score1 = 0;
	    int Score2 = 0;
	    int RealSelectByOneAndTwo = 0;
	    char SelectByOneAndTwo[100] = {0};
        char FindMsg[100] = {0};
	    char iStuScore[100] = {0};
	    char CScore[100] = {0};
//	    char SumScore[100] = {0};
	    int SumScore = 0;
        int InteriStuScore[100] = {0};
        int NumiStuScore = 0;
        int kScore = 1;
	    int InterSelectByOneAndTwo[100] = {0};
	    char nOrder[100] = {0};
	    k = 1;
	    int SwitchNumber = 0;
	    int InterNOrder[100] = {0};
		printf ("\t\t请输入指令(10、查看指令):\n");
	//	getchar();//必须加gechar()要不然前面有%s
	printf("\t\t");
		scanf("%s",nOrder);
//		printf("strlen(nOrder) = %d\n",strlen(nOrder));
		for ( i = 0; i < strlen(nOrder); i++ ){
            InterNOrder[i] = nOrder[i] - 48;
  //          printf("%d\n",InterNOrder[i]);
		}
		for ( i = strlen(nOrder)-1; i >= 0; i-- ){
            SwitchNumber += k * InterNOrder[i];
            k *= 10;
		}
	//	getchar();
//        int i;
        int Flag1;
        int Num1;
        int Num2;
        int Num3;
        int Num4;
        char strBuf[200] = {0};
        char strStuNum[10] = {0};
	    int nCount;
//	    int j;
	    int MarkOrLogo;
	    int LogoIfTextHaveReapper;
  //      atoi(nOrder);


   //     printf("SwitchNumber= %d\n",SwitchNumber);
        if ( SwitchNumber < 1 || SwitchNumber > 14 ){
            printf("\t\t您输入的指令有误，请重新输入！\n");
            printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
        }
        else {
             //   getchar();
		switch (SwitchNumber)//两种可能 输入错误的话还得加一种 选择退出或者是继续输入。
		{
		case 1:
      //      int InterSelectByOneAndTwo[100] = {0};
            nCount = 0;
            LogoIfTextHaveReapper = 0;
            j = 0;
            MarkOrLogo = 0;
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
		    system("cls");
		    //尾添加
		    //把他们也写到一个函数中去
		//    JudgeIfRFight();
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		    }else {
			//添加一个学生的信息
			printf ("\t\t请输入8位学号:\n");
			printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			fp = NULL;


			fp = fopen("dat.dat", "rb+");

	if (NULL == fp)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, fp) && LogoIfTextHaveReapper == 0 )  //EOF  feof   3部分
	{

		i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
		}
		if ( strcmp(arrStuNum, strStuNum) == 0 ){
		    printf("\t\t您输入的学号和之前系统中保存的学号相同\n\t\t请仔细检查您的学号输入是否有误！\n");
		    MarkOrLogo = 1;
		    LogoIfTextHaveReapper = 1;
		}
		if ( MarkOrLogo == 1 ){
		    printf ("\t\tPS:这次不要再输入重复学号啦！\n\t\t请输入8位学号:\n");
		    printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
				if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }





        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
    //    if ( AgainCarryOut != 1 && Num2 != 2)

        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}




		}
	}
	fclose(fp);



		if ( MarkOrLogo == 0 ){

			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( AgainCarryOut != 1 && Num2 != 2 ){

        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
		}

             /*   printf("您输入的学号不够8位，您还有一次输入机会，如果您再次因粗心输入错误，将退出程序！\n请认真核对后重新输入学号:\n");
                Num2 = 1;
			}else{
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("您输入的学号不正确，可能是您输入了字母或键入学号不够8位，您还有一次输入机会，如果您再次因粗心输入错误，将退出程序！\n请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }
			if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                scanf ("%s", arrStuNum);
			}*/
			printf ("\t\t请输入姓名:\n");
			printf("\t\t");
			scanf ("%s", arrStuName);

			getchar();
	//		printf("strlen(arrStuName) = %d\n",strlen(arrStuName));
			for ( i = 0; i < strlen(arrStuName); i++ ){
        //            printf("arrStuName[i] = %d\n",arrStuName[i]);
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t您输入的姓名格式不正确，可能是您输入了数字\n\t\t因为您已经成功输入了正确的学号,系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生姓名:\n");
                    Num3 = 1;
                    break;
                }
			}
                if (Num3 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}
			//下面这些函数声明 写到上面去 最后
		//	char iStuScore[100] = {0};
		//	int InteriStuScore[100] = {0};
		//	int NumiStuScore = 0;
		//	int kScore = 1;
			printf ("\t\t请输入托福分数:\n");
		//	scanf ("%d", &iStuScore);
		printf("\t\t");
		scanf("%s",iStuScore);
		getchar();
		for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;



			if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还有极大可能您输入了字母\n\t\t因为您已经成功输入了正确的学号和姓名,系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", iStuScore);
                getchar();
                kScore = 1;
                NumiStuScore = 0;

                for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;


                for ( i = 0; i < strlen(iStuScore); i++ ){
                    if ( iStuScore[i] < 48 || iStuScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			NumiStuScore = 0;
			kScore = 1;
			Num4 = 0;




			printf ("\t\t输入雅思分数:\n");
		//	scanf ("%d", &iStuScore);
		printf("\t\t");
		scanf("%s",CScore);
		getchar();
		for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;



			if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还有极大可能您输入了字母\n\t\t因为您已经成功输入了正确的学号和姓名,系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", CScore);
                getchar();
                kScore = 1;
                NumiStuScore = 0;

                for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;



                for ( i = 0; i < strlen(CScore); i++ ){
                    if ( CScore[i] < 48 || CScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			SumScore = (Score1 + Score2) / 2;










			AddStuMSG(arrStuNum, arrStuName, iStuScore, CScore, SumScore);
		}
	}

		printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();


			break;

		case 11:  //中间插入添加
		    NumiStuScore = 0;
		    nCount = 0;
            LogoIfTextHaveReapper = 0;
            j = 0;
            MarkOrLogo = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
		    system("cls");
		    //尾添加
		    //把他们也写到一个函数中去
		//    JudgeIfRFight();
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
		        printf ("\t\t以下为已有学生信息\n\t\t请输入8位学号(已有学生的学号)，来选择将新学生插入到哪个学生的后面去:\n");//输入已添加学号
		        ShowStuData();
		        printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			//判断是否重复


			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);
                ;
            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }


        if ( Num2 == 2 ){
            break;
        }
        printf("\t\tstrlen(arrStuNum) = %d\n",strlen(arrStuNum));
        if ( strlen(arrStuNum) == 8 ){
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
         if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;

			pTemp = FindStuByNum(arrStuNum);
			if (NULL != pTemp)  //200501013  1254
			{
				//TODO：插入
				printf ("\t\t请输入新添加学生的8位学号:\n");
				printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			fp = NULL;


			fp = fopen("dat.dat", "rb+");

	if (NULL == fp)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, fp) && LogoIfTextHaveReapper == 0 )  //EOF  feof   3部分
	{

		i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}



		}
		if ( strcmp(arrStuNum, strStuNum) == 0 ){
		    printf("\t\t您输入的学号和之前系统中保存的学号相同\n\t\t请仔细检查您的学号输入是否有误！\n");
		    MarkOrLogo = 1;
		    LogoIfTextHaveReapper = 1;
		}
		if ( MarkOrLogo == 1 ){
		    printf ("\t\tPS:这次不要再输入重复学号啦！\n\t\t请输入8位学号:\n");
		    printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
				if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}




		}
	}
	fclose(fp);



		if ( MarkOrLogo == 0 ){





			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
			}
			if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
            if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
         if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
		}




			printf ("\t\t请输入新添加的学生的姓名:\n");
			printf("\t\t");
			scanf ("%s", arrStuName);
			getchar();
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t您输入的姓名格式不正确，可能是您输入了数字。\n\t\t因为您已经将新添加的学生学号输入正确，系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生姓名:\n");
                    Num3 = 1;
                    break;
                }
			}
                if (Num3 == 1){//输入的学号格式不正确,重新输入printf("\t\t");
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}







			printf ("\t\t请输入新添加的学生的托福分数:\n");
			printf("\t\t");
			scanf ("%s", iStuScore);
			getchar();


				for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;
		NumiStuScore = 0;
		kScore = 1;



			if (Score1 < 0 || Score1 > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分，还可能是您输入了字母。\n\t\t因为您已经将新添加的学生学号和姓名输入正确，系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", iStuScore);
                getchar();
                NumiStuScore = 0;
		        kScore = 1;

				for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;



                for ( i = 0; i < strlen(iStuScore); i++ ){
                    if ( iStuScore[i] < 48 || iStuScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }


			}
			NumiStuScore = 0;
			kScore = 1;
			Num4 = 0;
			printf ("\t\t请输入新添加的学生的雅思分数:\n");
			printf("\t\t");
			scanf ("%s", CScore);
			getchar();


				for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;



			if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分，还可能是您输入了字母。\n\t\t因为您已经将新添加的学生学号和姓名输入正确，系统默认您要把该生信息全部输入完毕。此时系统只有继续输入的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对分数后重新输入学生分数:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", CScore);
                getchar();
                NumiStuScore = 0;
                kScore = 1;


                for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;


                for ( i = 0; i < strlen(CScore); i++ ){
                    if ( CScore[i] < 48 || CScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }


			}
			SumScore = ( Score2 + Score1) / 2;










				InsertNode(pTemp, arrStuNum, arrStuName, iStuScore, CScore, SumScore);
        //111}
			}
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
			break;
		case 2: //查找\打印指定学生的信息
			//输入一个学号
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			printf("\t\t想通过什么方式查找信息？\n\t\t键入1.通过学号查找 键入2.通过姓名查找\n");
			printf("\t\t");
			scanf("%s",FindMsg);
			getchar();
			for ( i = 0; i < strlen(FindMsg); i++ ){
			    InterSelectByOneAndTwo[i] = FindMsg[i] - 48;
			}
			for ( i = strlen(FindMsg)-1; i >= 0; i-- ){
			    RealSelectBy += InterSelectByOneAndTwo[i] * kNum;
			    kNum *= 10;
			}
			printf("RealSelectBy = %d\n",RealSelectBy);

			if ( RealSelectBy == 1 ){//通过学号查找
                printf ("\t\t请输入8位指定学号，以便于查找学生信息:\n");
                printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			//判断
			kNum = 1;

			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
			//查找
			pTemp = FindStuByNum(arrStuNum);

			//打印
			if (NULL != pTemp)  //200501013  1254
			{
				printf("\t\t以下为该学生信息：\n学号:%-10s, 姓名:%-12s, 托福分数:%-4d， 托福分数:%-4d， 平均分数:%-4d\n ", pTemp->arrStuNum, pTemp->arrStuName, pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
			}else{
			    printf("\t\t您输入的学号有误！\n");
            }
			}
			else if ( RealSelectBy == 2 ){//通过姓名查找
			NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
                printf("\t\t请输入学生姓名,以便于查找学生信息：\n");
                printf("\t\t");
            scanf("%s", arrStuName);
            getchar();
            for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t由于您输入的姓名的格式输入有误，可能是您输入了数字。系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
                    printf("\t\t");
                   scanf("%s",SelectByOneAndTwo);
                   getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的姓名的格式输入有误，可能是您输入了数字。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入姓名:\n");
                Num3 = 1;
                break;
            default:
                Num3 = 2;
                printf("\t\t您输入的不符合任何，将重新返回选择命令行\n");
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                break;
            }

                }
                break;
			}
			if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
            if ( Num3 == 2 ){
                break;
            }

                if (Num3 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}
            pTemp = FindMSGByName(arrStuName);
            if ( pTemp ){
                printf("\t\t以下为该学生信息：\n");
                printf("\t\t学号：%-10s 姓名：%-12s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
            }else{
                printf("\t\t系统中没有您要查找的学生信息,系统将重新返回选择命令行\n");
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
            }
			}
			else {//NUM不等于1也不等于2时
			    printf("\t\t您输入的指令错误，系统重回命令选择界面\n");
			    printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
			    break;
			}
			}
				printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();

			break;
		case 3:  //修改指定学生的信息
		    nCount = 0;
            LogoIfTextHaveReapper = 0;
            j = 0;
            MarkOrLogo = 0;
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            //判断指令是否输入正确
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else{
			//输入一个学号
			printf ("\t\t以下为已有学生信息：\n");
			ShowStuData();
			printf("\t\t请输入8位指定学号(已有学生)，用于修改已有学生信息:\n");
			printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }

        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();

			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
                }
			pTemp = FindStuByNum(arrStuNum);


			//查找
			NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;

			//打印
			if (NULL != pTemp)  //200501013  1254
			{
				//修改学好
				printf ("\t\t请输入修改后的学号:\n");
				printf("\t\t");
				scanf("%s", arrStuNum);
				getchar();




				/*if (strlen(arrStuNum) != 8){
                printf("\t\t您输入的学号不够8位。\n\t\t因为您已经成功输入了要修改学生的学号,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生学号:\n");
                Num2 = 1;
			    }else{
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母。\n\t\t因为您已经成功输入了要修改学生的学号,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }
            if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                    printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}*/

			fp = NULL;


			fp = fopen("dat.dat", "rb+");

	if (NULL == fp)
	{
		printf("\t\t文件打开失败\n");
		return 0;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, fp) && LogoIfTextHaveReapper == 0 )  //EOF  feof   3部分
	{

		i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}



		}
		if ( strcmp(arrStuNum, strStuNum) == 0 ){
		    printf("\t\t您输入的学号和之前系统中保存的学号相同\n\t\t请仔细检查您的学号输入是否有误！\n");
		    MarkOrLogo = 1;
		    LogoIfTextHaveReapper = 1;
		}
		if ( MarkOrLogo == 1 ){
		    printf ("\t\tPS:这次不要再输入重复学号啦！\n\t\t请输入8位学号:\n");
		    printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
				if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}




		}
	}
	fclose(fp);



		if ( MarkOrLogo == 0 ){





			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                break;
            }
			}
			if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
            if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
         if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}
		}

				strcpy(pTemp->arrStuNum, arrStuNum);

				//修改名字、
				printf ("\t\t请输入修改后的名字:\n");
				printf("\t\t");
				scanf("%s", arrStuName);
				getchar();
				for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                    printf("\t\t您输入的姓名格式不正确，可能是您输入了数字。\n\t\t因为您已经成功输入了修改后学生的学号,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生姓名:\n");
                    Num3 = 1;
                    break;
                }
			}
                if (Num3 == 1){//输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuName);
                getchar();
                for ( i = 0; i < strlen(arrStuName); i++ ){
                    if (arrStuName[i] >= 48 && arrStuName[i] <= 57){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;
                    }
                }

			}

				strcpy(pTemp->arrStuName, arrStuName);

				//修改分数
				printf ("\t\t请输入修改后的托福分数:\n");
	//			printf("\t\t");
				scanf("%s", iStuScore);
				getchar();
				for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;

				if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还可能您输入了字母。\n\t\t因为您已经成功输入了修改后学生的学号和姓名,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生成绩:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", iStuScore);
    //            printf("\t\t");
                getchar();

                for ( i = 0; i < strlen(iStuScore); i++ ){
                    if ( iStuScore[i] < 48 || iStuScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			NumiStuScore = 0;
			kScore = 1;
			for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }
            }
			for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;

				pTemp->iStuScore = NumiStuScore;

				NumiStuScore = 0;
				kScore = 1;
				Num4 = 0;


				printf ("\t\t请输入修改后的雅思分数:\n");
	//			printf("\t\t");
				scanf("%s", CScore);
				getchar();
				for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }else{
                InteriStuScore[i] = 1000;//分数有两种可能
                break;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;

				if (NumiStuScore < 0 || NumiStuScore > 650){
                printf("\t\t您输入的分数超过了满分650分，也可能是您输入了负分,还可能您输入了字母。\n\t\t因为您已经成功输入了修改后学生的学号和姓名,系统默认您要把该生信息全部修改完毕。此时系统只有继续修改的选项。\n\t\t您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学生成绩:\n");
                Num4 = 1;
			}
			if (Num4 == 1){
                    printf("\t\t");
                scanf ("%s", CScore);
          //      printf("\t\t");
                getchar();

                for ( i = 0; i < strlen(CScore); i++ ){
                    if ( CScore[i] < 48 || CScore[i] > 57 ){
                        printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                        return 0;

                    }
                }
			}
			NumiStuScore = 0;
			kScore = 1;
			for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }
            }
			for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;

				pTemp->CScore = NumiStuScore;

				SumScore = (Score2 + Score1) / 2;

				pTemp->SumScore = SumScore;







			}
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
		case 4://保存信息
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//保存学生信息
			SaveStuToFile();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
/*        case 5:
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		    }else {
            RankStuByminNum();//升序排序学生
		    }
		    	printf("该指令已经执行完毕\n下面为您显示选择命令行，方便进行下一个指令的输入\n");
		ShowOrder();
            break;*/
		case 6://删除学生信息
			//输入一个学号
			  NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
            printf("\t\t以下为您显示已有学生信息：\n");
            ShowStuData();
			printf ("\t\t输入要删除的学生的8位学号:\n");
			printf("\t\t");
			scanf ("%s", arrStuNum);
			getchar();
			if (strlen(arrStuNum) != 8){
			    printf("\t\t由于您学号格式输入有误，系统自动进入以下选择界面：\n\t\t键入1：我不想继续输入了，返回至选择命令界面\n\t\t键入2：收到系统提示并进行第二次输入\n\t\t键入其他，将返回选择命令行\n");
			    printf("\t\t");
                scanf("%s",SelectByOneAndTwo);
                getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i]-48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);

            switch(RealSelectByOneAndTwo)
            {
            case 1:
            	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                AgainCarryOut = 1;
                break;
            case 2:
                printf("\t\t您输入的学号不够或超过8位，您还有一次输入机会，如果您再次因粗心输入错误，将回到选择界面！\n\t\t请认真核对后重新输入学号:\n");
                Num2 = 1;
                break;
            default:
                Num2 = 2;
                printf("\t\t您输入的不符合任何，将重新返回选择命令行\n");
                printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                break;
            }
         //   if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
         //       break;
          //  }
        }
        if ( AgainCarryOut == 1 ){//不行的话把这句话放外面 变成 else if
                break;
            }
        if ( Num2 == 2 ){
            break;
        }
        if ( strlen(arrStuNum) == 8 ){//else 里面是判断如果输入学号刚好8位，那么是否全是数字
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){

                    printf("\t\t您输入的学号不正确，可能是您输入了字母，您还有一次输入机会，如果您再次因粗心输入错误，将结束程序！\n\t\t请认真核对后重新输入学号:\n");
                    Num1 = 1;
                    break;
                }
			}
        }

                if (Num1 == 1 || Num2 == 1){//这两种可能都是因为输入的学号格式不正确,重新输入
                        printf("\t\t");
                scanf ("%s", arrStuNum);
                getchar();
			}
			if ( strlen(arrStuNum) != 8 ){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                return 0;
			}
			for ( i = 0; i < strlen(arrStuNum); i++ ){
                if (arrStuNum[i] < 48 || arrStuNum[i] > 57){
                    printf("\t\t粗心使人倒退！希望您早日改掉粗心的坏习惯！\n\t\t您太粗心了，系统关闭\n");
                    return 0;
                }
			}

			//查找
			pTemp = FindStuByNum(arrStuNum);

			//删除这个节点
			if (NULL != pTemp)  //200501013  1254
			{
				//调用删除学生的函数
				DeleteStuNode(pTemp);
			}
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
		case 7:
			//,释放
			system("cls");
			if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			FreeLinkData();
			g_pHead = NULL;
			g_pEnd = NULL;
			//回复 添加节点
			ReadStuFromFile();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();

			break;
 /*       case 8://按成绩由高到低对学生进行排序
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		    }else {
            RankStuBymaxNum();
		    }
		    	printf("该指令已经执行完毕\n下面为您显示选择命令行，方便进行下一个指令的输入\n");
		ShowOrder();
            break;*/
		case 8://显示所有学生信息
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//显示链表内容
			ShowStuData();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
		case 10://查看指令
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//查看指令
			ShowOrder();
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
			break;
   /*     case 12:
            //统计成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
        case 13:
            //统计成绩低于60分学生的数量
            AddUpNumOfScoreLower60();
            break;
            /*
        /*case 14://通过姓名查找学生信息
            printf("请输入学生姓名：");
            scanf("%s", arrStuName);

            pTemp = FindMSGByName(arrStuName);
            if ( pTemp ){
                printf("以下为该学生信息：\n");
                printf("学号：%s 姓名：%s 成绩：%d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore);
            }
            break;
            */
		case 13://结束程序
		    system("cls");
		    if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
			//退出
			nFlag = 0;
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，系统将自动退出\n");
		    	getchar();
			break;
        case 14://统计成绩
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {

            printf("\t\t键入1：统计托福成绩低于600分学生的数量 \n\t\t键入2：统计托福成绩高于600分的学生并输出\n\t\t键入其他错误指令，您还有一次输入机会\n");
            printf("\t\t");
            scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                printf("\t\tRealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);
            switch(RealSelectByOneAndTwo)
            {
                case 1://统计成绩低于60分学生的数量
            AddUpNumOfScoreLower60();
            break;
                case 2://统计成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
                default:
                    kNum = 1;
                    Num2 = 2;
                    RealSelectByOneAndTwo = 0;
                printf("\t\t您输入的不符合任何，您还有一次输入机会，如果再次输入错误指令，将返回选择命令行\n\t\t请输入指令：\n");
                printf("\t\t键入1：统计托福成绩低于600分学生的数量 \n\t\t键入2：统计托福成绩高于600分的学生并输出\n\t\t键入其他，返回选择命令行\n");
                printf("\t\t");
            scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                switch(RealSelectByOneAndTwo)
            {
                case 1://统计托福成绩低于60分学生的数量并输出
            AddUpNumOfScoreLower60();
            break;
                case 2://统计托福成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
                default:
                	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                    printf("\t\t第二次您又输入了错误的指令，请您细心一些，粗心不成事！\n\t\t系统将返回选择命令行\n");
                break;

            }
            break;
		    }
		    }
		    	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
            break;
        case 12://排序集合
            NumiStuScore = 0;
            kScore = 1;
            RealSelectBy = 0;
            kNum = 1;
            RealSelectByOneAndTwo = 0;
		    Num1 = 0;
            Num2 = 0;
            Num3 = 0;
            Num4 = 0;
            AgainCarryOut = 0;
            system("cls");
            if (JudgeIfRFight() == 1)//判断指令是否输入正确,如果 == 1 说明指令输入不正确
		    {
		        printf("\t\t指令输入不正确,请重新输入指令\n");//break一般只跳出一层大括号，进入上一层的下一句。
		        printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		        ShowOrder();
		    }else {
		        printf("\t\t键入1：按托福成绩由低到高对学生进行排序\n\t\t键入2：按托福成绩由高到低对学生进行排序\n\t\t键入其他错误指令，您还有一次输入机会\n");
		        printf("\t\t");
		        scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
            //    printf("RealSelectByOneAndTwo = %d\n",RealSelectByOneAndTwo);
            switch(RealSelectByOneAndTwo)
            {
                 case 1:
                RankStuByminNum();//升序排序学生
                break;
              case 2:
                 RankStuBymaxNum();//降序排序学生
                 break;
                default:
                    kNum = 1;
                    Num2 = 2;
                    RealSelectByOneAndTwo = 0;
                printf("\t\t您输入的不符合任何，您还有一次输入机会，如果再次输入错误指令，将返回选择命令行\n\t\t请输入指令：\n");
                printf("\t\t键入1：按成绩由低到高对学生进行排序 \n\t\t键入2：按成绩由高到低对学生进行排序\n\t\t键入其他，返回选择命令行\n");
                printf("\t\t");
            scanf("%s",SelectByOneAndTwo);
            getchar();
                for ( i = 0; i < strlen(SelectByOneAndTwo); i++ ){
                    InterSelectByOneAndTwo[i] = SelectByOneAndTwo[i] - 48;
                }
                for ( i = strlen(SelectByOneAndTwo)-1; i >= 0; i-- ){
                    RealSelectByOneAndTwo += InterSelectByOneAndTwo[i] * kNum;
                    kNum *= 10;
                }
                switch(RealSelectByOneAndTwo)
            {
                case 1://统计成绩低于60分学生的数量
            AddUpNumOfScoreLower60();
            break;
                case 2://统计成绩高于60分的学生并输出
            AddUpScoreHigher60();
            break;
                default:
                	printf("\t\t为您显示选择命令行：\n");
            	ShowOrder();
                printf("\t\t回到选择命令行，重新输入指令\n");
                    printf("\t\t第二次您又输入了错误的指令，请您细心一些，粗心不成事！\n\t\t系统将返回选择命令行\n");
                break;

            }
            	printf("\t\t该指令已经执行完毕\n");
		    	printf("\t\t键入任意键，下面为您显示选择命令行，方便进行下一个指令的输入\n");
		    	getchar();
		ShowOrder();
            break;
        }
		    }
    }
	}



    }

	//保存
	SaveStuToFile();
	//释放链表
	FreeLinkData();
	//system("pause");

    system("pause");
    }
//},这是账户信息正确 那里 的 while循环的右括号



   if (strcmp(useraccount, account) == 0 && strcmp(userpassword, password) == 0){




        puts("\t\t您已作为学生端用户登录学生管理系统,您只能行使查看学生信息的权限。\n");
        puts("\t\t以下为系统中所有学生的信息：\n");
        STUReadStuFromFile();
        system("pause");
    }else{
        puts("\t\t您输入的账号或密码不正确\n");
    }
}
else{
	printf("\t\t您输入的指令不正确！程序结束\n");
}
	return 0;
}
int JudgeIfRFight()//判断是否输入错误？？？
{
    getchar();
    int k;
    char judge[20];
    printf("\t\t是否输入错误?如果输入指令有误，请输入'n'。\n");//如果输入错误，直接break;
    int num = 0;
    printf("\t\t");
    scanf("%s",judge);
    if ( strlen(judge) != 1){
        k = 0;
        printf("\t\t既然指令输入正确，那就请继续执行\n");
            getchar();
        return k;//输入指令正确,继续执行
    }
    if ( judge[0] == 'n' ){
            k = 1;//指令输入不正确
                getchar();
            return k;
    }else{//输入指令正确
        printf("\t\t既然指令输入正确，那就请继续执行\n");
        k = 0;
    }
    getchar();
    return k;
}

//添加一个学生的信息
void AddStuMSG(char *arrStuNum, char arrStuName[10], char  iStuScore[100], char CScore[100], int SumScore) //函数定义
{
	//逻辑
	//创建一个节点
	STUNODE* pTemp = (STUNODE *)malloc(sizeof (STUNODE));
    int ScoreReal[100] = {0};
    int i;
    int kScor = 1;
    int RealSc = 0;
    int RealCScore = 0;
    //转化成整数
	for ( i = 0; i < strlen(iStuScore); i++ ){
		if ( iStuScore[i] >= 48 && iStuScore[i] <= 57 ){
			ScoreReal[i] = iStuScore[i]-48;
		}
	}
	for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
		RealSc += ScoreReal[i] * kScor;
		kScor *= 10;
	}
	kScor = 1;

	for ( i = 0; i < strlen(CScore); i++ ){
		if ( CScore[i] >= 48 && CScore[i] <= 57 ){
			ScoreReal[i] = CScore[i]-48;
		}
	}
	for ( i = strlen(CScore)-1; i >= 0; i-- ){
		RealCScore += ScoreReal[i] * kScor;
		kScor *= 10;
	}




	//第一步，检验参数的合法性
	if (NULL == arrStuNum || NULL == arrStuName || iStuScore < 0)
	{
		printf ("\t\t学生信息输入错误!\n");
		return ;
	}
	//节点成员符初始值
	strcpy(pTemp->arrStuNum, arrStuNum);
	strcpy(pTemp->arrStuName, arrStuName);
//	把 iStuScorechar类型 先转化为 int类型在赋值给 pTemp->iStuScore  因为pTemp->iStuScore 是int类型的

	pTemp->iStuScore = RealSc;
	pTemp->CScore = RealCScore;
	pTemp->SumScore = SumScore;
	pTemp->pNext = NULL;

	//接在链表上
	if (NULL == g_pHead || NULL == g_pEnd)
	{
		g_pHead = pTemp;
		//g_pEnd = pTemp;
	}
	else
	{
		g_pEnd->pNext = pTemp;  //链接
		//g_pEnd = pTemp;         //向后移动
	}
	g_pEnd = pTemp;
}


//清空链表
void FreeLinkData()
{
	STUNODE* pTemp = g_pHead;
	STUNODE * q = NULL;
	while (pTemp)
	{
		//记录节点
		q = pTemp;

		//向后移动了一个
		pTemp = pTemp->pNext;

		//删除节点
		free(q);
	}
}

//打印数据
void ShowStuData()
{
	STUNODE* pTemp = g_pHead;
	while (pTemp != NULL)
	{
		printf("\t\t学号：%-8s 姓名：%-10s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
		//向下走一步
		pTemp = pTemp->pNext;
	}
}

//显示指令
void ShowOrder()
{
	printf("\t\t***********您已进入学生信息管理系统——教师端*************\n");
	printf("\t\t**********首先为您显示系统内保存的学生历史信息**********\n");
	printf("\t\t*******************您拥有以下操作权限*******************\n");
	printf("\t\t***             1、 增加一个学生信息(尾添加)         ***\n");
//	printf("***            111、 增加一个学生信息(头添加)         ***\n");
	printf("\t\t***           11、 增加一个学生信息(在指定位置添加)  ***\n");
	printf("\t\t***             2、 查找指定学生的信息（姓名/学号）  ***\n");
	printf("\t\t***             3、 修改指定学生的信息               ***\n");
	printf("\t\t***             4、 保存业主的信息到文件中           ***\n");
//	printf("***             5、 按成绩由低到高对学生进行排序     ***\n");
	printf("\t\t***             6、 删除指定学生的信息               ***\n");
	printf("\t\t***             7、 读取文件中学生信息               ***\n");
//	printf("***             8、 按成绩由高到低对学生进行排序     ***\n");
	printf("\t\t***             8、 显示所有学生的信息               ***\n");
//	printf("***             12、 统计成绩高于60分的学生并输出    ***\n");
	printf("\t\t***             10、 查看指令                        ***\n");
//	printf("***             9、 通过姓名查找指定学生信息        ***\n");
	printf("\t\t***             14、 统计学生信息集合                ***\n");
	printf("\t\t***            12、 对学生进行排序集合               ***\n");
	printf("\t\t***             13、 退出系统                         ***\n");
	printf("\t\t********************************************************\n");
}


//查找制定学生
STUNODE* FindStuByNum(char* arrStuNum)  //200501013  1254
{
	STUNODE* pTemp = g_pHead;
	//检测参数的合法性
	if (NULL == arrStuNum)
	{
		printf ("学号输入错误！\n");
		return NULL;
	}

	//判断链表是否是空
	if (NULL == g_pHead || NULL == g_pEnd)
	{
		printf ("\t\t链表为NULL！\n");
		return NULL;
	}

	//遍历链表
	while(pTemp != NULL)
	{
		if (0 == strcmp(pTemp->arrStuNum, arrStuNum))
		{
			return pTemp;
		}
		pTemp = pTemp->pNext;
	}

	printf ("\t\t查无此节点！\n");
	return NULL;
}

//指定位置插入节点
void InsertNode(STUNODE* pTemp, char *arrStuNum, char arrStuName[10], char iStuScore[100], char CScore[100], int SumScore)
{
	int ScoreReal[100] = {0};
    int i;
    int kScor = 1;
    int RealSc = 0;
    int RealCScore = 0;
	//创建节点
	STUNODE* pNewTemp = (STUNODE *)malloc(sizeof(STUNODE));
	//转化成整数
	for ( i = 0; i < strlen(iStuScore); i++ ){
		if ( iStuScore[i] >= 48 && iStuScore[i] <= 57 ){
			ScoreReal[i] = iStuScore[i] - 48;
		}
	}
	for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
		RealSc += ScoreReal[i] * kScor;
		kScor *= 10;
	}
	kScor = 1;
	for ( i = 0; i < strlen(CScore); i++ ){
		if ( CScore[i] >= 48 && CScore[i] <= 57 ){
			ScoreReal[i] = CScore[i] - 48;
		}
	}
	for ( i = strlen(CScore)-1; i >= 0; i-- ){
		RealCScore += ScoreReal[i] * kScor;
		kScor *= 10;
	}



	//成员赋值
	strcpy(pNewTemp->arrStuNum, arrStuNum);
	strcpy(pNewTemp->arrStuName, arrStuName);
	pNewTemp->iStuScore = RealSc;
	pNewTemp->CScore = RealCScore;
	pNewTemp->SumScore = SumScore;
	pNewTemp->pNext = NULL;    ///


	//插入
	if (pTemp == g_pEnd)  //是尾节点
	{
		g_pEnd->pNext = pNewTemp;
		g_pEnd = pNewTemp;
	}
	else
	{
		//
		pNewTemp->pNext = pTemp->pNext;
		pTemp->pNext = pNewTemp;
	}
}

//删除指定学生
void DeleteStuNode(STUNODE* pNode)
{
	//只有一个节点
	if (g_pHead == g_pEnd)
	{
		free(g_pHead);
		g_pHead = NULL;
		g_pEnd = NULL;
	}
	//只有两个节点
	else if (g_pHead->pNext == g_pEnd)
	{
		if (g_pHead == pNode)
		{
			free(g_pHead);
			g_pHead = g_pEnd;
		}
		else
		{
			free(g_pEnd);
			g_pEnd = g_pHead;
			g_pHead->pNext = NULL;
		}
	}
	else // >=3
	{
		STUNODE* pTemp = g_pHead;
		//判断头
		if(g_pHead == pNode)
		{
			//记住头
			pTemp = g_pHead;
			g_pHead = g_pHead->pNext;
			free(pTemp);
			pTemp = NULL;
			return ;  //结束
		}

		while(pTemp)
		{
			if(pTemp->pNext == pNode)
			{
				//删除
				if (pNode == g_pEnd)
				{
					free(pNode);
					pNode = NULL;
					g_pEnd = pTemp;
					g_pEnd->pNext = NULL;
					return ;
				}
				else
				{
					//记住要删除的节点
					STUNODE* p = pTemp->pNext;
					//链接
					pTemp->pNext = pTemp->pNext->pNext;
					//释放节点
					free(p);
					p = NULL;
					return ;
				}
			}

			pTemp = pTemp->pNext;
		}
	}
}

//保存信息进文件
void SaveStuToFile()
{
	//判断链表是否是NULL
	FILE* pFile = NULL;
	STUNODE* pTemp = g_pHead;
	char strBuf[100] = {0};
//	char strScore[20] = {0};
//    char CScore[10] = {0};
 //   char SumScore[10] = {0};
	if (NULL == g_pHead)
	{
		printf("\t\t没有学生\n");
		return ;
	}

	//打开文件
	pFile = fopen("dat.dat", "wb+");
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return ;
	}
	//操作文件指针
	while(pTemp)
	{
	    char strScore[20] = {0};
        char CScore[20] = {0};
        char SumScore[20] = {0};
		//学号赋值进去
		strcpy(strBuf, pTemp->arrStuNum);
		strcat(strBuf, ".");
		//姓名
		strcat(strBuf, pTemp->arrStuName);
		strcat(strBuf, ".");
		//分数
		itoa(pTemp->iStuScore, strScore, 10);
		strcat(strBuf, strScore);
		strcat(strBuf, ".");
      //  strcat(strBuf, ".");
        itoa(pTemp->CScore, CScore, 10);
		strcat(strBuf, CScore);
		strcat(strBuf, ".");

		itoa(pTemp->SumScore, SumScore, 10);
		strcat(strBuf, SumScore);
		strcat(strBuf, ".");

		fwrite(strBuf, 1, strlen(strBuf), pFile); //
		fwrite("\r\n", 1, strlen("\r\n"), pFile);

		pTemp = pTemp->pNext;
	}

	//关闭文件
	fclose(pFile);
}

//读取文件中学生信息
void ReadStuFromFile()
{
	FILE* pFile = fopen("dat.dat", "rb+"); //

	char strBuf[200] = {0};
//	char strStuNum[10] = {0};
//	char strStuName[10] = {0};
//	char strStuScore[20] = {0};
	int nCount = 0;
	int j;
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return ;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, pFile))  //EOF  feof   3部分
	{
	    char strStuNum[10] = {0};
	    char strStuName[10] = {0};
	    char strStuScore[20] = {0};
	    char CScore[10] = {0};
       char SumScore[10] = {0};
       int NumiStuScore = 0;
       char iStuScore[10] = {0};
       int kScore = 1;
       int  InteriStuScore[20] = {0};
       int Score1 = 0;
       int Score2 = 0;
       int Score3 = 0;

		int i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[j] = strBuf[i];
				j++;
				if ('.' == strBuf[i])
				{
					strStuNum[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
			else if (1 == nCount) //第一个'.'
			{
				strStuName[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					strStuName[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}

			else if (2 == nCount) //第一个'.'
			{
				iStuScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					iStuScore[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}


			else if ( 3 == nCount )  //第二个'.' 2 == nCount
			{
				CScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					CScore[j-1] = '\0';
					nCount++;
					j = 0;
				}

			}
			else if ( 4 == nCount) {
                SumScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					SumScore[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
		}
		//这里存的有问题，SUnScore先转换为整数在存储！
		for ( i = 0; i < strlen(SumScore); i++ ){
                if ( 48 <=  SumScore[i] && SumScore[i] <= 57){
            InteriStuScore[i] = SumScore[i] - 48;
                }
		}
		for ( i = strlen(SumScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score3 = NumiStuScore;
		NumiStuScore = 0;
		kScore = 1;
		for ( i = 0; i < strlen(CScore); i++ ){
                if ( 48 <=  CScore[i] && CScore[i] <= 57){
            InteriStuScore[i] = CScore[i] - 48;
                }
		}
		for ( i = strlen(CScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score2 = NumiStuScore;

		NumiStuScore = 0;
		kScore = 1;
		for ( i = 0; i < strlen(iStuScore); i++ ){
                if ( 48 <=  iStuScore[i] && iStuScore[i] <= 57){
            InteriStuScore[i] = iStuScore[i] - 48;
                }
		}
		for ( i = strlen(iStuScore)-1; i >= 0; i-- ){
            NumiStuScore += InteriStuScore[i] * kScore;
            kScore *= 10;
		}
		Score1 = NumiStuScore;


		//插入到链表
		AddStuMSG(strStuNum, strStuName, iStuScore, CScore, Score3);
	//	printf("strlen(CScore) = %d strlen(strStuScore) = %d\n strlen(SumScore) = %d",strlen(CScore),strlen(iStuScore),strlen(SumScore));
		printf("\t\t学号:%-10s 姓名:%-12s 托福分数:%-4d 雅思分数:%-4d 平均分数:%-4d\n",strStuNum, strStuName, Score1, Score2, Score3);
	}

	fclose(pFile);
}
//通过学号升序排序学生
void RankStuByminNum()
{
    STUNODE * pTemp = g_pHead;
    STUNODE * tail = NULL;
  //  char temp1[20] = {0};
   // char temp2[20] = {0};
    int temp;
    int CScore = 0;
    int SumScore = 0;
    while ( pTemp != tail ){
            while ( pTemp->pNext != tail ){
                if ( pTemp->iStuScore > pTemp->pNext->iStuScore ){
                    char temp1[20] = {0};
                    char temp2[20] = {0};
                    temp = pTemp->pNext->iStuScore;
                    pTemp->pNext->iStuScore = pTemp->iStuScore;
                    pTemp->iStuScore = temp;

                    CScore = pTemp->pNext->CScore;
                    pTemp->pNext->CScore = pTemp->CScore;
                    pTemp->CScore = CScore;

                    SumScore = pTemp->pNext->SumScore;
                    pTemp->pNext->SumScore = pTemp->SumScore;
                    pTemp->SumScore = SumScore;

                strcpy(temp2, pTemp->pNext->arrStuNum);
                strcpy(pTemp->pNext->arrStuNum, pTemp->arrStuNum);
                strcpy(pTemp->arrStuNum, temp2);
                strcpy(temp1, pTemp->pNext->arrStuName);
                strcpy(pTemp->pNext->arrStuName, pTemp->arrStuName);
                strcpy(pTemp->arrStuName, temp1);
                }
                pTemp = pTemp->pNext;
            }
            tail = pTemp;
            pTemp = g_pHead;
    }
    ShowStuData();
}
void RankStuBymaxNum()
{
    STUNODE * pTemp = g_pHead;
    STUNODE * tail = NULL;
  //  char temp1[20] = {0};
   // char temp2[20] = {0};
    int temp;
    int CScore = 0;
    int SumScore = 0;
    while ( pTemp != tail ){
            while ( pTemp->pNext != tail ){
                if ( pTemp->iStuScore < pTemp->pNext->iStuScore ){
                    char temp1[20] = {0};
                    char temp2[20] = {0};
                    temp = pTemp->pNext->iStuScore;
                    pTemp->pNext->iStuScore = pTemp->iStuScore;
                    pTemp->iStuScore = temp;

                    CScore = pTemp->pNext->CScore;
                    pTemp->pNext->CScore = pTemp->CScore;
                    pTemp->CScore = CScore;

                    SumScore = pTemp->pNext->SumScore;
                    pTemp->pNext->SumScore = pTemp->SumScore;
                    pTemp->SumScore = SumScore;

                strcpy(temp2, pTemp->pNext->arrStuNum);
                strcpy(pTemp->pNext->arrStuNum, pTemp->arrStuNum);
                strcpy(pTemp->arrStuNum, temp2);
                strcpy(temp1, pTemp->pNext->arrStuName);
                strcpy(pTemp->pNext->arrStuName, pTemp->arrStuName);
                strcpy(pTemp->arrStuName, temp1);
                }
                pTemp = pTemp->pNext;
            }
            tail = pTemp;
            pTemp = g_pHead;
    }
    ShowStuData();
}
//统计托福成绩高于600分的学生并输出
void AddUpScoreHigher60()
{
    STUNODE * pTemp = g_pHead;
    while (pTemp){
        if ( pTemp->iStuScore > 600 ){
            printf("\t\t学号：%-8s 姓名：%-10s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
        }
        pTemp = pTemp->pNext;
    }
}
//统计成绩低于600分学生的数量并输出
void AddUpNumOfScoreLower60()
{
    STUNODE * pTemp = g_pHead;
    int num = 0;
    while (pTemp){
        if ( pTemp->iStuScore < 600 ){
                printf("\t\t学号：%-8s 姓名：%-10s 托福成绩：%-4d 雅思成绩：%-4d 平均成绩：%-4d\n",pTemp->arrStuNum,pTemp->arrStuName,pTemp->iStuScore, pTemp->CScore, pTemp->SumScore);
            num++;
        }
        pTemp = pTemp->pNext;
    }
    printf("\t\t托福成绩低于600分的学生一共有：%d人\n",num);
}
//通过姓名查找学生信息
STUNODE * FindMSGByName(char* arrStuName)
{
    STUNODE * pTemp = g_pHead;
    while (pTemp){
        if ( strcmp(pTemp->arrStuName, arrStuName) == 0 ){
            return pTemp;
        }
        pTemp = pTemp->pNext;
    }
    return NULL;
}
void STUReadStuFromFile()
{
	FILE* pFile = fopen("dat.dat", "rb+"); //

	char strBuf[200] = {0};

	char strStuNum[10] = {0};
	char strStuName[10] = {0};
	char strStuScore[20] = {0};
	int nCount = 0;
	int j = 0;
	if (NULL == pFile)
	{
		printf("\t\t文件打开失败\n");
		return ;
	}//操作指针，读取函数
	while( NULL !=  fgets(strBuf, 200, pFile))  //EOF  feof   3部分
	{
	    char strStuNum[10] = {0};
	    char strStuName[10] = {0};
	    char strStuScore[20] = {0};
	    char CScore[10] = {0};
       char SumScore[10] = {0};
		int i = 0;
		nCount = 0;
		j = 0;
		for (i = 0; strBuf[i] != '\r'; i++)
		{
			if(0 == nCount) //没到'.'
			{
				strStuNum[i] = strBuf[i];
				if ('.' == strBuf[i])
				{
					strStuNum[i] = '\0';
					nCount++;
				}
			}
			else if (1 == nCount) //第一个'.'
			{
				strStuName[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					strStuName[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
			else if ( 2 == nCount )  //第二个'.' 2 == nCount
			{
				CScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					CScore[j-1] = '\0';
					nCount++;
					j = 0;
				}

			}
			else if ( 3 == nCount) {
                SumScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					SumScore[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}



		}
		//插入到链表
		printf("\t\t学号:%-10s 姓名:%-12s 托福分数:%-4d 雅思分数:%-4d 平均分数:%-4d\n",strStuNum, strStuName, atoi(strStuScore), atoi(CScore), atoi(SumScore));
	}

	fclose(pFile);
}
void RankStuBymaxNum111()
{
    STUNODE * pTemp = g_pHead;
    STUNODE * tail = NULL;
    STUNODE * p1, *p2, *p3,*tem,*end;
    end = NULL;
    if ( g_pHead->next == NULL ){
        return 0;
    }
    if ( head->next->next==NULL ){
        return 0;
    }
  //  char temp1[20] = {0};
   // char temp2[20] = {0};
    int i;
    int CScore = 0;
    int SumScore = 0;
    while ( g_pHead->pNext != end ){
        for ( p1=g_pHead,p2=p1->pNext,p3=p2->pNext; p3 != end; p1=p1->pNext,p2=p2->pNext,p3=p3->pNext ){
            if ( p2->iStuScore < p3->iStuScore ){
                p1->pNext = p2->pNext;
                p2->pNext = p3->pNext;
                p3->pNext = p2;
                tem = p2;
                p2 = p3;
                p3 = tem;
            }
        }
        end = p2;
    }
    ShowStuData();
}


				strStuName[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					strStuName[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}
			else if ( 2 == nCount )  //第二个'.' 2 == nCount
			{
				CScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					CScore[j-1] = '\0';
					nCount++;
					j = 0;
				}

			}
			else if ( 3 == nCount) {
                SumScore[j] = strBuf[i];
				j++;//j++不能在这里！！！
				if ('.' == strBuf[i])
				{
					SumScore[j-1] = '\0';
					nCount++;
					j = 0;
				}
			}



		}
		//插入到链表
		printf("\t\t学号:%-10s 姓名:%-12s 托福分数:%-4d 雅思分数:%-4d 平均分数:%-4d\n",strStuNum, strStuName, atoi(strStuScore), atoi(CScore), atoi(SumScore));
	}

	fclose(pFile);
}
/*
void RankStuBymaxNum111()
{
    STUNODE * pTemp = g_pHead;
    STUNODE * tail = NULL;
    STUNODE * p1, *p2, *p3,*tem,*end;
    end = NULL;
    if ( g_pHead->next == NULL ){
        return 0;
    }
    if ( head->next->next==NULL ){
        return 0;
    }
  //  char temp1[20] = {0};
   // char temp2[20] = {0};
    int i;
    int CScore = 0;
    int SumScore = 0;
    while ( g_pHead->pNext != end ){
        for ( p1=g_pHead,p2=p1->pNext,p3=p2->pNext; p3 != end; p1=p1->pNext,p2=p2->pNext,p3=p3->pNext ){
            if ( p2->iStuScore < p3->iStuScore ){
                p1->pNext = p2->pNext;
                p2->pNext = p3->pNext;
                p3->pNext = p2;
                tem = p2;
                p2 = p3;
                p3 = tem;
            }
        }
        end = p2;
    }
    ShowStuData();
}*/
```
