# Lab Report 3

## Part 1 - Bugs

I will be analyzing the Array Functions.

# Failure-inducing Inputs
Below is the test code that produces errors
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    int[] input2 = {5, 7, 9};
    int[] input3 = {1, 4, 6, 8};
    ArrayExamples.reverseInPlace(input1);
    ArrayExamples.reverseInPlace(input2);
    ArrayExamples.reverseInPlace(input3);
    assertArrayEquals(new int[]{ 3 }, input1);
    assertArrayEquals(new int[] {9, 7, 5}, input2);
    assertArrayEquals(new int[] {8, 6, 4, 1}, input3);
	}


  @Test
  public void testReversed() {
    int[] input1 = { };
    int[] input2 = {0, 1, 2};
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
    assertArrayEquals(new int[]{2, 1, 0}, ArrayExamples.reversed(input2));
  }
  
  @Test
  public void testAverageWithoutLowest() {
    double[] input1 = {1.0, 2.0, 3.0};
    double[] input2 = {1.0, 1.0, 2.0, 3.0};
    assertEquals(2.5, ArrayExamples.averageWithoutLowest(input1), 0.0001);
    assertEquals(2.0, ArrayExamples.averageWithoutLowest(input2), 0.0001);
  }
    
}
```
