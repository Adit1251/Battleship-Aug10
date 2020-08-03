# Battleship-Aug10

/* 
Algorithm:
1.Create initial grid
2.Design grid
3.Initiate tank positions(5)
4.Initiate mine positions(3)
5.Take in hitting co-ordinates
6.Count score:
  *Add 50 for each tank hit
  *Subtract 30 for each mine hit
  *hit all mines, u're out of the game
  *+30 bonus point for hitting two tanks in a row
  *-20 for hitting two mines in a row
  *disquaification for hitting a missile out of hostile compoun
*/

  #include <iostream>
  #include <algorithm>
  #include <string>
  #include <cstring>
  
  using namespace std;
  
  int main(void) {
    char grid[6][6];
    int i,j;
    char ch='a';
    char CH='A';
    char con_ch;
    int Missile_count;
    int game_score=0;
    int tank_streak;
    int miss_streak;
    
    //***************
    /*grid design*/
    grid[0][0]='o';
    
    for(i=0,j=1;j<6;j++){
    grid[i][j]=ch;
    ch++; 
    }
    
    for(i=1,j=0;i<6;i++){
    grid[i][j]=CH;
    CH++;
    }
    
    for(i=1;i<6;i++){
    for(j=1;j<6;j++){
    grid[i][j]='-';
    }
    }
    
    //initial grid output:*****
    for(i=0;i<6;i++){
    for(j=0;j<6;j++){
    cout<<grid[i][j]<<" ";
    }
    cout<<endl;
    }
    
    //**************************
    //co-ordinating tank and missile positions
    int tank1r,tank2r,tank3r,tank4r,tank5r;
    int tank1c,tank2c,tank3c,tank4c,tank5c;
    
    int min1r,min2r,min3r;
    int min1c,min2c,min3c;
    
    int ml_row,ml_col;
    
    int tank_hit_count=0;
    int mine_hit_count=0;
    int miss_count=0;
    
    
    //**************************
    tank1r=1;tank2r=2;tank3r=3;tank4r=4;tank5r=5;
    
    srand((unsigned)time(0));
    
    tank1c=rand()%5+1;
    tank2c=rand()%5+1;
    tank3c=rand()%5+1;
    tank4c=rand()%5+1;
    tank5c=rand()%5+1;
    
    
    //*************
    min1r=2;min2r=4;min3r=5;
    
    do{
    min1c=rand()%5+1;
    }while(min1c==tank2c);
    
    do{
    min2c=rand()%5+1;
    }while(min2c==tank4c);
    
     
    do{
    min3c=rand()%5+1;
    }while(min3c==tank5c);

    
    //***************
    //Attack code
    do{
    
        
    //*****************
    //Taking co-ordinate input.
    cout<<"Enter co-ordinate to launch a missile: "<<endl;
    cout<<"Enter row sequence: ";
    cin>>ml_row;
    cout<<endl;
    cout<<"Enter column sequence: ";
    cin>>ml_col;
    
    
    if(ml_row<1 || ml_row>5){
    cout<<"Missile target is out of hostile compound, you are disqualified as a dangerous missileman"<<endl;
    return -1;
    }
    
    if(ml_col<0 || ml_col>5){
    cout<<"Missile target is out of hostile compound, you are disqualified as a dangerous missileman"<<endl;
    return -1;
    }
    
    //******General hitting codes******
    
    //Roughing out prevs
    if(grid[ml_row][ml_col]=='$'){
    cout<<"You have already tried this co-ordinate, it was a hit."<<endl;
    tank_hit_count--;
    }
    
    if(grid[ml_row][ml_col]=='x'){
    cout<<"You have already tried this co-ordinate, it was a miss."<<endl;
    miss_count--;
    }
    
    if(grid[ml_row][ml_col]=='*'){
    cout<<"You have already tried this co-ordinate, it was a mine-spot."<<endl;
    mine_hit_count--;
    miss_count--;
    }
    
    //Initiate altering gridmap
    grid[ml_row][ml_col]='x';
    miss_count++;
    tank_streak=0;
    miss_streak++;
    if(miss_streak==10){
    cout<<"Oh! No, it's a 10 streak miss!"<<endl;
    game_score-=20;    
    
    //*******Tank hitting codes****
    if(ml_row==1 && ml_col==tank1c){
    if(tank_streak==1){
    cout<<"It's a streak hit!!!"<<endl;
    game_score+=50;
    }
    tank_hit_count++;
    miss_count--;
    grid[1][tank1c]='$';
    game_score+=50;
    tank_streak=1;
    miss_streak--;
    }
    
    if(ml_row==2 && ml_col==tank2c){
    if(tank_streak==1){
    cout<<"It's a streak hit!!!"<<endl;
    game_score+=50;
    }
    tank_hit_count++;
    miss_count--;
    grid[2][tank2c]='$';
    game_score+=50;
    tank_streak=1;
    miss_streak--;
    }
    
    if(ml_row==3 && ml_col==tank3c){
    if(tank_streak==1){
    cout<<"It's a streak hit!!!"<<endl;
    game_score+=50;
    }
    tank_hit_count++;
    miss_count--;
    grid[3][tank3c]='$';
    game_score+=50;
    tank_streak=1;
    miss_streak--;
    }
    
    if(ml_row==4 && ml_col==tank4c){
    if(tank_streak==1){
    cout<<"It's a streak hit!!!"<<endl;
    game_score+=50;
    }
    tank_hit_count++;
    miss_count--;
    grid[4][tank4c]='$';
    game_score+=50;
    tank_streak=1;
    miss_streak--;
    }
    
    if(ml_row==5 && ml_col==tank5c){
    if(tank_streak==1){
    cout<<"It's a streak hit!!!"<<endl;
    game_score+=50;
    }
    tank_hit_count++;
    miss_count--;
    grid[5][tank5c]='$';
    game_score+=50;
    tank_streak=1;
    miss_streak--;
    }
    
    //****mine hitting codes*****
    if(ml_row==2 && ml_col==min1c){
    mine_hit_count++;
    grid[2][min1c]='*';
    game_score-=30;
    }
    
    if(ml_row==4 && ml_col==min2c){
    mine_hit_count++;
    grid[4][min2c]='*';
    game_score-=30;
    }
    
    if(ml_row==5 && ml_col==min3c){
    mine_hit_count++;
    grid[5][min3c]='*';
    game-score-=30;
    }
    
    //tank hitting outputs********
    //TODO
    if(tank_hit_count==1){}
    if(tank_hit_count==2){}
    if(tank_hit_count==3){}
    if(tank_hit_count==4){}
    if(tank_hit_count==5){}
    
    
    //**mine hittin' output********
    //TODO
    if(mine_hit_count==1){}
    if(mine_hit_count==2){}
    if(mine_hit_count==3){}
    
    //Attack track
    for(i=0;i<6;i++){
    for(j=0;j<6;j++){
    cout<<grid[i][j]<<" ";
    }
    cout<<endl;
    }
    
    Missile_count++;
    
    cout<<"Tank hit count: "<<tank_hit_count<<endl;
    cout<<"Mine hit count: "<<mine_hit_count<<endl;
    cout<<"Miss count: "<<miss_count<<endl;
    cout<<"Number of missiles used: "<<Missile_count<<endl;
    
    cout<<"Press y to continue and n to exit: ";
    cin>>con_ch;

    }while(con_ch=='y');
    
    
    }
  
