// 9바이9인 스도쿠 맞는지 아닌지 판별

import java.io.*;
import java.util.*;

public class SudokuCheck {
	public static void main(String[] args) throws Exception {
		Scanner input = new Scanner(System.in);
		int num = 0;
		int[][] sudokuSave = new int[9][9];
		boolean[][] sudokuRight1 = new boolean[9][9];
		boolean right1=true;
		boolean[][] sudokuRight2 = new boolean[9][9];
		boolean right2=true;
		boolean[][] sudokuRight3 = new boolean[9][9];
		boolean right3=true;
		while (input.hasNext()) {
			String sudokuLine = input.nextLine();
			String[] Arr = sudokuLine.split("[ \t]");
			for (int i=0; i<9; i++){
				sudokuSave[num][i] = Integer.parseInt(Arr[i]);
			}
			num++;
		}
		
		// FIRST : row
		for(int i = 0; i<9; i++){
			for(int k=0;k<9;k++) sudokuRight1[i][k]=false;
			for(int j = 0; j<9; j++){
				sudokuRight1[i][sudokuSave[i][j]-1]=true;
			}
			for(int u=0; u<9; u++) {
				if(!sudokuRight1[i][u]){
					right1 = false;
				}
			}
		}
		
		// SECOND : column
		for(int i=0; i<9; i++){
			for(int k=0; k<9; k++) {
				sudokuRight2[k][i]=false;
				sudokuRight3[k][i]=true;
			}
			for(int j=0; j<9; j++){
				sudokuRight2[i][sudokuSave[j][i]-1]=true;
			}
			for(int u=0; u<9; u++){
				if(!sudokuRight2[i][u]){
					right2 = false;
				}
			}
		}
		
		
		// THIRD : 3*3 box
		for(int i=0; i<9; i++){
			for(int k=i-i%3;k<i-i%3+3;k++){
				for(int j=(i%3)*3;j<(i%3+1)*3;j++){
					sudokuRight3[i][sudokuSave[j][k]-1]=true;
				}
			}
			for(int r=0;r<9;r++){
				if(!sudokuRight3[i][r]){
					right3 = false;
				}
			}
		}
		
		
		if(right1&&right2&&right3) System.out.println("yes");
		else System.out.println("no");
		
	}
}
