# DAT355_First_BX_Assignment



Exercise 1:

a) <br>
It is possible to define a get(int, int) that will result in the product of the two numbers.<br>
get(a, b) -> c<br>

    get(int a, int b) {
        return a * b; 
    }

It is not possible to define a get(int) that will result in the two different numbers that the number is a product of.<br>
The best thing that the function could do is returning a list of possible number pairs,<br>
that multiplied with each other result in the same product<br>
(e.g., <br>
1 * 10 = 10,<br>
2 * 5 = 10, <br>
5 * 2 = 10, <br>
10 * 1 = 10, <br>
-10 * -1 = 10, <br>
-2 * -5 = 10, etc.).


It is possible to define a put(int, int') that results in the product of the new numbers.<br>
get(a, put((a, b), b')) -> get(a, b') -> c'<br>

    put(int a, int b) {
        this.b = b; // Update stored value of b.
        return a * b;
    }

It is also possible to define a put(int') that will update one of the numbers that result in the product;<br>
but only one of the numbers would be changed, while the other has to remain the same in order to find the new value of the second number.<br>
put(c') -> get(a, (c' / a)) -> get(a, b') -> a, b'<br>

    put(int c') {
        this.b = c' / a;
    }


b) <br>
It is possible to define a get(firstName, lastName) that results in the whole name.<br>
get(firstName, lastName) -> name<br>

    get(String firstName, String lastName) {
        return firstName + " " + lastName;
    }

It is possible to define a get(name) that results in firstName and lastName,<br>
but only if the lastName is consisting of a single word.<br>
get(name) -> firstName, lastName<br>

    get(name) {
        String[] nameComponents = name.split(" ");
        String lastName = nameComponents[nameComponents.length - 1];
        String firstName = "";
        for (int i = 0; i < nameComponents.length - 1; i++) {
            firstName += nameComponents[i] + " ";
        }
        firstName = firstName.strip();
        String[] names = {firstName, lastName};
        return names;
    }


It is possible to define a put(firstName', lastName') that results in result in a new name.<br>
get(firstName, put((firstName, lastName), lastName')) -> get(firstName, lastName') -> name'<br>
get(put((firstName, lastName), firstName'), lastName) -> get(firstName', lastName) -> name'<br>

    put(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
        return firstName + " " + lastName;
    }

It is possible to define a put(name') that result in the new first and last names.<br>
put(name') -> get(firstName', lastName') -> firstName', lastName'<br>

    put(String name) {
        this.name = name;
        String[] nameComponents = name.split(" ");
        String lastName = nameComponents[nameComponents.length - 1];
        String firstName = "";
        for (int i = 0; i < nameComponents.length - 1; i++) {
            firstName += nameComponents[i] + " ";
        }
        firstName = firstName.strip();
        String[] names = {firstName, lastName};
        return names;
    }

c) <br>
It is possible to define a get(set) that goes from a set of unordered, unique values,<br>
to a list of ordered, non-unique values, as long as the values in the list are not required to have duplicates (i.e., must contain non-unique elements).<br>
get({element2, element1, ..., elementN}) -> [element1, element2, ..., elementN]<br>

    Map<Integer, String> set = new HashMap<>();
    set.put(3, "a");
    set.put(2, "d");
    set.put(5, "c");
    set.put(1, "b");
    get(set) {
        List<String> list = new ArrayList<>();
        list.addAll(set.values());
        Collections.sort(list);
        return list;
    }

It is not possible to define a get(list) that goes from a list of ordered, non-unique values,<br>
to a set of unordered, unique values, as there would be multiple versions of the different element<br>
values that are required to be unique (unless all elements in the list happens to be unique).<br>



It is possible to define a put(set) that results in a valid list of ordered, non-unique elements,<br>
as long as the values of the list are not required to be non-unique.<br>
put({element1, elementN, ..., element1}, element1') -> [element1', element2, ..., elementN]<br>


    Map<Integer, String> set = new HashMap<>();
    set.put(3, "a");
    set.put(2, "d");
    set.put(5, "c");
    set.put(1, "b");
    
    put(key, value) {
        set.put(key, value);
        List<String> listPrime = new ArrayList<>(set.values());
        for (int i = 0; i < listPrime.size(); i++) {
            for (int j = 0; j < listPrime.size(); j++) {
                String element = listPrime.get(i);
                String otherElement = listPrime.get(j);
                if (element.compareTo(listPrime.get(j)) < 0) {
                    listPrime.set(i, otherElement);
                    listPrime.set(j, element);
                }
            }
        }
    }


It is not possible to define a put(list) that results in a valid set of unordered, unique values,<br>
unless the operation happens to make the last non-unique element in the list unique.<br>




Exercise 2:





Exercise 3:


a) <br>

b) <br>




Exercise 4:

a) <br>

b) <br>

c) <br>


Exercise 5:

a) <br>

b) <br>







