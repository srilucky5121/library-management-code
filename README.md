class Book:
    def __init__(self, title, author, ISBN, available=True):
        self.title = title
        self.author = author
        self.ISBN = ISBN
        self.available = available

    def __str__(self):
        return f"{self.title} by {self.author} (ISBN: {self.ISBN})"

class Library:
    def __init__(self):
        self.books = []

    def add_book(self, book):
        self.books.append(book)

    def display_available_books(self):
        available_books = [book for book in self.books if book.available]
        if available_books:
            for book in available_books:
                print(book)
        else:
            print("No available books in the library.")

class Member:
    def __init__(self, name, member_id):
        self.name = name
        self.member_id = member_id
        self.borrowed_books = []

    def borrow_book(self, book):
        if book.available:
            book.available = False
            self.borrowed_books.append(book)
            print(f"{self.name} borrowed: {book}")
        else:
            print("Sorry, the book is currently not available.")

    def return_book(self, book):
        if book in self.borrowed_books:
            book.available = True
            self.borrowed_books.remove(book)
            print(f"{self.name} returned: {book}")
        else:
            print("This book was not borrowed by the member.")

# Example usage:
book1 = Book("To Kill a Mockingbird", "Harper Lee", "9780061120084")
book2 = Book("The Great Gatsby", "F. Scott Fitzgerald", "9780743273565")

library = Library()

library.add_book(book1)
library.add_book(book2)

member1 = Member("Alice", "001")
member2 = Member("Bob", "002")

member1.borrow_book(book1)
member2.borrow_book(book2)

library.display_available_books()

member1.return_book(book1)
library.display_available_books()
