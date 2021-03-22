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
    
    put(set, key, value) {
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
        return listPrime;
    }


It is not possible to define a put(list) that results in a valid set of unordered, unique values,<br>
unless the operation happens to make the last non-unique element in the list unique.<br>




Exercise 2: <br>

I would propose using an asymmetric lens, because while updating the attributes between the two models is fine,<br>
we cannot without further information, restore the operations in the class model, since that information is not kept in the data model.<br>

get(classModel) -> dataModel<br>
get(dataModel) -> classModel<br>

get(put((classModel, attribute), attribute')) -> get(classModel') -> dataModel'<br>
get(put((dataModel, attribute), attribute')) -> get(dataModel') -> classModel'<br>


Exercise 3: <br>


a) <br>

Correctness<br>

By the definition of correctness on slide 42, having a modified model A1' or A2',<br>
using a forward or backwards restoration must result in a model pair that are consistent.<br>

For the forward restoration function, we need to prove that by giving a modified model A1' and an unmodified model A2,<br>
the result will be a model that are consistent with model A1'.<br>
Likewise for the backwards restoration function, where the result of giving an unmodified model A1 and a modified model A2',<br>
is a model A1' that is consistent with A2'.<br>

The forward restoration function on slide 40, is implemented by taking a modified model A1',<br>
and an unmodified model A2, and for each object in A1', if such an object does not exist in A2,<br>
we construct one and add it to A2.<br>
For each object in A2, if such an object does not exist in A1', it is deleted from A2.<br>
The result is two models that have the same set of (name, nationality) pairs, and are therefore consistent according to the red box on slide 40.<br>

The backwards restoration function would likewise take a modified model A2',<br>
and an unmodified model A1, and add each object in A2' (not already present) to A1,<br>
and delete each object in A1 that is not present in A2'.<br>
The result is likewise two consistent models with the same set of (name, nationality) pairs.<br>


Hippocraticness<br>

From the definition of hippocraticness on slide 42, we have that a restoration function is hippocratic,<br>
if given a pair of consistent models, it will leave the same unmodified pair of consistent models.<br>

For the forward and backwards restoration functions, if given a pair of unmodified, consitent models,<br>
there would be no (name, nationality) pair in one model that is not already in the other,<br>
therefore no changes will be made, as it only adds or deletes objects that are not present in the other model.<br>

Conclusion: the restoration functions are both correct and hippocratic.<br>


b) <br>




Exercise 4: <br>

a) <br>

b) <br>

c) <br>


Exercise 5: <br>

a) <br>

b) <br>








I am not entirely sure if I undeerstood exercise 2 correctly,<br>
so please let me know if I did something wrong.<br>





