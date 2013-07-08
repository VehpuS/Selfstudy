//Set up the deck constructor;
var CardDeck = function(){
  stack = [];
	
	suits = {clubs:1,diamonds:2,hearts:3,spades:4};
	ranks = {"A":1,2:2,3:3,4:4,5:5,6:6,7:7,8:8,9:9,10:10,"J":11,"Q":12,"K":13};

	//Stack a new deck
	this.stackdeck = function(){
		for(var suit in suits) {
			for(var rank in ranks){
				stack.push([suits[suit],ranks[rank]]);
			}
		}
	};


	//Create a new shuffle function
	this.shuffle = function() {
		stack.sort(
			function(){
				return 0.5-Math.random();
			}
		);
	};

	this.deal = function() {
		if (stack.length > 0){
			var newcard = stack.pop();
			var dealtcard = new Card(newcard[0],newcard[1]);
			return dealtcard;
		}
		else {
			this.stackdeck();
			this.shuffle();
			var newcard1 = stack.pop();
			var dealtcard1 = new Card(newcard1[0],newcard1[1]);
			return dealtcard1;			
		}
	};
};

var Deck = new CardDeck();
Deck.stackdeck();
Deck.shuffle();


//translators for ranks and suits
function translateCard(suit,rank){
	suitname = "";
	rankname = rank;
	//translate the rank of your card (number)
	if (rank === 1) {
		rankname = "Ace";
	}
	else if (rank === 11) {
		rankname = "Jack";
	}
	else if (rank === 12) {
		rankname = "Queen";
	}
	else if (rank === 13) {
		rankname = "King";
	}

	//translate suits: clubs are 1, diamonds are 2, hearts are 3, spades are 4
	if (suit === 1) {
		suitname = "clubs";
	}
	else if (suit === 2) {
		suitname = "diamonds";
	}	
	else if (suit === 3) {
		suitname = "hearts";
	}	
	else if (suit === 4) {
		suitname = "spades";
	}
	var translation = rankname + " of " + suitname;
	return translation;
}


//A function to handle Ace values by giving users a choise. Wasn't used in the end, but kept here for reference.
function chooseAceValue(){
	var choise = prompt("You have an Ace - does it count for 1 or 11?");
	if (choise === "1" | choise === "11") {
		choise = +choise;
		return choise;
	}
	else {
		chooseAceValue();
	}
}

// Card Constructor
function Card(suit,rank) {
	var cardSuit = suit;
	var cardNumber = rank;
	this.getNumber = function() {
		return cardNumber;
	};
	this.getSuit = function(){
		return cardSuit;
	};
	this.getValue = function() {
		if (this.getNumber() === 11|this.getNumber() === 12|this.getNumber() === 13) {
			return 10;
		}
		else if (this.getNumber() === 1) {
			return 11;
		}
		else {
			return this.getNumber();
		}
	};
}

// The hand constructor, which practically will represent the player or the dealer.
function Hand() {
	var hand = [Deck.deal(),Deck.deal()];
	this.getHand = function() {
		return hand;
	};
	this.score = function() {
		var totalscore = 0;
		for (var card in hand) {
			totalscore += hand[card].getValue();	
		}
		if (totalscore > 21) {
			totalscore = 0;
			for (var card2 in hand) {
				if (hand[card2].getValue() === 11) {
					totalscore += 1;
				}
				else {
					totalscore += hand[card2].getValue();	
				}
			}
		}
		return totalscore;
	};
	this.printHand = function(){
		var string = "";
		var i = 1;
		for (var card in hand) {
			string = string +
				"Card " + i + ": " +
				translateCard(hand[card].getSuit(),hand[card].getNumber()) +
				", \n\n"
				;
			i++;
		}
		string = string.substring(0,string.length - 3);
		return string;
	};
	this.hitMe = function() {
		hand.push(Deck.deal());
	};
}

//Create the dealer
var playAsDealer = function() {
	var dealersHand = new Hand();
	while (dealersHand.score() < 17) {
		dealersHand.hitMe();
	}
	console.log("The dealer's hand contains the following cards: \n\n" + dealersHand.printHand() + ".");
	return dealersHand;
};


//Give the player control
var playAsUser = function() {
	var playerHand = new Hand();
	var hit = confirm("Your hand contains the following cards: \n\n" + playerHand.printHand() + ". \n\nYour current score is "+ playerHand.score() +". \n\nWould you like another card?");
	while(hit === true)
	{
		playerHand.hitMe();
		if (playerHand.score() > 21) {
			alert("Your hand contains the following cards: \n\n" + playerHand.printHand() + ". \n\nYour current score is "+ playerHand.score() +". \n\n \n\nYou can't hit any more!");
			hit = false;	
		}
		else{
			hit = confirm("Your hand contains the following cards: \n\n" + playerHand.printHand() + ". \n\nYour current score is "+ playerHand.score() +". \n\nWould you like another card?");
		}
	}
	console.log("Your hand contains the following cards: " + playerHand.printHand() + ".");
	return playerHand;
};

//Declaring the winner!
var declareWinner = function(userHand,dealerHand) {
	var result = ("You got a score of " + userHand.score() + " and the dealer got a score of " + dealerHand.score());	
	if (userHand.score() === dealerHand.score() | (userHand.score() > 21 && dealerHand.score() > 21)){
		result += "\n\nYou tied!";
	}
	else if (userHand.score() > 21 | (userHand.score() < dealerHand.score() && dealerHand.score() <= 21)) {
		result += "\n\nYou lose!";
	}
	else {
		result += "\n\nYou win!";
	}
	return result;
};

function playGame() {
	alert(declareWinner(playAsUser(),playAsDealer()));
}

playGame();
