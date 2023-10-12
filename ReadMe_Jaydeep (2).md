# Compiler Design Assignment 1
This Assignment was intended to make one LLVM pass to find anticipated expressions in the code (from LLVM IR) and then hoist those anticipated expressions.

# Anticipated Expressions
They are those expressions which are executed no matter what path the program takes.

# hoisting
Hoist anticipated expressions at the most upper common dominator means we hoist expression at the common path from start to those anticipated expressions but at the closest to the start node possible.

# Algorithm
We need USE, DEF, IN and OUT sets of the each basic block of each function to find anticipated expressions and hoist them.

# step 1:
we will find USE, and DEF sets of each basic block and store them along with their expressions. for that i have created one class blueprint for to save different kind of expressions.

# step 2:
after creating DEF, USE, we need to find IN and OUT sets of each basic blocks. those IN and OUT are sets of anticipated expressions at before basic block and sets of anticipated expressions at after basic blocks respectively. 

# step 3:
once we have all 4 sets, we have anticipated expressions. so we run algorithm to hoist those anticipated expressions.
starting from start node for each basic block we traverse them in their Defth First Serach order to ensure that we have hoisted at highest possible hight (closer to start node). 

# step 4:
For each of basic block we take their IN and OUT sets and if any expressions are present at both IN and OUT then we hoist it at start of basic block becuase we do not have any defination of that expression in that basic block.
if we have any expression present at end of basic block ( OUT SET ) but not in IN set so, we hoist them at end of current basic block.

# step 5:
after that we again use Depth First Traversal from current node and look for that expression in each of basic block and find if we have that expression present in that basic block to path then we replace all uses of that basic block and delete them. 

# step 6:
we repeate that process untill we have all zeros in OUT set. means no more anticipated expressions that can be hoisted.


# Limitations:
1. we can optimise the code for time, as i have used at many places bruetforce methods instead of optimised ones.
2. i have ignored load and stores as of now in this pass.
