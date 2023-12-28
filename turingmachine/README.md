# Turingmachine (20 points)

#### Submission:

The turing machine simulator to create and run your submission can be found at [https://focs.ist.tugraz.at/turingmachine/](https://focs.ist.tugraz.at/turingmachine/). <br/>
**Name your file** `addition.json` <br/>
Follow the `How to submit` section of the [online turing machine guide](https://tc.tugraz.at/main/mod/page/view.php?id=19268).
In addition to the exported JSON, you should also explain how your TM works in English using 80 to 120 words in the file `addition.md`.


#### Introduction
First of all, you should understand what binary numbers are and how to add two of them.
This is well explained by:

1. During the FOCS lecture
2.  [WikiHow: Adding Binary Numbers](https://www.wikihow.com/Add-Binary-Numbers)
3. [YouTube/Khan Academy: Adding in binary](https://www.youtube.com/watch?v=RgklPQ8rbkg)

Example addition of `9` and `4` (in binary):
```
1001
0100
----
   1 <-- 1 + 0 = 1

1001
0100
----
  01 <-- 0 + 0 = 0

1001
0100
----
 101 <-- 1 + 0 = 1

1001
0100
----
1101 <-- 1 + 0 = 1

Result = 1101
```

In this case we get:
2<sup>3</sup> + 2<sup>2</sup> + 2<sup>0</sup> = 8 + 4 + 1 = 13


##### Overflow

Example addition of `9` and `14`:
```
1001
1110
----
   1 <-- 1 + 0 = 1

1001
1110
----
  11 <-- 0 + 1 = 1

1001
1110
----
 111 <-- 0 + 1 = 0

1001
1110
----
0111 <-- 1 + 1 = 0 and carry 1

Result = 10111
```
In this case we get: 2<sup>4</sup> + 2<sup>2</sup> + 2<sup>1</sup> + 2<sup>0</sup> = 16 + 4 + 2 + 1 = 23. This causes an overflow. See further below what to do if the addition overflows.

#### Task description:

You are tasked with creating a Turing machine that adds two binary numbers. <br/>
**Both input numbers have the same length** (number of bits) and are **separated by a `+`**. <br/>
To the left and the right of the equation the TM tape is filled with underscores (`_`). <br/>
At the beginning, the TM starts in the `Start` state and the **cursor is placed at the underscore (`_`) immediately right of the least significant bit of the second number** (the rightmost bit).

Example tape: (the TM starts at \*_\*)

<table>
  <tr>
    <td>...</td>
    <td>_</td>
    <td>1</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>+</td>
    <td>0</td>
    <td>0</td>
    <td>1</td>
    <td>0</td>
    <td>*_*</td>
    <td>...</td>
  </tr>
</table>

Once your TM halts by switching to the `End` state, the tape shall only contain the result of the addition (and underscores (`_`) to the left and right) and cursor shall be placed at the most significant bit (leftmost bit) of the solution. <br/>
If the addition causes an overflow, the TM must instead halt in the `Overflow` state. In this case the resulting tape is irrelevant.

Example result for `9+2` (at the end of the addition the cursor must point to \*1\* in this case):
<table class="tm-table">
  <tr>
    <td>...</td>
    <td>_</td>
    <td>*1*</td>
    <td>0</td>
    <td>1</td>
    <td>1</td>
    <td>_</td>
    <td>...</td>
  </tr>
</table>


#### Noteworthy:

- Use `Start` as initial state.
- Set only `End` and `Overflow` as final states.
- At the beginning, the tape will never be empty and both binary numbers to be added be at least 2 bits long. (e.g. `0,0,+,0,0` or `0,1+1,0`).
- If a combination of symbol and state cannot be reached during execution of the TM, you may leave that field empty.
- Any encounter of the TM with an empty field during execution will be regarded as an error!
- Your TM must be able to solve binary additions of any two binary numbers that have the same length of at least 2 bits!
- The binary numbers to be added always have the same length.
- Once you push a solution it will automatically be tested by our pipeline and you will receive the output of the public test cases. You will also see how many private test cases you pass/fail.

#### Changelog

* **2023-11-26 19:30** [YB]: Description init. 
* **2023-11-30 13:00** [YB]: Fixing some mistakes.
* **2023-12-17 14:08** [SG]: Update heading
