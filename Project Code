#include <iostream>
#include <fstream>
#include <string>

using namespace std;

const int MAX_BOOKS = 100; 

struct Book {
    string title;
    string author;
    string ISBN;
    bool isAvailable;
};

Book books[MAX_BOOKS];
int numBooks = 0;

void loadBooksFromFile() 
{
    ifstream file("books.txt");
    if (file.is_open()) 
	{
        int i = 0;
        while (file >> books[i].title >> books[i].author >> books[i].ISBN >> books[i].isAvailable && i < MAX_BOOKS) 
		{
            i++;
        }
        numBooks = i;
        file.close();
    }
}

void saveBooksToFile() {
    ofstream file("books.txt");
    if (file.is_open()) {
        for (int i = 0; i < numBooks; ++i) {
            file << books[i].title << " " << books[i].author << " " << books[i].ISBN << " " << books[i].isAvailable << endl;
        }
        file.close();
    }
}

void addBook() {
    if (numBooks < MAX_BOOKS) {
        cout << "Enter book title: ";
        getline(cin, books[numBooks].title);
        cout << "Enter author: ";
        getline(cin, books[numBooks].author);
        cout << "Enter ISBN: ";
        getline(cin, books[numBooks].ISBN);
        books[numBooks].isAvailable = true;
        numBooks++;
        saveBooksToFile();
    } else {
        cout << "Maximum number of books reached." << endl;
    }
}

void removeBook() {
    string ISBN;
    cout << "Enter ISBN of the book to remove: ";
    getline(cin, ISBN);
    for (int i = 0; i < numBooks; ++i) {
        if (books[i].ISBN == ISBN) {
            for (int j = i; j < numBooks - 1; ++j) {
                books[j] = books[j + 1];
            }
            numBooks--;
            saveBooksToFile();
            cout << "Book removed successfully." << endl;
            return;
        }
    }
    cout << "Book not found." << endl;
}

void updateBook() {
    string ISBN;
    cout << "Enter ISBN of the book to update: ";
    getline(cin, ISBN);
    for (int i = 0; i < numBooks; ++i) {
        if (books[i].ISBN == ISBN) {
            cout << "Enter new title: ";
            getline(cin, books[i].title);
            cout << "Enter new author: ";
            getline(cin, books[i].author);
            saveBooksToFile();
            cout << "Book updated successfully." << endl;
            return;
        }
    }
    cout << "Book not found." << endl;
}

void borrowBook() {
    string ISBN;
    cout << "Enter ISBN of the book to borrow: ";
    getline(cin, ISBN);
    for (int i = 0; i < numBooks; ++i) {
        if (books[i].ISBN == ISBN && books[i].isAvailable) {
            books[i].isAvailable = false; 
            saveBooksToFile(); 
            cout << "Book borrowed successfully." << endl;
            return; 
        }
    }
    cout << "Book not available or not found." << endl; 
}

void returnBook() {
    string ISBN;
    cout << "Enter ISBN of the book to return: ";
    getline(cin, ISBN);
    for (int i = 0; i < numBooks; ++i) {
        if (books[i].ISBN == ISBN && !books[i].isAvailable) {
            books[i].isAvailable = true;
            saveBooksToFile();
            cout << "Book returned successfully." << endl;
            return;
        }
    }
    cout << "Book not found or not borrowed." << endl;
}

void displayBooks() {
    cout << "Available Books:" << endl;
    for (int i = 0; i < numBooks; ++i) {
        if (books[i].isAvailable) {
            cout << "Title: " << books[i].title << endl;
            cout << "Author: " << books[i].author << endl;
            cout << "ISBN: " << books[i].ISBN << endl;
            cout << "--------------------" << endl;
        }
    }
}

int main() {
    loadBooksFromFile();

    int choice;
    do {
        cout << "\nLibrary Management System\n";
        cout << "1. Add Book\n";
        cout << "2. Remove Book\n";
        cout << "3. Update Book\n";
        cout << "4. Borrow Book\n";
        cout << "5. Return Book\n";
        cout << "6. Display Books\n";
        cout << "7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore(); // Clear newline character

        switch (choice) {
            case 1:
                addBook();
                break;
            case 2:
                removeBook();
                break;
            case 3:
                updateBook();
                break;
            case 4:
                borrowBook();
                break;
            case 5:
                returnBook();
                break;
            case 6:
                displayBooks();
                break;
            case 7:
                cout << "Exiting..." << endl;
                break;
            default:
                cout << "Invalid choice." << endl;
        }
    } while (choice != 7);

    return 0;
}
