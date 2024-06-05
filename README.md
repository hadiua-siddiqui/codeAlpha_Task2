# codeAlpha_Task2
Basic File Manager Build a command-line file manager that allows users to navigate directories, view files, create directories, and copy or move files. Use C++ file handling for this project....
//BASIC FILE MANAGER
#include<iostream>
#include<fstream>
#include<string>
#include<cstdlib>

using namespace std;
void listFiles(const string& path) {
	ifstream dir(path.c_str());
	if(!dir){
		cerr<<"ERROR: UNABLE TO OPEN DIRECTORY."<<endl;
		return;
			}
			string item;
			while(getline(dir, item)){
				cout<<item<<endl;
			}
			dir.close();
}
void copyFile(const string& source, const string& destination){
	ifstream sourceFile(source.c_str(),ios::binary);
	ofstream destFile(destination.c_str(),ios::binary);
	destFile<< sourceFile.rdbuf();
	sourceFile.close();
	destFile.close();
	cout<<"File copied successfully." <<endl;
}

void moveFile(const string&source, const string& destination){
	if(rename(source.c_str(),destination.c_str())==0)
	cout<<"file moved successfully"<<endl;
	else
	cerr<<"Erro:unable  to move file."<<endl;
}

void viewFile(const string & filename){
	ifstream file(filename.c_str());
	if(file.is_open()) {
		string line;
		while (getline(file, line)){
			cout<<line<<endl;
		}
		file.close();
	}else {
		cerr<<"Erro:unable  to move file."<<endl;
	}
}

int main() {
	string command;
	string path= ".";
	while(true){
		cout<<"CURRENT DIRECTORY :"<<path<<endl;
		cout<<"enter command(list,creat,copy,view,move,exit):";
		cin>>command;
		if(command=="list"){
			listFiles(path);
		}
		else if(command=="create"){
			string dirname;
			cout<<"enter directory name:";
			cin>>dirname;
		}
		else if(command=="copy"){
			string source, destination;
			cout<<"enter source file path:";
			cin>>source;
			cout<<"Enter destination file path:";
			cin>>destination;
			copyFile(source, destination);
		}
		else if(command=="move"){
			string source,destination;
			cout<<"enter source file path:";
			cin>>source;
			cout<<"Enter destination file path:";
			cin>>destination;
			moveFile(source, destination);
			
		}else if(command=="view"){
			string filename;
		  cout<<"enter a filename";
		  cin>>filename;
		  viewFile(path+"/"+ filename);
		}
		else if (command=="exit"){
			break;
		}else{
			cerr<<"INVALID COMMAND.PLEASE TRY AGAIN."<<endl;
		
		}
	}
	return 0;
}

