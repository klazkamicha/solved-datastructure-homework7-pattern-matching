Download Link: https://assignmentchef.com/product/solved-datastructure-homework7-pattern-matching
<br>
For this assignment you will be coding 3 different pattern matching algorithms: Boyer-Moore, KnuthMorris-Pratt (KMP), and Rabin-Karp. There is information about all three in the javadocs with additional implementation details for KMP below. If you implement any of the three algorithms in an unexpected manner (i.e. contrary to what the Javadocs and PDF specify), <strong>you may receive a 0</strong>.

For all of the algorithms, make sure you check the simple failure cases as soon as possible. For example, if the pattern is longer than the text, don’t do any preprocessing on the pattern/text.

<h2>Knuth-Morris-Pratt</h2>

<strong>Failure Table Construction</strong>

The Knuth-Morris-Pratt (KMP) algorithm relies on using the prefix of the pattern to determine how much to shift the pattern by. The algorithm itself uses what is known as the failure table (also called failure function). There are different ways of calculating the failure table, but we are expecting one specific format described below.

For any string pattern, have a pointer i starting at the first letter, a pointer j starting at the second letter, a table called table that is the length of the pattern. Then, while j is still a valid index within pattern:

<ul>

 <li>If the characters pointed to by i and j match, then write i + 1 to index j of the table and increment i and j.</li>

 <li>If the characters pointed to by i and j do not match:

  <ul>

   <li>If i is not at 0, then change i to table[i – 1]. Do not increment j or write any value to the table.</li>

   <li>If i is at 0, then write i to index j of the table. Increment only j.</li>

  </ul></li>

</ul>

For example, for the string abacab, the failure table will be:

<table width="137">

 <tbody>

  <tr>

   <td width="23">a</td>

   <td width="23">b</td>

   <td width="23">a</td>

   <td width="23">c</td>

   <td width="23">a</td>

   <td width="23">b</td>

  </tr>

  <tr>

   <td width="23">0</td>

   <td width="23">0</td>

   <td width="23">1</td>

   <td width="23">0</td>

   <td width="23">1</td>

   <td width="23">2</td>

  </tr>

 </tbody>

</table>

For the string ababac, the failure table will be:

<table width="137">

 <tbody>

  <tr>

   <td width="23">a</td>

   <td width="23">b</td>

   <td width="23">a</td>

   <td width="23">b</td>

   <td width="23">a</td>

   <td width="23">c</td>

  </tr>

  <tr>

   <td width="23">0</td>

   <td width="23">0</td>

   <td width="23">1</td>

   <td width="23">2</td>

   <td width="23">3</td>

   <td width="23">0</td>

  </tr>

 </tbody>

</table>

For the string abaababa, the failure table will be:

<table width="183">

 <tbody>

  <tr>

   <td width="23">a</td>

   <td width="23">b</td>

   <td width="23">a</td>

   <td width="23">a</td>

   <td width="23">b</td>

   <td width="23">a</td>

   <td width="23">b</td>

   <td width="23">a</td>

  </tr>

  <tr>

   <td width="23">0</td>

   <td width="23">0</td>

   <td width="23">1</td>

   <td width="23">1</td>

   <td width="23">2</td>

   <td width="23">3</td>

   <td width="23">2</td>

   <td width="23">3</td>

  </tr>

 </tbody>

</table>

For the string aaaaaa, the failure table will be:

<table width="135">

 <tbody>

  <tr>

   <td width="23">a</td>

   <td width="23">a</td>

   <td width="23">a</td>

   <td width="23">a</td>

   <td width="23">a</td>

   <td width="23">a</td>

  </tr>

  <tr>

   <td width="23">0</td>

   <td width="23">1</td>

   <td width="23">2</td>

   <td width="23">3</td>

   <td width="23">4</td>

   <td width="23">5</td>

  </tr>

 </tbody>

</table>

<strong>Searching Algorithm</strong>

For the main searching algorithm, the search acts like a standard brute-force search for the most part, but in the case of a mismatch:

<ul>

 <li>If the mismatch occurs at index 0 of the pattern, then shift the pattern by 1.</li>

 <li>If the mismatch occurs at index j of the pattern and index i of the text, then shift the pattern such that index failure[j-1] of the pattern lines up with index i of the text, where failure is the failure table. Then, continue the comparisons at index i of the text (or index failure[j-1] of the pattern). Do <strong>not </strong>restart at index 0 of the pattern.</li>

</ul>

In addition, when a match is found, instead of shifting the pattern over by 1 to continue searching for more matches, the pattern should be shifted over by failure[j-1], where j is at pattern.length.

<h2>CharacterComparator</h2>

CharacterComparator is a comparator that takes in two characters. This allows you to see how many times you have called compare(). We will be looking at the number of times you call compare() while grading.

If you do not use the passed in comparator, this will cause tests to fail and will significantly lower your grade on this assignment.

<strong>You must implement the algorithms as they were taught in class. </strong>We are expecting <strong>exact </strong>comparison counts for this homework. If you are getting fewer comparison counts than expected, it means one of two things, either you implemented the algorithm wrong (most likely) or you are using an optimization not taught in the class (unlikely).