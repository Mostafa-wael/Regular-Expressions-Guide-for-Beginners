# Natural Language Processing (Lec 1)
## What is Natural Language Processing (NLP)?
- A field that deals with Artificial Intelligence (AI) that is concerned with enabling computers to **understand** and **process** human language.
## Problem?
- **Computer**: Need structured data.
- **Human speech**: Unstructured and ambiguous in nature.

## Early NLP Systems (ELIZA)
- Simple program that **uses pattern matching** to recognize phrases like “I need X” and translate them into suitable outputs like “What would it mean to you if you got X?”.
- Many people who interacted with ELIZA came to believe that it really understood them and their problems.
- One of the most important tools for describing text patterns: **the regular expression**.

---
## Regular Expressions
- Formally, a regular expression is an **algebraic notation** for characterizing a set of strings.
- Useful for searching in texts, we have:
  - A pattern to search for
  - And a corpus of texts to search through.
- They are case sensitive.
- Regular expressions always match the largest string they can -> Greedy
- we will use the online tool [RegEx Pal](https://www.regexpal.com/) for testing our regular expressions.
- You can use this [dummy text](https://www.lipsum.com/) for testing.

>> Note: we may show some regular expressions delimited by slashes but slashes are not part of the regular expressions.
>> Can set flag to ignore case

### Simple text
- **String**: Typing a string of characters will match that string.
    - E.g.: `/hello/` will match every `hello` in the passage.
- **Single Character**: Typing a solo characters will match that characters.
    - E.g.: `/!/` will match every `!` in the passage.
### Disjunction
- **Disjunction**: Typing characters enclosed by square brackets `[]` to match any of the characters from this list.
    ![img](img/[hH]ello.svg)
    - E.g.: `/[hH]ello/` will match every `hello` or `Hello` in the passage.
### Range
- **Range**: Typing a range of characters enclosed by square brackets `[]` and separated by dashes `-` to match any of the characters from this range.
    - E.g.: `/[a-c]ello/` will match every `aello`, `bello`, `cello` in the passage.
    - E.g.: `/[0-9]ello/` will match every `0ello`, `1ello`, `2ello`, `3ello`, `4ello`, `5ello`, `6ello`, `7ello`, `8ello`, `9ello` in the passage.
### Caret
-  **Caret**: The square braces can also be used to specify what a single character cannot be, by use of the caret `^`.
   - If the caret `^` is the first symbol after the open square brace `[`, the resulting pattern is negated.
   - E.g.: `/[^a]/` will match any single character (including special characters) except `a`.
   - E.g.: `/[^A-Z]/` will match every character that is not a capital letter.
   - E.g.: `/[^0-9]/` will match every character that is not a number.
   - E.g.: `/a[^0-9]b/` will match every `a` followed by a character that is not a number and then a `b`.
   - This is only true when the caret is the first symbol after the open square brace. If it occurs anywhere else, it usually stands for a caret.
   - E.g.: `/a^b/` will match every `a^b`.
### Quantifiers
- **Question Mark**: The `?` indicates **zero** or **one** occurrences of the **preceding** element. 
  ![img](img/colou_r.svg)
  - E.g.: `/colou?r/` matches both `color` and `colour`.
- **Asterisk**: The `*` indicates **zero** or **more** occurrences of the **preceding** element. 
  ![img](img/ab_c.svg)
  - E.g.: `/ab*c/` matches `ac`, `abc`, `abbc`, `abbbc`, and so on.
- **Plus Sign**: The `+` indicates **one** or **more** occurrences of the **preceding** element. 
  ![img](img/ab+c.svg)
  - E.g.: `/ab+c/` matches `abc`, `abbc`, `abbbc`, and so on, but not `ac`.
- **{n}**: The **preceding** item is matched **exactly n** times.
  ![img](img/ab{2}c.svg)
  - E.g.: `/ab{2}c/` matches `abbc`.
- **{min,}**: The **preceding** item is matched **min** or **more** times.
  ![img](img/ab{2,}c.svg)
  - E.g.: `/ab{2,}c/` matches `abbc`, `abbbc`, `abbbbc`, and so on.
- **{,max}**: The **preceding** item is matched **max** or **less** times.
  - E.g.: `/ab{,2}c/` matches `ac`, `abc`, `abbc`.
- **{min,max}**: The **preceding** item is matched at **between min and max** times.
  ![img](img/NLP{3,5}.svg)
  - E.g.: `/NLP{3,5}/` matches `NLPPP`, `NLPPPP`, `NLPPPPP` ,but not `NLP` or `NLPP`.
### Wildcard & Anchors
- **Dot**: The `.` matches any single character except the newline character `\n`.
  - E.g.: `/a.c/` matches `abc`, `a c`, `a1c`, `a-c`, and so on.
>> a “word” for the purposes of a regular expression is defined as any sequence of digits, underscores, or letters
- **Anchors**: 
  - **Caret**: The `^` matches the **beginning** of a **string** or a **new line** if the multiline flag is on.
    - E.g.: `/^a/` matches `a` in `abc`, but not `a` in `bac`.
  - **Dollar Sign**: The `$` matches the **end** of a **string** or a **line** if the multiline flag is on.
    - E.g.: `/a$/` matches `a` in `bca`, but not `a` in `abc` or `bac`.
  - **Word Boundary**: The `\b` matches a **word boundary** which is any non-word characters(digits, underscores, or letters).
    - E.g.: `/\bworld/` matches `world` in `hello world` and `hello-world`, but not `world` in `hello_world` or `hello5world` or `helloworld`. 
  - **Non-Word Boundary**: The `\B` matches a **non-word boundary** which is any word characters(digits, underscores, or letters).
    - E.g.: `/hello\B/` matches `hello` in `hello` in `hello world` or `hello-world` or `helloworld`, but not `hello_world` and `hello5world`.
### Grouping
- **Pipe Symbol**: The `|` matches either the **preceding** or the **following** element.
    ![img](img/hobby_ies.svg)
  - E.g.: `/hobby|ies/` matches `hobby` in `my hobby` and `ies` in `hobbies`.
- **Parenthesis**: The `()` matches one of the words in the parenthesis.
    ![img](img/hobb(y_ies).svg)
  - E.g.: `/hobb(y|ies)/` matches `hobby` in `my hobby` and `hobbies` in `my hobbies`.
#### Aliases
- **Aliases**: To save typing for common ranges.
  - **\d**: Expands to `[0-9]` and matches any digit.
    - E.g.: `/[0-9]/` matches `0` in `0abc` and `9` in `9abc`.
  - **\D**: Expands to `[^0-9]` and matches any non-digit.
    - E.g.: `/[^0-9]/` matches `abc` in `0abc5` and `bac` in `9abc8`.
  - **\w**: Expands to `[a-zA-Z0-9_]` and matches any word character(digits, underscores, or letters).
    - E.g.: `/[a-zA-Z0-9_]/` matches `ab` and `c` in `ab-c`.
  - **\W**: Expands to `[^a-zA-Z0-9_]` and matches any non-word character(digits, underscores, or letters).
    - E.g.: `/[^a-zA-Z0-9_]/` matches `-` in `ab-c`.
  - **\s**: Expands to `[ \t\n\r\f\v]` and matches any whitespace/tabs character.
    - E.g.: `/[ \t\n\r\f\v]/` matches ` ` in `a b`.
  - **\S**: Expands to `[^ \t\n\r\f\v]` and matches any non-whitespace/tabs character.
    - E.g.: `/[^ \t\n\r\f\v]/` matches `a` and `-b` in `a -b`.
### Backslash
- **Backslashes**: To refer to characters that are special themselves. 
  - **\\***: Matches the `*`.
  - **\\.**: Matches the `.`.
  - **\?**: Matches the `?`.
  - **\n**: Matches the newline character.
  - **\t**: Matches the tab character. 

## Simple Example
Write a RegEx to find cases of the English word `the`.
1. `the`:
    ![the](img/the.svg)
   - Wrong!
   - Misses The with capital `T`.
2. `[tT]he`: 
    ![tT](img/[tT]he.svg)
   - Wrong!
   - Incorrectly return texts with the embedded in other words.
   - E.g.: `other` or `theology`.
3. `\b[tT]he\b`: 
    ![\b[tT]he\b](img/_b%5BtT%5Dhe_b.svg)
   - Wrong!
   - Won’t treat underscores and numbers as word boundaries.
   - But, we want to detect sequences as `the_` or `the25`.
4. `[^a-zA-Z][tT]he[^a-zA-Z]`: 
    ![img](img/[^a-zA-Z][tT]he[^a-zA-Z].svg)
   - Wrong!
   - Here we specify that we want instances in which there are no alphabetic letters on either side of the but it misses the when it begins a line.
5. `(^|[^a-zA-Z])[tT]he([^a-zA-Z]|$)`:
    ![img](img/(^_[^a-zA-Z])[tT]he([^a-zA-Z]_$).svg)
   - Correct! 
   - By specifying that before the `the` we require either `the` beginning-of-line or a non-alphabetic character, and `the` same at the end of the line. 
   - Problems with consecutive `the`.

## Types of Errors
- The process we just went through was based on fixing two kinds of errors:
  - **False positives**, strings that we incorrectly **matched** like `other` or `there`.
  - **False negatives**, strings that we incorrectly **missed**, like `The`.
- Reducing the overall error rate for an application thus involves two antagonistic efforts:
  - Increasing **precision** (minimizing false **positives**).
  - Increasing **recall** (minimizing false **negatives**).

## Lookaround Assertions
For performing matches based on information that follows or precedes a pattern, without the information within the lookaround assertion forming part of the returned text → do not consume characters in the string, but only assert whether a match is possible or not (zero-length assertions).
- Types of lookaround assertion:
  - Positive Lookahead `(?=f)` : 
    ![img](img/a(_=b).svg)
    - Asserts that what immediately follows the current position in the string is `f`
    - `a(?=b)` will match `a` in `abc` but will not match `a` in `acb` or `bac`.
  - Positive Lookbehind `(?<=f)` : 
    - Asserts that what immediately precedes the current position in the string is `f`
    - `(?<=y)z` will match `z` in `xyz` but will not match `z` in `zyx`.
  - Negative Lookahead `(?!f)` : 
    ![img](img/a(_!b).svg)
    - Asserts that what immediately follows the current position in the string is not `f`
    - `a(?!b)` will match `a` in `acb` but will not match `a` in `abc`.
  - Negative Lookbehind `(?<!f)` : 
    - Asserts that what immediately precedes the current position in the string is not `f`
    - `(?<!y)z` will match `z` in `zyx` but will not match `z` in `xyz`.