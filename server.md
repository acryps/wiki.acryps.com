# Server
When creating API Endpoints with extended services from **vlserver** a certain method order has to be met.

This rule applies for services as well as managers if an additional layer is required. Use Managers if the application (or a single endpoint) reaches a size where it feels right to separate logic into multiple layers.

| | |
:-- | :--
Services | Authentication, Authorization, ViewModel <-> DatabaseModel conversion
Manager | Vlquery, Data calculations, Mailing, Logging, ...

## Basic
The methods in a service and a manager should follow this order:
1. Get multiple
2. Get single
3. Create
4. Update
5. Delete
7. Private helpers

```ts
export class BookService extends Service {
	getBooks() {}

	getBook(id: string) {}

	createBook(book: BookViewModel) {}

	updateBook(book: BookViewModel) {}

	updateBookState(id: string, state: BookStateViewModel) {}

	deleteBook(id: string) {}

	// Preload thumbnail for a book
	// Used in getBooks and getBook therefore extracted into a private helper
	private getThumbnail(bookId: string): Blob {}
}
```

## Exceptions
Sooner or later, this pattern is bound to stumble upon exceptions. Handle them as follows:
Exception | Solution
:-- | :--
Manipulation of another table | Books have a state column referencing another table (available, rented, reserved). Now it is better to implement `getBookStates` inside the book endpoint instead of creating a new one. But the moment there are multiple methods creating book states and more this has to be extracted into a new endpoint to enhance readability.
Complex manipulation | If a method can't be determined as any of the CRUD methods just apply them between the delete methods and private helpers.

```ts
export class BookService extends Service {
	getBooks() {}

	// Manipulation of another table
	getBookStates() {}

	getBook(id: string) {}

	createBook(book: BookViewModel) {}

	updateBook(book: BookViewModel) {}

	updateBookState(id: string, state: BookStateViewModel) {}

	deleteBook(id: string) {}

	// Complex manipulation
	rentBook(id: string, renter: UserViewModel) {
		// User can only rent 5 books at the same time
		// If user exceeded limit notify user and show their rented books
	}

	// Complex manipulation
	prepareInventoryCheck() {
		// The library has to do an inventory check. All books must be returned
		// Remove all reservations
		// If book is rented notify the users via email and in-app message
	}

	private getThumbnail(bookId: string): Blob {}
}
```