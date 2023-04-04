
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Task2
{
    class Program
    {
        static void printArr(int[][] arr, int sizex, int sizey)//print array to screen
        {
            Console.ForegroundColor = ConsoleColor.White;//default color white
            Console.WriteLine("\n\n");
            for (int i = 0; i < sizey; i++)
            {
                for (int j = 0; j < sizex; j++)
                {
                    if (i == j) Console.ForegroundColor = ConsoleColor.Green;//if main diag - change color to green
                    else Console.ForegroundColor = ConsoleColor.White;//else - use white
                    Console.Write($"{arr[i][j]}\t");
                }
                Console.ForegroundColor = ConsoleColor.White;
                Console.WriteLine();
            }
        }
        static int[][] randArr(int[][] arr, int sizex, int sizey)//random every element of array from 0 to 100 and return changed array
        {
            Random rnd = new Random();
            for (int i = 0; i < sizey; i++)
            {
                for (int j = 0; j < sizex; j++)
                {
                    arr[i][j] = rnd.Next(0, 100);
                }
            }
            return arr;
        }
        static void printSnail(int[][] arr, int sizex, int sizey)
        {
            int posx = 0, posy = 0;
            int direction = 0; //0 - right, 1 - down, 2 - left, 3 - up
            int lbord = 0, rbord = sizex, ubord = 0, dbord = sizey;

            Console.ForegroundColor = ConsoleColor.Green;
            for (int i = 0; i < sizey*sizey; i++)
            {
                if(posx >= rbord)
                {
                    direction = 1;
                    posx--;
                    posy++;
                    ubord++;
                    Console.ForegroundColor = ConsoleColor.Red;
                }
                if(posx < lbord)
                {
                    posx++;
                    posy--;
                    direction = 3;
                    dbord--;
                    Console.ForegroundColor = ConsoleColor.Red;
                }
                if(posy >= dbord)
                {
                    posy--;
                    posx--;
                    direction = 2;
                    rbord--;
                    Console.ForegroundColor = ConsoleColor.Green;
                }
                if(posy < ubord)
                {
                    posy++;
                    posx++;
                    direction = 0;
                    lbord++;
                    Console.ForegroundColor = ConsoleColor.Green;
                }

                Console.Write($"{arr[posy][posx]}, ");

                if (direction == 0) posx++;
                if (direction == 1) posy++;
                if (direction == 2) posx--;
                if (direction == 3) posy--;
            }

        }
        static int matrixTrace(int[][] arr, int sizex, int sizey)//find trace = sum of elements on main diagonal
        {
            int res = 0;
            for(int i = 0; i < sizey; i++)
            {
                for (int j = 0; j < sizex; j++)
                {
                    if (i == j) res += arr[i][j];
                }
            }
            return res;
        }
        static void Main(string[] args)
        {
            int sizex, sizey;
            
            Console.Write("Enter x size: "); sizex = Convert.ToInt32(Console.ReadLine());
            Console.Write("Enter y size: "); sizey = Convert.ToInt32(Console.ReadLine());

            int[][] arr = new int[sizey][];//array memory for rows
            for(int i = 0; i < sizey; i++)
            {
                arr[i] = new int[sizex];//for cols
            }

            arr = randArr(arr, sizex, sizey);
            printArr(arr, sizex, sizey);

            Console.Write($"\n\nMatrix trace = {matrixTrace(arr, sizex, sizey)}\n\n");
            printSnail(arr, sizex, sizey);
            Console.WriteLine("\n\n");

            Console.ReadKey(true);
        }
    }
}
