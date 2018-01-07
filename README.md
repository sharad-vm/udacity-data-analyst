# Udacity Data Analyst - Practice

### 1. Describe a data project you worked on recently.

### 2. You are given a ten piece box of chocolate truffles. You know based on the label that six of the pieces have an orange cream filling and four of the pieces have a coconut filling. If you were to eat four pieces in a row, what is the probability that the first two pieces you eat have an orange cream filling and the last two have a coconut filling?

  chocolate truffles in the box = 10
  truffles with orange cream filling (C) = 6
  truffles with coconut filling (O) = 4
  
  ##### eat four pieces in a row
  
  1st piece
  > Probability of 1st piece being a truffle with orange filling, P(O) = 6/10
  
  2nd piece
  > Probability of 1st piece being a truffle with orange filling, P(O) = 5/9
  
  3rd piece
  > Probability of 3rd piece being a truffle with coconut filling, P(C) = 4/8

  4th piece
  > Probability of 4th piece being a truffle with coconut filling, P(C) = 3/7
  
  Since all of the above probabilities are related 1 event of eating 4 truffles in a row from the box, we multiply the above probabilities
  > 6/10 * 5/9 * 4/8 * 3/7 = 0.07
 
  Therefore, the probability of the first 2 pieces of truffle having an orange cream filling when 4 pieces are eaten in a row = 0.07
  
### Follow-up question: If you were given an identical box of chocolates and again eat four pieces in a row, what is the probability that exactly two contain coconut filling?
    
  Number of combinations in which 2 truffles out of the four couls contain coconut filling = 2C4
  > 2C4 = 4!/2! (4-2)! = 6
    
  Since we already know that the probability of 2 truffles being coconut is 0.07 and we have 6 combinations where 2 truffles could be coconut, 
  > P = 0.07 * 6 = 0.42
    
  Therefore, the probability that exactly 2 out of 4 chocolate truffles contain coconut = 0.42

### 3. Given the table users:
  Table "users"
     
| Column      | Type      |
 -------------|------------
| id          | integer   |
| username    | character |
| email       | character |
| city        | character |
| state       | character |
| zip         | integer   |
| active      | boolean   |

construct a query to find the top 5 states with the highest number of active users. Include the number for each state in the query result. Example result:

| state      | num_active_users |
 ------------|------------------
| New Mexico | 502              |
| Alabama    | 495              |
| California | 300              |
| Maine      | 201              |
| Texas      | 189              |
---
    # Sum() could be used as well, but, count(*) is slightly faster
    SELECT state, count(*) AS num_active_users
    FROM users
    WHERE active = 1
    GROUP BY state
    ORDER BY count(*)
    LIMIT 5;

### 4. Define a function first_unique that takes a string as input and returns the first non-repeated (unique) character in the input string. If there are no unique characters return None. Note: Your code should be in Python.

    def first_unique(string):
    # Your code here
    return unique_char

    > first_unique('aabbcdd123')
    > c

    > first_unique('a')
    > a

    > first_unique('112233')
    > None
---
    def first_unique(string):
      unique_char = None
      for c in range(len(string)):
          # for each character, if it is not the same as any of the characters before or after it, assigns it to unique_char
          # since we only need the first character, when it finds one, it breaks out of the loop 
          if string[c] not in string[c+1:] and string[c] not in string[:c]:
              unique_char = string[c]
              break
      print (unique_char)


### 5. What are underfitting and overfitting in the context of Machine Learning? How might you balance them?

Underfitting refers to a model that performs poorly on training data and testing data. It can neither perform well on training data nor generalize and fit to testing data.

Overfitting refers to a model that performs exceptionally well on training data but poorly on training data. This happens when the algorithm picks up noise and fluctuations as concepts and matches with the training data too closely. It fails to generalize and impacts the performance on new/testing data negatively.

A balance can be obtained by picking the right features and the right number of features without over tuning the algorithm. In reality, this is a difficult step – to find the right spot between underfitting and overfitting. 

### 6. If you were to start your data analyst position today, what would be your goals a year from now?

