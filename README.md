# War
Classic War Card Game Using C++

## Introduction
  This project was created my sophomore year at Jacksonville State University. It’s the classic card game “War”, except this time it’s the user versus the computer. The code is object oriented C++. The project contains five files, each of which are going to be explained. To run the program, simply download all of the files and select the Project_3.dev file. Feel free to open up the files and follow along here for each file.

## Card.h File
  To begin, I created the card.h file and created a class called Card that has public and private methods. In the public method of this class I created a constructor that takes 2 variables: an enumeration called suit, that contains the 4 possible suit options in a deck of cards, and a char to hold the number of the card, Ace to King. Next, I needed a definition to print the cards suit and rank to the screen so I added a “to string” method. In the private method, I added rank and suit. After that, I created two additional definitions called get_rank, which is a char, and get_suit, which is of class suit from the enumeration, so that I could retrieve them from the private method as needed.
  
## Card.cpp File
   Once I had the Card class, within the card.h file, in place I needed to create methods for those empty definitions. So, the next file I created was card.cpp. I included card.h to this file to make sure to use the proper definitions from the class card. Firstly, I used the card constructor to create a basis for how the suit and the rank will be stored. I chose to use a switch to validate the rank and put a default error message to make sure I wasn’t to get any bad variable. I created my to_string method next. This takes the rank and suit and concatenates them together to form a printable version to the screen when it is called. In this, I used another switch for the suit to be able to match whatever was chosen by the computer and be concatenated to the end of the string. The next two methods I created were to simply return the rank and suit using the definitions I created toward the end of the Card class.
   
Establishing constuctor initaialized in Card.h, in Card.cpp:

    Card::Card(Suit s, char r) {
	
	next = nullptr;
	suit = s;
	
	/* Validate Rank */
	
	switch( r ) {
		
		case 'A': case '2': case '3': case '4': case '5':
		case '6': case '7': case '8': case '9': case 'T':
		case 'J': case 'Q': case 'K':
			rank = r;
			break;
		default:
			throw runtime_error("ERROR: Bad Card Constructor Argument!");
			
	 }
	}  

## Deck.h file
   After finishing the card part of the project, I still needed to create definitions and methods for drawing and randomly choosing the cards being played. So, I created the deck.h file to begin mapping out a new class called Deck. The Deck class would need to use parts of the card class to be able to choose what ranks and suits to choose randomly so the card.h file needed to be included. I began creating the deck class and adding a constructor that takes a boolean. This is so that when the value is "true" it will cause the deck to be filled with cards and "false" will leave it empty. I then created 2 definitions that point to the card class. The first being to draw the first card from a player’s deck and then the next to subsequently draw random cards after words. The next two definitions are void methods are used to output something in the program. The first definition being insert_card that contains a pointer to the Card object which represents the card to be added to the deck. The following definition is print_deck, and only prints a card from each hand. The last public definition called get_size, is used to return the size of each player’s deck. The private method draw_card is used to draw a specific number of cards. The final two private methods, size and head, are used in support of the two public methods get_size and drawing the first and random cards.
  
## Deck.cpp File
   Similarly, with how I implemented a card.cpp file to create methods from my card.h file, I’m going to do the same here. I created a deck.cpp file and included my deck.h file. The firt thing that I did in the deck.cpp file was to create a method for my constructor. First thing I did was create two constant integer variables. One called NUM_RANKS that is set to thirteen, for the thirteen possible choices of ranks, and the other called NUM_SUITS set to four, for the four possible choices of spade, club, diamond, and heart. Next, I created an if statement with a nested for loop inside. This takes each card and pairs a suit with every rank. It will then insert that paired card in a deck. I then create the method for drawing the first card. This uses a pointer for the Card class. The next method uses a random module to draw any card from a deck. The destructor at the end of the deck.cpp file is used to traverse each deck after the game has ended and delete each card so that the program can refill each deck at the start of a new game. 
   
Establishing Costructor for Deck.cpp:

      Deck::Deck(bool fill) {

    size = 0;
    head = nullptr;

    const int NUM_RANKS = 13;
    const int NUM_SUITS = 4;

    /* If "fill" argument is TRUE, fill the deck; otherwise, leave it empty */

    if (fill) {

      /* Fill the deck with cards */

      Suit suits[] = { CLUB, DIAMOND, HEART, SPADE };
      char ranks[] = { 'A','2','3','4','5','6','7','8','9','T','J','Q','K' };

      Card *c;

      for ( int i = 0; i < NUM_RANKS; ++i ) {

        for ( int j = 0; j < NUM_SUITS; ++j ) {

          /* Create new cards by pairing up each suit with every rank */

          c = new Card(suits[j], ranks[i]);

          /* Insert new card at the end of the deck */

          insert_card(c);

        } // End inner for()

      } // End outer for()

    } // End if()

    } // End constructor 
    
## War.cpp File and Conclusion
   Now that all the instructions of the project are written, it is time to piece all of them together to create the game. So, I created the war.cpp file that is essentially the main file. The first thing that I did was create a void function that returns a set of instructions at the beginning of each game. I wrote this at the bottom of the code so that It wasn’t too distracting from the rest of the file. Within the main function, I began by creating one shared deck and then two separate decks, one for the computer and one for the player. Next I create some state variables to use in future for loops for the program. The first for loop I have deals with issuing separate stacks to players. The next loop I have is the main while loop that continues to loop while its still not game_over or the player chooses to quit the program. In that case the program exits the while loop. Otherwise it begins the loop by having each player draw a card, then determine the rank of that card. It prints what cards were chosen to the screen then has separate if statements to print different outputs based on the cards chosen. If it determines that the card is the same then it runs through an else if loop to draw up to 6 cards and runs the same card comparing code to determine who wins the war. Based on who wins it then awards all those card to the winner. After the player or computer stack reaches zero, it then declares a winner and ends the program by saying thanks for playing.
   
Program comparing both cards and determing who wins the battle:
                 
    else {
			
			/* Human and computer players each draw one card */
			
			player_card = player_stack.draw_first_card();
			computer_card = computer_stack.draw_first_card();
			
			/* Determine rank and corresponding value of each card */
			
			player_card_rank = ( player_card -> get_rank() );
			computer_card_rank = ( computer_card -> get_rank() );
			
			player_card_value = rank_to_value( player_card_rank );
			computer_card_value = rank_to_value( computer_card_rank );
			
			/* Show both cards */
			
			cout << "\nYour Card: " << ( player_card -> to_string() ) << '\n';
			cout << "Computer's Card: " << ( computer_card -> to_string() ) << "\n\n";
			
			/* Is player rank greater?  If so, add both cards to player's stack */
			
			if ( player_card_value > computer_card_value ) {
				
				cout << "You won this round!\n\n";
				player_stack.insert_card(player_card);
				player_stack.insert_card(computer_card);
				
			} // End if() (player wins round)
			
			/* Is computer rank greater?  If so, add both cards to computer's stack */
			
			else if ( computer_card_value > player_card_value ) {
				
				cout << "The computer won this round!\n\n";
				computer_stack.insert_card(computer_card);
				computer_stack.insert_card(player_card);
				
			} // End if() (computer wins round)
