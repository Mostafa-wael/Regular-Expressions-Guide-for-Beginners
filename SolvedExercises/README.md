# Exercises
## 1) Write regular expressions for the following:
1. The set of all alphabetic strings:
   - We mean all the alphabetic characters repeated any number of time.
   - `[a-zA-Z]+`.
   - We can's use `\w+` as it also includes numbers and underscores.
2. The set of all lower case alphabetic strings ending in b:
   - `[a-z]*b`.
   - We used `*b` instead of `+b` because we want to match something like `b`.
   - We should always assume the possibility of matching an empty string. 
3. The set of all strings from the alphabet `a`,`b` such that each `a` is immediately preceded by and immediately followed by `b`:
   - This means that we can't see the `a` alone, it should be preceded or followed by any number of `b`s.
   - That means that we should have something like `(ab+)` in our sequence.
   - This simple regex should be preceded by any number of `b`s. Hence, it would be something like `b+(ab+)` in our sequence.
   - The previously mentioned regex will capture patters like `bbbbabbb`, but won't match `bbbabab`. 
   - We will add an asterisk after the last pattern to match any number of occurrences. 
   -  The final regex is: `b+(ab+)*`.
4. The set of all binary strings with at least four ones:
   - We are searching for `1` and `0` only patterns where the `1` should appear at least four times.
   - We can hardly code it as four ones each preceded and followed by any number of `0`s.
   - This will look like this: `0*10*10*10*10*[01]*` which is equivalent to `(0*1){4}[01]*`.
   - We can assume that the string is always binary and use a wild card like this: `([01]*1){4}[01]*`.
   - We can take more advantage of this assumption, as all the ones should be separated by a number of `0`s.
   - So, we can represent it as: `(0*1){4,}0*`. Which can be written as `(0*10*){4,}`.
   - This is another possible answer: `0*1+0*1+0*1+0*1+0*` which is equivalent to `(0*1+0*){4,}`.
5. The set of all binary strings where the number of zeros is a multiple of 3:
   - We need 3, 6, 9, ... `0`s. Zero occurrences is not allowed.
   - Those zeros can be separated by `1`s. 
   - This a possible solutions: `(1*01*01*01*)+`. 
   - Which can be rewritten as : `((1*01*){3})+`.

## 2) Write regular expressions for the following languages. 
>> By “word”, we mean an alphabetic string separated from other words by whitespace, any relevant punctuation, line breaks, and so forth. That's to say we can't use `\b` as a word boundary-can be used as string boundary- here.
1. The set of all strings with two consecutive repeated words in the same case (e.g., “Humbert Humbert” and “the the” but not “the bug” or “the big bug”):
   - When we are asked to search for repeated strings we should recall the capturing groups.
   - We need to match any word: `[a-zA-Z]+`
   - Words can be followed -separated- by any number of spaces: `([a-zA-Z]+)\s+`
   - We want to see another occurrence of the same word after the spaces: `([a-zA-Z]+)\s+\1`
   - Now we can safely add a word boundary to match whitespace, new lines, etc: `\b([a-zA-Z]+)\s+\1\b`.
2. All strings that start at the beginning of the line with an integer and that end at the end of the line with a word:
   - Start with an integer: `^\d+`.
   - End with a word -alphabetic string-: `[a-zA-Z]+$`.
   - Any string is: `.*\b`, we added `\b` because the end of the string must be a separator.
   - Combine them: `^\d+.*\b[a-zA-Z]+$`.
   - We can go a more sophisticated way and use `^(-)?\d` instead of `^\d` to capture negative numbers: `^(-)?\d+.*\b[a-zA-Z]+$`.
3. All strings that have both the word grotto and the word raven in them (but not, e.g., words like grottos that merely contain the word grotto):
   - Capture the `grotto` word: `\bgrotto\b`.
   - Capture the `raven` word: `\braven\b`.
   - Capture the string with both `grotto` and `raven`: `.*\bgrotto\b.*\braven\b.*`.
   - This will capture them only in this order, we should consider the other order using `|` like this: `.*\bgrotto\b.*\braven\b.* | .*\braven\b.*\bgrotto\b.*`
   - What if too many permutations?

## 3) Write a regular expression that matches responses to this question: “What are blue, grey and red?” The following 6 responses should be matched:
- colours, colors: 
  - Optional `u`.
  - `colou?rs`.
- they're colours, they're colors: 
  - Optional `they're`.
  - `(they're )?colou?rs`.
- they are colours, they are colors: 
  - `they are` is also accepted.
  - `(they('|a)re )?colou?rs`.