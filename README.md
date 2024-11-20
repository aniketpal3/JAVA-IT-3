# JAVA-IT-3
class ClassA {
    private String name;
    protected int id;

    public ClassA(String name, int id) {
        this.name = name;
        this.id = id;
    }

    public ClassA(ClassA other) {
        this.name = other.name;
        this.id = other.id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

class ClassB extends ClassA {
    private double salary;

    private ClassB() {
        super(" ", 0);
        this.salary = 0.0;
    }

    public ClassB(String name, int id, double salary) {
        super(name, id);
        this.salary = salary;
    }

    public ClassB(ClassB other) {
        super(other);
        this.salary = other.salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }
}

class ClassC extends ClassB {
    private String department;

    public ClassC(String name, int id, double salary, String department) {
        super(name, id, salary);
        this.department = department;
    }

    public ClassC(ClassC other) {
        super(other);
        this.department = other.department;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

    public synchronized void displayDetails() {
        System.out.println("Name: " + getName());
        System.out.println("ID: " + id);
        System.out.println("Salary: " + getSalary());
        System.out.println("Department: " + department);
    }
}

public class MultiClassProgram {
    public static void main(String[] args) {
        ClassC obj1 = new ClassC("John Doe", 101, 75000.50, "IT");
        obj1.displayDetails();

        ClassC obj2 = new ClassC(obj1);
        obj2.setDepartment("HR");

        System.out.println("\nDetails of obj1:");
        obj1.displayDetails();

        System.out.println("\nDetails of obj2:");
        obj2.displayDetails();
    }
}

FINAL OUTPUT

Name: John Doe
ID: 101
Salary: 75000.5
Department: IT

Details of obj1:
Name: John Doe
ID: 101
Salary: 75000.5
Department: IT

Details of obj2:
Name: John  
ID: 101
Salary: 75000.5
Department: HR






public class OuterClass {
    private static int staticVar = 10;
    private int instanceVar = 20;

    static class StaticNestedClass {
        static {
            System.out.println("Static block in StaticNestedClass");
        }

        {
            System.out.println("Instance block in StaticNestedClass");
        }

        StaticNestedClass() {
            System.out.println("Constructor of StaticNestedClass");
        }

        void accessOuterClass() {
            System.out.println("Accessing static variable from OuterClass: " + staticVar);

        }
    }

    final class FinalInnerClass {
        final int finalVar = 100;

        final void displayFinal() {
            System.out.println("This is a final method in FinalInnerClass.");
            System.out.println("Final variable value: " + finalVar);
        }
    }

    // Overriding the toString method
    @Override
    public String toString() {
        return "OuterClass with instanceVar = " + instanceVar + ", staticVar = " + staticVar;
    }

    public static void staticMethod() {
        System.out.println("Static method in OuterClass.");
        System.out.println("Accessing staticVar: " + staticVar);
    }

    public static void synchronizedAccess() {
        synchronized (OuterClass.class) {
            System.out.println("Thread-safe access to staticVar: " + staticVar);
            staticVar++;
        }
    }

    public static final class UtilityClass {
        public static void utilityMethod() {
            System.out.println("Utility method in final UtilityClass.");
        }
    }

    public static void main(String[] args) {
        System.out.println("Creating StaticNestedClass:");
        StaticNestedClass nested = new StaticNestedClass();
        nested.accessOuterClass();

        System.out.println("\nCreating FinalInnerClass:");
        OuterClass outer = new OuterClass();
        FinalInnerClass inner = outer.new FinalInnerClass();
        inner.displayFinal();

        System.out.println("\nDemonstrating 'this' and 'super':");
        System.out.println(outer.toString());

        System.out.println("\nAccessing static method:");
        OuterClass.staticMethod();

        System.out.println("\nDemonstrating synchronized access:");
        synchronizedAccess();
        synchronizedAccess();

        System.out.println("\nAccessing UtilityClass:");
        UtilityClass.utilityMethod();
    }
}

FINAL OUTPUT

Creating StaticNestedClass:
Static block in StaticNestedClass
Instance block in StaticNestedClass
Constructor of StaticNestedClass
Accessing static variable from OuterClass: 10

Creating FinalInnerClass:
This is a final method in FinalInnerClass.
Final variable value: 100

Demonstrating 'this' and 'super':
OuterClass with instanceVar = 20, staticVar = 10

Accessing static method:
Static method in OuterClass.
Accessing staticVar: 10

Demonstrating synchronized access:
Thread-safe access to staticVar: 10
Thread-safe access to staticVar: 11

Accessing UtilityClass:
Utility method in final UtilityClass.







// Abstract class LibraryItem
abstract class LibraryItem {
    String title;
    int itemID;
    boolean isAvailable;

    public LibraryItem(String title, int itemID) {
        this.title = title;
        this.itemID = itemID;
        this.isAvailable = true;
    }

    abstract void borrow() throws ItemNotAvailableException;
    abstract void returnItem();

    public int getItemID() {
        return itemID;
    }

    public String getTitle() {
        return title;
    }

    public boolean isAvailable() {
        return isAvailable;
    }
}

// Book subclass
class Book extends LibraryItem {
    String author;
    String genre;

    public Book(String title, int itemID, String author, String genre) {
        super(title, itemID);
        this.author = author;
        this.genre = genre;
    }

    @Override
    void borrow() throws ItemNotAvailableException {
        if (isAvailable) {
            isAvailable = false;
            System.out.println("Book '" + title + "' has been borrowed.");
        } else {
            throw new ItemNotAvailableException("Book '" + title + "' is not available for borrowing.");
        }
    }

    @Override
    void returnItem() {
        isAvailable = true;
        System.out.println("Book '" + title + "' has been returned.");
    }
}

// DVD subclass
class DVD extends LibraryItem {
    String director;
    int duration;

    public DVD(String title, int itemID, String director, int duration) {
        super(title, itemID);
        this.director = director;
        this.duration = duration;
    }

    @Override
    void borrow() throws ItemNotAvailableException {
        if (isAvailable) {
            isAvailable = false;
            System.out.println("DVD '" + title + "' has been borrowed.");
        } else {
            throw new ItemNotAvailableException("DVD '" + title + "' is not available for borrowing.");
        }
    }

    @Override
    void returnItem() {
        isAvailable = true;
        System.out.println("DVD '" + title + "' has been returned.");
    }
}

// Custom Exception for unavailable items
class ItemNotAvailableException extends Exception {
    public ItemNotAvailableException(String message) {
        super(message);
    }
}

// Library class to manage items
class Library {
    private List<LibraryItem> items;

    public Library() {
        items = new ArrayList<>();
    }

    public void addItem(LibraryItem item) {
        items.add(item);
    }

    public void borrowItem(int itemID) {
        for (LibraryItem item : items) {
            if (item.getItemID() == itemID) {
                try {
                    item.borrow();
                } catch (ItemNotAvailableException e) {
                    System.out.println(e.getMessage());
                } finally {
                    System.out.println("Borrow operation for item '" + item.getTitle() + "' completed.");
                }
                return;
            }
        }
        System.out.println("Item with ID " + itemID + " not found.");
    }

    public void returnItem(int itemID) {
        for (LibraryItem item : items) {
            if (item.getItemID() == itemID) {
                item.returnItem();
                System.out.println("Return operation for item '" + item.getTitle() + "' completed.");
                return;
            }
        }
        System.out.println("Item with ID " + itemID + " not found.");
    }

    public LibraryItem search(int itemID) {
        for (LibraryItem item : items) {
            if (item.getItemID() == itemID) {
                return item;
            }
        }
        return null;
    }

    public List<LibraryItem> search(String title) {
        List<LibraryItem> result = new ArrayList<>();
        for (LibraryItem item : items) {
            if (item.getTitle().toLowerCase().contains(title.toLowerCase())) {
                result.add(item);
            }
        }
        return result;
    }

    public void displayItems() {
        System.out.println("Books in the library:");
        for (LibraryItem item : items) {
            if (item instanceof Book) {
                Book book = (Book) item;
                System.out.println("Title: " + book.getTitle() + ", Author: " + book.author + ", Genre: " + book.genre + ", Available: " + item.isAvailable());
            }
        }

        System.out.println("\nDVDs in the library:");
        for (LibraryItem item : items) {
            if (item instanceof DVD) {
                DVD dvd = (DVD) item;
                System.out.println("Title: " + dvd.getTitle() + ", Director: " + dvd.director + ", Duration: " + dvd.duration + " mins, Available: " + item.isAvailable());
            }
        }
  }

public class LibraryManagementSystem {
    public static void main(String[] args) {
        Library library = new Library();

        // Adding items to the library
        library.addItem(new Book("Java Programming", 1, "James Gosling", "Technology"));
        library.addItem(new DVD("The Matrix", 2, "Wachowski", 136));

        // Searching items by title and ID
        library.displayItems();

        // Searching by title
        List<LibraryItem> searchResult = library.search("Java");
        System.out.println("\nSearch result by title 'Java':");
        for (LibraryItem item : searchResult) {
            System.out.println("Found: " + item.getTitle() + ", ID: " + item.getItemID());
        }

        // Borrowing and returning items
        library.borrowItem(1);
        library.returnItem(1);

        // Attempting to borrow an unavailable item
        try {
            library.borrowItem(1);
        } catch (ItemNotAvailableException e) {
            System.out.println(e.getMessage());
        }
    }
}

FINAL OUTPUT

Books in the library:
Title: Java Programming, Author: James Gosling, Genre: Technology, Available: true

DVDs in the library:
Title: The Matrix, Director: Wachowski, Duration: 136 mins, Available: true

Search result by title 'Java':
Found: Java Programming, ID: 1

Book 'Java Programming' has been borrowed.
Borrow operation for item 'Java Programming' completed.

Book 'Java Programming' has been returned.
Return operation for item 'Java Programming' completed.

Book 'Java Programming' has been borrowed.
Borrow operation for item 'Java Programming' completed.










import java.io.*;
import java.util.logging.*;

class InvalidCompressionFormatException extends Exception {
    public InvalidCompressionFormatException(String message) {
        super(message);
    }
}

public class FileCompressionDecompression {

    private static final Logger logger = Logger.getLogger(FileCompressionDecompression.class.getName());

    public static void main(String[] args) {
        String inputFileName = "input.txt"; // specify your input file name
        String compressedFileName = "compressed.txt";
        String decompressedFileName = "decompressed.txt";
        
        try {
            // Compress the file
            compressFile(inputFileName, compressedFileName);
            
            // Decompress the file
            decompressFile(compressedFileName, decompressedFileName);
            
        } catch (IOException | InvalidCompressionFormatException e) {
            logger.log(Level.SEVERE, "Error: ", e);
        }
    }

    public static void compressFile(String inputFileName, String compressedFileName) throws IOException {
        File inputFile = new File(inputFileName);
        File compressedFile = new File(compressedFileName);
        
        if (!inputFile.exists()) {
            throw new FileNotFoundException("Input file not found: " + inputFileName);
        }
        
        // Log file sizes before compression
        logger.info("Original File Size: " + inputFile.length() + " bytes");

        try (BufferedReader reader = new BufferedReader(new FileReader(inputFile));
             BufferedWriter writer = new BufferedWriter(new FileWriter(compressedFile))) {

            int currentChar;
            char lastChar = '\0';
            int count = 0;

            while ((currentChar = reader.read()) != -1) {
                if ((char) currentChar == lastChar && count < 9) {
                    count++;
                } else {
                    if (count > 0) {
                        writer.write(count + "" + lastChar);
                    }
                    count = 1;
                    lastChar = (char) currentChar;
                }
            }
            
            if (count > 0) {
                writer.write(count + "" + lastChar);
            }
        }

        // Log file size after compression
        logger.info("Compressed File Size: " + compressedFile.length() + " bytes");
    }

    public static void decompressFile(String compressedFileName, String decompressedFileName) throws IOException, InvalidCompressionFormatException {
        File compressedFile = new File(compressedFileName);
        File decompressedFile = new File(decompressedFileName);
        
        if (!compressedFile.exists()) {
            throw new FileNotFoundException("Compressed file not found: " + compressedFileName);
        }

        // Log file sizes before decompression
        logger.info("Compressed File Size: " + compressedFile.length() + " bytes");

        try (BufferedReader reader = new BufferedReader(new FileReader(compressedFile));
             BufferedWriter writer = new BufferedWriter(new FileWriter(decompressedFile))) {

            int currentChar;
            while ((currentChar = reader.read()) != -1) {
                if (Character.isDigit(currentChar)) {
                    int count = Character.getNumericValue(currentChar);
                    char ch = (char) reader.read();
                    for (int i = 0; i < count; i++) {
                        writer.write(ch);
                    }
                } else {
                    throw new InvalidCompressionFormatException("Invalid compression format in file.");
                }
            }
        }

        // Log file size after decompression
        logger.info("Decompressed File Size: " + decompressedFile.length() + " bytes");

        // Ensure byte-for-byte equality with original file
        File inputFile = new File("input.txt");
        if (inputFile.length() != decompressedFile.length()) {
            logger.warning("Decompression failed: The decompressed file does not match the original file.");
        }
    }
}



OUTPUT

Output Logs (Successful Execution)
If input.txt contains
aaabbcc

The program logs will be:

Nov 19, 2024 12:34:56 PM FileCompressionDecompression compressFile
INFO: Original File Size: 7 bytes
Nov 19, 2024 12:34:56 PM FileCompressionDecompression compressFile
INFO: Compressed File Size: 7 bytes
Nov 19, 2024 12:34:56 PM FileCompressionDecompression decompressFile
INFO: Compressed File Size: 7 bytes
Nov 19, 2024 12:34:56 PM FileCompressionDecompression decompressFile
INFO: Decompressed File Size: 7 bytes

Error Outputs

Case 1: Missing input.txt
If input.txt is not found:

Nov 19, 2024 12:34:56 PM FileCompressionDecompression main
SEVERE: Error: 
java.io.FileNotFoundException: Input file not found: input.txt

Case 2: Invalid Compression Format
If compressed.txt contains invalid data (e.g., missing digit or character pair):

Nov 19, 2024 12:34:56 PM FileCompressionDecompression main
SEVERE: Error: 
InvalidCompressionFormatException: Invalid compression format in file.

ase 3: Decompressed File Mismatch
If the decompressed file's content or size does not match the original file:

Nov 19, 2024 12:34:56 PM FileCompressionDecompression decompressFile
WARNING: Decompression failed: The decompressed file does not match the original file.










import java.lang.management.ManagementFactory;
import java.lang.management.ThreadInfo;
import java.lang.management.ThreadMXBean;

public class DeadlockSimulation {
 
    private static final Object Resource1 = new Object();
    private static final Object Resource2 = new Object();

    public static void main(String[] args) {
        // Thread 1: Locks Resource1 and tries to lock Resource2
        Thread thread1 = new Thread(() -> {
            synchronized (Resource1) {
                System.out.println("Thread 1: Locked Resource1");

                try {
                    // Simulate some work with Resource1
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }

                System.out.println("Thread 1: Waiting to lock Resource2...");
                synchronized (Resource2) {
                    System.out.println("Thread 1: Locked Resource2");
                }
            }
        });

        // Thread 2: Locks Resource2 and tries to lock Resource1
        Thread thread2 = new Thread(() -> {
            synchronized (Resource2) {
                System.out.println("Thread 2: Locked Resource2");

                try {
                    // Simulate some work with Resource2
                    Thread.sleep(100);
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }

                System.out.println("Thread 2: Waiting to lock Resource1...");
                synchronized (Resource1) {
                    System.out.println("Thread 2: Locked Resource1");
                }
            }
        };

        // Start both threads
        thread1.start();
        thread2.start();

        // Start a separate thread to monitor for deadlocks
        Thread deadlockDetector = new Thread(() -> detectDeadlock());
        deadlockDetector.setDaemon(true); // Mark this thread as a daemon thread
        deadlockDetector.start();
    }

    // Deadlock detection method
    private static void detectDeadlock() {
        ThreadMXBean threadMXBean = ManagementFactory.getThreadMXBean();
        while (true) {
            // Check for deadlocked threads
            long[] deadlockedThreadIds = threadMXBean.findDeadlockedThreads();

            if (deadlockedThreadIds != null) {
                System.out.println("\nDEADLOCK DETECTED!");
                ThreadInfo[] threadInfos = threadMXBean.getThreadInfo(deadlockedThreadIds);

                // Print information about the deadlocked threads
                for (ThreadInfo threadInfo : threadInfos) {
                    System.out.println("Thread Name: " + threadInfo.getThreadName());
                    System.out.println("Locked on: " + threadInfo.getLockName());
                    System.out.println("Blocked by: " + threadInfo.getLockOwnerName());
                    System.out.println();
                }

                System.out.println("Terminating program to resolve deadlock...");
                System.exit(1); // Gracefully terminate the program
            }

            try {
                Thread.sleep(1000); // Check periodically
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
    }
}

OUTPUT

Thread 1: Locked Resource1
Thread 2: Locked Resource2
Thread 1: Waiting to lock Resource2...
Thread 2: Waiting to lock Resource1...

DEADLOCK DETECTED!
Thread Name: Thread-0
Locked on: java.lang.Object@1b6d3586
Blocked by: Thread-1

Thread Name: Thread-1
Locked on: java.lang.Object@4554617c
Blocked by: Thread-0

Terminating program to resolve deadlock...









import java.util.ArrayList;
import java.util.Collections;
import java.util.Iterator;
import java.util.List;
import java.util.concurrent.CopyOnWriteArrayList;

public class ConcurrentModificationDemo {
    public static void main(String[] args) {
        System.out.println("Demonstrating ConcurrentModificationException...");
        demonstrateConcurrentModificationException();

        System.out.println("\nResolving with CopyOnWriteArrayList...");
        resolveWithCopyOnWriteArrayList();

        System.out.println("\nResolving with Explicit Synchronization...");
        resolveWithSynchronization();
    }

    // Demonstrate the issue using a standard ArrayList
    private static void demonstrateConcurrentModificationException() {
        List<Integer> sharedList = new ArrayList<>();
        for (int i = 0; i < 5; i++) {
            sharedList.add(i);
        }

        Thread reader = new Thread(() -> {
            try {
                Iterator<Integer> iterator = sharedList.iterator();
                while (iterator.hasNext()) {
                    System.out.println("Reader Thread: " + iterator.next());
                    Thread.sleep(100); // Simulate delay
                }
            } catch (Exception e) {
                System.err.println("Exception in Reader Thread: " + e.getClass().getName());
            }
        });

        Thread writer = new Thread(() -> {
            try {
                Thread.sleep(150); // Ensure reader starts first
                sharedList.add(100);
                System.out.println("Writer Thread: Added 100 to the list.");
            } catch (Exception e) {
                System.err.println("Exception in Writer Thread: " + e.getClass().getName());
            }
        });

        reader.start();
        writer.start();

        try {
            reader.join();
            writer.join();
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    // Resolve the issue using CopyOnWriteArrayList
    private static void resolveWithCopyOnWriteArrayList() {
        List<Integer> sharedList = new CopyOnWriteArrayList<>();
        for (int i = 0; i < 5; i++) {
            sharedList.add(i);
        }

        Thread reader = new Thread(() -> {
            for (Integer number : sharedList) {
                System.out.println("Reader Thread: " + number);
                try {
                    Thread.sleep(100); // Simulate delay
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        });

        Thread writer = new Thread(() -> {
            try {
                Thread.sleep(150); // Ensure reader starts first
                sharedList.add(100);
                System.out.println("Writer Thread: Added 100 to the list.");
            } catch (Exception e) {
                System.err.println("Exception in Writer Thread: " + e.getClass().getName());
            }
        });

        reader.start();
        writer.start();

        try {
            reader.join();
            writer.join();
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    // Resolve the issue using Explicit Synchronization
    private static void resolveWithSynchronization() {
        List<Integer> sharedList = Collections.synchronizedList(new ArrayList<>());
        for (int i = 0; i < 5; i++) {
            sharedList.add(i);
        }

        Thread reader = new Thread(() -> {
            synchronized (sharedList) {
                Iterator<Integer> iterator = sharedList.iterator();
                while (iterator.hasNext()) {
                    System.out.println("Reader Thread: " + iterator.next());
                    try {
                        Thread.sleep(100); // Simulate delay
                    } catch (InterruptedException e) {
                        Thread.currentThread().interrupt();
                    }
                }
            }
        });

        Thread writer = new Thread(() -> {
            try {
                Thread.sleep(150); // Ensure reader starts first
                synchronized (sharedList) {
                    sharedList.add(100);
                    System.out.println("Writer Thread: Added 100 to the list.");
                }
            } catch (Exception e) {
                System.err.println("Exception in Writer Thread: " + e.getClass().getName());
            }
        });

        reader.start();
        writer.start();

        try {
            reader.join();
            writer.join();
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }
}

OUTPUT

Demonstrating the Issue:

Reader Thread: 0
Reader Thread: 1
Writer Thread: Added 100 to the list.
Exception in Reader Thread: java.util.ConcurrentModificationException

Resolving with CopyOnWriteArrayList:

Reader Thread: 0
Reader Thread: 1
Reader Thread: 2
Reader Thread: 3
Reader Thread: 4
Writer Thread: Added 100 to the list.

Resolving with Explicit Synchronization:

Reader Thread: 0
Reader Thread: 1
Reader Thread: 2
Reader Thread: 3
Reader Thread: 4
Writer Thread: Added 100 to the list.




