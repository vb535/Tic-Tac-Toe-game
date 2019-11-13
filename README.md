# Tic-Tac-Toe-game
package GameDeveploment;
import java.awt.Font;
import java.awt.GridLayout;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JOptionPane;

public class TicTacToe extends JFrame implements ActionListener {
	static int BOARD_SIZE=3;
	boolean crossTurn=true;
	JButton[][] buttons=new JButton[BOARD_SIZE][BOARD_SIZE];
	public static enum GameStatus{
		XWins,ZWins,Tie,Incomplete
	}
	public TicTacToe(){
		super.setTitle("TicTcToe");
		super.setSize(800,800);
		super.setVisible(true);
		super.setResizable(false);
		GridLayout grid=new GridLayout(BOARD_SIZE,BOARD_SIZE);
		super.setLayout(grid);
		Font font=new Font("Comic Sans",1,150);
		for(int row=0;row<BOARD_SIZE;row++){
			for(int col=0;col<BOARD_SIZE;col++){
				JButton button=new JButton();
				buttons[row][col]=button;
				button.setFont(font);
				
				button.addActionListener(this);
				super.add(button);
				
			}
		}
		
		
	}
	@Override
	public void actionPerformed(ActionEvent e) {
		
		JButton clickedButton=(JButton)e.getSource();
		makeMove(clickedButton);
		GameStatus gs=this.getGameStatus();
		if(gs==GameStatus.Incomplete){
			return;
		}
		
		declareWinner(gs);
		int choice=JOptionPane.showConfirmDialog(this,"Do you want to restart the game");
		if(choice==JOptionPane.YES_OPTION){
			for(int row=0;row<BOARD_SIZE;row++){
				for(int col=0;col<BOARD_SIZE;col++){
		buttons[row][col].setText("");
					
				}
			}
			crossTurn=true;
		}
		else{
			super.dispose();
		}
		
	}
	
	private void makeMove(JButton clickedButton){
		String btntext=clickedButton.getText();
		if(btntext.length()>0){
			JOptionPane.showMessageDialog(this, "Invalid Move");
		}
		else{
			if(crossTurn){
				clickedButton.setText("X");
			}
			else{
				clickedButton.setText("0");
			}
			crossTurn=!crossTurn;
		}
	}
	private GameStatus getGameStatus(){
		String text1="";
		String text2="";
		int row=0,col=0;
		row=0;
		while(row<BOARD_SIZE){
			col=0;
			while(col<BOARD_SIZE-1){
				text1=buttons[row][col].getText();
				text2=buttons[row][col+1].getText();
				
				if(!text1.equals(text2) || text1.length()==0){
					break;
				}
				col++;
			}
			if(col==BOARD_SIZE-1){
				if(text1.equals("X")){
					return GameStatus.XWins;
				}
				else{
					return GameStatus.ZWins;
				}
			}
			
			row++;
		}
		col=0;
		while(col<BOARD_SIZE){
			row=0;
			while(row<BOARD_SIZE-1){
				text1=buttons[row][col].getText();
				text2=buttons[row+1][col].getText();
				
				if(!text1.equals(text2) || text1.length()==0){
					break;
				}
				row++;
			}
			if(row==BOARD_SIZE-1){
				if(text1.equals("X")){
					return GameStatus.XWins;
				}
				else{
					return GameStatus.ZWins;
				}
			}
			
			col++;
		}
		
		row=0;
		col=0;
		while(row<BOARD_SIZE-1){
			text1=buttons[row][col].getText();
			text2=buttons[row+1][col+1].getText();
			
			if(!text1.equals(text2) || text1.length()==0){
				break;
			}
			row++;
			col++;
			
			
			
		}
		
		if(row==BOARD_SIZE-1){
				if(text1.equals("X")){
					return GameStatus.XWins;
				}
				else{
					return GameStatus.ZWins;
				}
			}
			
			row=BOARD_SIZE-1;
			col=0;
			while(row>0){
				text1=buttons[row][col].getText();
				text2=buttons[row-1][col+1].getText();
				
				if(!text1.equals(text2) || text1.length()==0){
					break;
				}
				row--;
				col++;
				
				
				
			}
			
			
					if(row==0){
					if(text1.equals("X")){
						return GameStatus.XWins;
					}
					else{
						return GameStatus.ZWins;
					}
				}
				
			
			 String txt="";
			 for(row=0;row<BOARD_SIZE;row++){
				 for(col=0;col<BOARD_SIZE;col++){
					 txt=buttons[row][col].getText();
					 if(txt.length()==0){
						 return GameStatus.Incomplete;
					 }
				 }
			 }
		
		return GameStatus.Tie;
		
	}
	
	private void declareWinner(GameStatus gs){
		if(gs==GameStatus.XWins){
			JOptionPane.showMessageDialog(this,"Xwins");
			
		}
		else if(gs==GameStatus.ZWins){
			JOptionPane.showMessageDialog(this,"Zwins");
			
		}
		else{
			
			JOptionPane.showMessageDialog(this,"Tie");
			
		}
		
	}
	

}
