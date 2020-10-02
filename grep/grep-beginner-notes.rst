grep Invocations
-----------------

    ``grep -r <pattern> <directory>``

        Recursively search the directory and print lines containing
        pattern. (Case sensitive search)

        NOTE:  If any of the files in other examples refer to a
        directory specify -r to recursively search.

    ``grep <pattern> file1 [file2] [file3]...``

        Search the specified file(s) and print lines containing
        pattern. (Case sensitive search)

    ``grep --color <pattern> <files>``

        Highlight the matching pattern in line. (Case sensitive)

    ``grep -ri <pattern> <files>``

        Default is case-sensitive search. Use -i to ignore case.

    ``grep -v <pattern> <files>``

        Print lines that do NOT match pattern

    ``grep -l <pattern> <files>``

        Print only file names of files that contain pattern.

    ``grep -L <pattern> <files>``

        Print only file names of files that do NOT contain pattern.

    ``grep -C 2 <pattern> <files>``

        Also print 2 lines BEFORE and two lines AFTER along with
        lines matching pattern. (i.e print a context around the
        matching line).

Tips
----

    I recommend creating following alias in your .bashrc file. egrep
    is more powerful and also because it is frustrating when a pattern
    does not work with grep. You may end up debugging your pattern
    forgetting that grep is not smart enough.

    ``alias grep="egrep --color"``

Patterns
--------

.. list-table:: **Basics**
    :widths: 25 55

    * - **Pattern**
      - **Action**

    * - abcdef
      - Look for exact pattern `abcdef`. Case-sensitive unless -i is
        specified with grep.

    * - [a-z]*
      - Asterisk indicates ZERO OR MORE.
        Match zero or more lower case alphabets. Matches "abc" "xyz" etc
        but not "a23bc". To match ABC, must use -i or see below.

    * - [a-z]+
      - The plus indicates ONE OR MORE
        Match one or more lower case alphabets

    * - [a-z]?
      - The question-mark indicates ZERO OR ONE
        Match 0 or 1 occurrences of a lower-case alphabet.

    * - . (period)
      - Match any character. Eg: abc.ef will match abcDef abcXef, abc$ef
        etc. You can attach a * , +, ? or * to indicate "zero or more",
        "one or more" or "zero or 1" as described above

    * - abc.def
      - Match abc followed by any single character, followed by def.
        (The period can match space, tab, special character, digit but
        not newline (I think) or NULL). Matches "abcXdef", "abc&def",
        "abc7def", "abc def", but NOT "abcdef". "abcdDef"

    * - [abc]
      - Match any character in the set abc. Square brackets define a
        set of characters to match

    * - [a-zA-Z]
      - Match lower or upper case alphabet

    * - [^A-Z]
      - Match any character that is NOT in the set [A-Z]

    * - []]
      - Match the closing square bracket itself (on some implementations
        it may need to be first character in the set to override its
        special meaning)

    * - ^abc
      - Match abc only if its at the beginning of the line

    * - abc$
      - Match abc only if its at the end of the line

    * - [0-9a-zA-Z]
      - Match an alpha numeric character
    
    * - 30\+4

      - Match a 3 followed by 1 or more zeroes, followed by 4.
        Matches 304, 3004, 300004 etc but not 34, 314 30014

    * - 300\+4
      - Match a 3 followed by 2 or more zeroes, followed by 4.
        Matches 3004, 300004 etc but not 34, 304, 314, 30014 etc

    * - 3[0-9]\+4

      - Match a 3 followed by ONE OR MORE digits and ending with a 4.
        Matches 304, 314, 3111114, 3221234566774 etc. But not 34, 3x4,
        3x6, 3000, etc

    * - 3[0-9]{4}5

      - Match a 3 followed by EXACTLY 4 digits and then followed by a 5.
        Matches 312345, 322335, 399995, but not 395 or 3x5 etc.

    * - 3[0-9]{,4}5

      - Match a 3 followed by UPTO 4 digits and then followed by a 5.
        Matches 3145, 31245, 312345, 322335, 399995, but not 3666695
        or 30000005

    * - ``3([0-9][0-9])5 xyz 3\16``

      - This is a trickier pattern. We enclose two digits in parenthesis
        and refer to that sub pattern later, using the ``\1`` syntax.

        Except for the parenthesis, the first part of pattern is like
        what we have already seen. Match 3 followed by 2 digits followed
        by a 5.

        Now this pattern must be followed by a space, then "xyz ", then
        a 3. Then it must be followed by **whatever** digits matched the
        part of pattern in the parenthesis. This must be followed by a 6.

        i.e this matches `3125 xyz 3126` and `3475 xyz 3476` because the
        **47** is common. But it dos not match `3125 xyz 3136` (because
        middle two digits 12 and 13 are different)

        Essentially, we can group parts of patterns with parenthesis
        and re-use that part (called back reference) using the backslash
        followed by n where n is a single digit number. In our example n
        is 1.

    * - "abc|def"
      - Match either "abc" OR "def" (or both). Matches abcxyz and defghi

        i.e syntax is "pattern1|pattern2"  to match either pattern1 OR
        pattern2 - where pattern1 or pattern2 can be any other legal
        pattern.

vim: ft=rst et
