import java.util.Scanner;


//Tic Tac Toe


public class TicTacToe {
	
	
	public static void main(String args[]) {
		Scanner in = new Scanner(System.in);
		System.out.print("How many players? ");
		int numPlayers = in.nextInt();
		in.close();
		if(numPlayers == 1)
			askPlayerNum();
		else if(numPlayers == 2)
			multiplayer();
	}

	
	public static void askPlayerNum() {
		Scanner in = new Scanner(System.in);
		System.out.print("Are player one or player two? ");
		int playerNum = in.nextInt();
		in.close();
		if(playerNum == 1)
			player1();
		else if(playerNum == 2)
			player2();
		
	}
	
	public static void player1() {
		Scanner in = new Scanner(System.in);
		String[][] board = {{" ", " ", " "}, {" ", " ", " "}, {" ", " ", " "}};
		int turns = 0;
		while(true) {
			Scanner input2 = new Scanner(askForInput(in, board, 2));
			board[input2.nextInt() - 1][input2.nextInt() - 1] = "O";
			input2.close();
			turns++;
			
			printBoard(board);
			
			if(turns == 9 && !checkForWinner(board)) {
				System.out.println("It's a Draw!");
				break;
			}
			if(checkForWinner(board)) {
				System.out.println("Player 1 won!");
				break;
			}
			
			board = AI(board, "O");
			turns++;
			
			printBoard(board);
					
			
			if(checkForWinner(board)) {
				System.out.println("AI won!");
				break;
			}
			
		}
	}
	
	public static void player2() {
		Scanner in = new Scanner(System.in);
		String[][] board = {{" ", " ", " "}, {" ", " ", " "}, {" ", " ", " "}};
		int turns = 0;
		while(true) {
			board = AI(board, "X");
			turns++;
			
			printBoard(board);
			
			if(turns == 9 && !checkForWinner(board)) {
				System.out.println("It's a Draw!");
				break;
			}
			if(checkForWinner(board)) {
				System.out.println("AI won!");
				break;
			}
			
			Scanner input2 = new Scanner(askForInput(in, board, 2));
			board[input2.nextInt() - 1][input2.nextInt() - 1] = "O";
			input2.close();
			turns++;
			
			printBoard(board);
					
			
			if(checkForWinner(board)) {
				System.out.println("Player 2 won!");
				break;
			}
			
		}
		
	}
	
	public static String[][] AI(String[][] board, String player) {
		boolean bool = true;
		for(int n = 0; n < board.length; n++) {
			if(isEmpty(board[n])) {
				bool = false;
				break;
			}
		}
		if(bool)
			board[2][2] = player;
		else {
			
		}
		
		return board;
	}
	
	public static void multiplayer() {
		Scanner in = new Scanner(System.in);
		String[][] board = {{" ", " ", " "}, {" ", " ", " "}, {" ", " ", " "}};
		int turns = 0;
		while(true) {
			Scanner input1 = new Scanner(askForInput(in, board, 1));
			board[input1.nextInt() - 1][input1.nextInt() - 1] = "X";
			input1.close();
			turns++;
			
			printBoard(board);
			
			if(turns == 9 && !checkForWinner(board)) {
				System.out.println("It's a Draw!");
				break;
			}
			if(checkForWinner(board)) {
				System.out.println("Player 1 won!");
				break;
			}
									
			Scanner input2 = new Scanner(askForInput(in, board, 2));
			board[input2.nextInt() - 1][input2.nextInt() - 1] = "O";
			input2.close();
			turns++;
			
			printBoard(board);
					
			
			if(checkForWinner(board)) {
				System.out.println("Player 2 won!");
				break;
			}
			
		}
		in.close();
	}

	public static boolean checkForWinner(String[][] board) {
		for(int n = 0; n < board.length; n++) {
			if((board[n][0] == "X" && board[n][1] == "X" && board[n][2] == "X") || (board[n][0] == "O" && board[n][1] == "O" && board[n][2] == "O"))
				return true;				
		}
		for(int n = 0; n < board.length; n++) {
			if((board[0][n] == "X" && board[1][n] == "X" && board[2][n] == "X") || (board[0][n] == "O" && board[1][n] == "O" && board[2][n] == "O"))
				return true		;		
		}
		if((board[0][0] == "X" && board[1][1] == "X" && board[2][2] == "X") || (board[0][0] == "O" && board[1][1] == "O" && board[2][2] == "O"))
			return true;
		if((board[0][2] == "X" && board[1][1] == "X" && board[2][0] == "X") || (board[0][2] == "O" && board[1][1] == "O" && board[2][0] == "O"))
			return true;
		return false;
	}
	
	public static String askForInput(Scanner in, String[][] board, int player) {
		boolean bool = true;
		int prow = 0, pcolumn = 0;
		while(bool) {
			System.out.print("P" + player + " input row and column seperated by spaces: ");
			prow = in.nextInt();
			while(true) {
				if(prow > 3 || prow < 1) {
					System.out.println("INVALID, TRY AGAIN");
					in.nextLine();
					prow = in.nextInt();
				} else 
					break;			
			}
			pcolumn = in.nextInt();
			while(true) {
				if(pcolumn > 3 || pcolumn < 1) {
					System.out.println("INVALID, TRY AGAIN");
					in.nextLine();
					pcolumn = in.nextInt();
				} else 
					break;			
			}
			if(board[prow - 1][pcolumn - 1] == " ")
				bool = false;
		}
		
		return prow + " " + pcolumn;
	}
	
	public static void printBoard(String[][] board) {
		System.out.println();
		System.out.println(board[0][0] + "|" + board[0][1] + "|" + board[0][2]);
		drawSeperator();
		System.out.println(board[1][0] + "|" + board[1][1] + "|" + board[1][2]);
		drawSeperator();
		System.out.println(board[2][0] + "|" + board[2][1] + "|" + board[2][2]);
		System.out.println();
	}
		
	public static void drawSeperator() {
		System.out.println("-+-+-");
	}

	public static boolean isEmpty(String[] array) {
		boolean bool = true;
		for(int n = 0; n < array.length; n++) {
			if(array[n].equals(" ")) {
				bool = false;
				break;
			}
				
		}
		return bool;
	}
}



