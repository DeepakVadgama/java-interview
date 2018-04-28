class D {
    public static void main(String args[]) {
        Integer b2=128;
        Integer b3=128;
        System.out.println(b2==b3);
    }
}
Output:

false
class D {
    public static void main(String args[]) {
        Integer b2=127;
        Integer b3=127;
        System.out.println(b2==b3);
    }
}
Output:

true

/////
It is memory optimization in Java related.

To save on memory, Java 'reuses' all the wrapper objects whose values fall in the following ranges:

All Boolean values (true and false)

All Byte values

All Character values from \u0000 to \u007f (i.e. 0 to 127 in decimal)

All Short and Integer values from -128 to 127.

Note:

if you create Boolean with new Boolean(value); you will always get new object

if you create String with new String(value); you will always get new object

if you create Integer with new Integer(value); you will always get new object

------------------------------------------------------------------------------------------------------

