<!-- @format -->

# The Basics Of Moving In Vim

The first thing you’ll want to learn is how to move around a file. When you’re in command mode, you’ll want to remember the following keys and what they do:

**_`h`_** moves the cursor one character to the left.

**_`l`_** moves the cursor one character to the right.

**_`j`_** moves the cursor down one line.

**_`k`_** moves the cursor up one line.

**_`0`_** moves the cursor to the beginning of the line.

**_`$`_** moves the cursor to the end of the line.

**_`w`_** move forward one word.

**_`b`_** move backward one word.

**_`G`_** to go to the last line in a file.

**_`gg`_** move to the beginning of the file.

**_` `. `_** move to the last edit.

## Editing Vim Style

**_`d`_** starts the delete operation.

**_`dd`_** deletes an entire line

**_`x`_** deletes the character that the cursor was on.

**_`dw`_** will delete a word.

**_`d0`_** will delete to the beginning of a line.

**_`d$`_** will delete to the end of a line.

**_`dgg`_** will delete to the beginning of the file.

**_`u`_** will undo the last operation.

**_`Ctrl-r`_** will redo the last undo.

## Editing Vim Style

**_`/search expression`_** search for text in the document, going forward.

**_`n`_** move the cursor to the next instance of the text from the last search. This will wrap to the beginning of the document.

**_`N`_** move the cursor to the previous instance of the text from the last search.

**_`?text`_** search for text in the document, going backwards.

**_`:%s/text/replacement text/g`_** search through the entire document for text and replace it with replacement text.

**_`:%s/text/replacement text/gc`_** search through the entire document and confirm before replacing text.

**_`:s/Mary/Jane/g`_** This will replace "Mary" with "Jane" on the current line, and you can use n to move to the next occurrence on the same line.

**_`:1delete`_** will redo the last undo.

## Copying And Pasting

**_`v`_** highlight one character at a time.

**_`V`_** highlight one line at a time.

**_`Ctrl-v`_** highlight by columns.

**_`p`_** paste text after the current line.

**_`P`_** paste text on the current line.

**_`y`_** yank text into the copy buffer.

**_`:y / yy `_** to copy the current line
