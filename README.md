# Library_Manegement_System
package whileloop;

import java.util.*;

public class Library_Manegement_System {
    private static final Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        Library lib = new Library();


        lib.addBook("1984", "George Orwell");
        lib.addBook("The Hobbit", "J.R.R. Tolkien");
        lib.registerMember("Alice");
        lib.registerMember("Bob");

        while (true) {
            printMenu();
            String choice = sc.nextLine().trim();
            switch (choice) {
                case "1": addBook(lib); break;
                case "2": listBooks(lib); break;
                case "3": searchBooks(lib); break;
                case "4": registerMember(lib); break;
                case "5": listMembers(lib); break;
                case "6": borrowBook(lib); break;
                case "7": returnBook(lib); break;
                case "8": listBorrowed(lib); break;
                case "9": System.out.println("Exiting..."); return;
                default: System.out.println("Invalid option, try again.");
            }
            System.out.println();
        }
    }

    private static void printMenu() {
        System.out.println("=== Library Management System ===");
        System.out.println("1. Add book");
        System.out.println("2. List all books");
        System.out.println("3. Search books by title");
        System.out.println("4. Register member");
        System.out.println("5. List members");
        System.out.println("6. Borrow book");
        System.out.println("7. Return book");
        System.out.println("8. List borrowed books");
        System.out.println("9. Exit");
        System.out.print("Choose an option: ");
    }

    private static void addBook(Library lib) {
        System.out.print("Title: ");
        String title = sc.nextLine().trim();
        System.out.print("Author: ");
        String author = sc.nextLine().trim();
        Book b = lib.addBook(title, author);
        System.out.println("Added: " + b);
    }

    private static void listBooks(Library lib) {
        System.out.println("Books:");
        for (Book b : lib.listAllBooks()) System.out.println("  " + b);
    }

    private static void searchBooks(Library lib) {
        System.out.print("Search query: ");
        String q = sc.nextLine().trim();
        List<Book> res = lib.searchByTitle(q);
        if (res.isEmpty()) System.out.println("No books found.");
        else for (Book b : res) System.out.println("  " + b);
    }

    private static void registerMember(Library lib) {
        System.out.print("Member name: ");
        String name = sc.nextLine().trim();
        Member m = lib.registerMember(name);
        System.out.println("Registered: " + m);
    }

    private static void listMembers(Library lib) {
        System.out.println("Members:");
        for (Member m : lib.listAllMembers()) System.out.println("  " + m);
    }

    private static void borrowBook(Library lib) {
        try {
            System.out.print("Book ID to borrow: ");
            int bid = Integer.parseInt(sc.nextLine().trim());
            System.out.print("Member ID: ");
            int mid = Integer.parseInt(sc.nextLine().trim());
            boolean ok = lib.borrowBook(bid, mid);
            System.out.println(ok ? "Borrowed successfully." : "Could not borrow (check IDs or already borrowed).");
        } catch (NumberFormatException ex) {
            System.out.println("Invalid number.");
        }
    }

    private static void returnBook(Library lib) {
        try {
            System.out.print("Book ID to return: ");
            int bid = Integer.parseInt(sc.nextLine().trim());
            System.out.print("Member ID: ");
            int mid = Integer.parseInt(sc.nextLine().trim());
            boolean ok = lib.returnBook(bid, mid);
            System.out.println(ok ? "Returned successfully." : "Could not return (check IDs and borrower).");
        } catch (NumberFormatException ex) {
            System.out.println("Invalid number.");
        }
    }

    private static void listBorrowed(Library lib) {
        List<String> list = lib.listBorrowed();
        if (list.isEmpty()) System.out.println("No borrowed books.");
        else for (String s : list) System.out.println("  " + s);
    }
}
