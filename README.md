## Inter Process Communication
~~~c
#include<stdlib.h>
#include<stdio.h>
#include<string.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
int main()
{
int fd[10],child,len;
char a[20],b[20];
scanf("%s",a);
len=strlen(a);
pipe(fd);
child=fork();
if(!child)
{
close(fd[0]);
write(fd[1],a,len);
wait(0);
}
else
{
close(fd[1]);
read(fd[0],b,len);
printf("string recieved from pipe is : %s",b);
}
return 0;
}
~~~
## Integer file style
~~~c

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<sys/stat.h>
#include<fcntl.h>
int main()
{
int f1,f2,i=0;
char c,str[100],b[20];
f1=open("data",O_RDWR|O_CREAT|O_TRUNC
);
fgets(str,100,stdin);
i=strlen(str);
write(f1,str,i);
close(f1);
f2=open("data",O_RDONLY);
read(f2,b,i);
b[i]='\0';
printf("\n%s\n",b);
close(f2);
}
~~~
## scan 
~~~c
#include<stdio.h>
int main()
{
int n,i,j,head,c,tot;
printf("enter request no: ");
scanf("%d",&n);
int req[n+1];
printf("enter request sequence: ");
for(i=0;i<n;i++)
{
scanf("%d",&req[i]);
}
printf("enter initial head pos: ");
scanf("%d",&head);
printf("enter total disk size: ");
scanf("%d",&tot);
req[n]=head;
for(i=0;i<n+1;i++)
{
for(j=0;j<n;j++)
{
if(req[j+1]<req[j])
{
int temp=req[j];
req[j]=req[j+1];
req[j+1]=temp;
}
}
}
printf("enter direction(forward-1/backward-0:) ");
scanf("%d",&c);
if(c==0)
{
printf("Total head Movement: %d",head+req[n]);
}
else
{
printf("Total head Movement: %d",(tot-head)+(tot-req[0]));
}
~~~
## look 
~~~c 
#include<stdio.h>
int main()
{
int n,i,j,head,c,tot;
printf("enter request no: ");
scanf("%d",&n);
int req[n+1];
printf("enter request sequence: ");
for(i=0;i<n;i++)
{
scanf("%d",&req[i]);
}
printf("enter initial head pos: ");
scanf("%d",&head);
req[n]=head;
for(i=0;i<n+1;i++)
{
for(j=0;j<n;j++)
{
if(req[j+1]<req[j])
{
int temp=req[j];
req[j]=req[j+1];
req[j+1]=temp;
}
}
}
printf("enter direction(forward-1/backward-0:) ");
scanf("%d",&c);
if(c==0)
{
printf("Total head Movement: %d",(head-req[0])+(req[n]-req[0]));
}
else
{
printf("Total head Movement: %d",(req[n]-head)+(req[n]-req[0]));
}
}
~~~
## FCFS 
~~~c
#include<stdio.h>
int main()
{
int n,i,j,head,c,tot,thm=0;
printf("enter request no: ");
scanf("%d",&n);
int req[n];
printf("enter request sequence: ");
for(i=0;i<n;i++)
{
scanf("%d",&req[i]);
}
printf("enter initial head pos: ");
scanf("%d",&head);
for(i=0;i<n;i++)
{
thm+=abs(req[i]-head);
head=req[i];
}
printf("Total head Movement: %d",thm);
}
~~~
