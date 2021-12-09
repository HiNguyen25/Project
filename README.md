#include<iostream>
#include<string>

using namespace std;

// data node for speaker
class NodeData {
private:
   //
   string Name;
   long ph_num;
   string topic;
   double fee;
public:
   NodeData(){}
   NodeData(string a, long b, string c, double d) {
       Name = a;
       ph_num = b;
       topic = c;
       fee = d;
   }
   void setName(string a) { Name = a; }
   void setPhoneNumber(long a) { ph_num = a; }
   void setTopic(string a) { topic = a; }
   void setFee(double a) { fee = a; }

   string getName() { return Name; }
   long getPhoneNumber() { return ph_num; }
   string getTopic() { return topic; }
   double getFee() { return fee; }
};


// node for linked
class Node {
private:
   NodeData *data;
   Node *next;
public:

   // constructor
   Node(){
       data = NULL;
       next = NULL;
   }
  
   Node(NodeData *d) {
       data = d;
       next = NULL;
   }

   Node(string a,long b,string c,double d ) {
       data = new NodeData(a,b,c,d);
       next = NULL;
   }

   // setter and getter
   void setData(NodeData *d) {
       data = d;
   }
   void setnext(Node *n) {
       next = n;
   }

   NodeData *getData() {
       return(data);
   }
   Node *getnext() {
       return(next);
   }
};

// data base
class DataBase {
private:
   Node *root;
public:
   // constructor
   DataBase() {
       root = NULL;
   }

   // insert data at first
   void insertData(string a, long b, string c, double d) {
       Node *node = new Node(a,b,c,d);
       node->setnext(root);
       root = node;
   }

   // serack topic from data base
   bool search(string d) {
       Node *cur = root;
       while (cur!=NULL) {
           if (cur->getData()->getTopic() == d) {
               return true;
           }
           cur = cur->getnext();
       }
       return false;
   }

   // check duplicate name exist in database
   bool exist(string d) {
       Node *cur = root;
       while (cur != NULL) {
           if (cur->getData()->getName() == d) {
               return true;
           }
           cur = cur->getnext();
       }
       return false;
   }

   // display list
   void displayAll() {
       Node *cur = root;
       int index = 1;
       while (cur != NULL) {
           cout << "Speaker " << index << " --- \n";
           cout << "\tName : "<<cur->getData()->getName();
           cout << "\n\tPhone Number : " << cur->getData()->getPhoneNumber();
           cout << "\n\tTopic : " << cur->getData()->getTopic();
           cout << "\n\tFee : " << cur->getData()->getFee();
           cur = cur->getnext();
           index++;
           cout << endl;
       }
   }

   // display list of speakers on a specific topic
   void displayByTopic(string d) {
       Node *cur = root;
       int index = 1;
       while (cur != NULL) {
           if (cur->getData()->getTopic() == d) {
               cout << "Speaker " << index << " --- \n";
               cout << "\tName : " << cur->getData()->getName();
               cout << "\n\tPhone Number : " << cur->getData()->getPhoneNumber();
               cout << "\n\tTopic : " << cur->getData()->getTopic();
               cout << "\n\tFee : " << cur->getData()->getFee();
               index++;
               cout << endl;
           }
           cur = cur->getnext();
       }
   }
};


int main() {

   DataBase dtabase;

   while (true)
   {
       cout << "1) Enter record";
       cout << "\n2) Search Speaker with topic";
       cout << "\n3) Display All speaker";
       cout << "\n4) Exit";
       cout << "\nEnter your choice [1 - 4] : ";
       int n;
       cin >> n;

       if (n >= 1 && n <= 4) {
           if(n==1){
               string n;
               long ph;
               string topic;
               double fee;
              
               cout << "Enter name : ";
               cin >> n;
               if (dtabase.exist(n) == true) {
                   cout << "This Speaker already exist\n";
               }
               else {
                   cout << "Enter phone number : ";
                   cin >> ph;
                   cout << "Enter topic : ";
                   cin >> topic;
                   cout << "Enter fee : ";
                   cin >> fee;

                   dtabase.insertData(n,ph,topic,fee);
                   cout << "\nData added succesfully\n";
               }
              
           }
           if (n == 2) {
               cout << "Enter topic : ";
               string topic;
               cin >> topic;

               if (dtabase.search(topic) == true) {
                   cout << "\nList \n\n";
                   dtabase.displayByTopic(topic);
               }
               else
               {
                   cout << "Sorry No Speaker found on "<<topic<<endl;
               }

           }
           if (n == 3) {
               dtabase.displayAll();
           }
           if (n == 4) {
               break;
           }
       }
       else {
           cout << "\nPlease choose correct oprion.\n";
       }

   }

   system( "pause" );
   return 0;
}

