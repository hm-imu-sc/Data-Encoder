#include<bits/stdc++.h>
#include<conio.h>
#include<windows.h>

using namespace std;

//struct Beeper{
//
//    private int x;
//
//    void selected_beep(){
//        Beep(1000,150);
//        Beep(1500,200);
//    }
//
//    void option_beep(){
//        Beep(1500,200);
//    }
//
//};
//
//Beeper beeper1;

vector< vector<string> > master_record;
string pUsers="files/user_files/";
string pBase="files/base_files/";
string pTemp="files/temp_files/";
vector< vector<string> > users;
vector< string > user_files;

map<char,int> charecters;
int current_user;

void initiate_charecters(){
    for(int i=0;i<=93;i++){
        charecters[33+i]=i;
    }

//    for(auto x:charecters){
//        cout<<x.first<<" "<<x.second<<endl;
//    }
}

int char_cat_chk(char c){
    if((charecters[c]>=0 && charecters[c]<=14) || (charecters[c]>=25 && charecters[c]<=31)){
        return 0;
    }
    if((charecters[c]>=58 && charecters[c]<=63) || (charecters[c]>=90 && charecters[c]<=93)){
        return 0;
    }
    if((charecters[c]>=15 && charecters[c]<=24)){
        return 1;
    }
    if((charecters[c]>=32 && charecters[c]<=57)){
        return 2;
    }
    if((charecters[c]>=64 && charecters[c]<=89)){
        return 3;
    }
}

void initiate_loader(){
    master_record.clear();
    ifstream read(pUsers+user_files[current_user]);
    string title,key,code;
    vector<string> str;
    str.push_back("Name");
    str.push_back("Key");
    str.push_back("Data");
    master_record.push_back(str);
    while(read>>title>>key){
        getline(read,code);
        getline(read,code);
        str.clear();
        str.push_back(title);
        str.push_back(key);
        str.push_back(code);
        master_record.push_back(str);
    }
    read.close();
}

void load_users(){
    ifstream is(pBase+"users.txt");
    ifstream is1(pBase+"user_file_names.txt");
    string name,key,pcode;
    while(is>>name){
        is>>key;
        getline(is,pcode);
        getline(is,pcode);
        vector<string> user;
        user.push_back(name);
        user.push_back(key);
        user.push_back(pcode);
        users.push_back(user);
    }
    while(is1>>name){
        user_files.push_back(name);
    }
    is.close();
    is1.close();
}

void save_updates(vector<vector<string> > data,string file,int start,string format){
    ofstream os(file);
    for(int i=start;i<data.size();i++){
        os<<data[i][0]<<format<<data[i][1]<<endl;
        os<<data[i][2]<<endl;
    }
    os.close();
}

void save_file_names(){
    ofstream os(pBase+"user_file_names.txt");
    for(int i=0;i<user_files.size();i++){
        os<<user_files[i]<<endl;
    }
    os.close();
}

int option_viewer_s(bool get,int control,int opt,vector<string> options,string title){
    cout<<title;
    int mx=0;
    for(int i=0;i<options.size();i++){
        if(options[i].size()>mx){
            mx=options[i].size();
        }
    }
    mx+=0;///floor(log10(options.size()));
    if(control==80){
        opt++;
    }
    else if(control==72){
        opt--;
    }
    if(opt<0){
        opt=options.size()-1;
    }
    else if(opt>=options.size()){
        opt=0;
    }

    printf("%c",201);
    int ex=5+floor(log10(options.size()));
    for(int i=0;i<mx+ex;i++)
        printf("%c",205);
    printf("%c\n",187);

    for(int i=0;i<options.size();i++){
        char a;
        (i==opt) ? a='>'/**175**/:a=' ';
        printf("%c%c%d. %s",186,a,i+1,options[i].c_str(),186);
        for(int j=0;j<(mx-options[i].size())+floor(log10(options.size()))-log10(i+1);j++){
            cout<<" ";
        }
        printf(" %c\n",186);
    }

    char op;

    if(get)
        op=203;
    else
        op=205;

    printf("%c%c",200,op);
    for(int i=0;i<mx+ex-1;i++)
        printf("%c",205);
    printf("%c\n",188);

    if(get){
        printf(" %c\n %c%c%c Select option : %d\n",186,211,196,175,opt+1);
        return opt;
    }
    else
        return -1;
}

int navigate_options(vector<string> options,string title){

    int control=72,opt=0;
    system("cls");
    option_viewer_s(true,77,opt,options,title);

    while(true){
        char c=getch();
        control=c;
        if(control==77 || control==13){
            break;
        }
        if(control==72 || control==80){
            system("cls");
            opt=option_viewer_s(true,control,opt,options,title);
//            beeper1.option_beep();
        }
    }

//    if(opt==0){
//        cout<<"Option number : ";
//        cin>>opt;
//        return opt;
//    }

    return opt+1;
}

void create_table(vector< vector<string> > data,string title){

    printf(" %c%c Title : %s\n",214,175,title.c_str());

    vector<int> maxs;

    maxs.assign(data[0].size(),0);

    for(int i=0;i<data[0].size();i++){
        for(int j=0;j<data.size();j++){
            if(data[j][i].size()>maxs[i]){
                maxs[i]=data[j][i].size();
            }
        }
    }

    int row_size=(3*maxs.size())+1;

    for(int i=0;i<maxs.size();i++){
        row_size+=maxs[i];
    }

    bool dt=false;

    int row=(2*data.size())+1;
    int d=0;

    for(int i=0;i<row;i++){
        int split;
        int s_i=1;
        int di=0;
        if(dt){
            split=0;
        }
        else{
            split=3+maxs[0];
        }
        for(int j=0;j<row_size;j++){
            if(dt){
                if(j==split){
                    printf("%c",186);
                    split+=(3+maxs[di]);
                    if(j==row_size-1){
                        cout<<endl;
                    }
                }
                else{
                    j+=(1+maxs[di]);
                    int spaces=2+(maxs[di]-data[d][di].size());
                    for(int k=0;k<spaces;k++){
                        if(k==1){
                            cout<<data[d][di++];
                        }
                        cout<<" ";
                    }
                }
            }
            else{
                if(j==0){
                    if(i==0){
                        printf("%c",201);
                    }
                    else if(i==row-1){
                        printf("%c",200);
                    }
                    else{
                        printf("%c",204);
                    }
                }
                else if(j==row_size-1){
                    if(i==0){
                        printf("%c\n",187);
                    }
                    else if(i==row-1){
                        printf("%c\n",188);
                    }
                    else{
                        printf("%c\n",185);
                    }
                }
                else if(j==split){
                    if(i==0){
                        printf("%c",203);
                    }
                    else if(i==row-1){
                        printf("%c",202);
                    }
                    else{
                        printf("%c",206);
                    }
                    split+=(3+maxs[s_i++]);
                }
                else if(j==1 && i==0){
                    printf("%c",202);
                }
                else{
                    printf("%c",205);
                }
            }
        }
        if(dt){
            d++;
            dt=false;
        }
        else{
            dt=true;
        }
    }
}

int get_time_code(string key=""){
    int h,m,s;
    if(key!=""){
        h=(key[0]-'0')*10;
        h+=(key[1]-'0');
        m=(key[2]-'0')*10;
        m+=(key[3]-'0');
        s=(key[4]-'0')*10;
        s+=(key[5]-'0');
        return (h*3600)+(m*60)+s;
    }
    srand(time(0));
    h=rand()%24;
    m=rand()%60;
    s=rand()%60;
    return (h*3600)+(m*60)+s;
}

int uname_validity(string uname){
    for(int i=0;i<users.size();i++){
        if(uname==users[i][0]){
            return i;
        }
    }
    for(int i=0;i<uname.size();i++){
        if(uname[i]==' '){
            return -1;
        }
    }
    return -2;
}

string get_pass(bool show_strength=false,bool masked=true,string ref_string=""){

    string pass="";
    string pass_mask="";
    string strength_criteria="";
    char c='\0';
    int strength_level=0,char_cat;;
    vector<string> strength_levels;
    string cursor;

    cursor.push_back(222);
//    cursor.push_back('<');
//    cursor.push_back(174);
//    cursor.push_back(180);

    strength_levels.push_back("unlocked");
    strength_levels.push_back("weak");
    strength_levels.push_back("average");
    strength_levels.push_back("above average");
    strength_levels.push_back("strong");

    system("cls");
    cout<<ref_string<<pass_mask<<cursor;
    if(show_strength){
        cout<<" Strength : "<<strength_levels[strength_level]<<endl;
    }
    else{
        cout<<endl;
    }

    while(true){
        c=getch();
        if(c==8 || c==127){
            if(pass.size()==0){
                continue;
            }
            bool decrese=true;
            char_cat=char_cat_chk(pass[pass.size()-1]);
            for(int i=0;i<pass.size()-1;i++){
                if(char_cat_chk(pass[i])==char_cat){
                    decrese=false;
                    break;
                }
            }
            if(decrese){
                strength_level--;
                for(int i=0;i<strength_criteria.size();i++){
                    if(strength_criteria[i]-'0'==char_cat){
                        strength_criteria.erase(strength_criteria.begin()+i);
                        break;
                    }
                }
            }
            pass.pop_back();
            pass_mask.pop_back();
            system("cls");
            cout<<ref_string<<pass_mask<<cursor;
            if(show_strength){
                cout<<" Strength : "<<strength_levels[strength_level]<<endl;
            }
            else{
                cout<<endl;
            }
            continue;
        }
        if(c==13){
            break;
        }

        char_cat=char_cat_chk(c);

        bool skip=false;
        for(int i=0;i<strength_criteria.size();i++){
            if(strength_criteria[i]-'0'==char_cat){
                skip=true;
                break;
            }
        }

        if(!skip){
            strength_level++;
            strength_criteria+=('0'+char_cat);
        }

        if(masked){
            pass_mask+="*";
        }
        else{
            pass_mask+=c;
        }

        pass+=c;
        system("cls");
        cout<<ref_string<<pass_mask<<cursor;
        if(show_strength){
            cout<<" Strength : "<<strength_levels[strength_level]<<endl;
        }
        else{
            cout<<endl;
        }
    }

    return pass;
}

void show_codes(){
    create_table(master_record,"All Codes of you");
}

string decrypt(string data,string key){

    int time=get_time_code(key)+data.size()-1;

    for(int i=data.size()-1;i>=0;i--,time--){
        if(data[i]==' '){
            continue;
        }
        if(time%94>charecters[data[i]]){
            data[i]=(94-(time%94))+charecters[data[i]]+33;
        }
        else{
            data[i]=33+charecters[data[i]]-(time%94);
        }
    }

    return data;
}

pair<string,string> encrypt(string data){

    ofstream test(pTemp+"test.txt");

    int time=get_time_code();

    if(time/3600<10){
        test<<"0";
    }
    test<<time/3600;
    if((time%3600)/60<10){
        test<<"0";
    }
    test<<(time%3600)/60;
    if(time%60<10){
        test<<"0";
    }
    test<<time%60<<endl;
    test.close();

    ifstream test1(pTemp+"test.txt");
    string key;
    test1>>key;
    test1.close();

    for(int i=0;i<data.size();i++,time++){
        if(data[i]==' '){
            continue;
        }
        data[i]=33+((charecters[data[i]]+time)%94);
    }
    return make_pair(data,key);
}

void initiate_removal(){
    while(true){
        system("cls");
//        cout<<"\nErase Code >\n"<<endl;
//        create_table(master_record,"Codes");
        vector<string> options;
        for(int i=1;i<master_record.size();i++){
            options.push_back(master_record[i][0]);
        }
        options.push_back("back");
        int to_delete=navigate_options(options,"\n Erase Code >\n\n [+] Select to erase >\n");

        if(to_delete==options.size()){
            return;
        }

        options.clear();

        options.push_back("Yes");
        options.push_back("No");

        system("cls");
//        cout<<"\nErase Code >\n"<<endl;
//        create_table(master_record,"Codes");

        int conf=navigate_options(options,"\n Erase Code >\n\n Are you sure to erase \""+master_record[to_delete][0]+"\" ?\n");

        if(conf==1){
            master_record.erase(master_record.begin()+to_delete);
            save_updates(master_record,pUsers+user_files[current_user],1," ");
        }
    }
}

void change_user(){
    string uname,pass,temp=users[current_user][0],r_string;
    users[current_user][0]="";
    int chk;

    cout<<" New username\t  : ";
    getline(cin,uname);
    chk=uname_validity(uname);
    if(chk>=0){
        cout<<"\n [!] Username \""+uname+"\" is not available !!!\n\n\n ";
        system("pause");
        uname="";
        users[current_user][0]=temp;
        return;
    }
    else if(chk==-1){
        cout<<"\n [!] Username can't contain spaces !!!\n\n\n ";
        system("pause");
        uname="";
        users[current_user][0]=temp;
        return;
    }

    r_string="\n [-] Change Username > \n\n New username\t  : "+uname+"\n Current password : ";
    cout<<" Current password : ";
    pass=get_pass(false,true,r_string);

    if(pass==decrypt(users[current_user][2],users[current_user][1])){

        users[current_user][0]=uname;

        string nfn=uname+".txt";
        string o=pUsers+user_files[current_user];
        string n=pUsers+nfn;
        rename(o.c_str(),n.c_str()); /*********here********/
        user_files[current_user]=nfn;

        save_file_names();
        save_updates(master_record,pUsers+user_files[current_user],1," ");
        save_updates(users,pBase+"users.txt",0,"\n");

        cout<<"\n\n Username changed successfully !!!\n"<<endl;
        cout<<" ";
        system("pause");
    }
    else{
        cout<<"\n\n [!] Username did not changed !!!, the password is incorrect !!!\n"<<endl;
        cout<<" ";
        system("pause");
        users[current_user][0]=temp;
        return;
    }
}

void change_pass(){
    string n_pass,cn_pass,s_pass,pass,user,key,r_string,mask="";

    r_string="\n [-] Change Password > \n\n Current password\t: ";
    cout<<" Current password\t: ";
    pass=get_pass(false,true,r_string);

    for(int i=0;i<pass.size();i++){mask+="*";}

    r_string+=(mask+"\n\n New password\t\t: ");
    cout<<"\n\n New password\t\t: ";
    n_pass=get_pass(true,false,r_string);

    r_string+=(n_pass+"\n Confirm new password\t: ");
    cout<<" Confirm new password\t: ";
    cn_pass=get_pass(false,true,r_string);

    if(pass==decrypt(users[current_user][2],users[current_user][1]) && n_pass==cn_pass){
        pair<string,string> raw=encrypt(n_pass);
        users[current_user][2]=raw.first;
        users[current_user][1]=raw.second;
        save_updates(users,pBase+"users.txt",0,"\n");
        cout<<"\n Password changed successfully !!!\n"<<endl;
        cout<<" ";
        system("pause");
    }
    else{
        if(pass!=decrypt(users[current_user][2],users[current_user][1])){
            cout<<"\n [!] Password is incorrect !!!\n"<<endl;
        }
        else{
            cout<<"\n [!] New password didn't match !!!\n"<<endl;
        }
        cout<<" ";
        system("pause");
    }
}

bool get_authorization(){

    string uname,pcode,pass,key,r_string;

    cout<<" Username : ";
    cin>>uname;

    int user=uname_validity(uname);

    if(user<0){
        cout<<"\n [!] User not found !!!\n\n\n ";
        system("pause");
        return false;
    }

    r_string="\n [-] Sign In > \n\n Username : "+uname+"\n Password : ";
    cout<<" Password : ";
    pass=get_pass(false,true,r_string);

    if(pass==decrypt(users[user][2],users[user][1])){
        current_user=user;
        return true;
    }
    else{
        cout<<"\n [!] Wrong password !!!\n\n\n ";
        getline(cin,pass);
        system("pause");
        return false;
    }
}

void initiate_sign_up(string title="Sign Up"){
    string uname="",pass,cpass,r_string;
    pair<string,string> enc;
    int chk;
    while(true){
        system("cls");
        cout<<"\n [-] "<<title<<" > \n"<<endl;
        cout<<" Username\t  : ";
        if(uname==""){
            getline(cin,uname);
            chk=uname_validity(uname);
            if(chk>=0){
                cout<<"\n [!] Username \""+uname+"\" is not available !!!\n\n\n ";
                system("pause");
                uname="";
                continue;
            }
            else if(chk==-1){
                cout<<"\n [!] Username can't contain spaces !!!\n\n\n ";
                system("pause");
                uname="";
                continue;
            }
        }
        else{
            cout<<uname<<endl;
        }
        r_string="\n [-] "+title+" > \n\n Username\t  : "+uname+"\n\n Password\t  : ";
        cout<<"\n Password\t  : ";
        pass=get_pass(true,false,r_string);
        r_string+=(pass+"\n Confirm password : ");
        cout<<" Confirm password : ";
        cpass=get_pass(false,true,r_string);

        if(pass!=cpass){
            cout<<"\n [!] Password didn't match !!!\n\n\n ";
            system("pause");
            continue;
        }
        enc=encrypt(pass);
        vector<string> user;

        user.push_back(uname);
        user.push_back(enc.second);
        user.push_back(enc.first);
        users.push_back(user);

        save_updates(users,pBase+"users.txt",0,"\n");
        ofstream os(pUsers+uname+".txt");
        os.close();

        user_files.push_back(uname+".txt");
        save_file_names();

        cout<<"\n Registration successful !!!\n\n\n ";
        system("pause");
        break;
    }
}

/*******************/

int primary_options(){
    vector<string> options;
    options.push_back("Encrypt");
    options.push_back("Decrypt");
    options.push_back("Erase Code");
    options.push_back("View Codes");
    options.push_back("Change Login Information");
    options.push_back("Sign Out");
    options.push_back("Sign Out & Exit");
    return navigate_options(options,"\n [+] Main Menu\n");
}

int main_menu(){
    vector<string> options;
    options.push_back("Sign In");
    options.push_back("Sign Up");
    options.push_back("Exit");
    return navigate_options(options,"\n [+] Sign In\n");
}

int change_log_ops(){
    vector<string> options;
    options.push_back("Change username");
    options.push_back("Change password");
    options.push_back("Destroy my account");
    options.push_back("Back");
    return navigate_options(options,"\n [+] Change Logins\n");
}

int decrypt_options(){
    vector<string> options;
    options.push_back("Manual decrypt");
    options.push_back("Auto decrypt");
    options.push_back("Back");
    return navigate_options(options,"\n [+] Decrypt\n");
}

/*******************/

void test(){

//    beeper1.x = 10;

    string pass,pass_p;

    pass_p="\n Enter password > \n\n Password\t: ";

    pass=get_pass(true,false,pass_p);

    cout<<pass<<endl;

    return;
}

int main(){

    system("title Data Encrypter");

    initiate_charecters();

//    test();
//    return 0;

    load_users();

    int choice=-1;
    string data,key,title;
    vector<string> options;

    while(true){
        choice=main_menu();
        switch(choice){
        case 1: /// Login
            system("cls");
            printf("\n [-] Sign In > \n\n");
            if(get_authorization()){
                initiate_loader();
                getline(cin,data);
                bool brk=false;
                while(!brk){
                    pair<string,string> raw;
                    choice=primary_options();
                    switch(choice){
                    case 1: /// encrypt
                        system("cls");
                        cout<<"\n [-] Encrypt Data > "<<endl;
                        cout<<"\n Data : ";
                        getline(cin,data);cout<<endl;

                        raw=encrypt(data);

                        cout<<" Decryption KEY : "<<raw.second<<" (Sensitive information, DON'T SHARE)\n"<<endl;;

                        cout<<" Code : "<<raw.first<<"\n"<<endl;

                        cout<<" ";
                        system("pause");

                        options.clear();
                        options.push_back("Yes");
                        options.push_back("No");
                        choice=navigate_options(options,"\n [+] Save ?\n");

                        switch(choice){
                        case 1:/// save yes
                            cout<<" Title : ";
                            cin>>title;
//                            cout<<"key : "<<key<<endl;
//                            system("pause");

                            options.clear();
                            options.push_back(title);
                            options.push_back(raw.second);
                            options.push_back(raw.first);
                            master_record.push_back(options);
                            save_updates(master_record,pUsers+user_files[current_user],1," ");
                            cout<<" Code saved..."<<endl;
                            cout<<" ";
                            system("pause");
                            getline(cin,data);
                            break;
                        case 2:/// save no
                            break;
                        }
                        break;
                    case 2:/// decrypt
                        choice=-1;
                        while(choice!=3){
                            choice=decrypt_options();
                            switch(choice){
                            case 1:/// manual decrypt
                                system("cls");
                                cout<<"\n [-] Manual decrypt > "<<endl;
                                cout<<"\n Codes : ";
                                getline(cin,data);
                                cout<<endl;

                                cout<<" Key : ";
                                cin>>key;
                                cout<<endl;

                                cout<<" Data : "<<decrypt(data,key)<<"\n"<<endl;
                                cout<<" ";
                                system("pause");

                                getline(cin,data);
                                break;
                            case 2:/// auto decrypt
                                while(true){
                                    options.clear();
                                    for(int i=1;i<master_record.size();i++){
                                        options.push_back(master_record[i][0]);
                                    }
                                    options.push_back("back");
                                    int to_decrypt=navigate_options(options,"\n [-] Auto decrypt > \n\n\n [-] Select to decrypt >\n");

                                    if(to_decrypt==options.size()){
                                        break;
                                    }
                                    data=master_record[to_decrypt][2];
                                    key=master_record[to_decrypt][1];

                                    system("cls");
                                    cout<<"\n [-] Auto decrypt > \n\n ";
                                    cout<<options[to_decrypt-1]<<" : "<<decrypt(data,key)<<"\n"<<endl;

                                    cout<<" ";
                                    system("pause");
                                }
                                break;
                            case 3:/// back
                                break;
                            }
                        }

                        break;
                    case 3:/// erase code
                        initiate_removal();
                        break;
                    case 4:
                        system("cls");
                        cout<<endl;
                        show_codes();
                        cout<<" ";
                        system("pause");
            //            getline(cin,data);
                        break;
                    case 5:/// change login information
                        choice=-1;
                        while(choice!=4){
                            choice=change_log_ops();
                            switch(choice){
                            case 1: /// change username
                                system("cls");
                                printf("\n [-] Change Username > \n\n");
                                change_user();
                                break;
                            case 2:/// change password
                                system("cls");
                                printf("\n [-] Change Password > \n\n");
                                change_pass();
                                break;
                            case 3: /// delete account
                                srand(time(0));
                                data="";
                                for(int i=6;i--;){
                                    data+=('A'+rand()%26);
                                }
                                system("cls");
                                cout<<"\n [-] Discard account > \n\n [#] Caution: Your account is going to be destroyed . . ."<<endl;
                                cout<<"\n [#] Enter \""<<data<<"\" for confirmation : ";
                                cin>>key;
                                getline(cin,title);
                                if(data==key){
                                    users.erase(users.begin()+current_user+1);
                                    string t=pUsers+user_files[current_user];
                                    remove(t.c_str());
                                    user_files.erase(user_files.begin()+current_user+1);
                                    save_file_names();
                                    save_updates(users,pBase+"users.txt",0,"\n");
                                    cout<<"\n [#] ACCOUNT REMOVED SUCCESSFULLY.\n\n ";
                                    system("pause");
                                    choice=4;
                                    brk=true;
                                    break;
                                }
                                cout<<"\n [!] Confirmation failed  !!!\n\n ";
                                system("pause");

                                break;
                            case 4: /// back
                                break;
                            }
                        }
                        break;
                    case 6: /// logout
                        brk=true;
                        break;
                    case 7:/// logout & exit
                        return 0;
                    }
                }
            }
            break;
        case 2:/// sign up
            initiate_sign_up();
            break;
        case 3: /// exit
            return 0;
        }
    }
    return 0;
}
/// main
