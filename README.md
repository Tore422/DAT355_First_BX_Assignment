# DAT355_First_BX_Assignment



Exercise 1:

a) <br>
It is possible to define a get(int, int) that will result in the product of the two numbers.<br>
get(int a, int b) { <br>
    return a * b; <br>
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
put(int a, int b) {<br>
    this.b = b; // Update stored value of b.<br>
    return a * b;<br>
}

It is also possible to define a put(int') that will update one of the numbers that result in the product;<br>
but only one of the numbers would be changed, while the other has to remain the same in order to find the new value of the second number.<br>
put(int c') {<br>
    this.b = c' / a;<br>
}


b) <br>
It is possible to define a get(firstName, lastName) that results in the whole name.<br>
get(String firstName, String lastName) {<br>
    return firstName + " " + lastName;<br>
}

It is possible to define a get(name) that results in firstName and lastName,<br>
but only if the lastName is consisting of a single word.<br>
get(name) {<br>
    String[] nameComponents = name.split(" ");<br>
    String lastName = nameComponents[nameComponents.length - 1];<br>
    String firstName = "";<br>
    for (int i = 0; i < nameComponents.length - 1; i++) {<br>
        firstName += nameComponents[i] + " ";<br>
    }<br>
    firstName = firstName.strip();<br>
    String[] names = {firstName, lastName};<br>
    return names;<br>
}


It is possible to define a put(firstName', lastName') that results in result in a new name.<br>
put(String firstName, String lastName) {<br>
    this.firstName = firstName;<br>
    this.lastName = lastName;<br>
    return firstName + " " + lastName;<br>
}

It is possible to define a put(name') that result in the new first and last names.<br>
put(String name) {<br>
    this.name = name;<br>
    String[] nameComponents = name.split(" ");<br>
    String lastName = nameComponents[nameComponents.length - 1];<br>
    String firstName = "";<br>
    for (int i = 0; i < nameComponents.length - 1; i++) {<br>
        firstName += nameComponents[i] + " ";<br>
    }<br>
    firstName = firstName.strip();<br>
    String[] names = {firstName, lastName};<br>
    return names;<br>
}

c) <br>




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







