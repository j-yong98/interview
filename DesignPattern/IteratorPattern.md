이터레이터 패턴
=
이터레이터 패턴이란?
-

- 이터레이터 패턴은 이터레이터를 사용하여 컬렉션 구현 방법을 노출시키지 않으면서도 접근하는 디자인 패턴입니다.
- 이를 통해 순회할 수 있는 여러 가지 자료형의 구조와는 상관없이 이터레이터라는 하나의 인터페이스로 순회가 가능합니다.

예제
-

~~~
public class Book{
    private String name;

    public Book(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

public interface Iter {
    Iterator createIterator();
}

public class BookShelfIterator implements Iterator<Book> {
    private BookShelf bookShelf;
    private int idx = 0;

    public BookShelfIterator(BookShelf bookShelf) {
        this.bookShelf = bookShelf;
    }

    @Override
    public boolean hasNext() {
        return idx < bookShelf.getLength();
    }

    @Override
    public Book next() {
        return bookShelf.getBooks(idx++);
    }
}
public class BookShelf implements Iter{
    private Book[] books;
    //맨 뒤의 책의 인덱스
    private int last = 0;

    public BookShelf(int size) {
        books = new Book[size];
    }

    public int getLength(){
        return last;
    }

    public Book getBooks(int idx) {
        return books[idx];
    }

    public void addBook(Book book) {
        if (last < books.length) {
            this.books[last++] = book;
            return;
        }
        System.out.println("공간이 없습니다!");
    }

    @Override
    public Iterator createIterator() {
        return new BookShelfIterator(this);
    }
}
~~~

~~~
public class Main {
    public static void main(String[] args) {
        BookShelf bookShelf = new BookShelf(10);
    
        Book book1 = new Book("클린 코드");
        Book book2 = new Book("면접을 위한 CS 전공지식 노트");
    
        System.out.println("현재 꽂혀있는 책의 개수 : " + bookShelf.getLength());
        Iterator iterator = bookShelf.createIterator();
        while (iterator.hasNext()) {
            Book book = (Book) iterator.next();
            System.out.println(book.getName());
    }
}
~~~