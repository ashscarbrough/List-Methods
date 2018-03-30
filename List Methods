/*************************************************************************

AUTHOR  :  Ash Scarbrough (with John Russo and modified some by Matt Holloway)

SOURCE  :  hw08.cpp with the help from shell program a8shell.cpp

DATE    : 4/12/2015

COMPILER: Visual Studio 2013

ACTION  : The program tests routines designed to perform various
operations on singly linked lists. The lists have a
dummy head node that holds the "Happy Face" character.
The tail of the lists points to NULL.

*************************************************************************/


/*****************************   ZapList  ********************************
DESCRIPTION  Frees all the storage space currently occupied by the
linked list pointed to by List. Does NOT delete the dummy head node.

PARAMETER

OUT, List  A pointer to a singly linked list with a dummy head node.
After this call, List will contain only the dummy head node.

PRECONDITION List must point to a linked list that has a dummy head node
and a tail node that points at NULL.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -*/
void ZapList(NodePtr List)
{
	NodePtr Temp;

	if (List == NULL)	//Error if List does not point to dummy head node
	{
		cerr << "\nList is empty, missing head node. Closing Program.\n";
		exit(1);
	}

	else if (List->Link == NULL)	//If List only has dummy head node,
		return;						//List is already "empty"

	else
	{
		Temp = List;		//Temp points to dummy head node
		List = List->Link;	//List is progressed to Next Node
		Temp->Link = NULL;	//Dummy head node linked to NULL

		while (List->Link != NULL)	//While next node is not pointing to NULL
		{
			Temp = List;		//Temp is points to next node, where list points
			List = List->Link;	//List is progressed to next node
			delete Temp;		//Temp node is deleted and memory is reallocated
		}
		delete List;	//Final Node pointed to by List is also deleted
	}
}


/****************************   AddNode  *********************************
DESCRIPTION  Adds a node containing NewChar to the end of List.

PARAMETERS

IN, NewChar The character to be added to the end of the list.

IN, List    A pointer to a singly linked list with a dummy head node.
The value of List (address of dummy head node) is not
changed by this routine, so List is passed by value.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -*/
void AddNode(char NewChar, NodePtr List)
{
	NodePtr NewNode;

	if (List == NULL)	//Error if List is missing dummy head node
	{
		cerr << " - List is empty, missing head node. Closing Program.\n";
		exit(1);
	}

	NewNode = List;	//NewNode used insert new list item

	while (NewNode->Link != NULL)	//NewNode searches for end of list
	{
		NewNode = NewNode->Link;
	}

	NewNode->Link = new(nothrow)Node;	//New Node is created
	if (NewNode->Link == NULL)	//If error in memory allocation exists
	{							//New Node will return NULL, displaying error
		cerr << "Memory allocation error for new list item";
		exit(1);
	}

	NewNode = NewNode->Link;	//Progress NewNode pointer
	NewNode->Ch = NewChar;		//User supplied character added to list
	NewNode->Link = NULL;		//Final list node points to NULL
}

/****************************    DeleteNode   ****************************
DESCRIPTION  Deletes the first node of List that contains the char
CharToDelete. The storage occupied by the deleted
node is returned to the heap.

PARAMETERS

IN, CharToDelete  The character to be deleted.

IN, List    A pointer to a singly linked list with a dummy head node.
The value of List is not changed by this routine but the
linked list itself is changed.

OUT, CharFound Set to 1 if the CharToDelete is found and deleted and
0 otherwise.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -*/
void DeleteNode(char CharToDelete, NodePtr List, int &CharFound)
{
	NodePtr NodeToBeDeleted;
	CharFound = 0;		//Default - Character Not Found

	if (List == NULL)	//If List does not have dummy head node, display error
	{
		cerr << "List is empty, missing head node. Closing Program.\n";
		exit(1);
	}

	else
	{
		NodeToBeDeleted = List;

		if (NodeToBeDeleted->Link == NULL)	//If only dummy head node is present, return
			return;
		
		else
		{
			while (NodeToBeDeleted->Link != NULL)  //While not at the end of the list
			{
			   if (NodeToBeDeleted->Link->Ch == CharToDelete)  //If user character is found
			   {
			        List = NodeToBeDeleted;  //List pointer progresses to location of NodeToBeDeleted pointer
				NodeToBeDeleted = NodeToBeDeleted->Link;  //NodeToBeDeleted moved to node containing char
				List->Link = List->Link->Link;	//Previous list item made to point to item following
										//node to be deleted
				delete NodeToBeDeleted;		//Desired node and list item deleted

				CharFound = 1;		//display CharacterFound
				return;
			   }

			   else		//Otherwise progress NodeToBeDeleted to the next Node
			   {
				NodeToBeDeleted = NodeToBeDeleted->Link;
		 	   }
			}
		}
	}
}

/****************************   BuildList    *****************************
DESCRIPTION   Builds a singly linked list with a dummy head node. The
characters in the list are in the same order in which the
user enters them, i.e. new characters are added to the tail
end of the list.

Input terminates when the enter key is pressed.

PARAMETERS

IN, List    A pointer to a singly linked list with a dummy head node.
It is imperative that List be initialized before calling
this routine.

NOTE          Before building the new list, ZapList is called. This
ensures that a memory leak does not develop.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -*/
void BuildList(NodePtr List)
{
	ZapList(List);

	char NewChar;

	cout << "Enter List: ";  //List entered by user

	cin.get(NewChar);	// Get first character from input buffer
	while (NewChar != '\n')
	{
		List->Link = new(nothrow)Node;	//Creates a new Node for List
		if (List->Link == NULL)			//Checks to see if there is enough memory
		{								//If not, Link will point to NULL
			cerr << "Memory allocation error for new list item";
			exit(1);
		}

		List = List->Link;		//Moves List to the next Node in sequence
		List->Ch = NewChar;		//Insert user provided character into next Node;
		List->Link = NULL;		//Initializes last pointer to NULL
		cin.get(NewChar);		//Obtains next char input from user
	}
}
