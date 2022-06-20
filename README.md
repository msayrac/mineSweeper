# mineSweeper

# main.java
import java.lang.reflect.Array;
import java.util.Arrays;
import java.util.Random;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        System.out.println("Mayin Tarlasina Hosgeldiniz");
        System.out.println("Satir sayisini giriniz : ");
        int row = input.nextInt();
        System.out.println("Sutun Sayisini giriniz : ");
        int col = input.nextInt();

        MineSweeper mineSweeper = new MineSweeper(row, col);

        mineSweeper.run();

    }
}


# mineSweeper.java

import java.sql.SQLOutput;
import java.util.Arrays;
import java.util.Scanner;

public class MineSweeper {
    String[][] minedMap;
    String[][] game;
    int row;
    int col;
    int mineNumber;


    MineSweeper(int row, int col) {
        this.row = row;
        this.col = col;
        this.minedMap = new String[row][col];
        this.game = new String[row][col];
        this.mineNumber = (row * col) / 4;
    }

    void minePlace() {
        System.out.println("Mayinlarin Konumu");
        for (int i = 0; i < this.row; i++) {
            for (int j = 0; j < this.col; j++) {
                this.game[i][j] = "-";
                System.out.print(game[i][j] + " ");
            }
            System.out.println();
        }
    }

    void minedMap() {
        for (int i = 0; i < mineNumber; i++) {
            int tempRow = (int) (Math.random() * row);
            int tempCol = (int) (Math.random() * col);

            if (this.minedMap[tempRow][tempCol] != "*") {
                this.minedMap[tempRow][tempCol] = "*";
            } else {
                i--;
            }
        }

        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                if (this.minedMap[i][j] != "*") {
                    this.minedMap[i][j] = "-";
                }
            }
        }

        for (int i = 0; i < this.row; i++) {
            for (int j = 0; j < this.col; j++) {
                System.out.print(minedMap[i][j] + " ");
            }
            System.out.println();
        }
    }

    void showMinedMap() {
        for (int i = 0; i < this.row; i++) {
            for (int j = 0; j < this.col; j++) {
                System.out.print(minedMap[i][j] + " ");
            }
            System.out.println();
        }
    }

    void run() {
        Scanner input = new Scanner(System.in);

        int totalmove = row * col - mineNumber;

        minePlace();
        minedMap();

        while (totalmove > 0) {
            int mineVision = 0;
            System.out.println("lutfen bir satir numarasi giriniz : ");
            int rowInput = input.nextInt();

            System.out.println("lutfen bir sutun numarasi giriniz : ");
            int colInput = input.nextInt();

            if ((rowInput < 0 || rowInput >= row) || (colInput < 0 || colInput >= col)) {
                System.out.println("Hatali giris yaptiniz. Lutfen sinirlar icinde secim yapiniz !");
                continue;
            } else {

                if (this.minedMap[rowInput][colInput] == "*") {
                    System.out.println("Mayina bastiniz");
                    showMinedMap();
                    break;
                } else {
                    int minusRow = (rowInput - 1), sumRow = (rowInput + 1);
                    int minusCol = (colInput - 1), sumCol = (colInput + 1);
                    if (minusRow < 0 || minusCol < 0) {
                        minusRow = 0;
                        minusCol = 0;
                    }
                    if (sumRow >= row || sumCol >= col) {

                        sumRow = rowInput;
                        sumCol = colInput;
                    }

                    for (int i = minusRow; i <= sumRow; i++) {
                        for (int j = minusCol; j <= sumCol; j++) {
                            if (this.minedMap[i][j] == "*") {
                                mineVision++;
                            }
                        }
                    }


                    String converMineVision = String.valueOf(mineVision);

                    this.game[rowInput][colInput] = converMineVision;

                    totalmove--;
                }
            }
        }
        if (totalmove == 0) {
            System.out.println("Tebrikler Oyunu Kazandiniz");
        }
    }
}

