**1. Given two strings s and t, determine whether some anagram of t is a substring of s. 
For example: if s = "udacity" and t = "ad", then the function returns True. 
Your function definition should look like: question1(s, t) and return a boolean True or False.**

```
def  question1(s,t):
    #check if some anagram of t is a substring of s
    if type(s) != str or type(t) != str:
        return 'At least one of the inputs is not a string'
    result = 'False'
    
    # loop through the string against which we check for an anagram 
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
    # check if a string is a palindrome
    if s == s[::-1] :
        return True


def question2(s):
    palstring=''
    if type(s) != str:
        return 'The input is not a string. Please provide a string.'
        
    # to handle capitals in the string
    s=s.lower() 
    
    # loop through the string twice so as to get their cartesian combinations
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

**3. Given an undirected graph G, find the minimum spanning tree within G. A minimum spanning tree connects all vertices in a graph with the smallest possible total weight of edges. Your function should take in and return an adjacency list structured like this:**

>{'A': [('B', 2)],  
> 'B': [('A', 2), ('C', 5)],   
> 'C': [('B', 5)]}
 
```
def question3(G):
def question3(G):
    # using Kruskal's algorithm

    if type(G) != dict:
        return 'The input is not a dictionary. Please provide a dictionary.'

    # get the keys/vertices
    keys = G.keys()

    # get unique set of edges
    edges = set()
    for i in keys:
        for j in G[i]:
            if i > j[0]:
                edges.add((j[1], j[0], i))
            elif i < j[0]:
                edges.add((j[1], i, j[0]))

    # sort the edges by weight and make it a list
    edges = sorted(list(edges))

    # loop through the edges and store the edges necessary
    output_edges = []
    keys = [set(i) for i in keys]
    for i in edges:
        # get indices of both keys
        for j in range(len(keys)):
            if i[1] in keys[j]:
                i1 = j
            if i[2] in keys[j]:
                i2 = j

        # store union in the smaller index and pop the larger index
        # also store the edge in output_edges
        if i1 < i2:
            keys[i1] = set.union(keys[i1], keys[i2])
            keys.pop(i2)
            output_edges.append(i)
        if i1 > i2:
            keys[i2] = set.union(keys[i1], keys[i2])
            keys.pop(i1)
            output_edges.append(i)

        # terminate early when all vertices are in one graph
        if len(keys) == 1:
            break
            
    # generate the ouput graph from output_edges
    output_graph = {}
    for i in output_edges:
        if i[1] in output_graph:
            output_graph[i[1]].append((i[2], i[0]))
        else:
            output_graph[i[1]] = [(i[2], i[0])]

        if i[2] in output_graph:
            output_graph[i[2]].append((i[1], i[0]))
        else:
            output_graph[i[2]] = [(i[1], i[0])]
    return output_graph
```
***Test Cases***
```
def test3():
    G = {'A': [('B', 2)],
         'B': [('A', 2), ('C', 5)],
         'C': [('B', 5)]}
    
    print 'Testing...'
    print (question3(G)) 
    print (question3(890))
    print (question3({}))
```
