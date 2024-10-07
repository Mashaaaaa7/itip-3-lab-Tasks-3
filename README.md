# itip-3

Задача 1

import java.util.HashMap;
import java.util.Map;

class KeyValue {
    private String key;
    private String value; //значение

    public KeyValue(String key, String value) {
        this.key = key;
        this.value = value;
    }

    public String getKey() {
        return key;
    }

    public String getValue() {
        return value;
    }
}

public class HashTable {
    private HashMap<String, KeyValue> keyMap; // создает поле keyMap типа HashMap, которое
    // будет хранить пары ключ-значение.
    public HashTable() {
        keyMap = new HashMap<>();
    }

    public void put(String key, KeyValue value) {
        keyMap.put(key, value);
    }

    public KeyValue get(String key) {
        return keyMap.get(key);
    }

    public void remove(String key) {
        keyMap.remove(key);
    }
    public int size() {
        return keyMap.size();
    }

    public boolean isEmpty() {
        return keyMap.isEmpty();
    }

    public static void main(String[] args) {
        HashTable hashTable = new HashTable();
        hashTable.put("name", new KeyValue("name", "John Doe"));
        hashTable.put("age", new KeyValue("age", "30"));

        System.out.println("Размер таблицы: " + hashTable.size()); // Вывод: 2

        KeyValue value = hashTable.get("name");
        if (value != null) {
            System.out.println("Значение для ключа 'name': " + value.getValue()); // Вывод: John Doe
        } else {
            System.out.println("Ключ 'name' не найден.");
        }

        hashTable.remove("age");

        System.out.println("Размер таблицы: " + hashTable.size()); // Вывод: 1

        System.out.println("Пуста ли таблица: " + hashTable.isEmpty()); // Вывод: false
    }
}



Задача 2

import java.util.HashMap;

class Book { //определяет класс, который представляет книгу
    private String title;
    private String author;
    private int copies;

    public Book(String title, String author, int copies) { //инициализирует объект Book
        this.title = title;
        this.author = author;
        this.copies = copies;
    }


    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public int getCopies() {
        return copies;
    }

    // Метод для изменения количества копий
    public void setCopies(int copies) {
        this.copies = copies;
    }
}

public class Library {
    private HashMap<String, Book> bookMap; // Явное объявление HashMap

    public Library() {
        bookMap = new HashMap<>(); //создает поле bookMap типа HashMap, которое будет хранить книги с ключом ISBN.
    }

    public void addBook(String isbn, Book book) {
        bookMap.put(isbn, book); // Добавление
    }

    public Book findBook(String isbn) {
        return bookMap.get(isbn); // Поиск
    }

    public void removeBook(String isbn) {
        bookMap.remove(isbn); // Удаление
    }

    public static void main(String[] args) {
        Library library = new Library(); //создает объект Library

        // Добавление книг
        library.addBook("978-0143034231", new Book("1984", "George Orwell", 5));
        library.addBook("978-0141439501", new Book("Pride and Prejudice", "Jane Austen", 3));

        // Поиск книги
        Book foundBook = library.findBook("978-0143034231");
        if (foundBook != null) { //проверяет, найдена ли книга.
            System.out.println("Найдена книга: " + foundBook.getTitle() + " by " + foundBook.getAuthor());
        } else {
            System.out.println("Книга не найдена.");
        }

        // Удаление книги
        library.removeBook("978-0141439501");

        // Поиск удаленной книги
        foundBook = library.findBook("978-0141439501");
        if (foundBook != null) {
            System.out.println("Книга найдена.");
        } else {
            System.out.println("Книга не найдена.");
        }
    }
}
