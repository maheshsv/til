# Shunting-yard Algorithm

[Shunting-yard algorithm](https://en.wikipedia.org/wiki/Shunting-yard_algorithm)

> from [here](http://www.geeksforgeeks.org/expression-evaluation/).

```
1. While there are still tokens to be read in,
   1.1 Get the next token.
   1.2 If the token is:
       1.2.1 A number: push it onto the value stack.
       1.2.2 A variable: get its value, and push onto the value stack.
       1.2.3 A left parenthesis: push it onto the operator stack.
       1.2.4 A right parenthesis:
         1 While the thing on top of the operator stack is not a
           left parenthesis,
             1 Pop the operator from the operator stack.
             2 Pop the value stack twice, getting two operands.
             3 Apply the operator to the operands, in the correct order.
             4 Push the result onto the value stack.
         2 Pop the left parenthesis from the operator stack, and discard it.
       1.2.5 An operator (call it thisOp):
         1 While the operator stack is not empty, and the top thing on the
           operator stack has the same or greater precedence as thisOp,
           1 Pop the operator from the operator stack.
           2 Pop the value stack twice, getting two operands.
           3 Apply the operator to the operands, in the correct order.
           4 Push the result onto the value stack.
         2 Push thisOp onto the operator stack.
2. While the operator stack is not empty,
    1 Pop the operator from the operator stack.
    2 Pop the value stack twice, getting two operands.
    3 Apply the operator to the operands, in the correct order.
    4 Push the result onto the value stack.
3. At this point the operator stack should be empty, and the value
   stack should have only one value in it, which is the final result.
```

## Evaluate Expression in Python (half baked)

```Python
def evaluate_expression(expression):
"""
Assume expression is a list of tokens including '+', '-', '*', '/', integers and parenthesis.
"""
    val_stack, op_stack = [], []
    for token in expression:
        if type(token) is int:
            val_stack.append(token)
        elif token == '(':
            val_stack.append(token)
        elif token == ')':
            while op_stack[-1] != '(':
                operator = op_stack.pop()
                operand2 = val_stack.pop()
                operand1 = val_stack.pop()
                val_stack.append(eval_helper(operand1, operand2, operator))
            op_stack.pop()  # pop out '('
        else:
            while (len(op_stack) != 0) and has_precedence(op_stack[-1], token):
                operator = op_stack.pop()
                operand2 = val_stack.pop()
                operand1 = val_stack.pop()
                val_stack.append(eval_helper(operand1, operand2, operator)
            op_stack.append(token)
    while len(op_stack) > 0:
        operator = op_stack.pop()
        operand2 = val_stack.pop()
        operand1 = val_stack.pop()
        val_stack.append(eval_helper(operand1, operand2, operator)
    return val_stack.pop()
```
