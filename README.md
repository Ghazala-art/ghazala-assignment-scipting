# Library Management System

# Initialize book records as a list of dictionaries
books = [
    # Example book
    {"title": "The Great Gatsby", "author": "F. Scott Fitzgerald", "ISBN": "123456789", "available": True},
    {"title": "1984", "author": "George Orwell", "ISBN": "987654321", "available": True}
]

# Function to display the menu
def display_menu():
    print("\nLibrary Management System")
    print("1. Add Book")
    print("2. Remove Book")
    print("3. Search Book")
    print("4. Check Out Book")
    print("5. Check In Book")
    print("6. List Books")
    print("7. Exit")

# Function to add a book
def add_book():
    title = input("Enter book title: ")
    author = input("Enter book author: ")
    ISBN = input("Enter book ISBN: ")

    # Check if the book already exists
    for book in books:
        if book["ISBN"] == ISBN:
            print("Book already exists.")
            return

    # Add the book
    books.append({"title": title, "author": author, "ISBN": ISBN, "available": True})
    print("Book added successfully.")

# Function to remove a book
def remove_book():
    ISBN = input("Enter ISBN of the book to remove: ")

    # Find and remove the book
    for book in books:
        if book["ISBN"] == ISBN:
            books.remove(book)
            print("Book removed.")
            return
    
    print("Book not found.")

# Function to search for a book
def search_book():
    search_term = input("Enter search term (title, author, or ISBN): ")

    # Search for the book
    found_books = [book for book in books if search_term.lower() in book["title"].lower() or search_term.lower() in book["author"].lower() or search_term in book["ISBN"]]

    if found_books:
        print("Matching books:")
        for book in found_books:
            print(f"Title: {book['title']}, Author: {book['author']}, ISBN: {book['ISBN']}, Available: {'Yes' if book['available'] else 'No'}")
    else:
        print("No matching books found.")

# Function to check out a book
def check_out_book():
    ISBN = input("Enter ISBN of the book to check out: ")

    # Find the book by ISBN
    for book in books:
        if book["ISBN"] == ISBN:
            if book["available"]:
                book["available"] = False
                print("Book checked out.")
                return
            else:
                print("Book not available.")
                return
    
    print("Book not found.")

# Function to check in a book
def check_in_book():
    ISBN = input("Enter ISBN of the book to check in: ")

    # Find the book by ISBN
    for book in books:
        if book["ISBN"] == ISBN:
            book["available"] = True
            print("Book checked in.")
            return
    
    print("Book not found.")

# Function to list all books
def list_books():
    if books:
        print("All Books:")
        for book in books:
            print(f"Title: {book['title']}, Author: {book['author']}, ISBN: {book['ISBN']}, Available: {'Yes' if book['available'] else 'No'}")
    else:
        print("No books available.")

# Main loop
def main():
    while True:
        display_menu()
        try:
            choice = int(input("Enter your choice: "))
        except ValueError:
            print("Invalid input. Please enter a number between 1 and 7.")
            continue

        if choice == 1:
            add_book()
        elif choice == 2:
            remove_book()
        elif choice == 3:
            search_book()
        elif choice == 4:
            check_out_book()
        elif choice == 5:
            check_in_book()
        elif choice == 6:
            list_books()
        elif choice == 7:
            print("Exiting the system...")
            break
        else:
            print("Invalid choice. Try again.")

if __name__ == "__main__":
    main()
