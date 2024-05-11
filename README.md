Java Program to find the First non repeating character in a string
In this article, we will learn how to code a java program to find the first non repeating character in a string 
Java program to find non repeating characters in a string
Method discussed
Method 1 – Using indexOf() and lastIndexOf() methods
Method 2 – This method builds a frequency array
Method 3 – This method uses Linked Hashmap
Method 4 – This method uses Set and ArrayList
Method 5 – This method uses Java 8
Find First non repeating character in a String in Java
Method 1
Using indexOf() and lastIndexOF() methods.

As soon as we find the first item that only appears once print stop further.

Run
class Main
{
    public static void main(String args[])
    {
        String inputStr ="prepinsta";
        boolean flag = true;

        for(char i :inputStr.toCharArray())
        {
            // if current character is the last occurrence in the string
            if (inputStr.indexOf(i) == inputStr.lastIndexOf(i))
            {
                System.out.println("First non-repeating character is: "+ i);
                flag = false;
                break;
            }
        }

        if(flag)
            System.out.println("There is no non repeating character in input string");
    }
}
Output
First non-repeating character is: r
Method 2
This method builds a frequency array
With a frequency count of each ASCII character between 0 – 255
We then find iterate the input string from the start
Print the first character with frequency count == 1
Run

class Main {
    static final int NO_OF_CHARS = 256;
    static char count[] = new char[NO_OF_CHARS];

    // this method builds count array which updates frequency for each
    // ascii character (0-255)
    // example for 'p' ascii value is 112, in the array
    // count[112] value would be 2 (p appears twice)
    static void buildCharCountArray(String str)
    {
        for (int i = 0; i < str.length(); i++) {
            count[str.charAt(i)]++;
        }
    }

    // this method finds first non repeating character
    // returns the index of the first non repeating character
    static int findFirstNonRepeating(String string)
    {
        // build char count array
        buildCharCountArray(string);

        int pos = -1, i;

        for (i = 0; i < string.length(); i++) {
            if (count[string.charAt(i)] == 1) {
                pos = i;
                break;
            }
        }

        return pos;
    }

    // Driver method
    public static void main(String[] args)
    {
        String string = "prepinsta";
        int pos = findFirstNonRepeating(string);

        System.out.println(
                pos == -1
                        ? "All characters are repeating "
                        : "First non-repeating character is "
                        + string.charAt(pos));
    }
}
Output
First non-repeating character is: r
Related Pages
Juggling algorithm for array rotation
 
Balanced Parenthesis Problem
 
Toggle each character in a string

Count the number of vowels

Length of the string without using strlen() function

Method 3
This method uses Linked Hashmap

Run
import java.util.*;
import java.util.Map.Entry;

class Main {

    public static void main(String[] args)
    {

        String string = "prepinsta";
        char ch = findFirstNonRepeating(string);
            System.out.println("First non-repeating character is : " + ch);
    }

    public static Character findFirstNonRepeating(String str)
    {
        HashMap  charhashtable =
                new LinkedHashMap();
        int len;
        Character ch;
        len = str.length();  // Scan string and build hash table

        for (int i = 0; i < len; i++)
        {
            ch = str.charAt(i);

            if(charhashtable.containsKey(ch))
                // increment count corresponding to ch
                charhashtable.put(ch, charhashtable.get(ch) + 1);
            else
                charhashtable.put(ch , 1);

        }
        for(Entry entry: charhashtable.entrySet())
        {
            if(entry.getValue() == 1)
                return entry.getKey();
        }
        return null;
    }
}
Output
First non-repeating character is: r
Method 4
This method uses Set and ArrayList

Run
import java.util.*;

class Main {


    public static Character findFirstNonRepeating(String str)
    {
        // set stores characters that are repeating
        Set charRepeatingSet = new HashSet<>();

        // ArrayList stores characters that are non repeating
        List charNonRepeatingList = new ArrayList<>();

        for(int i=0; i < str.length(); i++)
        {

            char ch = str.charAt(i);

            // if set already contains character ch
            if(charRepeatingSet.contains(ch))
                continue;

            // if Array List contains character ch
            // remove existing ch from ArrayList and
            // add ch to set
            if(charNonRepeatingList.contains(ch)) {
                charNonRepeatingList.remove((Character) ch);
                charRepeatingSet.add(ch);
            }

            // else add to ArrayList as character must be first occurrence
            else {
                charNonRepeatingList.add(ch);
            }
        }
        return charNonRepeatingList.get(0);
    }

    public static void main(String[] args)
    {

        String string = "prepinsta";
        char ch = findFirstNonRepeating(string);
        System.out.println("The first non repeated character is :  " + ch);
    }
}
Output
First non-repeating character is: r
Method 5
This method uses Java 8

Run
import java.util.*;

class Main {

    public static Character findFirstNonRepeating(String string) {
        Map map = new LinkedHashMap();

        for (Character ch : string.toCharArray()) {
            map.put(ch, map.containsKey(ch) ? map.get(ch) + 1 : 1);
        }
        return map.entrySet().stream().filter(x -> x.getValue() == 1).findFirst().get().getKey();
    }


    public static void main(String[] args)
    {
        String string = "prepinsta";
        char character = findFirstNonRepeating(string);
        System.out.println("First non-repeating character is : " + character);
    }
}
Output
First non-repeating character is: r
Algorithm :
Take String as a input from the user.
Create array of 256 element to store frequency of each character.
Iterate a loop from 0 to length of the string to calculate frequency of each character.
Again iterate a loop from 0 to 256 to find the character whose frequency is 1 and also print that character.
we will get the desired output.
Solution in Java for finding the non repeating characters in a string
Run
class Main
{
    public static void main(String args[])
    {
        String inputStr ="prepinsta";
        boolean flag = true;

        for(char i :inputStr.toCharArray())
        {
            // if current character is the last occurrence in the string
            if (inputStr.indexOf(i) == inputStr.lastIndexOf(i))
            {
                System.out.println("First non-repeating character is: "+ i);
                flag = false;
                break;
            }
        }

        if(flag)
            System.out.println("There is no non repeating character in input string");
    }
}
Output :
Enter the string
prepinsta
The non repeating characters are :
a e i n r s t
