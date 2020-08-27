# Regular expressions
Regular expressions are algebric notations used to match patters in a string.

# Meta Characters
* Unlike literal characters, they need to be escaped when matching.
* Examples are : `.` `$` `[` `]` `{` `}` `(` `)` `\` `^` `|` `?` `*` `+`

# Basics
```
1)  .       - Match all characters except New Line.
2)  ^abc    - Match "abc" at the beginning of a line.
3)  abc$    - Match "abc" at the end of a line.
4)  []      - Matches Characters within parantheses. Meta characters within these (character sets) are treated as literal chars.
5)  [^ ]    - Matches Characters NOT in brackets.
6)  |       - Either / logical OR.
7)  \       - Is used to escape special characters.
```

**NOTE**:
* In C++, character and string literals also escape characters using the backslash character (\), and this affects the syntax for constructing regular expressions with escape.
* because we pass our regex as a string literal when creating an object of regex type. We must use two backslashes if we want to skip a character in the regex. The first one would escape the next backslash and then the escaped backslash would escape the next character in the regex. Thus, if we want to do a `\*` we must do a `\\*`.

# Syntax for matching characters
* `\d`        : Digit (0-9)
* `\D`        : Not a Digit (0-9)

* `\w`        : Word Character (a-z, A-Z, 0-9, _)
* `\W`        : Not a Word Character

* `\s`        : Whitespace (space, tab, newline)
* `\S`        : Not Whitespace (space, tab, newline)

* `\b`        : Word Boundary
* `\B`        : Not a Word Boundary
* Three different positions qualify for word boundaries :
  * Before the first character in the string, if the first character is a word character.
  * Between two characters in the string, where one is a word character and the other is not a word character.
  * After the last character in the string, if the last character is a word character.

* Sometimes a particular whitespace has to be matched
  * `\n`      : Match new line
  * `\t`      : Match space

**NOTE:** In c++, for escapes such as `\d` and `\w` we must do a `\\d` and `\\w` because these are not pre-known escapes like `\n`


# Examples with digit matching
```
eg 1:       To match a phone number pattern like `123-456-789` or 123.456.789`

ans:        \d\d\d[.-]\d\d\d[.-]\d\d\d

breakdown:  \d\d\d   : first three digits
            [.-]     : dot or dash
            \d\d\d   : next three digits
            [.-]     : dot or dash
            \d\d\d   : last three digits
```

```
eg 2:       To match a phone number pattern starting with 800 or 900 like `800-456-789` or 900.456.789`

ans:        [89]00[.-]\d\d\d[.-]\d\d\d

breakdown:  [89]     : first digit 8 or 9
            00       : Next two digits = 0
            ..remaining is same as the last example
```

```
eg 3:       To match a phone number starting with digits 1-7

ans:        [1-7]00[.-]\d\d\d[.-]\d\d\d

breakdown:  Dash serves as a special character that specifies range, when used between two digits/alphabets in a char set,
            otherwise it acts as a literal character.

Follow up:  Matching multiple ranges simultaneously.... [1-7a-hA-F] (matches b/w `1-7` && `a-h` && `A-F`)
```

# Quantifiers
* Till now, our regular expressions did character matching on a one to one basis. Take a look at example 1 of digit matching, our regex is `\d\d\d[.-]\d\d\d[.-]\d\d\d`. Note how we write a seperate `\d` for each digit.
* Using quantifiers, we can specify how many instances of character/character class/group must be present to declare a match, thus allowing us to reduce the size of regex while also making them easy to read.
* The quantifiers available to us are...

```
*       - Match 0 or More
+       - Match 1 or More
?       - Match 0 or 1
{3}     - Match exactly these many
{2,}    - Match these many or more
{3,4}   - Match in this range of numbers (Minimum, Maximum)
```
* Using these, the regex from first example of digit matching can be re-written as `\d{3}[.-]\d{3}[.-]\d{3}`
* We often use either of `.*` or `.*?` to specify an *any character after this* type of pattern.
* The difference is that, `.*` is greedy and will match as much as possible, whereas  `.*?` is lazy and will match as little as possible.
* eg: When we are trying to extract comments in C++ code given string = `/*comment*/NotComment*/`
* `/\*.*\*/` will match `/*comment*/NotComment`
* `/\*.*?\*/` will match `/*comment*/`.

```
Given:

Mr. Singh is good.
Mr Singhal is smart.
Ms Saxena is dumb.Mr. Singh
Mrs. Kumar is average.
Mr. Naidu is fallen.
Mr. Y6dav is immortal.

eg 1:       Get the names of people who are males and whose names are alphanumeric.

ans:        Mr\.?\s[a-zA-Z]+\b

breakdown:  Mr          : First two characters
            \.?         : Followed by 0 or 1 `.`   (`\` is used for escaping `.`)
            \s          : Followed by a space
            [a-zA-Z]$   : Followed by 1 or more alphabets.
            \b          : A word boundary to finally extract the name (Note that "Mr. Y" would be selected without thee \b)
```

# Groups
* Groups allow us to match several different patters and they are created usind parentheses `()`.
```
eg 1: Given same data as above, get names of people whose names are alphanumeric

ans:  M(r|s|rs)\.?\s[a-zA-Z]+\b
```

* Groups can also be used to capture sections of matched regular expressions
* Given...
```
https://www.google.com
http://sudeepam.me
https://youtube.com
https://www.nasa.gov
```
* regex to capture websites: `https?://(www\.)?(\w+)(\.\w+)`
* Note that we have three groups in this regex. The groups are indexed from 1 so..
```
(www\.) : Group 1
(\w+)   : Group 2
(\.\w+) : Group 3
```
* Besides these three there is a default group 0 which is the entire matched pattern.
* We can capture a group by typing `$` or `\` (depending on the flavor of regex), followed by group number. eg: `$1`.
* This is useful for replacement operations. Say I want to replace the url with just the name of the website, I can just type `$2` in the replace option.

```
ex 2: "email one is SudeepaMpandey@gmail.com email two is sudeepam.pandey@jaypee.edu and email three is xyz_123-frd@my-work.net". Extract all emails from this sentence.

ans: [\w.-]+@[\w.-]+\.[\w.-]+
```

# Using regex with C++
* Possible in C++11 and onwards

* Initializing a regex and `regex_match()` function.
```cpp
# include <iostream>
# include <string>
# include <regex>     // to use regex in c++

using namespace std;

int main(){
  // creating a sample string
  string str = "a sample string";

  // creating a regular expression.
  regex pattern("\w{5}.*");
  
  // this function returns true if the regex pattern matches in the string str, and returns false otherwise
  bool does_match = regex_match(a, b);

  // you can also specify a range in the string as
  regex_match(a.begin(), a.begin() + 5, b);
}
```

* `regex_search()` function.
```cpp
# include <iostream>
# include <string>
# include <regex>     // to use regex in c++

using namespace std;

int main(){
    string s = "the best search engine is https://www.google.com "
               "and my peronal website is http://sudeepam.me and "
               "I watch videos at https://youtube.com and read "
               "articles at https://www.nasa.gov";

    cout << s << endl;
    regex r("https?://(www\\.)?(\\w+)(\\.\\w+)");

    // this is an object of a class called `match_results` and it
    // stores all groups from 0 to n for each matched expression
    smatch m;

    while (regex_search(s, m, r)){    // regex_search searches for the first match of r in s
        for (int i = 0; i < m.size(); i++)
            cout << m[i] << " ";
            
        s = m.suffix().str(); // s = string after the current match
        cout << "\n";
    }
    return 0;
} 
```

* `regex_replace()` function.
```cpp
#include <iostream> 
#include <string> 
#include <regex> 

using namespace std; 
  
int main() {  
    string str = "/*comment*/NotComment*/";
    regex pattern("/\\*.*?\\*/");
    
    // regex_replace() for replacing the c++ type comment in str with ""  
    string result = regex_replace(str, pattern, ""); 

    cout << str << "\n";
  	cout << result << "\n"; 
  
    return 0; 
}
```