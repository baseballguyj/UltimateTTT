# UltimateTTT
/**Ultimate Tic Tac Toe
 * James and Jordan
 * December 12, 2016
 * PLAN ONLY
 */

import javax.swing.*;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.awt.event.*;
import java.io.*;
import javax.imageio.*;
//import java.util.*;
import javax.sound.sampled.*;



public class UltimateTTT extends JFrame implements ActionListener{
  
  //Declare Key variables and GUI components
  JFrame gameFrame = new JFrame();
  JPanel background = new JPanel();
  JPanel gameScreen = new JPanel();
  JPanel instructionScreen = new JPanel();
  BufferedImage backImage;
  BufferedImage backImageInstruction;
  BufferedImage instructionPic;
  BufferedImage playGamePic;
  BufferedImage leaderBoardPic;
  BufferedImage mainMenuPic;
  BufferedImage instrBoardPic;
  JButton instructionButton;
  JButton playGameButton;
  JButton leaderBoardButton;
  JButton menuButton;
  JLabel instructions;
  JLabel how2win;
  static Clip musicClip;
  

  
  //Declare constructor for JFrame
  public UltimateTTT() {
    setTitle("Ultimate Tic Tac Toe");
    setSize (1268, 720);
    setResizable (false);
    
    //*****MENU SCREEN*****
    
    
    //Create Menu Screen Panel 
    background.setLayout(null);
    gameScreen.setLayout(null);
    instructionScreen.setLayout(null);
    
    //Import images from file
    try {
      backImage = ImageIO.read(new File("BackImage.jpg"));
      backImageInstruction = ImageIO.read(new File("BackImage.jpg"));
      instructionPic = ImageIO.read(new File("Instructions.png"));
      playGamePic = ImageIO.read(new File("PlayGame.png"));
      leaderBoardPic = ImageIO.read(new File("LeaderBoard.png"));
      mainMenuPic = ImageIO.read(new File("MainMenu.png"));
      instrBoardPic = ImageIO.read(new File("instrBoard.jpg"));
    }
    catch (IOException ex) {
      System.out.println ("Picture File(s) Not Found");
    }
    
    //Create JButtons for menu screen
    instructionButton = new JButton (new ImageIcon(instructionPic));
    playGameButton = new JButton (new ImageIcon(playGamePic));
    leaderBoardButton = new JButton (new ImageIcon(leaderBoardPic));

    
    //Set background picture as JLabel
    JLabel picLabel = new JLabel(new ImageIcon(backImage));
    JLabel picLabelInstr = new JLabel (new ImageIcon(backImageInstruction));
    
    //Set visibilities to true
    picLabel.setVisible(true);
    instructionButton.setVisible(true);
    playGameButton.setVisible(true);
    leaderBoardButton.setVisible(true);
    
    //Set bounds of the buttons
    instructionButton.setBounds (950, 520, 300, 60);
    playGameButton.setBounds (950, 440, 300, 60);
    leaderBoardButton.setBounds (950, 600, 300, 60);
    
    //Set bounds of background pic
    picLabel.setBounds(0, 0, 1268, 720);
    picLabelInstr.setBounds(0, 0, 1268, 720);
    
    //Set bounds of background panel
    background.setBounds(0, 0, 1268, 720);
    
    //Add action listeners
    playGameButton.addActionListener(this);
    instructionButton.addActionListener(this);

    
    //Add components to background panel
    background.add(instructionButton);
    background.add(playGameButton);
    background.add(leaderBoardButton);
    
    background.add(picLabel);
    
    background.setVisible(true);
    
    
    //*****GAMESCREEN*****
    gameScreen.setBounds (0, 0, 1268, 720);
    gameScreen.setVisible(false);
    
    //*****INSTRUCTION SCREEN*****
    
    //Create Buttons
    menuButton = new JButton (new ImageIcon(mainMenuPic));
    
    //Create JLabel for instructions
    instructions = new JLabel ("<html>Player 1 is X <br> Player 2 is O <br> <br> Player 1 starts the game by placing and X in any one of the 81 squares.<br><br>Player 2 then follows by placing an O on any of the 9 squares on the mini board that mirrors the selection of Player 1.<br><br>The game continues alternating between Player 1 and Player 2 following the same pattern<html>", JLabel.RIGHT);
    instructions.setForeground (Color.blue);
    instructions.setFont(new Font("Arial", Font.BOLD, 20));
    
    //Create JLabel for how to win
    how2win = new JLabel ("<html>How to win:<br>Win a mini board by getting three in a row for the large 3x3 board. Get 3 in<br>a row on the big board to win the<br>game!<html>");
    how2win.setForeground(Color.blue);
    how2win.setBackground(Color.white);
    how2win.setFont(new Font("Arial", Font.BOLD, 20));
    
    //Create JLabel to display example board
    JLabel instrBoardLabel = new JLabel(new ImageIcon(instrBoardPic));
    
    //Set bounds of components
    menuButton.setBounds(960, 600, 300, 60);
    instructions.setBounds (800, 20, 400, 320);
    how2win.setBounds (610, 400, 400, 400);
    instrBoardLabel.setBounds(920, 340, 200, 200);
    
    //Add action listener
    menuButton.addActionListener(this);
    
    //Set bounds of instruction screen panel
    instructionScreen.setBounds(0, 0, 1268, 720);
    
    //Add components to instruction screen panel
    instructionScreen.add(menuButton);
    instructionScreen.add(instructions);
    instructionScreen.add(how2win);
    instructionScreen.add(instrBoardLabel);
    instructionScreen.add(picLabelInstr);
    
    
    //Set visibilty to false
    instructionScreen.setVisible(false);
    

    
    //Play music for main menu
    try{
    playMusic("MenuMusic.wav");
    }catch(IOException ex){
    }catch(LineUnavailableException ee){ 
    }catch(UnsupportedAudioFileException eee){ 
    }
    
    
    //Add components to JFrame
    add(instructionScreen);
    add(gameScreen);
    add(background);
    setVisible (true);
    

  }//end of constructor
    
    //Action Listener
  public void actionPerformed(ActionEvent event) {
   JButton buttonPressed;
   if (event.getSource() instanceof JButton) {
     buttonPressed = (JButton) (event.getSource());
     
     if (buttonPressed.equals(playGameButton)) {
       System.out.println("Play Game Button Pressed");
       background.setVisible(false);
       gameScreen.setVisible(true);
       
       //Stop Main Menu Music
       try {
       stopMusic();
       } catch (IOException ex){}
       catch (LineUnavailableException ee) {}
       catch (UnsupportedAudioFileException eee) {}
       
       //Play Game Music
       try{
       playMusic("GameMusic.wav");
       }catch(IOException ex){
       }catch(LineUnavailableException ee){ 
       }catch(UnsupportedAudioFileException eee){ 
       }
     }
     else if (buttonPressed.equals(instructionButton)) {
       System.out.println("Instruction Pressed");
       background.setVisible(false);
       instructionScreen.setVisible(true);
     }
     else if (buttonPressed.equals(menuButton)) {
      instructionScreen.setVisible(false);
      background.setVisible(true);
     }
   }//end of if
   
  }//end of action listener
  
  //Method to play music
  public static void playMusic (String fileName) throws IOException, LineUnavailableException, UnsupportedAudioFileException
  {
    try {
     File mainMenu = new File(fileName);
     AudioInputStream inputStream = AudioSystem.getAudioInputStream(mainMenu);
     musicClip = AudioSystem.getClip();
     musicClip.open(inputStream);
     musicClip.loop(Clip.LOOP_CONTINUOUSLY);
    }
    catch (Exception musicEx){
     System.out.println("Audio File Error"); 
    }
    //musicClip.stop()
  }
  
  //Method to stop music
  public static void stopMusic() throws IOException, LineUnavailableException, UnsupportedAudioFileException
  {
    musicClip.stop();
    musicClip.close();
  }
  
  
    
    
    

  
  //**METHOD** void highlightBox (parameter: index of button selected in mini board from previous turn
  //                              parameter: ultimateBoard array)
  {
    //DESCRIPTION:
    //Determines based on the users last move,
    //Which mini board is to be played on by current player
    //And set that panel's background green
    
    //Method will be called after every turn to highlight the appropriate miniBoard for the next turn
    
    //Set background of panel*Y* to the default background colour
    
    //If user's last click was miniBoard*Y* [x] and ultimateBoard [x] > 0 (that miniBoard has been won)
      //Set background of all panels to green
    
    //Else
      //Set background of panelx to green when user's last click was miniBoard*Y* [x]
        // x represents the index of the array for the mini board and the panel number of the ultimate board
        // *Y* represents the mini board that was last played on
        //For example: if player 2's selection was miniBoard4 [5], highlight panel5 green
  }
  
  //**METHOD** int advanceTurn (parameter: the player that took the previous turn
  {
    //DESCRIPTION:
    //Advances the turn to determine which player goes next
    
    //Method will be called after every turn to determine which player is going next
    
    //If previous turn was 1 
      //Set current turn to 2
    //Else
      //Set current turn to 1
    
    //return: the current turn number
  }
  
  //**METHOD** boolean checkWinner (parameter: array which corresponds to the board being checked. ex miniBoard2, or 
  //                                                                                                     ultimateBoard)
  {
    //DESCRIPTION:
    //Checks to see if a board of 3x3 tic tac toe has been won by a player
    //Method is able to check mini boards and ultimate board (the ultimateBoard will still be referred to a miniBoard
      //locally in this method)
    //*Y* represents which miniBoard is being checked, determined by the parameter
    
    //Method will be called after every turn to see if the previous turn resulted in a miniBoard or the ultimate board
    //Being won
    
    //Check all possibilities of a winning board
    //If miniBoard*Y* [0] == miniBoard*Y* [1] and miniBoard*Y* [0] == miniBoard*Y* [2]
      //return true
    //Else if miniBoard*Y* [0] == miniBoard*Y* [3] and miniBoard*Y* [0] == miniBoard*Y* [6]
      //return true
    //Else if miniBoard*Y* [0] == miniBoard*Y* [4] and miniBoard*Y* [0] == miniBoard*Y* [8]
      //return true
    //Else if miniBoard*Y* [3] == miniBoard*Y* [4] and miniBoard*Y* [3] == miniBoard*Y* [5]
      //reutn true
    //Else if miniBoard*Y* [6] == miniBoard*Y* [7] and miniBoard*Y* [6] == miniBoard*Y* [8]
      //return true
    //Else if miniBoard*Y* [1] == miniBoard*Y* [4] and miniBoard*Y* [1] == miniBoard*Y* [7]
      //return true
    //Else if miniBoard*Y* [2] == miniBoard*Y* [5] and miniBoard*Y* [2] == miniBoard*Y* [8]
      //return true
    //Else if miniBoard*Y* [2] == miniBoard*Y* [4] and miniBoard*Y* [2] == miniBoard*Y* [6]
      //return true
    //Else
      //return false
  }
  
  //Menu Screen (Creates the menu screen that allows the user to select what they would like to do)
  //This will created on one large panel that will have it's visibility set to true when user needs to see it
  {
    //Set JPanels to the JFrame of the menu screen
    
    //Create GUI components like buttons for the user to press to decide where they will place their X or O
    //Also a button for the user to use for exiting 
    
    //Constructor to set up GUI
    
    //Create a window that has a title called "Ultimate Tic Tac Toe"
    
    //Set the size of the window for the gameplay screen
    
    //Create the layouts for each panel of the JFrame

    //Set a layout for each panel of the JFrame
    
    //Create action listeners for each button to see what the user presses and act on it
  
    //Add components to the panel like the buttons
  
    //Add panels to the frame
    
    //Call an image to set as the background
    //Output the image
    //Catch any exceptions

    //Set the frame to visible
  
  
    //If the user selects the play game button 
      //Send them to the play game screen
  
    //If the user selects the instruction button
      //Send them to the instruction screen
  
    //If the user selects the leaderboard button 
      //Send them to the leaderboard screen
  
  }//End Menu Screen


  //Gameplay Screen (The screen where the user will play the game. Outputs the board the number of moves
  //the X and O for the moves users have made)
  {
    //Set JPanels to the JFrame of the gameplay screen
    
    //Create GUI components like buttons for the user to press to decide where they will place their X or O
    //Also a button for the user to use for exiting and a text field for name input
    
    //Constructor to set up GUI
    
    //Create a window that has a title called "Ultimate Tic Tac Toe"
    
    //Set the size of the window for the gameplay screen
    
    //Create the layouts for each panel of the JFrame

    //Set a layout for each panel of the JFrame
    
    //Create action listeners for each button to see what the user presses and act on it
  
    //Add components to the panel like the buttons
    
    //Add panels to the frame
    
    //Call an image of the board to output
    //Output the image
    //Catch any exceptions

    //Set the frame to visible
  
    //Output a screen to get the players to input their names
    //If the user selects start game then begin the game
  
    //Start game loop
  
      //Call advanceTurn to determine who's turn it is
      //Alert users who's turn it is
  
      //Highlight the miniBoard or miniBoards that can be played on for this turn
      //Do this by calling highlightBox
  
      //Get user's button click using action listeners
        //Only the highlighted miniBoard's buttons will be enabled
        //As well, only empty buttons in the miniBoard will be enabled (spaces that are not X or O)
  
      //Set the button clicked to X or O depending on the current turn
  
      //Check if the miniBoard has been won by calling checkWinner
  
      //If the user has won miniBoard
        //Highlight the miniBoard either red for player 1 or blue for player 2
    
        //Check if the user has also won the ultimateBoard by calling checkWinner
  
        //If the user has won the ultimateBoard (the game is over)
          //Highlight the three squares that they won with their colour
          //Output a game over message for the user 
          //Send the total move that each player made to a text file that can be read from the leaderboard
          //Display main menu
  
      //If the ultimate game has not been won
        //Output the players name and their number of moves
        //Highlight the name of the user who is taking their turn
  
      //If the user selects exit
        //Output a game over message
        //Return them to the menu screen
    
  
    //End game loop
      //Exit when the game is over of the user selects the exit button
  
  }//end Gameplay Screen


  //Instruction screen(If the user selects the instruction screen button then send them to the instruction
  //screen where they can read the rules
  {
  
    //Set JPanels to the JFrame of the instruction screen
    
    //Create GUI components like buttons for exit
    
    //Constructor to set up GUI
    
    //Create a window that has a title called "Ultimate Tic Tac Toe"
    
    //Set the size of the window for the gameplay screen
    
    //Create the layouts for each panel of the JFrame

    //Set a layout for each panel of the JFrame
    
    //Create action listeners for each button to see what the user presses and act on it
  
    //Add components to the panel like the buttons
  
    //Add panels to the frame
  
    //Call an image to set as the background
    //Output the image
    //Catch any exceptions

    //Set the frame to visible
  
    //Output the instructions for the user to read in the main panel in the center 
  
    //If the user selects exit 
      //Return to the menu screen
  
  }//end instruction screen


  //Leaderboard screen (If the user selects the leaderboard button then send them to the leaderboard screen 
  //and read from a text file to output the highest score for each user
  {
    //Set JPanels to the JFrame of the instruction screen
    
    //Create GUI components like buttons for exit
    
    //Constructor to set up GUI
    
    //Create a window that has a title called "Ultimate Tic Tac Toe"
    
    //Set the size of the window for the gameplay screen
    
    //Create the layouts for each panel of the JFrame

    //Set a layout for each panel of the JFrame
    
    //Create action listeners for each button to see what the user presses and act on it
  
    //Add components to the panel like the buttons
  
    //Add panels to the frame
  
    //Call an image to set as the background
    //Output the image
    //Catch any exceptions

    //Set the frame to visible
  
    //Read from the text file and output the high scores from previous games
    //Close text file
  
  }//end leaderboard screen

  //Main 
  public static void main (String [] args) { 
    //Create a JFrame
    UltimateTTT frame = new UltimateTTT();
    //Close the frame if the user press the x button on the window
    frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
  
  }//End main
}
  
