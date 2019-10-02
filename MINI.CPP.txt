#include<iostream.h>
#include<conio.h>
#include<fstream.h>
#include<stdio.h>
#include<dos.h>

int n;


void first_page()
{
	cout<<"\n\t       Shri Ramdeobaba College of Engineering and Management";
	cout<<"\n\t\t   Department of Masters of Computer Application";
	cout<<"\n\t\t\t\t(Session 2018-2019)";
	cout<<"\n\n\n\t\t\t\tPROJECT SUBMISSION";
	cout<<"\n\t\t\tfor Object Oriented Programming Lab";
	cout<<"\n\n\n\t\t\t**********************************";
	cout<<"\n\t\t\t Title : Pet Shop Management";
	cout<<"\n\t\t\t**********************************";
	cout<<"\n\n\n\t\t\t\t  Submitted By :";
	cout<<"\n\t\t\t\tVaibhav S. Shewale";
	cout<<"\n\t\t\t\t(Shift-I)(Sem-II)";
	cout<<"\n\t\t\t\t   Roll No. 48";
	cout<<"\n\n\n\t\t\t\t   Guided By :";
	cout<<"\n\t\t\t       Prof. Lalit Agrawal";
	cout<<"\n\t\t\t\t   Head of MIS";
}

void second_page()
{
	cout<<"\n\n\n\n\n\n\n\t\t\t    Welcome to the Mini Project";
	cout<<"\n\n\t\t\t**********************************";
	cout<<"\n\t\t\t\t Title : Pet Shop Management";
	cout<<"\n\t\t\t**********************************";
	cout<<"\n\n\t\t\t   Press any key to continue...!";
	cout<<"\n\n\n\n\n\n\n\n\nRefrence: stackoverflow.com and Quora.com";
}

int third_page()
{
	cout<<"\n\n\n\n\n\n\t\t  ******************MENU******************";
	cout<<"\n\n\t\t  1. Add Pet Details";
	cout<<"\n\t\t  2. Display all Pet Details";
	cout<<"\n\t\t  3. Update existing Pet details";
	cout<<"\n\t\t  4. Add Customer Details";
	cout<<"\n\t\t  5. View Customer Details";
	cout<<"\n\t\t  6. Update Customer Details";
       //	cout<<"\n\t\t  7. Buy Pet";
	cout<<"\n\t\t  7. Exit";
	cout<<"\n\n\t\t  ***************************************";
	cout<<"\n\t\t  Enter your choice : ";
	int choice;
	cin>>choice;
	return(choice);
}


class pet
{
	protected:
		  char species[10];
		  char gender[10];
		  char color[10];
		  int pet_age;
		   int pet_id;

	public:
		int quant;
		void get()
		{
		 cout<<"\nEnter pet ID : ";
		 cin>>pet_id;
		 cout<<"Enter Species : ";
		 cin>>species;
		 cout<<"Enter the color of "<<species<<" : ";
		 cin>>color;
		 cout<<"Enter the Gender of "<<species<<" : ";
		 cin>>gender;
		 cout<<"Enter the Age of "<<species<<" : ";
		 cin>>pet_age;
		 cout<<"Enter the quantity of "<<species<<" : ";
		 cin>>quant;
		}
		void display()
		{
			cout<<"\nPet ID: " << pet_id;
			cout<<"\nPet Species: "<<species;
			cout<<"\nPet Color: "<<color;
			cout<<"\nPet Gender: "<<gender;
			cout<<"\nPet Age: "<<pet_age;
			cout<<"\nQuantity: "<<quant;
		}
		 int ret_pid()
		{
			return pet_id;
		}

};

//int pet::pet_id=100;

class customer
{
	protected:
		  char name[13];
		  int age;
		  char gender[10];
		   int customer_id;
		  char pet1[13];
	public:
		void fetch()
		{
			cout<<"\nEnter Customer ID:";
			cin>>customer_id;
			cout<<"Enter the name of the customer: ";
			cin>>name;
			cout<<"Enter the Age of "<<name<<" : ";
			cin>>age;
			cout<<"Enter Gender of the Owner : ";
			cin>>gender;
			cout<<"Pet Bought: ";
			cin>>pet1;
		}
		void display_customer()
		{
			cout<<"\nCustomer ID: "<<customer_id;
			cout<<"\nCustomer Name: "<<name;
			cout<<"\nCustomer Age: "<<age;
			cout<<"\nCustomer gender: "<<gender;
			cout<<"\nPet bought by the Customer: "<<pet1;
		}
		 int ret_cid()
		{
			return customer_id;
		}

};

//int customer::customer_id=100;

int main()
{
	clrscr();
	int ch=0;
	class pet p;
	class customer c;
	fstream fobj;
	first_page();
	delay(2000);
	clrscr();
	second_page();
	getch();
	do
		{
			clrscr();
			ch=third_page();
			switch(ch)
			{
			  case 1:
				 clrscr();
				 fobj.open("pet1.txt",ios::out|ios::app);
				 cout<<"\nEnter the number of data you want to enter: ";
				 cin>>n;
				 for(int i=1;i<=n;i++)
				 {
					p.get();
					fobj.write((char*)&p,sizeof(p));
				 }
				 fobj.close();
				 cout<<"\nPet Details have been noted!";
				 getch();
				 break;
			  case 2:
				 clrscr();
				 fobj.open("pet1.txt",ios::in | ios::binary);
				 while(fobj.read((char*)&p,sizeof(p)))
				 {
				       p.display();
				 }
				 cout<<"\nEnd of file...Nothing to display";
				 fobj.close();
				 getch();
				 break;
			  case 3:
				 clrscr();
				 fobj.open("pet1.txt",ios::in | ios::out | ios::binary);
				 cout<<"\nEnter Pet ID you want to Update";
				 int temp;
				 cin>>temp;
				 while(fobj.read((char*)&p,sizeof(p)))
				 {
					if(temp==p.ret_pid())
					{
						cout<<"\nDetails Found...!!!";
						cout<<"\nPlease enter new details...";
						p.get();
						int pos=fobj.tellg();
						int pos1=pos-sizeof(p);
						fobj.seekp(pos1);
						fobj.write((char*)&p,sizeof(p));
						cout<<"\nDetails updated succssfully...";
					}
					else
					{
						continue;
					}
				 }
				 fobj.close();
				 getch();
				 break;

			  case 4:
				 clrscr();
				 fobj.open("cust1.txt",ios::out|ios::app);
				 cout<<"\nEnter the number of data you want to enter: ";
				 int n1;
				 cin>>n1;
				 for(i=1;i<=n1;i++)
				 {
					c.fetch();
					fobj.write((char*)&c,sizeof(c));
				 }
				 fobj.close();
				 cout<<"\nCustomer Details have been noted!";
				 getch();
				 break;
			  case 5:
				 clrscr();
				 fobj.open("cust1.txt",ios::in | ios::binary);
				 while(fobj.read((char*)&c,sizeof(c)))
				 {
				       c.display_customer();
				 }
				 cout<<"\nEnd of file...Nothing to display";
				 fobj.close();
				 getch();
				 break;
			  case 6:
				 clrscr();
				 fobj.open("cust1.txt",ios::in | ios::out | ios::binary);
				 cout<<"\nEnter Customer ID you want to Update";
				 int temp1;
				 cin>>temp1;
				 while(fobj.read((char*)&c,sizeof(c)))
				 {
					if(temp1==c.ret_cid())
					{
						cout<<"\nDetails Found...!!!";
						cout<<"\nPlease enter new details...";
						c.fetch();
						int pos=fobj.tellg();
						int pos1=pos-sizeof(c);
						fobj.seekp(pos1);
						fobj.write((char*)&c,sizeof(c));
						cout<<"\nDetails updated succssfully...";
					}
					else
					{
						continue;
					}
				 }
				 fobj.close();
				 getch();
				 break;
		       /*	  case 7:
				 clrscr();
				 fobj.open("pet1.txt",ios::in);
				 cout<<sizeof(p);
				 cout<<"\nEnter the pet id which you want to buy";
				 int n4;
				 cin>>n4;
				 while(fobj.read((char*)&p,sizeof(p)))
				 {
				       //	cout<<"\ninside while";
				       //	cout<<p.ret_pid();
					if(n4==p.ret_pid())
					{
						p.display();
						cout<<"\nDo you want to buy this pet..? (y/n) : ";
						char ch4;
						cin>>ch4;
						if(p.quant>0)
						{
							if(ch4=='y')
							{
								cout<<"\nThank you for adding new family member to your family...";
								p.quant = p.quant - 1;
								int pos3=sizeof(p);
								fobj.seekp(pos3-2);
								fobj.write((char*)&p.quant,sizeof(p.quant));
								cout<<p.quant;
							}
							else
							{
								cout<<"\nThank you for visiting...!!!";
							}
						}
						else
						{
							cout<<"\nThe pet is not avaliable.. You can look for other pets.";
						}
					}
					else
					{
						cout<<"\nThank You for visting!";
					}
				 }
				 fobj.close();
				 getch();
				 break;     */
			  case 7:
				  goto x;
			  default:
				cout<<"\nInvalid choice... Enter correct choice.";

			}

		}while(ch!=7);
		x:getch();
		return 0;
}
