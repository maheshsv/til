# The Super Tiny Compiler

From [The Super Tiny Compiler](https://www.educative.io/collection/page/10370001/4170001/4180001) course on edicative.io.

### Three Stages

- Parsing: take raw code and turn it into AST.
- Transformation: manipulate AST.
- Code Generation: turn it into new (target) code.

***The compiler it builds compile lisp-like function calls into C-like function calls.***

### Code Excerpts

**Parsing**

```javascript

/* We're just going to take our string of code and break it down into an array
 * of tokens.
 *
 *   (add 2 (subtract 4 2))   =>   [{ type: 'paren', value: '(' }, ...]
 */

// We start by accepting an input string of code, and we're gonna set up two
// things...
function tokenizer(input) {

  // A `current` variable for tracking our position in the code like a cursor.
  var current = 0;

  // And a `tokens` array for pushing our tokens to.
  var tokens = [];

  // We start by creating a `while` loop where we are setting up our `current`
  // variable to be incremented as much as we want `inside` the loop.
  //
  // We do this because we may want to increment `current` many times within a
  // single loop because our tokens can be any length.
  while (current < input.length) {

    // We're also going to store the `current` character in the `input`.
    var char = input[current];

    // The first thing we want to check for is an open parenthesis. This will
    // later be used for `CallExpressions` but for now we only care about the
    // character.
    //
    // We check to see if we have an open parenthesis:
    if (char === '(') {

      // If we do, we push a new token with the type `paren` and set the value
      // to an open parenthesis.
      tokens.push({
        type: 'paren',
        value: '('
      });

      // Then we increment `current`
      current++;

      // And we `continue` onto the next cycle of the loop.
      continue;
    }

    // Next we're going to check for a closing parenthesis. We do the same exact
    // thing as before: Check for a closing parenthesis, add a new token,
    // increment `current`, and `continue`.
    if (char === ')') {
      tokens.push({
        type: 'paren',
        value: ')'
      });
      current++;
      continue;
    }

    // Moving on, we're now going to check for whitespace. This is interesting
    // because we care that whitespace exists to separate characters, but it
    // isn't actually important for us to store as a token. We would only throw
    // it out later.
    //
    // So here we're just going to test for existence and if it does exist we're
    // going to just `continue` on.
    var WHITESPACE = /\s/;
    if (WHITESPACE.test(char)) {
      current++;
      continue;
    }

    // The next type of token is a number. This is different than what we have
    // seen before because a number could be any number of characters and we
    // want to capture the entire sequence of characters as one token.
    //
    //   (add 123 456)
    //        ^^^ ^^^
    //        Only two separate tokens
    //
    // So we start this off when we encounter the first number in a sequence.
    var NUMBERS = /[0-9]/;
    if (NUMBERS.test(char)) {

      // We're going to create a `value` string that we are going to push
      // characters to.
      var value = '';

      // Then we're going to loop through each character in the sequence until
      // we encounter a character that is not a number, pushing each character
      // that is a number to our `value` and incrementing `current` as we go.
      while (NUMBERS.test(char)) {
        value += char;
        char = input[++current];
      }

      // After that we push our `number` token to the `tokens` array.
      tokens.push({
        type: 'number',
        value: value
      });

      // And we continue on.
      continue;
    }

    // The last type of token will be a `name` token. This is a sequence of
    // letters instead of numbers, that are the names of functions in our lisp
    // syntax.
    //
    //   (add 2 4)
    //    ^^^
    //    Name token
    //
    var LETTERS = /[a-z]/i;
    if (LETTERS.test(char)) {
      var value = '';

      // Again we're just going to loop through all the letters pushing them to
      // a value.
      while (LETTERS.test(char)) {
        value += char;
        char = input[++current];
      }

      // And pushing that value as a token with the type `name` and continuing.
      tokens.push({
        type: 'name',
        value: value
      });

      continue;
    }

    // Finally if we have not matched a character by now, we're going to throw
    // an error and completely exit.
    throw new TypeError('I dont know what this character is: ' + char);
  }

  // Then at the end of our `tokenizer` we simply return the tokens array.
  return tokens;
}

//Now we initialize the input to (add 2 (sbutract 4 2)) 
var input = '(add 2 (subtract 4 2))';

//We  will pass this input to the 'tokenizer' function that we created above.
//We will store this data in the 'tokens' array
var tokens = tokenizer(input);

//Let us print our 'tokens' array
console.log(tokens);
```

output:

```text
[ { type: 'paren', value: '(' },
  { type: 'name', value: 'add' },
  { type: 'number', value: '2' },
  { type: 'paren', value: '(' },
  { type: 'name', value: 'subtract' },
  { type: 'number', value: '4' },
  { type: 'number', value: '2' },
  { type: 'paren', value: ')' },
  { type: 'paren', value: ')' } ]
```

**Transformation**

```javascript

// So we define a traverser function which accepts an AST and a
// visitor. Inside we're going to define two functions...
function traverser(ast, visitor) {

  // A `traverseArray` function that will allow us to iterate over an array and
  // call the next function that we will define: `traverseNode`.
  function traverseArray(array, parent) {
    array.forEach(function(child) {
      traverseNode(child, parent);
    });
  }

  // `traverseNode` will accept a `node` and its `parent` node. So that it can
  // pass both to our visitor methods.
  function traverseNode(node, parent) {

    // We start by testing for the existence of a method on the visitor with a
    // matching `type`.
    var method = visitor[node.type];

    // If it exists we'll call it with the `node` and its `parent`.
    if (method) {
      method(node, parent);
    }

    // Next we are going to split things up by the current node type.
    switch (node.type) {

      // We'll start with our top level `Program`. Since Program nodes have a
      // property named body that has an array of nodes, we will call
      // `traverseArray` to traverse down into them.
      //
      // (Remember that `traverseArray` will in turn call `traverseNode` so  we
      // are causing the tree to be traversed recursively)
      case 'Program':
        traverseArray(node.body, node);
        break;

      // Next we do the same with `CallExpressions` and traverse their `params`.
      case 'CallExpression':
        traverseArray(node.params, node);
        break;

      // In the case of `NumberLiterals` we don't have any child nodes to visit,
      // so we'll just break.
      case 'NumberLiteral':
        break;

      // And again, if we haven't recognized the node type then we'll throw an
      // error.
      default:
        throw new TypeError(node.type);
    }
  }

  // Finally we kickstart the traverser by calling `traverseNode` with our ast
  // with no `parent` because the top level of the AST doesn't have a parent.
  traverseNode(ast, null);
}

// So we have our transformer function which will accept the lisp ast.
function transformer(ast) {

  // We'll create a `newAst` which like our previous AST will have a program
  // node.
  var newAst = {
    type: 'Program',
    body: []
  };

  // Next I'm going to cheat a little and create a bit of a hack. We're going to
  // use a property named `context` on our parent nodes that we're going to push
  // nodes to their parent's `context`. Normally you would have a better
  // abstraction than this, but for our purposes this keeps things simple.
  //
  // Just take note that the context is a reference *from* the old ast *to* the
  // new ast.
  ast._context = newAst.body;

  // We'll start by calling the traverser function with our ast and a visitor.
  traverser(ast, {

    // The first visitor method accepts `NumberLiterals`
    NumberLiteral: function(node, parent) {
      // We'll create a new node also named `NumberLiteral` that we will push to
      // the parent context.
      parent._context.push({
        type: 'NumberLiteral',
        value: node.value
      });
    },

    // Next up, `CallExpressions`.
    CallExpression: function(node, parent) {

      // We start creating a new node `CallExpression` with a nested
      // `Identifier`.
      var expression = {
        type: 'CallExpression',
        callee: {
          type: 'Identifier',
          name: node.name
        },
        arguments: []
      };

      // Next we're going to define a new context on the original
      // `CallExpression` node that will reference the `expression`'s arguments
      // so that we can push arguments.
      node._context = expression.arguments;

      // Then we're going to check if the parent node is a `CallExpression`.
      // If it is not...
      if (parent.type !== 'CallExpression') {

        // We're going to wrap our `CallExpression` node with an
        // `ExpressionStatement`. We do this because the top level
        // `CallExpressions` in JavaScript are actually statements.
        expression = {
          type: 'ExpressionStatement',
          expression: expression
        };
      }

      // Last, we push our (possibly wrapped) `CallExpression` to the `parent`'s
      // `context`.
      parent._context.push(expression);
    }
  });

  // At the end of our transformer function we'll return the new ast that we
  // just created.
  return newAst;
}

function printAST(ast) {
  function traverseArray(array, parent, depth) {
    array.forEach(function(child) {
      traverseNode(child, parent,depth);
    });
  }

  function traverseNode(node, parent, depth) {
    let spaces = "";
    for(let i=0; i < depth; i ++) {
      spaces = spaces + "\t";
    }
    // Next we are going to split things up by the current node type.
    switch (node.type) {
      case 'Program':
        console.log(spaces, node.type);
        traverseArray(node.body, node, depth+1);
        break;
      case 'CallExpression':
        console.log(spaces, node.type);        
        traverseArray([node.callee], node, depth+1);
        traverseArray(node.arguments, node, depth+1);
        break;
      case 'ExpressionStatement':
        console.log(spaces, node.type);        
        traverseArray([node.expression], node, depth+1);
        break;
      case 'Identifier':
        console.log(spaces, node.type, ' - ', node.name);        
        break;
      case 'NumberLiteral':
        console.log(spaces, node.type,' - ', node.value);        
        break;
      default:
        throw new TypeError(node.type);
    }
  }
  traverseNode(ast, null, 0);
}

var ast = {
  type: 'Program',
  body: [{
    type: 'CallExpression',
    name: 'add',
    params: [{
      type: 'NumberLiteral',
      value: '2'
    }, {
      type: 'CallExpression',
      name: 'subtract',
      params: [{
        type: 'NumberLiteral',
        value: '4'
      }, {
        type: 'NumberLiteral',
        value: '2'
      }]
    }]
  }]
};

var newAst = transformer(ast);
printAST(newAst);
```

output

```text
Program
	 ExpressionStatement
		 CallExpression
			 Identifier  -  add
			 NumberLiteral  -  2
			 CallExpression
				 Identifier  -  subtract
				 NumberLiteral  -  4
				 NumberLiteral  -  2
```

**Code Generation**

```javascript
function codeGenerator(node) {

  // We'll break things down by the `type` of the `node`.
  switch (node.type) {

    // If we have a `Program` node. We will map through each node in the `body`
    // and run them through the code generator and join them with a newline.
    case 'Program':
      return node.body.map(codeGenerator)
        .join('\n');

    // For `ExpressionStatements` we'll call the code generator on the nested
    // expression and we'll add a semicolon...
    case 'ExpressionStatement':
      return (
        codeGenerator(node.expression) +
        ';' // << (...because we like to code the *correct* way)
      );

    // For `CallExpressions` we will print the `callee`, add an open
    // parenthesis, we'll map through each node in the `arguments` array and run
    // them through the code generator, joining them with a comma, and then
    // we'll add a closing parenthesis.
    case 'CallExpression':
      return (
        codeGenerator(node.callee) +
        '(' +
        node.arguments.map(codeGenerator)
          .join(', ') +
        ')'
      );

    // For `Identifiers` we'll just return the `node`'s name.
    case 'Identifier':
      return node.name;

    // For `NumberLiterals` we'll just return the `node`'s value.
    case 'NumberLiteral':
      return node.value;

    // And if we haven't recognized the node, we'll throw an error.
    default:
      throw new TypeError(node.type);
  }
}

var newAST = {
  type:'Program',
  body:[{
    type: 'ExpressionStatement',
    expression: {
      type: 'CallExpression',
      callee: {
        type: 'Identifier',
        name: 'add'
      },
      arguments: [{
        type: 'NumberLiteral',
        value: '2'
      }, {
        type: 'CallExpression',
        callee: {
          type: 'Identifier',
          name: 'subtract'
        },
        arguments: [{
          type: 'NumberLiteral',
          value: '4'
        }, {
          type: 'NumberLiteral',
          value: '2'
        }]
      }]
    }
  }]
};


var output = codeGenerator(newAST);
console.log(output);
```

output

```text
add(2, subtract(4, 2));
```

**Complete Compiler**

```javascript
var input = '(add 2 (subtract 4 2))';
console.log('Input: ' + input);

var tokens = tokenizer(input);

var ast = parser(tokens);

var newAst = transformer(ast);

var output = codeGenerator(newAst);
console.log('Output: ' + output);
```

output

```text
Input: (add 2 (subtract 4 2))
Output: add(2, subtract(4, 2));
```

