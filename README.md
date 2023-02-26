//# PROGRAMMING-3
//Dating Application | Compatibility Test 
//Raw file just in case the file I posted here wont run. 

using System;
using System.Collections.Generic;
using System.Collections.Specialized;

class User
{
    public string username;
    public string password;
    public string favouriteFruit;
    public string favouritePlace;
    public string favouriteColor;
    public string hobby;
    public string favouriteAnimal;
    public User(string username, string password)
    {
        this.username = username;
        this.password = password;
    }
}

class Program
{
    static List<User> users = new List<User>();
    static List<string> usernames = new List<string>();
    static User currentUser;
    static void Main(string[] args)
    {
        while (true)
        {
            Console.WriteLine("\n");
            Console.WriteLine("----------------------------------------------------------------------------------------------------");
            Console.WriteLine("|                            DATING APPLICATION | COMPATABILITY TEST                               |");
            Console.WriteLine("----------------------------------------------------------------------------------------------------");
            Console.WriteLine("");
            Login();
            Console.WriteLine("COMPATABILITY TEST: ANSWER WITH HONESTY!\n");
            Console.WriteLine("1. Favourite Fruit");
            Console.WriteLine("a. Mango");
            Console.WriteLine("b. Banana");
            Console.WriteLine("c. Watermelon");
            Console.WriteLine("d. Papaya");
            currentUser.favouriteFruit = GetUserChoice("Enter your favourite fruit (a-d): ");
            Console.WriteLine("");
            Console.WriteLine("2. Favourite Place");
            Console.WriteLine("a. Museum");
            Console.WriteLine("b. Park");
            Console.WriteLine("c. School");
            Console.WriteLine("d. Mall");
            currentUser.favouritePlace = GetUserChoice("Enter your favourite place (a-d): ");
            Console.WriteLine("");
            Console.WriteLine("3. Favourite Color");
            Console.WriteLine("a. Yellow");
            Console.WriteLine("b. Blue");
            Console.WriteLine("c. White");
            Console.WriteLine("d. Violet");
            currentUser.favouriteColor = GetUserChoice("Enter your favourite color (a-d): ");
            Console.WriteLine("");
            Console.WriteLine("4. Hobby");
            Console.WriteLine("a. Singing");
            Console.WriteLine("b. Dancing");
            Console.WriteLine("c. Eating");
            Console.WriteLine("d. Watching");
            currentUser.hobby = GetUserChoice("Enter your hobby (a-d): ");
            Console.WriteLine("");
            Console.WriteLine("5. Favourite Animal");
            Console.WriteLine("a. Dog");
            Console.WriteLine("b. Cat");
            Console.WriteLine("c. Fish");
            Console.WriteLine("d. Monkey");
            currentUser.favouriteAnimal = GetUserChoice("Enter your favourite animal (a-d): ");
            Console.WriteLine("\n");
            Console.WriteLine("-----------------------------------------");
            Console.WriteLine("|          INFORMATION SAVED!           |");
            Console.WriteLine("-----------------------------------------");
            Console.WriteLine("\n");
            users.Add(currentUser);
            Console.WriteLine("DO YOU WANT TO:");
            Console.WriteLine("--------------------------------------- ");
            Console.WriteLine("1. INPUT NEW USER");
            Console.WriteLine("2. TEST COMPABILITY WITH OTHER USER");
            Console.WriteLine("3. REMOVE USER");
            Console.WriteLine("4. EXIT");
            int choice = int.Parse(Console.ReadLine());
            switch (choice)
            {
                case 1:
                    currentUser = null;
                    break;
                case 2:
                    TestCompatibility();
                    break;
                case 3:
                    RemoveUser();
                    break;
                case 4:
                    Console.WriteLine("--------------------------------------------");
                    Console.WriteLine("|THANK YOU FOR USING OUR DATING APPLICATION|");
                    Console.WriteLine("--------------------------------------------");
                    Environment.Exit(0);
                    break;
                default:
                    Console.WriteLine("***** INVALID CHOICE ***** \n");
                    break;
            }
        }
    }

    static void Login()
    {
        Console.WriteLine("LOGIN YOUR EXISTING ACCOUNT OR REGISTER NEW ACCOUNT");
        Console.WriteLine("1. LOGIN   ");
        Console.WriteLine("2. REGISTER");
        int choice = int.Parse(Console.ReadLine());
        if (choice == 1)
        {
            Console.Write("USERNAME: ");
            string username = Console.ReadLine();
            Console.Write("PASSWORD: ");
            string password = Console.ReadLine();
            foreach (User user in users)
            {
                if (user.username == username && user.password == password)
                {
                    currentUser = user;
                    Console.WriteLine("");
                    Console.WriteLine("----------------------------------------------");
                    Console.WriteLine("|             LOGIN SUCCESSFULLY             |");
                    Console.WriteLine("----------------------------------------------");
                    Console.WriteLine("");
                    return;
                }
            }
            Console.WriteLine("***** INVALID USERNAME OR PASSWORD. LOGIN AGAIN. *****\n");
            Login();

        }
        else if (choice == 2)
        {
            Console.Write("ENTER YOUR NEW USERNAME: ");
            string username = Console.ReadLine();
            Console.Write("ENTER YOUR NEW PASSWORD: ");
            string password = Console.ReadLine();
            User newUser = new User(username, password);
            usernames.Add(username);
            Console.WriteLine("");
            Console.WriteLine("----------------------------------------------");
            Console.WriteLine("|             ACCOUNT REGISTERED             |");
            Console.WriteLine("----------------------------------------------");
            Console.WriteLine("");
            currentUser = newUser;
        }
        else
        {
            Console.WriteLine("***** INVALID CHOICE *****\n");
            Login();
        }
    }

    static string GetUserChoice(string prompt)
    {
        while (true)
        {
            Console.Write(prompt);
            string choice = Console.ReadLine().ToLower();
            if (choice == "a" || choice == "b" || choice == "c" || choice == "d")
            {
                return choice;
            }
            else
            {
                Console.WriteLine("***** INVALID CHOICE, CHOOSE FROM LETTER (a-d) ***** \n");
            }
        }
    }


    static void TestCompatibility()
    {
        Console.Write("ENTER YOUR DESIRED USERNAME: ");
        string username = Console.ReadLine();
        User secondUser = null;
        if (checkAcc(username))
        {
            foreach (User user in users)
            {
                if (user.username == username)
                {
                    secondUser = user;
                }
            }

            if (secondUser == null)
            {
                Console.WriteLine("***** USER NOT FOUND ***** \n");
                return;
            }

            int matches = 0;

            if (currentUser.favouriteFruit == secondUser.favouriteFruit)
            {
                matches++;
            }
            if (currentUser.favouritePlace == secondUser.favouritePlace)
            {
                matches++;
            }
            if (currentUser.favouriteColor == secondUser.favouriteColor)
            {
                matches++;
            }
            if (currentUser.hobby == secondUser.hobby)
            {
                matches++;
            }
            if (currentUser.favouriteAnimal == secondUser.favouriteAnimal)
            {
                matches++;
            }

            if (matches >= 3)
            {
                Console.WriteLine("");
                Console.WriteLine("----------------------------------------------");
                Console.WriteLine("|              YOU'RE COMPATIBLE             |");
                Console.WriteLine("----------------------------------------------");
                Console.WriteLine("");
                Console.WriteLine("WANT TO MEET UP? ");
                Console.WriteLine("--------------------------------------- ");
                Console.WriteLine("A. YES PLEASE ");
                Console.WriteLine("B. MAYBE NEXT TIME!");
                string choice = Console.ReadLine().ToLower();
                if (choice == "a")
                {
                    Console.WriteLine("");
                    Console.WriteLine("MEET UP DETAILS");
                    Console.WriteLine("-----------------------------------");
                    Console.WriteLine("MEET UP PLACE: BIÑAN PLAZA");
                    Console.WriteLine("MEET UP TIME : 9:00 PM");
                    Console.WriteLine("MEET UP DATE : MARCH 1, 2023 \n");
                    Console.WriteLine("WANT TO HIRE PHOTOGRAPHER? ");
                    Console.WriteLine("MODE OF PAYMENT (A) GCASH - 09217376108 (B) CASH - GIVE IT TO THE PHOTOGRAPHER");
                    Console.WriteLine("-----------------------------------");
                    Console.WriteLine("1 HOUR   - P 100.00");
                    Console.WriteLine("2 HOURS  - P 200.00");
                    Console.WriteLine("24 HOURS - P 1000.00 (GREAT DEAL)");
                    Console.WriteLine("-----------------------------------");
                    Console.WriteLine("A. I WOULD LOVE TO!");
                    Console.WriteLine("B. NAH! I CAN DO IT!");
                    string letter = Console.ReadLine().ToLower();
                    if (letter == "a")
                    {
                        Console.WriteLine("");
                        Console.WriteLine("PHOTOGRAPHER DETAILS");
                        Console.WriteLine("-----------------------------------");
                        Console.WriteLine("NAME       : SALMA FAE LUMAOANG");
                        Console.WriteLine("CONTACT NO.: 09123456789");
                        Console.WriteLine("");
                        Console.WriteLine("----------------------------------------------");
                        Console.WriteLine("| THANK YOU FOR USING OUR DATING APPLICATION |");
                        Console.WriteLine("----------------------------------------------");
                    }
                    else if (letter == "b")
                    {
                        Console.WriteLine("OH! YOU WANT TO BE ALONE! GOODLUCK ON YOUR FIRST MEET UP !");
                        Console.WriteLine("");
                        Console.WriteLine("----------------------------------------------");
                        Console.WriteLine("| THANK YOU FOR USING OUR DATING APPLICATION |");
                        Console.WriteLine("----------------------------------------------");
                    }
                }

                else if (choice == "b")
                {
                    Console.WriteLine("BEING SINGLE IS NOT BAD, WHY DON'T YOU GIVE IT A SHOT?");
                }

            }

            else
            {
                Console.WriteLine("");
                Console.WriteLine("----------------------------------------------");
                Console.WriteLine("|            YOU'RE NOT COMPATIBLE           |");
                Console.WriteLine("----------------------------------------------");
                Console.WriteLine("");
                Console.WriteLine("WHY DONT YOU TRY IT AGAIN?");
                Console.WriteLine("----------------------------------------------");
                Console.WriteLine("1. TRY AGAIN! ");
                Console.WriteLine("2. NAH! NEXT TIME! ");
                int choice = int.Parse(Console.ReadLine());
                if (choice == 1)
                {
                    TestCompatibility();
                }
                else if (choice == 2)
                {
                    Console.WriteLine("");
                    Console.WriteLine("----------------------------------------------");
                    Console.WriteLine("| THANK YOU FOR USING OUR DATING APPLICATION |");
                    Console.WriteLine("----------------------------------------------");
                }
                else
                {
                    Console.WriteLine("***** INVALID CHOICE ***** \n");
                }
            }
        }
        else
        {
            Console.WriteLine("***** NO USER DATA *****");
        }



    }
    static void RemoveUser()
    {
        Console.Write("ENTER THE USERNAME YOU WANT TO REMOVE: ");
        string userName = Console.ReadLine();
        if (checkAcc(userName))
        {
            usernames.Remove(userName);
            Console.WriteLine("***** SUCCESSFULLY REMOVED! ***** \n");
        }
        else
        {
            Console.WriteLine("***** USER NOT FOUND ***** \n");
        }
    }

    static bool checkAcc(string name)
    {
        int found = usernames.IndexOf(name);
        if (found == -1)
        {
            return false;
        }
        else
        {
            return true;
        }
    }

}

