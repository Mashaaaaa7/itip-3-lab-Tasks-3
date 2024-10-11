# itip-3

Задача 1

import java.util.HashMap;

class KeyValue { //представляет пару ключ-значение
    private String key;
    private String value;

    public KeyValue(String key, String value) { //хранит ключ и значение
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

public class Entry  {
    private HashMap<String, KeyValue> keyMap; //создает поле keyMap типа HashMap, которое будет хранить пары ключ-значение

    public Entry() {
        keyMap = new HashMap<>(); //инициализирует keyMap пустым HashMap.
    }

    public void put(String key, KeyValue value) { //добавляет пару ключ-значение в таблицу.
        keyMap.put(key, value);
    }

    public KeyValue get(String key) { //возвращает объект KeyValue, связанный с указанным ключом. Не найден=null
        return keyMap.get(key);
    }

    public void remove(String key) {
        keyMap.remove(key);
    }

    public int size() { //количество
        return keyMap.size();
    }

    public boolean isEmpty() { //пустая таблица
        return keyMap.isEmpty();
    }

    //*В методе main создается объект HashTable, добавляются пары ключ-значение, выводится размер таблицы,
    // и выводится результат проверки на пустоту таблицы.

    public static void main(String[] args) {
        Entry Entry  = new Entry(); //создает объект
        Entry.put("name", new KeyValue("name", "George Doe"));
        Entry.put("age", new KeyValue("age", "21"));

        System.out.println("Размер таблицы: " + Entry.size());

        KeyValue value = Entry.get("name"); //получение значения по ключу name
        if (value != null) {  //проверяет, найдено ли значение.
            System.out.println("Значение для ключа 'name': " + value.getValue());
        } else {
            System.out.println("Ключ 'name' не найден.");
        }

         value = Entry.get("age"); //получение значения по ключу age
        if (value != null) {  //проверяет, найдено ли значение
            System.out.println("Значение для ключа 'age': " + value.getValue());
        } else {
            System.out.println("Ключ 'age' не найден.");
        }

        Entry.remove("name"); //удаляет пару по ключу “name”
        Entry.remove("age"); //удаляет пару по ключу “age”

        System.out.println("Размер таблицы: " + Entry.size());
        System.out.println("Пуста ли таблица: " + Entry.isEmpty());
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

public class Library { //определяет класс Библиотека
    private HashMap<String, Book> bookMap; // Явное объявление HashMap

    public Library() {
        bookMap = new HashMap<>(); //создает поле bookMap типа HashMap, которое будет хранить книги с ключом ISBN.
    }

    public void addBook(String isbn, Book book) {
        bookMap.put(isbn, book); // Добавление книги в хэш-таблиц
    }

    public Book findBook(String isbn) {
        return bookMap.get(isbn);
    }

    public void removeBook(String isbn) {
        bookMap.remove(isbn);
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

        Book foundBook2 = library.findBook("978-0141439501");
        if (foundBook2 != null) {
            System.out.println("Найдена книга: " + foundBook2.getTitle() + " by " + foundBook2.getAuthor());
        } else {
            System.out.println("Книга не найдена.");
        }

        // Удаление книги
        library.removeBook("978-0141439501");
        library.removeBook("978-0141439501");

        // Поиск удаленной книги
        foundBook = library.findBook("978-0141439501");
        if (foundBook != null) {
            System.out.println("Книга найдена.");
        } else {
            System.out.println("Книга не найдена.");
        }

        foundBook2 = library.findBook("978-0141439501");
        if (foundBook2 != null) {
            System.out.println("Книга найдена.");
        } else {
            System.out.println("Книга не найдена.");
        }
    }
}
