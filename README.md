# maze-
c언어 자료구조이용한 미로문제
#c
#include <string.h>
#define SIZE 6
#define TRUE 1
#define FALSE 0 
typedef struct{
	short r;
	short c;
}element;
element here={1,0},endtry={1,0};
typedef struct{
	element stack[SIZE];
	int hight;
}StackType;
char maze[SIZE][SIZE]={{'1','1','1','1','1','1'},{'e','0','1','0','0','1'},{'1','0','0','0','1','1'},
{'1','0','1','0','1','1'},{'1','0','1','0','0','x'},{'1','1','1','1','1','1'}};

void pushloc(StackType *s,int r,int c){
	if(r<0||c<0){
	  return;}
	if(maze[r][c]!='1'&&maze[r][c]!='.'){
		element tmp;
		tmp.r=r;
		tmp.c=c;
		push(s,tmp);
	}
}
void mazeprint(char maze[SIZE][SIZE]){
	printf("\n");
	int r,c;
	for(r=0;r<SIZE;r++){
		for(c=0;c<SIZE;c++){
			printf("%c",maze[r][c]);}
		printf("\n");}
}
void init_stack(StackType *s){
	s->hight=-1;
}
int is_empty(StackType *s){
	return (s->hight==-1);
}
int is_full(StackType *s){
	return (s->hight==100-1);
}
void push(StackType *s,element t){
	if(is_full(s)){
		fprintf(stderr,"오류");
		exit(1);
	}
	else{
		s->stack[++(s->hight)]=t;
	}
}
element pop(StackType *s){
	if(is_empty(s)){
		fprintf(stderr,"오류");
		exit(1);
	}
	else{
		return s->stack[(s->hight)--];
	}
}
int main(){
	int r,c;
	StackType s;
	init_stack(&s);
	here=endtry;
	while(maze[here.r][here.c]!='x'){
		r=here.r;
		c=here.c;
		maze[r][c]='.';
		mazeprint(maze);
		pushloc(&s,r-1,c);
		pushloc(&s,r+1,c);
		pushloc(&s,r,c-1);
		pushloc(&s,r,c+1);
	if(is_empty(&s)){
		printf("실패");
		return; 
	}
	else here=pop(&s);}
	printf("성공");
	return 0; 
}


