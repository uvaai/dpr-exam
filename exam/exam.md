# Data Processing and Representations Exam

This is a digital exam. The exam consists of programming exercises that are purely based on input, output, and calculations. You will use these exercises to show that you can write a data processing program from scratch using tools covered in this course.

During the exam, **you are allowed use the internet and the code you have written for the PDP and DPR modules**. You are obviously not allowed to message other students, so make sure any and all messaging applications are closed for the entire duration of the exam. You are also not allowed to use ChatGPT or similar tools that can write code for you. The only allowed tools are an editor with your code, possibly with code from earlier assignments, your terminal and a browser for searching for other coding resources and documentation.

_You will not be graded on design, but only on the correctness of your code_ and whether you met the requirements. You do not have to comment your code, nor do you have to abide by any other styling rules (though this can greatly help you understand your code).

This exam consists of 3 parts. Each of the parts can be made separately and are fully independent of each other.

## Rules

- Finish all exercises in a file named `exam.py` and submit this file
- Define any functions and/or classes you write at the top of the file, and add the provided tests at the bottom of the file in order of the exercises.
- Make sure the provided tests are *all* printed (or shown) when running your program. Separate the prints for each exercise with an extra print like `print("\n=== Exercise 1 ===")`, so it is clear which output belongs to which exercise.
- Not all exercises need to be perfect to pass the exam. If you do not know how to proceed, describe what you want your code to do.
- You are allowed use the internet and the code you have written for the PDP and DPR modules
- You are *not* allowed to contact other students
- You are *not* allowed to use ChatGPT or similar tools that can write code for you.

*Before you leave the exam room, check with us that your submission was correctly submitted!*

# The Exam

## Part 1: OOP

You are working for a transportation company and need to keep track of vehicles and their routes. To do this, you will implement two classes: `Vehicle` and `Route`. `Vehicle` contains all information about a vehicle, such as its registration number, type, and capacity. The `Route` class contains information about routes, such as the route name, distance, and the list of vehicles assigned to the route.

The following UML describes these classes and their relation:

![](../umls/route.png)

Implement `Vehicle` with the following methods:

- `__init__(registration_number, vehicle_type, capacity)`: create a new instance with the information provided by the parameters.
- `add_repair(date, description)`: add a repair record to the vehicle. These should be stored as `(date, description)` tuples in the attribute named `repairs`, which is a list.
- `list_repairs()`: list all repairs done on the vehicle.

Implement `Route` with the following methods:

- `__init__(name, distance)`: create a new instance with the route name and distance provided in the parameters, and initialize any other required instance attributes.
- `add_vehicle(vehicle)`: add a given `Vehicle` instance to the route.
- `remove_vehicle(registration_number)`: remove a vehicle from the route by its registration number.
- `calculate_capacity()`: calculate the total capacity of all vehicles that have been assigned to this route. Should return 0 if no vehicles are assigned.
- `list_route_info()`: print the name of the route and the total capacity of all assigned vehicles. Then neatly print a list of the registration numbers of all vehicles assigned to the route.

Test your code by running the code below:

    print("\n=== Part 1: OOP ===")

    # Test Vehicle creation and adding repairs
    bus_1 = Vehicle('AB123', 'Bus', 50)
    truck_1 = Vehicle('CD456', 'Truck', 20)
    van_1 = Vehicle('EF789', 'Van', 10)

    # Check initial vehicle details
    print(f"Vehicle {bus_1.registration_number}: Type = {bus_1.vehicle_type}, Capacity = {bus_1.capacity}")
    print(f"Vehicle {truck_1.registration_number}: Type = {truck_1.vehicle_type}, Capacity = {truck_1.capacity}")
    print(f"Vehicle {van_1.registration_number}: Type = {van_1.vehicle_type}, Capacity = {van_1.capacity}")

    # Adding and checking repairs for bus_1
    print(f"\nAdding repairs for vehicle {bus_1.registration_number}:")
    bus_1.add_repair('2023-05-01', 'Engine maintenance')
    bus_1.add_repair('2023-06-15', 'Tire replacement')
    print(f"{bus_1.registration_number} now has {len(bus_1.repairs)} registered repairs.") # should be 2

    # Check if the repairs can be printed
    bus_1.list_repairs()

    # Test Route creation and adding vehicles
    route_1 = Route('Route 1', 100)
    route_2 = Route('Route 2', 200)

    # Checking if capacity properly returns 0
    print(f'\nBefore adding vehicles to the routes, the total capacity for {route_1.name} is {route_1.calculate_capacity()}')

    # Adding vehicles to routes
    route_1.add_vehicle(bus_1)
    route_1.add_vehicle(truck_1)
    route_2.add_vehicle(van_1)

    # Testing if the capacity is now 70
    print(f'After adding vehicles to the routes, the total capacity for {route_1.name} is {route_1.calculate_capacity()}')

    # Listing route info with vehicles
    print(f"\nListing information for {route_1.name}:")
    route_1.list_route_info()

    print(f"\nListing information for {route_2.name}:")
    route_2.list_route_info()

    # Removing a vehicle from a route
    print(f"\nRemoving vehicle {truck_1.registration_number} from {route_1.name}")
    route_1.remove_vehicle(truck_1.registration_number)

    # Listing route info after removal
    print(f"\nListing information for {route_1.name} after removal:")
    route_1.list_route_info()

Which should output:

    === Part 1: OOP ===
    Vehicle AB123: Type = Bus, Capacity = 50
    Vehicle CD456: Type = Truck, Capacity = 20
    Vehicle EF789: Type = Van, Capacity = 10

    Adding repairs for vehicle AB123:
    AB123 now has 2 registered repairs.
    2023-05-01: Engine maintenance
    2023-06-15: Tire replacement

    Before adding vehicles to the routes, the total capacity for Route 1 is 0
    After adding vehicles to the routes, the total capacity for Route 1 is 70

    Listing information for Route 1:
    The route Route 1 has the following vehicles with a total capacity of 70:
    - AB123
    - CD456

    Listing information for Route 2:
    The route Route 2 has the following vehicles with a total capacity of 10:
    - EF789

    Removing vehicle CD456 from Route 1

    Listing information for Route 1 after removal:
    The route Route 1 has the following vehicles with a total capacity of 50:
    - AB123

## Part 2: Pandas

For this assignment, you will use the file [widgets.csv](../data/widgets.csv). This file contains sales data for a retail company that sells "widgets". The contents of the file look as follows:

    2020-01-02,Widget A,9,92.52,New York
    2020-01-03,Widget G,17,23.15,Chicago
    2020-01-05,Widget H,8,68.1,Los Angeles
    ...
    2022-12-28,Widget I,9,10.85,Houston
    2022-12-29,Widget D,16,18.28,Chicago
    2023-01-01,Widget I,11,21.43,Houston

As you can see, the file has **no** header, and data fields are separated by comma's.

### Exercise 1

The different datafields contain the following information:

1. `date`: the date on which the sale has taken place, in YYYY-MM-DD format
2. `product`: the name of the product
3. `quantity`: the number of items that were sold
4. `price`: the price of the product
5. `location`: the location where the product was sold

Load the data into a `DataFrame` named `df` using pandas. Name the columns `'date'`, `'product'`, `'quantity'`, `'price'`, and `'location'`. Print the dataframe and make sure your result has 800 rows and 5 columns.

Printing the `DataFrame` should show you:

               date   product  quantity  price     location
    0    2020-01-02  Widget A         9  92.52     New York
    1    2020-01-03  Widget G        17  23.15      Chicago
    2    2020-01-05  Widget H         8  68.10  Los Angeles
    3    2020-01-06  Widget B        15  99.40      Houston
    4    2020-01-07  Widget E         9  91.47      Houston
    ..          ...       ...       ...    ...          ...
    795  2022-12-25  Widget H         2  86.42     New York
    796  2022-12-27  Widget F         3  82.16      Houston
    797  2022-12-28  Widget I         9  10.85      Houston
    798  2022-12-29  Widget D        16  18.28      Chicago
    799  2023-01-01  Widget I        11  21.43      Houston

    [800 rows x 5 columns]


### Exercise 2

Create a new column in `df` named `'sale_value'` which represents the total sale value for each row (quantity * price). Print the _head_ of the updated dataframe.

             date   product  quantity  price     location  sale_value
    0  2020-01-02  Widget A         9  92.52     New York      832.68
    1  2020-01-03  Widget G        17  23.15      Chicago      393.55
    2  2020-01-05  Widget H         8  68.10  Los Angeles      544.80
    3  2020-01-06  Widget B        15  99.40      Houston     1491.00
    4  2020-01-07  Widget E         9  91.47      Houston      823.23

### Exercise 3

Create a new `DataFrame` named `total_sales` that, for each different 'product', shows the total quantity sold and the total sales value of all products of that type. Your result should look like this:

              quantity  sale_value
    product
    Widget A       886    46279.15
    Widget B       667    36017.56
    Widget C       986    51864.49
    Widget D       778    45481.89
    Widget E       900    53367.31
    Widget F       974    52934.39
    Widget G       789    47891.86
    Widget H       913    52995.78
    Widget I       777    41982.50
    Widget J       738    42968.98

### Exercise 4

Create a new column in `df` named `'month'`. This column should contain the name of the month in which the sale was made:

               date   product  quantity  price     location  sale_value     month
    0    2020-01-02  Widget A         9  92.52     New York      832.68   January
    1    2020-01-03  Widget G        17  23.15      Chicago      393.55   January
    2    2020-01-05  Widget H         8  68.10  Los Angeles      544.80   January
    3    2020-01-06  Widget B        15  99.40      Houston     1491.00   January
    4    2020-01-07  Widget E         9  91.47      Houston      823.23   January
    ..          ...       ...       ...    ...          ...         ...       ...
    795  2022-12-25  Widget H         2  86.42     New York      172.84  December
    796  2022-12-27  Widget F         3  82.16      Houston      246.48  December
    797  2022-12-28  Widget I         9  10.85      Houston       97.65  December
    798  2022-12-29  Widget D        16  18.28      Chicago      292.48  December
    799  2023-01-01  Widget I        11  21.43      Houston      235.73   January

**Hint:** It might be easier to first create a column that contains the _number of the month_. You can then convert those numbers to the month-name strings!

<!-- ### Exercise 5

Compute the total sales amount for each month:

    month
    April        38653.43
    Augustus     39490.09
    December     38310.34
    February     36670.13
    January      34286.78
    July         45709.71
    June         40467.85
    March        41524.71
    May          39531.31
    November     40621.75
    Oktober      37326.55
    September    39191.26

Do not worry about the order in which your months are displayed. Any order is okay, as long as the sales amount is correct! -->

## Part 3: Built-in data structures

You have been assigned the task of developing a library management system for a local library. The library stores all information on the availability of books in a dictionary named `library`. In this dictionary, the keys each represent the title of a book, and the corresponding value is also a dictionary, containing information on the different copies the library owns. In this inner dictionary the keys represent a specific book's ID, and the values are tuples containing the borrower's name (or None if the book is available) and the due date (or None if the book is available).

    library = {
        'To Kill a Mockingbird': {1001: (None, None), 1002: ('Alice', '2024-06-15'), 1003: ('Carol', '2003-12-25')},
        '1984': {2001: (None, None), 2002: (None, None), 2003: ('Bob', '2024-07-01')},
        'Moby Dick': {3001: ('Charlie', '2024-06-30'), 3002: (None, None)},
        'The Great Gatsby': {4001: (None, None), 4002: (None, None)}
    }

### Exercise 1

Write a function named `list_borrowed_books(library)` that takes the `library` dictionary and returns a list of tuples, each containing the book title, book ID, borrower's name, and due date for all of the borrowed books.

Test the function with:

    borrowed_books = list_borrowed_books(library)
    print('The following books were borrowed:')
    print(borrowed_books)

Which should print:

    [('To Kill a Mockingbird', 1002, 'Alice', '2024-06-15'), ('To Kill a Mockingbird
    ', 1003, 'Carol', '2003-12-25'), ('1984', 2003, 'Bob', '2024-06-30'), ('Moby Dic
    k', 3001, 'Charlie', '2024-06-30')]


<!-- ### Exercise 2

Write a function named `list_books_due(library, due_date)` that takes the `library` dictionary and a due date. The function should return a list of tuples, each containing the book title, book ID, and borrower's name for all books due on the specified date.

Test the function with:

    due_date = '2024-06-30'
    books_due = list_books_due(library, due_date)
    print(f'\nThe following books are due on {due_date}:')
    print(books_due)

Which should print:

    The following books are due on 2024-06-30:
    [('To Kill a Mockingbird', 1002, 'Alice', '2024-06-30'), ('Moby Dick', 3001, 'Ch
    arlie', '2024-06-30')] -->

### Exercise 2

Implement a function named `borrow_book(library, book_title, borrower, due_date)` that takes the `library` dictionary, a `book_title` string, a `borrower` string containing a name, and the `due_date` string. The function should update the `library` to mark the book as borrowed by the given borrower and with the specified due date. If the book is not available (all copies are borrowed), the function should print `'No copies of {book_title} are available.'`. The function should return the ID of the borrowed book if successful.

Test the function with:

    # Let's try to rent #3002
    borrowed_book_id = borrow_book(library, 'Moby Dick', 'David', '2024-07-10')
    print(borrowed_book_id)
    print(library)

    # This should now print that there are no copies of Moby Dick available
    borrowed_book_id = borrow_book(library, 'Moby Dick', 'Marc', '2024-07-12')

Which should print:

    3002
    {'To Kill a Mockingbird': {1001: (None, None), 1002: ('Alice', '2024-06-15'), 10
    03: ('Carol', '2003-12-25')}, '1984': {2001: (None, None), 2002: (None, None), 2
    003: ('Bob', '2024-07-01')}, 'Moby Dick': {3001: ('Charlie', '2024-06-30'), 3002
    : ('David', '2024-07-10')}, 'The Great Gatsby': {4001: (None, None), 4002: (None
    , None)}}
    No copies of Moby Dick are available.

### Exercise 3

Write a function named `return_book(library, book_id)` that takes the `library` dictionary and a book id. The function should update the `library` to mark the book as available (with the tuple `(None, None)`). If the `book_id` is not found in the `library`, the function should print `'Book ID {book_id} not found in the library.'`.

Test the function with:

    # This should change #2003 to (None, None) instead of ('Bob', '2024-07-01')
    return_book(library, 2003)
    print(library)

    # This id should not be found
    return_book(library, 9001)

Which should print:

    {'To Kill a Mockingbird': {1001: (None, None), 1002: ('Alice', '2024-06-15'), 10
    03: ('Carol', '2003-12-25')}, '1984': {2001: (None, None), 2002: (None, None), 2
    003: (None, None)}, 'Moby Dick': {3001: ('Charlie', '2024-06-30'), 3002: ('David
    ', '2024-07-10')}, 'The Great Gatsby': {4001: (None, None), 4002: (None, None)}}
    Book ID 9001 not found in the library.

_Note:_ If the book is found in the library, but currently not set to checked out, your function can still just mark the book as available. Note that this will effectively not change anything in the library records.
