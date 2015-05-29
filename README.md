# Java

import java.awt.Container;
import java.awt.GridLayout;
import java.awt.HeadlessException;

import javax.swing.ImageIcon;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JMenu;
import javax.swing.JMenuBar;
import javax.swing.JMenuItem;
import javax.swing.JPanel;



public class play extends JFrame implements Runnable {
	
	private ButtonHandler bh = new ButtonHandler();
	private JMenuBar jmb;
	private final int ROW = 4 ;
	private final int COL = 4;
	private final int LOOK_SEC = 5 ; //設定一開始可看幾秒
	private final int ADD = 100,DECR=100; //得分100扣分100
	private final int SEC = 1; //設定翻開的排不相同時間格秒數會蓋回去
	private int imgH = 100, imgW=100 ,SCORE =0 ;

	private JMenu game = new JMenu("Game"),about =new JMenu("關於");
	private JMenuItem [] gm = new JMenuItem[3];  //遊戲
	private JMenuItem [] About = new JMenuItem[2]; //關於
	private JButton [] ImgButton = new JButton[ROW*COL]; //按鈕
	private ImageIcon [] img = new ImageIcon[ROW*COL]; //存放圖物件

	private JPanel jp = new JPanel(new GridLayout (4,4,0,0));
	private JLabel jl = new JLabel("Score:0");

	private int[]m; //存放每次重新完的圖片順序
	private int []TwoImg = {-1,-1}; //紀錄目前翻開的兩張圖編號
	private int[] ButtonIndex = {-1,-1}; //紀錄被翻開兩張圖的按鈕位置
	private boolean isChange = false ; //用來切換存放兩張圖順序
	private boolean isStart =false; //是否開始
	private boolean[] imgShow = new boolean[8]; //紀錄以配對成功過的圖
	private boolean[]ButtonBown = new boolean[16]; //紀錄備案過的按鈕






	public play() throws HeadlessException {
		super("MemoryCard");
		Container c = getContentPane();
		c = this.getContentPane();
		jmb = new JMenuBar();
		this.setJMenuBar(jmb); //加入工具列
		
		//初始化所有按鈕圖，不可按
		for(int i=0 ; i <img.length ; i++);
		{
			img[i] = new ImageIcon(getClass().getResource("cardimage/00.jpg));
			imgButton[i] = new JButton(img[i]);
			imgButton[i].addActionListen(bh);
			jp.add(imgButton[i]);
			jp.add(jl);
			
		}
			c.add(jp)
				
	}



	}



	@Override
	public void run() {
		// TODO Auto-generated method stub

	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub

	}

}
