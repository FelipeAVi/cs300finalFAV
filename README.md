# cs300finalFAV
//============================================================================
// Name        : Final Project.cpp
// Author      : Felipe A Villegas
// Version     : 1.0
// Copyright   : Copyright © 2017 SNHU COCE
// Description : Hello World in C++, Ansi-style
//============================================================================

#include <iostream>
#include <fstream>
#include <Windows.h>
#include <Mac.h>
#include <string>
#include <time.h>
#include <vector>

using namespace std;

const int GLOBAL_SLEEP_TIME = 5000; // this is a default timer for sleeping or the system to sleep after the time of 5000 hours has gone past

struct Course {
    string courseID;
    string courseName;
    vector<string> preList;
};                                  // this  section of code will keep a hold on the course info for us

class BinarySearchTree {
    Private:
    struct node {
        course Course;
        Node * right;
        Node * left; //this part is a default constructor

        Node() {
            left = nullptr;
            right = nullptr; 
        }
        Node (Course aCourse) { // this part is to initialize with the courses on file
            course = aCourse;
            left = nullptr;
            right = nullptr;
        }
    };
    Node * root;
    void inOrder(Node * node);
    int size = 0;
public:
BinarySearchTree();
void Inorder();
void Insert(Course aCourse);
void Remove(string courseID);
Course Search(string courseID);
int Size();
}; //this si the default constructor

BinarySearchTree::BinarySearchTree(){
    this->root = nullptr;
}

void BinarySearchTree::Inorder(){ // to move throught the tree in order
    inOrder(root);
}

void BinarySearchTree::Insert(Course aCourse){ // add a course or insert a course added to the school requirements
    Node * currentNode = root;
    if (root == NULL){
        root = new Node(aCourse);
    }
    else{
        while (currentNode != NULL){
            if(aCourse.courseID<currentNode->course.courseID){
                if(currentNode->left == nullptr){
                    currentNode->left = new Node(aCourse);
                    currentNode = NULL;
                }
                else{
                    currentNode = currentNode->left;
                }
            }
            else{
                if(currentNode->right == nullptr){
                    currentNode->right = new Node(aCourse);
                    currentNode = NULL;
                }
                else{
                    currentNode = currentNode->right;
                }
            }
        }
        size++;
    }
}

void BianrySearchTree::Remove(string courseID){   // This part is to remove a course 
    Node * par = NULL;
    Node * curr = root;
    while (curr != Null){
        if(curr->course.courseID == courseID){
            if(curr->left == NULL && curr->right == NULL){
                if(par == NULL){
                    root = nullptr;
                }
                else if (par->left == curr){
                    par->left = NULL;
                }
                else{
                    par->right = NULL;
                }
            }
            else if (curr->right == NULL){
                if (par == NULL){
                    root = curr->left;
                }
                else if (par->left == curr){
                    par->left = curr->left;
                }
                else{
                    par->right = curr->left;
                }
            }
            else if (curr->left == NULL){
                if (par == NULL){
                    root = curr->right;
                }
                else if (par->left == curr){
                    par->left = curr->right;
                }
                else{
                    par->right = curr->right;
                }
            }
            else {
                Node * suc = curr->right;
                while (suc->left != NULL){
                    suc = suc->left;
                }
                Node successorData = Node(suc->course);
                Remove(suc->course.courseID);
                curr->course = successorData.course;
            }
            return; // this is to remove the Node when found and to be removed
        }
        else if (curr->course.courseID<courseID){
            par = curr;
            curr = curr->right;
        }
    }
    cout << "\nValue not found" <<endl;
    return;
}
Course BinarySearchTree::Search(string courseID){
    Course aCourse;
    Node * currentNode = root;
    while(currentNode != NULL){
        if(currentNode->course.courseID == courseID){
            return currentNode->course;
        }
        else if (courseID < currentNode->course.courseID){
            currentNode = currentNode->left;
        }
        else{
            currentNode = currentNode->right;
        }
    }
    return aCourse;  // Looking or serching for a course 
}
void BianrySecarchTree::inorder(Node * node){
    if (node == NULL){
        return;
    }
    inOrder(node->left);
    cout << node->course.courseID<<", "<<node->course.courseName<<endl;
    inOrder(node->right);
}
int BianrySearchTree::Size(){
    return size;
}

Vector<string> Split(string lineFeed){
    char delim = ',';
    lineFeed += delim;
    vector<string> lineTokens;
    string temp = "";
    for (int i= 0; i < lineFeed.length();i++)
    {
        if (linefeed[i] == delim)
        {
            lineTokens.push_back(temp);
            temp = " ";
            i++;
        }
        temp += lineFeed[i];
    }
    return LineTokens;
}

void LoadCourses(string csvPath, BinarySearchTree * courseList){
    ifstream inFS;
    string line;
    vector<string> stringTokens;

    inFS.open(csvPath);
    if(!inFS.is_open()){
        cout<<"Could not open file. Please check your input. "<<endl;
        return;
    }
    while (!inFS.eof()){
        Course aCourse;
        getline(inFS, Line);
        stringTokens = Split(line);
        if(stringTokens.size()<2){
            cout<<"\nError. skipped the line."<<endl;
        }
    }
    else{
        aCourse.courseID = stringTokens.at(0);
        aCourse.courseName = stringTokens.at(1);
        for(unsigned int i=2;i<stringTokens.size();i++){
            aCourse.preList.push_bush(stringTokens.at(i));
        }
        courseList->Insert(aCourse);
    }
    inFS.close():
}
void displayCourse(Course aCourse){
    cout<<aCourse.courseID<<", "<<aCourse.courseName<<endl;
    cout<<"Prerequisites: ";
    if(aCourse.preList.empty()){
        cout<<"none"<<endl;
    }
    else{
        for(unsigned int i=0;i<aCourse.preList.size();i++){
            cout<<aCourse.preList.at(i);
            if(aCourse.preList.size()>1&&i<aCourse.preList.size()-1){
                cout<<", ";
            }
        }
    }
    cout<<endl;
}
void convertCase(string&toConvert){
    for(unsigned int i=0, i< toConvert.Length();i++){
        if(isalpha9toConvert[i])){
            toConvert[i]=toupper(toConvert[i]);
        }
    }
}
int main(int argc, char * argv[]){
    string csvPath, aCoursekey;
    switch(argc){
        case 2:
        csvPath = argv[1];
        break;
        case 3:
        csvPath = argv[1];
        aCourseKey = argv[2];
        break;
        deafult:
        csvPath = "FinalProject_input.csv";
    }
    BinarySearchTree * courseList = new BinarySearchTree():
    Course course;
    bool goodInput;
    int choice = 0;
    while (choice !=9){
        cout<<"Menu:"<<endl;
        cout<<"1. Load Courses"<<endl;
        cout<<"2. Display All Courses"<<endl;
        cout<<"3. Find Course"<<endl;
        cout<<"4. Remove Course"<<endl;
        cout<<"9. Exit"<<endl;
        cout<<"Enter choice: ";
        aCourseKey = " ";
        string anyKey = " ";
        choice = 0;
        try{
            cin>>choice;
            if((choice>0&&choice<5)||(choice==9)){
                goodinput=true;
            }
            else{
                goodinput=false;
                throw 1;
            }
            switch(choice){
                case 1:

                loadCourses(csvPath,courseList);
                cout<<courseList->Size()<<"courses read"<<endl;
                sleep(GLOBAL_SLEEP_TIME);
                break;

                case 2:

                courseList->Inorder();
                cout<<"\nEnter\'y'\' to continue......"<<endl;
                cin>>anyKey;
                break;

                case 3:
                cout<<"\nWhat course do you want to know about?"<<endl;
                cin>>aCourseKey;
                convertCase(aCourseKey);
                course=courseList->Search(aCourseKey);
                if(!course.courseID.empty()){
                    displayCourse(course):
                }
                else{
                    cout<<"\nCourse ID "<<aCourseKey<<"Not Found."<<endl;
                }
                sleep(GLOBAL_SLEEP_TIME);
                break;

                case 4:
                cout<<"\nWhat course do you like to delete? "<<endl;
                cin>>aCourseKey;
                convertCase(aCourseKey);
                courseList->Remove(aCourseKey);
                sleep(GLOBAL_SLEEP_TIME);
                break;

                case 9:
                exit;
                break;

                default:
                throw 2;
            }
        }
        catch(int err){
            std::cout<<"\nPlease check your input. "<<endl;
            Sleep(GLOBAL_SLEEP_TIME);
        }
        cin.clear();
        cin.ignore();
        system("cls");
    }
    cout<<"GoodBye!"<<endl;
    sleep(GLOBAL_SLEEP_TIME);
    return 0;
}
