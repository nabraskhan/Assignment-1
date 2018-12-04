# Assignment-1



This project contains 5 files:
1.main.cpp
2.complex.cpp
3.complex.h
4.linkedlist.cpp
5.linkedlist.h




the link to github code is   https://github.com/nabraskhan/Assignment-1/edit/master/README.md





In the main file the following numbers are created 
1 – 4 + 5j
2 – 3 – 3j
3 – 4 + 3j
Then delete add the first two number and store in the list. Sub 1 and 3 and store at last. Mul 2 and 3 and store at last. Divide 1 and 3 and delete the element at 4 and and at an element at last. Print the list after each step.
after that functions on linked list are implemented which are:
1.getting the value of complex number at a desired position.
2.inserting a complex number after a desired position in linked list.
3.inserting a complex number at the end of linked list.
4.deleting the complex number at a specific position.
5.displaying the list.






source code is:





complex.h

#ifndef complex_H//to clarify the cons=fusion of adding one header files more than once in a program
#define complex_H
//defining a class named complex to define a complex number
class complex
{
public:
	float re, imag;
	complex* ptr;

	//Constructors
	complex();
	complex(float real, float imaginary);

	//functions
	void setvalue(float re,float imag);
	complex operator+ (complex c);
	complex operator- (complex c);
	complex operator* (complex c);
	complex operator/ (complex c);
};

#endif



complex.cpp



#include <iostream>
#include "complex.h"

using namespace std;

//constructor
complex::complex()	{
	re=0;
	imag=0;
}

complex::complex(float real, float imaginary)	{
	re=real;
	 imag=imaginary;
	  ptr=NULL;
}
void complex::setvalue(float real, float imaginary )
{
    re=real;
	 imag=imaginary;
	  ptr=NULL;
}


//defining four operators using operator overloading

complex complex::operator* (complex c)	{

	complex pro;
	pro.re=re * c.re - imag * c.imag ;
	pro.imag=re * c.imag + imag * c.re;
	return pro;
}



complex complex::operator+ (complex c)	{

	complex sum;
	sum.re=c.re+ re;
	sum.imag=c.imag+ imag;
	return sum;
}


complex complex::operator/ (complex c)	{

	complex div;
	try	{
	    float denomerator = (c.re * c.re + c.imag * c.imag);


		if (denomerator==0)
			throw 0;

		div.re= ( re * c.re + imag * c.imag) / denomerator ;
		div.imag=( -re * c.imag + imag * c.re ) / denomerator ;
		return div;

	}
	catch (...)	{
		cerr << "Denomenator can not be zero\n";
		return div;
	}
}


complex complex::operator- (complex c)	{

	complex sub;
	sub.re=	re-c.re;
	sub.imag=imag-c.imag;
	return sub;
}



linkedlist.h




#ifndef linked_list_H//to clarify the cons=fusion of adding one header files more than once in a program
#define linked_list_H

#include "complex.h"
//defining a class named linked-list to make linked list of complex numbers
class linked_list	{
private:
	complex* head;//head of the linked list class
public:
	linked_list ();	//constructor

	//functions to insert and delete values from different positions

	void valatposition (int position);

	void insertafterposition (complex c, int position);

	void insertatend(complex c);

	void print ();

	void deleteposition (int position);
};

#endif






linkedlist.cpp



#include <iostream>
#include "complex.h"
#include "linked_list.h"

using namespace std;

linked_list::linked_list ()	{
	head=NULL;
}

void linked_list::deleteposition (int position)	{

	complex* previous=head;
	complex* current=head->ptr;

	int a=1;
	while (a<position-1)	{
		previous=previous->ptr;
		a++;
	}
	current=previous->ptr;
	previous->ptr=current->ptr;
	delete current;
}

void linked_list::valatposition (int position)		{
	complex* temp=head;
	int a=1;
	while (a<position)	{
		temp=temp->ptr;
		a++;
	}
	cout << temp->re << "+" << temp->imag << "i\n";
}

void linked_list::insertafterposition (complex c, int position)	{
	complex* temp=head;
	complex* newnode=new complex;

	newnode->re=c.re;
	newnode->imag=c.imag;
	newnode->ptr=NULL;

	int a=1;
	while (a<position)	{
		temp=temp->ptr;
		a++;
	}
	newnode->ptr=temp->ptr;
	temp->ptr=newnode;
}

void linked_list::print()
{
	complex*temp= head;

	while (temp)	{
		cout <<"(" <<temp->re << ")+(" << temp->imag << ")i    ";
		temp=temp->ptr;
	}
	cout << endl;
}

void linked_list::insertatend(complex c)	{
	complex* temp= head;
	complex* newnode=new complex;

	newnode->re=c.re;
	newnode->imag=c.imag;
	newnode->ptr=NULL;

	if (temp==NULL)		head=newnode;
	else
	{
		while (temp->ptr)	temp=temp->ptr;
		temp->ptr=newnode;
	}
}





main.cpp


#include <iostream>
#include "complex.h"
#include "linked_list.h"

using namespace std;

int main ()
{
	complex c1(4,5);
	complex c2, c3;
	c2.setvalue(3,-3);

    c3.setvalue(4,3);
	linked_list list;

	cout << "<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<  ASSIGNMENT-1  >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>\n";
	cout << "<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<  GC MUHAMMAD NABRAS KHAN  >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>\n";
	cout << "<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<  39 MTS(B)  >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>\n\n\n";
	cout << "Making the linked list of 3 complex numbers as:\n";
	list.insertatend(c1);
	list.insertatend(c2);
	list.insertatend(c3);
	list.print();

	cout << "\nAdding 1st and 2nd complex number and inserting it at the end of list:\n"	;
	list.insertatend(c1+c2);
	list.print();

	cout << "\nSubtracting 1st and 3rd complex number and inserting it at the end of list:\n";
	list.insertatend(c1-c3);
	list.print();

	cout << "\nMultiplying 3rd and 2nd complex number and inserting it at the end of list:\n";
	list.insertatend(c2*c3);
	list.print();

	cout << "\nAdding 1st and 3rd complex number and inserting it at the end of list:\n";
	list.insertatend(c1/c3);
	list.print();

	{
		complex c4;
		cout << "\nException for the division if denomenator is zero:\n";
		c4=c1/c4;
	}




	{complex c6;
	    cout<<"Enter the complex number you want to enter at the end of linked list:\n" ;
	    cin>> c6.re>>c6.imag;
	    list.insertatend(c6);
	list.print();
	}
	int position=0;
	cout << "\nDeleting at position\nEnter position: ";
	cin >> position;
	list.deleteposition(position);
	list.print();

	{
		cout << "\nInserting after a given position\n";
		float real, imag;
		cout << "Enter the complex number using space\n";
		cin >> real >> imag;

		complex c4(real, imag);

		cout << "Enter position: ";
		cin >> position;

		list.insertafterposition(c4, position);
		list.print();
	}

	cout << "\nValue at position\n";
	cout << "Enter position: ";
	cin >> position;
	list.valatposition(position);
	cout<<"\n\n\n The final linked list is:\n";
	list.print();
}


