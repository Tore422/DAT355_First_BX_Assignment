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

I would propose using a symmetric lens, as both meta-models from slide 32<br>
contain private information not known to the other class.<br>

Forward Restoration(classModel', dataModel) -> dataModel'<br>

The updated class model is mapped to a data model representation, as per the relational mapping stated in the exercise description;<br>
and in addition we set the typeKey in Tab_A, to the id that will reference the class.<br>


Backwards Restoration(classModel, dataModel') -> classModel'<br>

The changes in the data model are mapped to the class model.<br>
Each row in Tab_A is mapped to a class with attributes and a relation to the super class.<br>





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

The equation says, that given an update from A1 to A1' and an update from A1' to A1,<br>
we should get the original model A2 which is consistent with A1.<br>
In other words, making an update to a model, and then changing the model back to how it was,<br>
should result in the same consistent model pair.<br>

First perform the inner forward repair on modified model A1' and A2.<br>
Resulting in two consistent models A1' and A2'.<br>
Then perform the outer forward repair on the unmodified model A1 and the modified model A2'.<br>
Resulting in a consistent model A2.<br>


In the composer example from slide 40, if given an update from A1 -> A1', we get a consistent pair A1' and A2'.<br>
If we then were to apply an update A1' -> A1, we would get a consistent model pair A1 and A2,<br>
which are in correspondance with the given equation for this task.<br>

The model would add to the list all elements in the modified set that are not already there,<br>
and delete all elements in the list, not present in the modified set; giving a consistent pair A1' and A2'.<br>
If we then re-add the deleted elements to the list and remove those added in the first update,<br>
and perform the same add and remove operations as before to the set,<br>
we would get back the consisitent pair A1 and A2 that we started with.<br>


Exercise 4: <br>

a) <br>

From slide 30:<br>
Asymmetric if easy to go from one model to the other, but by doing so we loose information,<br>
preventing us from going back without external help.

The get(X, Y) function will result in the intersection of the two given sets.<br>
Going from the source to the view is therefore rather easy, but going from the view and back to the source directly,<br>
becomes impossible, as we only have the values that appear in both X and Y,<br>
while the rest of the information was lost in the transformation.<br>

The put((X, Y), Z') function will result in a pair (What is in both Z' and (what is in X, but not in Y), what is in Z' and in Y).<br>
Applying a change to the view Z, will modify the source pair (X, Y),<br>
and result in a modified source pair (values in only X and Z', values in Y and Z').<br>


b) <br>

The lens is correct, because it fulfills the criteria from slide 47.<br>
The set of all pairs ((X, Y), get(X, Y)) are elements in the consistentency relation;<br>
and get(put((X, Y), Z')) = get((Z' U (X - Y), Z' U Y)) = ((Z' U (X - Y)) intersection (Z' U Y))<br>
= Z' = the modified view v from put(s,v)<br>

For example, with sets: X = {1,2,3,4}, Y = {2,3,5,6}, Z' = {7,8,9}<br>
get(put(({1,2,3,4}, {2,3,5,6}), {7,8,9})) = <br>
get({1,4,7,8,9}, {2,3,5,6,7,8,9}) = <br>
{7,8,9} = Z'<br>


Y U Z' = {2,3,5,6,7,8,9}<br>
X - Y = {1,4}<br>
Z' U (X - Y) = {1,4,7,8,9}<br>
((Z' U (X - Y)) intersection (Z' U Y)) = <br>
{1,4,7,8,9} intersection {2,3,5,6,7,8,9} = {7,8,9} = Z'<br>



The lens is hyppocratic, because it fulfills the criteria from slide 47.<br>
The pair ((X,Y), Z) is part of the consistency relation,<br>
and put((X, Y), get(X,Y)) = put((X, Y), Z) = (Z U (X - Y), Z U Y) = (X, Y)<br>

For example, with sets: X = {1,2,3,4}, Y = {2,3,5,6}, Z = get(X,Y) = X intersection Y = {2,3}<br>
put(({1,2,3,4}, {2,3,5,6}), get({1,2,3,4}, {2,3,5,6})) = <br>
put(({1,2,3,4}, {2,3,5,6}), {2,3}) = <br>
({2,3} U {1,4}, {2,3} U {2,3,5,6}) = <br>
({1,2,3,4}, {2,3,5,6}) = (X, Y) = s<br>


c) <br>

Asking, is the lens history ignorant, is equivalent to asking if put(put(s0, v1), v2) = put(s0, v2)?<br>
In this case, is put(put((X, Y), Z'), Z'') = put((X, Y), Z'')?<br>

put(put((X, Y), Z'), Z'') = <br>
put((Z' U (X - Y), Z' U Y), Z'') = <br>
(Z'' U ((Z' U (X - Y)) - (Z' U Y)), Z'' U (Z' U Y)) = <br>
(Z'' U (X' - Y'), Z'' U Y')<br>

put((X, Y), Z'') = <br>
(Z'' U (X - Y), Z'' U Y) not the same as (Z'' U (X' - Y'), Z'' U Y').<br>


Example with sets: X = {1,2,3,4}, Y = {2,3,5,6}, Z' = {7,8,9}, Z'' = {10,11,12}<br>

put(put(({1,2,3,4}, {2,3,5,6}), {7,8,9}), {10,11,12}) = <br>
put(({7,8,9} U ({1,2,3,4} - {2,3,5,6}), {7,8,9} U {2,3,5,6}), {10,11,12}) = <br>
put(({7,8,9} U {1,4}, {2,3,5,6,7,8,9}), {10,11,12}) = <br>
put(({1,4,7,8,9}, {2,3,5,6,7,8,9}), {10,11,12}) = <br>
({10,11,12} U ({1,4,7,8,9} - {2,3,5,6,7,8,9}), {10,11,12} U {2,3,5,6,7,8,9}) = <br>
({10,11,12} U {1,4}, {2,3,5,6,7,8,9,10,11,12}) = <br>
({1,4,10,11,12}, {2,3,5,6,7,8,9,10,11,12})<br>


put(({1,2,3,4}, {2,3,5,6}), {10,11,12}) = <br>
({10,11,12} U ({1,2,3,4} - {2,3,5,6}), {10,11,12} U {2,3,5,6}) = <br>
({10,11,12} U {1,4}, {2,3,5,6,10,11,12}) = <br>
({1,4,10,11,12}, {2,3,5,6,10,11,12}) = <br>


Unless the elements from Z' are included in Z'', the result we would get would differ.<br>
The equation is therefore not history ignorant.<br>


Exercise 5: <br>

a) <br>

In order for an asymmetric lens to be called a constant complement, it must be history ignorant.<br>

In the case of the composer example on slide 52.<br>
If the lens removes an object from M1, and get an entry in M2 and a complement C,<br>
the only information we would have retained is the name and nationality, as that information is kept in M2.<br>
When doing a second transformation that tries to add a removed element back into M1,<br>
we might not be able to restore the models consistency, as the year of birth information <br>
has been lost or not depending on the order of the updates.<br>

The lens is not history ignorant, and it is therefore not possible for it to be <br>
a constant complement decomposition of M1 into M2 and a complement C.<br>



b) <br>

In the EMF case, the get(v,c) function would take the generated and manually written code,<br>
and return a class model;<br>
the put((v,c),v') function would take the generated and manually written code,<br>
and apply the modified class model to update the existing code.<br>
The manual changes are kept seperate in the set C,<br>
and are therefore protected from change when the code is updated.<br>

In this case, history ignorance means we can apply a change in the class model and update the code,<br>
while still retaining a consistent relation between the code and the model;<br>
as the code is generated to reflect the current class model, making any previous/intermediary changes irrelevant,<br>
and the manually written code is kept separate, so it is not affected by the model and code changes.<br>

Any syntax errors are not prevented when using the put() function, as the manually written code <br>
is protected from overwrite, and the class model itself is not protected from errors,<br>
making it somewhat problematic to use without external validation tools.<br>



