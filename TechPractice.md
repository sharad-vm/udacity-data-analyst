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

test1()
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
def test2():
    print 'Testing...'
    print 'question2('malayalam'):', 'Pass' if 'malayalam' == question2(malayalam) else 'Fail'
    print 'question2(890):', 'Pass' if 'The input is not a string. Please provide a string.' == question2(890) else 'Fail'
    print 'question2('adacity'):', 'Pass' if 'ada' == question2('adacity') else 'Fail'

test2()
```

**3. Given an undirected graph G, find the minimum spanning tree within G. A minimum spanning tree connects all vertices in a graph with the smallest possible total weight of edges. Your function should take in and return an adjacency list structured like this:**

>{'A': [('B', 2)],  
> 'B': [('A', 2), ('C', 5)],   
> 'C': [('B', 5)]}
 
```
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
    print 'question3(G):', 'Pass' if G == question3(G) else 'Fail'
    print 'question3(890):', 'Pass' if 'The input is not a dictionary. Please provide a dictionary.' == question3(890) else 'Fail'
    print 'question3({}}):', 'Pass' if {} == question3({}) else 'Fail'
    
test3()
```

**5. Find the element in a singly linked list that's m elements from the end. For example, if a linked list has 5 elements, the 3rd element from the end is the 3rd element. The function definition should look like question5(ll, m), where ll is the first node of a linked list and m is the "mth number from the end". You should copy/paste the Node class below to use as a representation of a node in the linked list. Return the value of the node at that position.**

>class Node(object):
>  def __init__(self, data):
>    self.data = data
>    self.next = None

```
class Node(object):
  def __init__(self, data):
    self.data = data
    self.next = None

def get_length(ll):
    # get the length of ll
    if ll.next == None:
        return 1
    
    length_ll = 0
    current_node = ll
    current_node2 = ll.next
    while current_node != None and current_node != current_node2:
        current_node = current_node.next
        if current_node2 != None:
            current_node2 = current_node2.next
        if current_node2 != None:
            current_node2 = current_node2.next
        length_ll += 1

    if current_node == None:
        return length_ll
    else:
        return -1

def question5(ll, m):
    
    # check if a list has been provided
    if type(ll) != Node:
        return 'The input does not have a valid node. Please provide a node.'

    # check if an integer has been provided
    if type(m) != int or m==0:
        return 'The input does not have a valid integer. Please provide a valid integer.'
    
    # get the length of ll
    length_ll = get_length(ll)

    # check if the linked list is circular
    if length_ll == -1:
        return 'The list provided is a circular list.'
        
    # check if the list is ling enough
    if length_ll < m:
        return 'The provided integer is greater than the length of the list.'
    
    # store the list as 2 pointers 
    h1=ll
    h2=ll
    
    # loop through the range of m integers
    for i in range(0,m):
	    if (h1 == None):
	        return None
	    h1 = h1.next
	
	# gets the mth element
    while (h1 != None):
        h1 = h1.next
        h2 = h2.next
    return h2.data
```
***Test Cases***
```
def test5():
    A = Node(6)
    B = Node(2)
    C = Node(4)
    D = Node(3)
    E = Node(5)
    
    A.next = B
    B.next = C
    C.next = D
    D.next = E
    
    print 'Testing...'
    print 'question5(B,2):', 'Pass' if 3 == question5(B,2) else 'Fail'
    print 'question5(A,3):', 'Pass' if 4 == question5(A,3) else 'Fail'
    print 'question5(D,5):', 'Pass' if 'The provided integer is greater than the length of the list.' == question5(D,5) else 'Fail'

test5()
```
