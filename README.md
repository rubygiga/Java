# Java  2048
import javax.swing.JFrame;

import java.awt.BorderLayout;

public class Win2048 {

	private JFrame frame;
	JButton[][] jb = new JButton[4][4];
	int[][] cells = new int[4][4];
	int emptyCells = 4*4;
	Random ran = new Random();
	
	public static void main(String[] args) {
		
		Win2048 window = new Win2048();
		window.frame.setVisible(true);
	}

	public Win2048() {
		initialize();
	}

	/**
	 * Initialize the contents of the frame.
	 */
	private void initialize() {
		frame = new JFrame();
		frame.setTitle("2048");
		frame.setResizable(false);
		frame.setBounds(100, 100, 450, 300);
		frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		frame.getContentPane().setLayout(new BorderLayout(0, 0));
		
		JPanel center = new JPanel();
		frame.getContentPane().add(center, BorderLayout.CENTER);
		GridLayout gl_center = new GridLayout(4, 4);
		center.setLayout(gl_center);
		
		
		for(int i = 0; i < 4; i++){
			for(int j=0; j< 4; j++){
				jb[i][j] = new JButton();
				center.add(jb[i][j]);
				jb[i][j].setEnabled(false);
				cells[i][j] = 0;
			}
		}
	
		JButton btnNewButton = new JButton("^");
		btnNewButton.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				shiftUp();
			}
		});
	
		frame.getContentPane().add(btnNewButton, BorderLayout.NORTH);
		
		JButton btnNewButton_3 = new JButton("v");
		btnNewButton_3.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				shiftDown();
			}
		});
		
		frame.getContentPane().add(btnNewButton_3, BorderLayout.SOUTH);
		
		JButton btnNewButton_1 = new JButton("<");
		btnNewButton_1.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				shiftLeft();
			}
		});
		frame.getContentPane().add(btnNewButton_1, BorderLayout.WEST);
		
		JButton btnNewButton_2 = new JButton(">");
		btnNewButton_2.addActionListener(new ActionListener() {
			@Override
			public void actionPerformed(ActionEvent e) {
				shiftRight();
			}
		});
		frame.getContentPane().add(btnNewButton_2, BorderLayout.EAST);
		
		JMenuBar menuBar = new JMenuBar();
		frame.setJMenuBar(menuBar);
		
		JMenu mnNewgame = new JMenu("NewGame");
		mnNewgame.addMenuListener(new MenuListener() {
			public void menuCanceled(MenuEvent arg0) {
			}
			public void menuDeselected(MenuEvent arg0) {
			}
			public void menuSelected(MenuEvent arg0) {
				emptyCells = 0;
				for(int i = 0; i < 4; i++){
					for(int j=0; j< 4; j++){
						cells[i][j] = 0;
					}
				}
				playOnce();
			}
		});
		mnNewgame.setMnemonic('N');
		menuBar.add(mnNewgame);
		
		JMenu mnExit = new JMenu("Exit");
		mnExit.addMenuListener(new MenuListener() {
			public void menuCanceled(MenuEvent e) {
			}
			public void menuDeselected(MenuEvent e) {
			}
			public void menuSelected(MenuEvent e) {
				System.exit(0);
			}
		});
		
		mnExit.setMnemonic('E');
		menuBar.add(mnExit);
		
		playOnce();
	}
	
	private void playOnce() {
		this.genCells();
		this.mapCells();		
		this.calcEmpty();
	}

	private void calcEmpty() {
		emptyCells = 0;
		for(int i = 0; i < 4; i++){
			for(int j=0; j< 4; j++){
				if (cells[i][j] == 0) 
					this.emptyCells++;
			}
		}
	}

	private void genCells(){
		int max = (int) Math.sqrt(16 - emptyCells);
		for(int i = 0; i < 4; i++){
			for(int j=0; j< 4; j++){
				if ((cells[i][j] == 0) &&(ran.nextInt(10)<=max))
					cells[i][j] = 2;
			}
		}
	}
	private void mapCells(){
		for(int i = 0; i < 4; i++){
			for(int j=0; j< 4; j++){
				jb[i][j].setText(Integer.toString(cells[i][j]));
			}
		}
	}
	protected void shiftDown() {
		for(int i = 0; i < 3; i++){
			for(int j=0; j< 4; j++){
				cells[3][j] += cells[i][j];
				cells[i][j] = 0;
			}
		}
		playOnce();		
	}

	protected void shiftRight() {
		for(int i = 0; i < 4; i++){
			for(int j=0; j< 3; j++){
				cells[i][3] += cells[i][j];
				cells[i][j] = 0;
			}
		}
		playOnce();			
	}

	protected void shiftUp() {
		for(int i = 1; i < 4; i++){
			for(int j=0; j< 4; j++){
				cells[0][j] += cells[i][j];
				cells[i][j] = 0;
			}
		}
		playOnce();	
		
	}

	protected void shiftLeft() {
		for(int i = 0; i < 4; i++){
			for(int j=1; j< 4; j++){
				cells[i][0] += cells[i][j];
				cells[i][j] = 0;
			}
		}
		playOnce();	
	}

}
