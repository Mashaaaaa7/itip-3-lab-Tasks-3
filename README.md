# itip-3

Задача 1

import java.util.LinkedList;
import java.util.Objects;

public class HashTable<K, V> {

    private static class Entry<K, V> {

        private final K key;
        private V value;
        public Entry(K key, V value) {
            this.key = key;
            this.value = value;
        }

        public K getKey() {
            return key;
        }

        public V getValue() {
            return value;
        }

        public void setValue(V value) {
            this.value = value;
        }

        @Override
        public boolean equals(Object obj) {

            if (this == obj) {
                return true;
            }

            if (!(obj instanceof Entry<?, ?> entry)) {
                return false;
            }

            return Objects.equals(getKey(), entry.getKey());
        }

        @Override
        public int hashCode() {
            return Objects.hash(getKey());
        }

    }

    private LinkedList<Entry<K, V>>[] table;
    private int size;

    public HashTable(int capacity) {
        table = new LinkedList[capacity];
        size = 0;
    }

    private int hash(K key) {
        return Math.abs(Objects.hashCode(key)) % table.length;
    }

    public void put(K key, V value) {

        int index = hash(key);

        if (table[index] == null) {
            table[index] = new LinkedList<>();
        }

        for (Entry<K, V> entry : table[index]) {
            if (entry.getKey().equals(key)) {
                entry.setValue(value);
                return;
            }
        }

        table[index].add(new Entry<>(key, value));
        size++;

    }

    public V get(K key) {

        int index = hash(key);

        LinkedList<Entry<K, V>> bucket = table[index];

        if (bucket != null) {
            for (Entry<K, V> entry : bucket) {
                if (entry.getKey().equals(key)) {
                    return entry.getValue();
                }
            }
        }

        return null;
    }

    public V remove(K key) {

        int index = hash(key);

        LinkedList<Entry<K, V>> bucket = table[index];

        if (bucket != null) {
            for (Entry<K, V> entry : bucket) {
                if (entry.getKey().equals(key)) {
                    V removedValue = entry.getValue();
                    bucket.remove(entry);
                    size--;
                    return removedValue;
                }
            }
        }

        return null;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
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
