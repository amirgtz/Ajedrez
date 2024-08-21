# Ajedrez
Código en C# para un juego de ajedrez

# Tablero
![Tablero](https://cdn-media-1.freecodecamp.org/images/1*fTWDdJ2m3L72X6rqce9_tQ.gif)

# Ejemplo de código
```
using System;
using System.Collections.Generic;

namespace ChessGame
{
    class Program
    {
        static void Main(string[] args)
        {
            ChessBoard board = new ChessBoard();
            board.PrintBoard();
            while (true)
            {
                Console.WriteLine("Enter move (e.g., 'e2 e4'): ");
                string move = Console.ReadLine();
                if (board.MakeMove(move))
                {
                    board.PrintBoard();
                }
                else
                {
                    Console.WriteLine("Invalid move. Try again.");
                }
            }
        }
    }

    public class ChessBoard
    {
        private readonly char[,] board;

        public ChessBoard()
        {
            board = new char[8, 8];
            InitializeBoard();
        }

        private void InitializeBoard()
        {
            // Initialize the board with pieces
            string initialSetup = 
                "rnbqkbnr" +
                "pppppppp" +
                "        " +
                "        " +
                "        " +
                "        " +
                "PPPPPPPP" +
                "RNBQKBNR";

            for (int i = 0; i < 64; i++)
            {
                board[i / 8, i % 8] = initialSetup[i];
            }
        }

        public void PrintBoard()
        {
            for (int i = 0; i < 8; i++)
            {
                for (int j = 0; j < 8; j++)
                {
                    Console.Write(board[i, j] + " ");
                }
                Console.WriteLine();
            }
        }

        public bool MakeMove(string move)
        {
            string[] parts = move.Split(' ');
            if (parts.Length != 2) return false;

            (int startX, int startY) = ParsePosition(parts[0]);
            (int endX, int endY) = ParsePosition(parts[1]);

            if (IsInBounds(startX, startY) && IsInBounds(endX, endY))
            {
                // Simple move logic: Move the piece to the new position
                char piece = board[startX, startY];
                board[startX, startY] = ' ';
                board[endX, endY] = piece;
                return true;
            }
            return false;
        }

        private (int x, int y) ParsePosition(string position)
```

