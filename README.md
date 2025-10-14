# AIA PRACTICALS

## PRACTICAL NO: 1





### 🅑TIC TAC TOE GAME

**Python:**
```
b=[" "]*9;p="X"
w=lambda: any(b[i]==b[i+1]==b[i+2]!=" " for i in[0,3,6])or any(b[i]==b[i+3]==b[i+6]!=" "for i in[0,1,2])or b[0]==b[4]==b[8]!=" "or b[2]==b[4]==b[6]!=" "
for _ in range(9):
    print(f"{b[0]}|{b[1]}|{b[2]}\n-+-+-\n{b[3]}|{b[4]}|{b[5]}\n-+-+-\n{b[6]}|{b[7]}|{b[8]}")
    m=int(input(f"{p}'s move(1-9):"))-1
    if b[m]==" ":b[m]=p
    if w():print(p,"wins!");break
    p="XO"[p=="X"]
else:print("Draw!")
```

### 🅑Constraint- Satisfaction Problem(CSP)



**PYTHON:**
```
colors = ['R', 'G', 'B']
neighbors = {'WA':['NT','SA'],'NT':['WA','SA','Q'],'SA':['WA','NT','Q','NSW','V'],
             'Q':['NT','SA','NSW'],'NSW':['Q','SA','V'],'V':['SA','NSW'],'T':[]}

def solve(assign={}):
    if len(assign)==len(neighbors): return assign
    r=[x for x in neighbors if x not in assign][0]
    for c in colors:
        if all(assign.get(n)!=c for n in neighbors[r]):
            res=solve(assign|{r:c})
            if res: return res

print(solve())

```

### 🅒 ALPHA BETA PRUNING (MINIMAX ALGORITHM)

**Algorithm:** ALPHA BETA PRUNING (MINIMAX ALGORITHM)

**index.html:**
```
def minimax(d, idx, maxP, s, a, b, h):
    if d == h: return s[idx]
    if maxP:
        v = float('-inf')
        for i in range(2):
            v = max(v, minimax(d+1, idx*2+i, 0, s, a, b, h))
            a = max(a, v)
            if b <= a: break
    else:
        v = float('inf')
        for i in range(2):
            v = min(v, minimax(d+1, idx*2+i, 1, s, a, b, h))
            b = min(b, v)
            if b <= a: break
    return v

print("The optimal value is: ",minimax(0, 0, 1, [3,5,6,9,1,2,0,-1], -999, 999, 3))

```

### 🅑 A* Algorithm

**Python:**
```
from simpleai.search import SearchProblem, astar

GOAL = 'HELLO WORLD'

class HelloProblem(SearchProblem):
    def actions(self, state):
        if len(state) < len(GOAL):
            return list(' ABCDEFGHIJKLMNOPQRSTUVWXYZ')
        else:
            return []

    def result(self, state, action):
        return state + action

    def is_goal(self, state):
        return state == GOAL

    def heuristic(self, state):
        wrong = sum([1 if state[i] != GOAL[i] else 0 for i in range(len(state))])
        missing = len(GOAL) - len(state)
        return wrong + missing

problem = HelloProblem(initial_state='')
result = astar(problem)
print(result.state)
print(result.path())

```

---

### 🅑Depth first search algorithm

**DFS:**
```
graph1 = { 
    'A': set(['B', 'C']), 
    'B': set(['A', 'D', 'E']), 
    'C': set(['A', 'F']), 
    'D': set(['B']), 
    'E': set(['B', 'F']), 
    'F': set(['C', 'E']) 
}

def DFS(graph, node, visited):
    if node not in visited:
        visited.append(node)
        for n in graph[node]:
            DFS(graph, n, visited)
    return visited

visited = DFS(graph1, 'A', [])
print(visited)

```

### 🅑Breadth First Search Algorithm

**BFS:**
```
graph1 = { 
    'A': set(['B','C']), 
    'B': set(['A','D','E']), 
    'C': set(['A','F','G']), 
    'D': set(['B']), 
    'E': set(['B']), 
    'F': set(['C','G']), 
    'G': set(['C','F']) 
}

def BFS(graph, start, explored):
    queue = [start]
    while queue:
        node = queue.pop(0)
        if node not in explored:
            explored.append(node)
            for neighbour in graph[node]:
                if neighbour not in explored:
                    queue.append(neighbour)
    return explored

explored = BFS(graph1, 'A', [])
print(explored)

```

### 🅑 4-Queen / N-Queen problem(PROLOG).

**4-Queen / N-Queen problem.:**
```
queens(Solution):- 
    permutation([1,2,3,4],Solution),safe(Solution). 
 
safe([]). 
safe([Q|Others]):- 
    safe(Others), 
    no_attack(Q,Others,1). 

no_attack(_,[],_). 
no_attack(Q,[Q1|Qs],D):- 
    Q=\=Q1+D, 
    Q=\=Q1-D, 
    D1 is D+1, 
    no_attack(Q,Qs,D1).
```

### 🅑 tower of Hanoi problem.

**tower of Hanoi problem**
```
def TOH(h, fp, tp, wp):
    if h >= 1:
        TOH(h - 1, fp, wp, tp)
        md(fp, tp)
        TOH(h - 1, wp, tp, fp)

def md(fp, tp):
    print("Moving disk from", fp, "to", tp)

# Call the function for 4 disks
TOH(4, "A", "B", "C")

```
### 🅑 Water-Jug Problem

**Water-Jug Problem:**
```
def pour(jug1, jug2):
    max1, max2, fill = 5, 7, 4
    print("%d\t%d" % (jug1, jug2))
    
    if jug2 == fill:
        return
    elif jug2 == max2:
        pour(0, jug1)
    elif jug1 != 0 and jug2 == 0:
        pour(0, jug1)
    elif jug1 == fill:
        pour(jug1, 0)
    elif jug1 < max1:
        pour(max1, jug2)
    elif jug1 < (max2 - jug2):
        pour(0, jug1 + jug2)
    else:
        pour(jug1 - (max2 - jug2), max2)

print("JUG1\tJUG2")
pour(0, 0)

```

### 🅑  shuffle deck of cards

**shuffle deck of cards:**
```
import itertools
import random

# Create a deck of 52 cards
deck = list(itertools.product(range(1, 14), ['Spade', 'Heart', 'Diamond', 'Club']))

# Shuffle the deck
random.shuffle(deck)

# Draw 5 cards
print("You got:")
for i in range(5):
    print(deck[i][0], "of", deck[i][1])
```

### 🅑  prolog code for associative law

**prolog code for associative law:**
```
associative_law(A,B,C,Result):- 
    Result is A+(B+C). 
 
expression1(2,3,4). 
expression2(5,6,7). 

derive_result:- 
    expression1(A,B,C), 
    associative_law(A,B,C,Result1), 
    expression2(X,Y,Z), 
    associative_law(X,Y,Z,Result2), 
    write('Result of expression1 using associative law:'),write(Result1),nl, 
    write('Result of expression2 using associative law:'),write(Result2),nl. 
```

### 🅑  prolog code for distributive law

**prolog code for distributive law:**
```
distributive_law(A,B,C,Result):- 
    Result is A*(B+C). 

expression1(2,3,4). 
expression2(5,6,7). 
 
derive_result:- 
    expression1(A,B,C), 
    distributive_law(A,B,C,Result1), 
    expression2(X,Y,Z), 
    distributive_law(X,Y,Z,Result2), 
    write('Result of expression1 using distributive law:'),write(Result1),nl, 
    write('Result of expression2 using distributive law:'),write(Result2),nl.
```

---

### 🅑  Derive the predicate: -->Sachin is a cricketer 

**Derive the predicate: -->Sachin is a cricketer :**

``` 
%----------- 
% Facts 
%-----------
 
% Sports domain 
isa(sachin, batsman). 
isa(batsman, cricketer). 
isa(cricketer, sportsperson). 
% Science domain 
isa(einstein, scientist). 
isa(scientist, human). 
 
% Vehicle domain 
isa(tesla_model3, car). 
isa(car, vehicle). 
isa(vehicle, machine). 
 
% Animal domain 
isa(parrot, bird). 
isa(bird, animal). 
 
%-----------
% Rules 
%-----------
% Direct or transitive relation 
isa(X, Y) :- 
isa(X, Z), 
isa(Z, Y).
```

### 🅑 Write a program which contains three predicates: male, female, and  parent. Make rules for following family relations: father, mother, grandmother, brother, sister, uncle, aunt, nephew, niece and cousin.

**Relationship:**
```
male(john).
male(mike).

female(susan).
female(lisa).

parent(john, mike). 
parent(susan, mike). 
parent(john, lisa). 
parent(susan, lisa).


father(X,Y) :- male(X), parent(X,Y).

mother(X,Y) :- female(X), parent(X,Y).

brother(X,Y) :- male(X), parent(Z,X), parent(Z,Y), X \= Y.

sister(X,Y) :- female(X), parent(Z,X), parent(Z,Y), X \= Y.

sibling(X,Y) :- parent(Z,X), parent(Z,Y), X \= Y.

uncle(X,Y) :- male(X), parent(Z,Y), brother(X,Z).

aunt(X,Y) :- female(X), parent(Z,Y), sister(X,Z).

nephew(X,Y) :- male(X), parent(Z,X), sibling(Z,Y).

niece(X,Y) :- female(X), parent(Z,X), sibling(Z,Y).

cousin(X,Y) :- parent(Z,X), sibling(Z,W), parent(W,Y).


     John ── Susan
      │
   -----------
   │         │
  Mike      Lisa

```


```







*Powered by Ajay! 🎯*
