# Boyer-Moore String Search Algorithm

Aka BM algorithm, developed by [Robert S. Boyer](https://en.wikipedia.org/wiki/Robert_S._Boyer) and [J Strother Moore](https://en.wikipedia.org/wiki/J_Strother_Moore) in 1977.

The best explanation of the algorithm can be found from Prof Moore's [website](http://www.cs.utexas.edu/~moore/best-ideas/string-searching/fstrpos-example.html).

### Main Ideas:

- compare from the right to the left of the pattern string.
- preprocess pattern string by bad character rule and good suffix rule(this later is complex).
- O(n/m) best performance.

My Implementation of the algorithm(simplified) in Python can be found [here](https://github.com/guihaojin/AI-Journey-Code/blob/master/boyer_moore.py).

