.. list-table:: **Basics**
    :widths: 10 60

    * - **Keys**
      - **Action**

    * - ESC
      - Enter command mode

    * - :q!
      - Quit file without saving changes

    * - :wq
      - Quit file after writing (saving) changes

    * - i
      - Leaves command mode and enter insert mode. In insert mode, all
        characters, except ESC are entered as text into the file.
            
    * - :n
      - Go to next file if any (ie if you opened several files using
        `vi file1 file2 file3`, :n will take you to next file.

    * - :n file7
      - Close current file and open the file named file7

    * - :n #
      - Return to file we were editing previously

    * - :se nu
      - Display line numbers

    * - :se nonu
      - Hide line numbers

    * - :se ts=4
      - Set tabstop to 4 spaces

    * - :help topic
      - Show help on topic

.. list-table:: **Navigating within a file**
    :widths: 10 60

    * - **Keys**
      - **Action**

    * - j
      - (In command mode) Move to next line (if any)

    * - k
      - Move to previous line (if any)

    * - l
      - Move to next character on the line (if any)

    * - h
      - Move to previous character on the line (if any)

    * - |
      - Go to first character on current line

    * - ^
      - Go to first non-space character of current line

    * - $
      - Go to end of current line

    * - H
      - (Home) Go to first line on screen (not file)

    * - L
      - (Last) Go to last line on screen

    * - M
      - (Middle) Go to middle line on screen

    * - ''(single quote aka forward tick)
      -  Return to previous location in same file. Repeating this will
         toggle between same two locations.  See also CTRL-O

    * - gg
      - Go to first line of file

    * - G
      - Go to last line of file

    * - b
      - Go to beginning of current word (not incl special chars)

    * - B
      - Go to beginning of current word (incl special chars)

    * - e
      - Go to end of current word

    * - E
      - Go to end of current word including special chars.

    * - w
      - Go to next word (alphanumeric)

    * - W
      - Go to next word (including special charrs)

    * - CTRL-O
      - Return to previous location (even if it was in a different file)
        This works like the Back button in web browser and keeps going
        back in history.

    * - CTRL-I
      - Go to the next location (i.e reverse of CTRL-O) and works like
        the "Forward" button in web browsers.

    * - CTRL-E
      - Scroll one line down, without moving cursor

    * - CTRL-Y
      - Scroll one line up, without moving cursor

    * - CTRL-D
      - Scroll half a screen (page) down

    * - CTRL-U
      - Scroll half a screen (page) up

    * - CTRL-F
      - Scroll one screen (page) down

    * - CTRL-B
      - Scroll one screen (page) up

.. list-table:: **Editing**
    :widths: 10 60

    * - **Keys**
      - **Action**

    * - A
      - Append at the end of line. Use ESC to end append.

    * - I
      - Insert at the beginning of the line. Use ESC to end insert.

    * - yy
      - Yank (copy) current line. Optionally prefix with a number to
        to copy more than one line. Eg: 23yy copies 23 lines.

    * - dd
      - Delete current line. Optionally prefix with a number to delete
        more than one line. Eg: 42dd deletes 42 lines.

    * - cc
      - Change current line (enters insert mode, hit ESC after changes are
        done to enter command mode again). Optionally prefix with a number
        to change more than one line. eg: 6cc changes 6 lines.

    * - p
      - Paste last copied/deleted line below cursor

    * - P
      - Paste last copied/deleted line above cursor

    * - D
      - Delete rest of line

    * - C
      - Change rest of line (enters insert mode, hit ESC after changes are
        done to enter command mode again)

    * - rX
      - Replace the character under cursor with X where X is any character.

    * - ~
      - Change the case of the character under cursor (toggle upper/lower
        case)

    * - . (Dot)
      - Repeat the previous command

    * - u
      - Undo previous change (can be repeated to undo all changes one by
        one)

    * - CTRL-R
      - Redo previous undo. Repeat to redo all previous undo's one by one.

    * - U
      - undo all changes on the current line

    * - dw
      - Delete word (i.e alphanumeric chars till next space). Optionally
        prefix with number to delete more than one word. Eg: 4dw

    * - dW
      - Delete word including special chars, till next space.  Optionally
        prefix with number to delete more than one word. Eg: 4dW

    * - cw
      - change word (i.e alphanumeric chars till next space). Hit enter ESC
        after change to enter command mode Optionally prefix with a number
        to change more than one word.

    * - cW
      - Change word including special chars, till next space.
        Optionally prefix with a number to change more than one word.

    * - /pattern
      - Search forward in the file for pattern

    * - ?pattern
      - Search backward in the file for pattern

    * - *
      - Find the next occurrence of the word that is under cursor

    * - n
      - Find the next occurence of pattern we were searching

    * - P
      - Find the previous occurence of pattern we were searching

    * - fX
      - Find character X on the current line (going forward) where X
        is any character

    * - FX
      - Find character X on the current line (going backward) where X
        is any character

    * - ;
      - Find the next occurrence of X on the line (i.e continue the
        previous `fX` or `FX` search in same direction)

    * - , (comma)
      - Find the previous occurrence of X on the line (i.e continue
        the previous `fX` or `FX` search in opposite direction)

    * - dfX or dFX
      - Delete all characters from the current position until the
        next occurrence of X on current line. i.e this builds upoon
        the fX or FX commands above.

    * - cfX or cFX
      - Similar to dfX and dFX, except, this changes all characters
        until next occurrence of X (i.e we enter INSERT mode now.
        Hit ESC after you are done with the changes).

        With the line 

            ABC DEF ghi 123

        and cursor on g, type following chars exactly see what happens:

                    cf3GHI JKL

        followed by ESC.  (cf3 says change everything till the '3' (inclusive)
        Then we are in insert mode and "GHI JKL" are entered literally. When
        we hit ESC we are back in command mode)

    * - Pattern substitution
      - Use ``:%s /pattern1/replacement text/`` to  substitute. i.e.
        replace 'pattern1` in file with `replacement text`. If `pattern1`
        occurs more than once on a single line, this will replace only the
        first occurence on the line. To replace all occurrences, add a `g`
        at the end:

            ``:%s /pattern1/replacement text/g``

        If you dont like the substitution, you can type `u` to undo

.. list-table:: **Bookmarks**
    :widths: 10 60

    * - **Keys**
      - **Action**

    * - mX
      - Create a mark (bookmark) named X (where X is any alphanumeric char)
        (you can create several such bookmarks with different characters)

    * - 'X
      - Return to bookmark named X

    * - y'X
      - Copy all lines from current line to the previously book marked
        location X (see mX above)

    * - d'X
      - delete all lines from current line to the previously book marked
        location X (see mX above)

    * - d/pattern
      - Delete all text until next occurrence of pattern (see /pattern
        above

    * - J
      - Join next line with current line

Named buffers
-------------
    You can copy one line into buffer 'a', another line into buffer 'b'
    etc and the line stays in the buffer until you overwrite it!. Unlike
    typical CTRL-C, CTRL-V where you can only save one piece of data at a
    time, you can copy and save several pieces of data in named buffers
    and retrieve them.

    **Note that while following commands appear to be complex, they just
    build on above commands and can be extremely useful. Take a few mins
    to break them down**

.. list-table:: **Named buffers**
    :widths: 10 60

    * - **Keys**
      - **Action**

    * - "Ayy
      - Copy current line and save it in a buffer named A (where A is any
        alphanum char)

    * - "Add
      - Delete the current line and save it into a buffer named A

    * - "A23yy
      - Copy 23 lines into the named buffer A

    * - "A13dd
      - Delete 13 lines and copy into the named buffer A

    * - "Ap
      - Paste the line that was previously saved into buffer named A
        (paste below current line)

    * - "AP
      - Paste the line that was previously saved  into buffer named A
        (paste above current line)

    * - "Ay'X
      - Save all lines from current line till the previously bookmarked
        location X, into a buffer named A (this is like y'X above, except
        we save in a named buffer)

    * - "Ad'X
      - Delete all lines from current line till the previously bookmarked
        location X and save them into a buffer named A (this is like d'X
        above, except we save in a named buffer)
