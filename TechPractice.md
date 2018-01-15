**1. Given two strings s and t, determine whether some anagram of t is a substring of s. 
For example: if s = "udacity" and t = "ad", then the function returns True. 
Your function definition should look like: question1(s, t) and return a boolean True or False.**

```
def  question1(s,t):
    #check if some anagram of t is a substring of s
    if type(s) != str or type(t) != str:
        return 'At least one of the inputs is not a string'
    result = 'False'
    for c in t:
        if c not in s:
            break
        elif sorted(s[s.index(t[t.index(c)]):s.index(t[t.index(c)])+len(t)]) == sorted(t):
            result = 'True'
            break
    return result
```
***Test Cases***
```
def test1():
    print 'Testing..."
    print 'question1('udacity', 'ad'):', 'Pass' if True == question1('udacity', 'ad') else 'Fail'
    print 'question1(2,5):', 'Pass' if 'At least one of the inputs is not a string' == question1(2, 5) else 'Fail'
    print 'question1('ad', 'udacity'):', 'Pass' if False == question1('ad', 'udacity') else 'Fail'
    print 'question1('abcd', 'abcd'):', 'Pass' if True == question1('abcd', 'abcd') else 'Fail'
```

**2. Given a string a, find the longest palindromic substring contained in a. Your function definition should look like question2(a), and return a string.**

```
def isPalindrome(s):
    if s == s[::-1] :
        return True


def question2(s):
    palstring=''
    if type(s) != str:
        return 'The input is not a string. Please provide a string.'
    s=s.lower()
    for i, char in enumerate(s):
        for j, char in enumerate(s):
            substring = s[i:j+1]
            if isPalindrome(substring) and (len(substring) > len(palstring)):
                palstring = substring
    return palstring
```
***Test Cases***
```
def test1():
    print 'Testing...'
    print 'question2('malayalam'):', 'Pass' if 'malayalam' == question2(malayalam) else 'Fail'
    print 'question2(890):', 'Pass' if 'The input is not a string. Please provide a string.' == question2(890) else 'Fail'
    print 'question2('adacity'):', 'Pass' if 'ada' == question2('adacity') else 'Fail'
```
