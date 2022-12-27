# Backtracking1
<h1>Bracktracking</h1>
    <p>Backtracking is a form of recursion</p><br>
    <p style="color: gray;">
       The usual scenario is that you are faced with a number of options ,and you most choose one of these .After you make your 
       choice you will get a new set of  option ; what set of options you get depends on what chpice you made. This procedure is
        repeated over and untill you reach a final state .If you made a good sequence of choices ,your final state is a goal state;
        if you did not,it is not. </p>
    <br>
    <p style="color: gray;">
        Conceptually ,you start at the root of tree ,the tree probably has some bad leaves,though it may be that 
        the leaves are all good or all bad.You want to get to a good leaf.AT each node ,begining with the root ,you choose one of its
         children to move to ,and you keep this up untill you get to a leaf</p><br>
         <p style="color: gray;">
            Suppose you get to a bad leaf .You can backtrack to continue the search for a good leaf by revoking your most recent choice,
            and trying out the next optin in thatset of options. If you run out of options , revoke the choice that got you here, and try
             another choice at that node. If you end up at the root with no option left, there are no good leaves to be found. </p>
         <br>
         <p>This needs an example</p><br>
         <img src="https://i.stack.imgur.com/nx9vl.gif" alt="this need an example">
 <ol type="1">
    <li>starting at Root,your optrion are A and B.you choose A.</li><br>
    <li>At A,your options are C and D,you choose C.</li><br>
    <li>D is bad Go back to A</li><br>
   <li>At A, you have no optipons left to try.Go back to Root.</li> <br>
   <li>At Root,you have already tried A.try B.</li><br>
   <li>At b, your options are E and F TryE.</li><br>
   <li>E is good Congratulations!</li><br>
 </ol>
 <p style="color: gray;">
 <p>In this example we drew a picture of a tree. The tree is an abstract model of the possible sequences of choices we could make. There is also a data structure called a tree, but usually we don't have a data structure to tell us what choices we have. (If we do have an actual tree data structure, backtracking on it is called depth-first tree searching.)</p>

 
 <h2> <B>The backtracking algorithm</h2></B>
  <fieldset style="color:#007EB4 ;"><pre> boolean solve(Node n){

  if n is a leaf node {
      if the leaf is a goal node,return true else return false 
    } else {
        for each child c of n {
            if solve(c) succeeds, return true 
          }
            return false  
           } 
          }</pre></fieldset>
 <p > Notice that the algorithm is expressed as a boolean function. This is essential to understanding the algorithm. If solve(n) is true, that means node n is part of a<br> solution--that is, node n is one of the nodes on a path from the root to some goal node We say that n is solvable. If solve(n) is false,<br> then there is no path that includes n to any goal node.Notice that the algorithm is expressed as a boolean function. This is essential to understanding1 the algorithm. If solve(n) is true, that means node n is part of a solution--that is,<br> node n is one of the nodes on a path from the root to some goal node. We say that n is solvable. If solve(n) is false, then there is no path that includes n to any goal node.</p>
</p>
<h2>How does this work?</h2>
<ul type="disk">
<li><p>If any child of n is solvable, then n is solvable.</p></li>
<li><p>If no child of n is solvable, then n is not solvable.</p></li></ul>
 <p>Hence, to decide whether any non-leaf node n is solvable (part of a path to a goal node),all you have to do is test whether any child of n<br> is solvable. This is done recursively, on each child of n. is solvable. This is done recursively, on each child of n. In the above code, this is doneIn the above code, this is done by the lines</p>
  <fieldset style="color:#007EB4 ;"/><pre >
  for each child c of n{ 
     if solve(c) succeeds, return true
     }
      return false
 </pre></fieldset>
 <p>Eventually the recursion will "bottom" out at a leaf node. If the leaf node is a goal node, it is solvable; if the leaf node is not a goal node, it is not solvable. This is our base case. <br>In the above code, this is done by the lines</p>
  
    <fieldset style="color: #007EB4 ;"/><pre>
  if n is a leaf node { 
    if the leaf is a goal node, return true
     else return false
    }
 </pre></fieldset>
 <p>The backtracking algorithm is simple but important. You should understand it thoroughly. Another way of stating it is as follows:</p>
 <ul type="disk">
 <li><h2><B>To search a tree:</h2></li></B></ul>
 <ol type="1">
  <li><p>If the tree consists of a single leaf, test whether it is a goal node.</p></li>
  <li><p>Otherwise, search the subtrees until you find one containing a goal node, or until you have searched them all unsuccessfully.</p></li>
 </ol>
 <h2> Non-recursive backtracking, using a stack</h2>
 <p> Backtracking is a rather typical recursive algorithm, and any recursive algorithm can be rewritten as a stack algorithm.<br> In fact, that is how your recursive algorithms are translated into machine or assembly language.</p>
 <fieldset><pre style="color:#007EB4 ;">boolean solve(Node n){ 
   put node n on the stack; 
     while the stack is not empty {
       if the node at the top of the stack is a leaf { 
           if it is a goal node, return true 
            else pop it off the stack 
          } 
           else { 
             if the node at the top of the stack has untried children <br>  push the next untried child onto the stack 
              else pop the node off the stack 
             }
              return false
            }</pre></fieldset>
<p > Starting from the root, the only nodes that can be pushed onto the stack are the children of the node currently on the top of the stack, and these are only pushed on one child at a time;<br> hence, the nodes on the stack at all times describe a valid path in the tree. Nodes are removed from the stack only when it is known that they have no goal nodes among their descendents. Therefore, if the root node gets removed (making the stack empty), there must have been no goal nodes at all, and no solution to the problem. <br> <br>
 When the stack algorithm terminates successfully, the nodes on the stack form (in reverse order) a path from the root to a goal node.<br> <br> 
 Similarly, when the recursive algorithm finds a goal node, the path information is embodied (in reverse order) in the sequence of recursive calls. Thus as the recursion unwinds, the path can be recovered one node at a time,<br>
  by (for instance) printing the node at the current level, or storing it in an array.<br> <br>
 Here is the recursive backtracking algorithm, modified slightly to print (in reverse order) the nodes along the successful path:</p>
 <fieldset style="color: #007EB4 ;"><pre>boolean solve(Node n) {
   if n is a leaf node {
     if the leaf is a goal node {
       print n
        return true 
      }
       else return false
       } else {
         for each child c of n { 
          if solve(c) succeeds {
             print n
              return true 
            } 
          }
           return false
           } 
          } </pre></fieldset>

         
          <h2>Keeping backtracking simple</h2>

          <p>All of these versions of the backtracking algorithm are pretty simple, but when applied to a real problem, they can get pretty cluttered up with details. Even determining whether the node is a leaf can be complex:
  for example, if the path represents a series of moves in a chess endgame problem, the leaves are the checkmate and stalemate solutions
 To keep the program clean, therefore, tests like this should be buried in methods. In a chess game, for example, you could test whether a node is a leaf by writing a<strong> gameOver method </strong>(or you could even call it<strong> isLeaf).</strong> This method would encapsulate all the ugly details of figuring out whether any possible moves remain.<br>

 
  <br><br> Notice that the backtracking altorithms require us to keep track,s for each node on the current path, which of its children have been tried already (so we don't have to try them again). In the above code we made this look simple, by just saying <strong> each child c of n.</strong> In reality, it may be difficult to figure out what the possible children are, and there may be no obvious way to step through them.<B> In chess, for example,</B> a node can represent one arrangement of pieces on a chessboard, and each child of that node can represent the arrangement after some piece has made a legal move. How do you find these children, and how do you keep track of which ones you've already examined?<br>
 
  <br> The most straightforward way to keep track of which children of the node have been tried is as follows: Upon initial entry to the node (that is, when you first get there from above), make a list of all its children. As you try each child, take it off the list. When the list is empty, there are no remaining untried children, and you can return "failure." This is a simple approach, but it may require quite a lot of additional work. <br>
  
  <br>There is an easier way to keep track of which children have been tried, if you can define an ordering on the children. If there is an ordering, and you know which child you just tried, you can determine which child to try next. <br>
 
 <br> For example, you might be able to number the <strong>children 1 through n,</strong> and try them in numerical order. Then, if you have just tried <B>child k,</B> you know that you have already tried children 1 through<strong> k-1, </strong>and you have not yet tried children<strong> k+1</strong> through<strong> n.</strong> Or, if you are trying to color a map with just four colors, you can always try1<strong> red first, then yellow, then green,then blue.</strong>  If child yellow fails, you know to try child green next. If you are searching a maze, you can try choices in the order left, straight, right<strong> (or perhaps north, east, south, west).</strong><br>
  
  <br><br> It isn't always easy to find a simple way to order the children of a node. <B>In the chess game example,</B> you might number your pieces (or perhaps the squares of the board) and try them in numerical order; but in addition each piece may also have several moves, and these must also be ordered. You can probably find some way to order the children of a node. If the ordering scheme is simple enough, you should use it; but if it is too cumbersome, you are better off keeping a list of untried children.</p><br>
  
  <h2>Example:Tree Search</h2>
  <p>For starters, let's do the simplest possible example of backtracking, which is searching an actual tree. We will also use the simplest kind of tree, a binary tree. A 
    <br><br>binary tree is a data structure composed of nodes. One node is designated as the root node. Each node can reference (point to) zero, one, or two other nodes, which are called its children. The children are referred to as the left child and/or the right child. All nodes are reachable (by one or more steps) from the root node, and there are no cycles. For our purposes, although this is not part of the definition of a binary tree,<br<br>
     we will say that a node might or might not be a goal node, and will contain its name. The first example in this paper (which we repeat here) shows a binary tree.<br><br> 
     Here's a definition of the BinaryTree class:</p>
     <fieldset style="color: #007EB4 ;"/><pre>public class BinaryTree { 
        BinaryTree leftChild = null;
        BinaryTree rightChild = null;
         boolean isGoalNode = false;
          String name; BinaryTree(String name, BinaryTree left, BinaryTree right, boolean isGoalNode) { 
            this.name = name; leftChild = left;
             rightChild = right;
              this.isGoalNode = isGoalNode; 
            } 
        }</pre></fieldset>
        <p>Next we will create a TreeSearch class, and in it we will define a method makeTree() which constructs the above binary tree.</p>
     
        <fieldset style="color:  #007EB4 ;">  <pre>static BinaryTree makeTree() {
         BinaryTree root, a, b, c, d, e, f;
          c = new BinaryTree("C", null, null, false); 
          d = new BinaryTree("D", null, null, false); 
          e = new BinaryTree("E", null, null, true);
           f = new BinaryTree("F", null, null, false);
            a = new BinaryTree("A", c, d, false); 
            b = new BinaryTree("B", e, f, false);
             root = new BinaryTree("Root", a, b, false);
              return root; 
            }</pre></fieldset>
            <p>Here's a main program to create a binary tree and try to solve it:</p>
     <p>And finally, here's the recursive backtracking routine to "solve" the binary tree by finding a goal node.</p>
    <fieldset style="color:  #007EB4 ;"><pre>public static void main(String args[]) {
         BinaryTree tree = makeTree();
          System.out.println(solvable(tree)); 
        }</pre></fieldset> 
        <p>And finally, here's the recursive backtracking routine to "solve" the binary tree by finding a goal node.s</p>
        <fieldset style="color:  #007EB4 ;"> <pre>static boolean solvable(BinaryTree node) { 
        /* 1 */ if (node == null) return false;
         /* 2 */ if (node.isGoalNode) return true;
          /* 3 */ if (solvable(node.leftChild)) return true;
           /* 4 */ if (solvable(node.rightChild)) return true;
            /* 5 */ return false; 
        }</pre></fieldset>
     <p>Here's what the numbered lines are doing:</p>
     <ol type="1">
     <li><p>If we are given a null node, it's not solvable. This statement is so that we can call this method with the children of a node, without first checking whether<br> those children actually exist.</p></li>
     <li><p>If the node we are given is a goal node, return success.</p></li>
    <li><p>See if the left child of node is solvable, and if so, conclude that node is solvable. We will only get to this line if node is non-null and is not a goal node, says to</p></li>
<li><p>Do the same thing for the right child.</p></li>
<li> <p>Since neither child of node is solvable, node itself is not solvable.</p></ol>
<p>This program runs correctly and produces the unenlightening result true.</p>
<p>Each time we ask for another node, we have to check if it is null. In the above we put that check as the first thing in solvable. An alternative would be to check <br>first whether each child exists, and recur only if they do. Here's that alternative version:</p>
    <fieldset style="color:  #007EB4 ;"><pre>static boolean solvable(BinaryTree node) { 
        if (node.isGoalNode) return true;
         if (node.leftChild != null && solvable(node.leftChild)) return true;
          if (node.rightChild != null && solvable(node.rightChild)) return true;
           return false; 
        }</pre></fieldset>
     <p>I think the first version is simpler, but the second version is slightly more efficient.</p>
     <h2>What are the children?</h2>
     <p>One of the things that simplifies the above binary tree search is that, at each choice point, you can ignore all the previous choices. Previous choices don't give you any information about what you should do next; as far as you know, both the left and the right child are possible solutions. In many problems, however, you may be able to eliminate children immediately, without recursion. <br>
        Consider, for example, the problem of four-coloring a map. It is a theorem of mathematics that any map on a plane, no matter how convoluted the countries are, can be colored with at most four colors, so that no two countries that share a border are the same color.
        <br> To color a map, you choose a color for the first country, then a color for the second country, and so on, until all countries are colored.
        <br> There are two ways to do this:</p>
    <ul type="disc">
    <li>Method 1. Try each of the four possible colors, and recur. When you run out of countries, check whether you are at a goal node.</li>
    <li>Method 2. Try only those colors that have not already been used for an adjacent country, and recur. If and when you run out of countries, you have successfully colored the map.</li></ul>
        </ul>
     <p>Let's apply each of these two methods to the problem of <br>
        coloring a checkerboard. This should be easily solvable; after all, a checkerboard only needs two colors.</p>
     <p><B>boolean mapIsOK()</B> Used by method 1 to check (at a leaf node) whether the entire map is colored correctly. 
        <br><B>boolean okToColor(int row, int column,  color)</B>
        <br> Used by method 2 to check, at every node, whether there is an adjacent node already colored with the given color. <br>
        <B>int[] nextRowAndColumn</B>
        <br>(int row, int column) Used by both methods to find the next "country" (actually, the row and column of the next square on the checkerboard).</p>
     <h2>Here's the code for method 1:</h2>
    <fieldset style="color:  #007EB4 ;"><pre>boolean explore1(int row, int column, int color) {
         if (row >= NUM_ROWS)return mapIsOK();
          map[row][column] = color;
           for (int nextColor = RED;nextColor = BLUE;nextColor++) { 
            int[] next = nextRowAndColumn(row, column); 
                if (explore1(next[0], next[1], nextColor)) return true;
             }
              return false;
             }</pre></fieldset>
     <p><B>And here's the code for method 2:</B></p>
     <fieldset style="color:  #007EB4 ;">  <pre>boolean explore2(int row, int column, int color){ 
        if (row >= NUM_ROWS)return true;
         if (okToColor(row, column, color)) {
             map[row][column] = color;
              for (int nextColor = RED; nextColor = BLUE; nextColor++) {
                 int[] next = nextRowAndColumn(row, column); 
                 if (explore2(next[0], next[1], nextColor)) return true;
                 } 
                } 
                return false;
             }</pre></fieldset>
     <p>Those appear pretty similar, and you might think they are equally good. However, the timing information suggests otherwise:</p>
      <table border ="1">
      <tr>
        <th></th>
        <th style="background-color:#D8D8D8 ;">2 by 3map </th>
        <th style="background-color:#D8D8D8 ;">3 by 3map </th>
        <th style="background-color:#D8D8D8 ;">3 by 4map </th>


      </tr>
      <tr>
      <td style="background-color:#D8D8D8 ;">Method 1:</td>
          <td>60 ms</td>
          <td>940 ms</td>
          <td>60530 ms (1 mintue)</td>
      
      </tr>
      <tr>
        <td style="background-color:#D8D8D8 ;">Method 2:</td>
        <td>0 ms</td>
        <td>0 ms</td>
        <td>0 ms</td>
      </tr>
      
        
  </table>
  <p>The zeros in the above table indicate times too short to measure (less than 1 millisecond). Why this huge difference? Either of these methods could have exponential growth. Eliminating a node automatically eliminates all of its descendents, and this will often prevent exponential growth. Conversely, by waiting to check until a leaf node is reached, exponential growth is practically guaranteed. If there is any way to eliminate children (reduce the set of choices), do so!</p>
      <h2>Debugging techniques</h2>
  <p>Often our first try at a program doesn't work, and we need to debug it. Debuggers are helpful, but sometimes we need to fall back on inserting print statements. There are some simple tricks to making effective use of print statements. These tricks can be applied to any program, but are especially useful when you are trying to debug recursive routines.</p>
  <h2>Trick #1: Indent when you print method entries and exits.</h2>
  <p> Often, the best debugging technique is to print every method call and return (or at least the most important ones). You probably want to print, for each method, what parameters it came in with, and what value it leaves with. However, if you just print a long list of these, it's hard to match up method exits with their corresponding entries. Indenting to show the level of nesting can help.</p>
  <h2>Trick #2: Use specialized print methods for debugging.</h2>
  <p> Don't clutter up your actual code more than you must. Also, remember that code inserted for debugging purposes can itself contain bugs, or (in the worst case) can affect the results, so be very careful with it.</p>
  <p>Here's our debugging code. For this trivial program, there's almost more debugging code than actual code, but in larger programs the proportions will be better.</p>
  <fieldset style="color: #007EB4  ;"><pre>static String indent = "";
     static String name(BinaryTree node) {
       if (node == null) return null;
        else return node.name;
       }
        static void enter(BinaryTree node) { 
          System.out.println(indent + "Entering solvable(" + name(node) + ")");
           indent = indent + "| ";
           }
            static boolean yes(BinaryTree node) { 
              indent = indent.substring(3); 
            System.out.println(indent + "solvable(" + name(node) + ") returns true"); 
            return true;
           } 
           static boolean no(BinaryTree node) {
             indent = indent.substring(3); 
             System.out.println(indent + "solvable(" + name(node) + ") returns false");
              return false; 
            }</pre></fieldset>
  <p>To use this code, we modify solvable as follows:</p>
  <fieldset style="color: #007EB4;"><pre>static boolean solvable(BinaryTree node) { 
    enter(node);
    if (node == null) return no(node);
      if (node.isGoalNode) return yes(node); 
      if (solvable(node.leftChild)) return yes(node);
       if (solvable(node.rightChild)) return yes(node);
        return no(node); 
      }</pre></fieldset>
  <p>And we get these results:</p>
  <p>Entering solvable(Root)
    <br> | Entering solvable(A) 
    <br>| | Entering solvable(C)
    <br> | | | Entering solvable(null) 
     <br>| | |solvable(null) returns false
     <br> | | | Entering solvable(null) 
     <br> | | | solvable(null) returns false 
    <br>  | | solvable(C) returns false 
     <br> | | Entering solvable(D) 
     <br> | | | Entering solvable(null)
      <br> | | | solvable(null) returns false 
      <br> | | | Entering solvable(null) 
      <br> | | | solvable(null) returns false
      <br>  | | solvable(D) returns false |
         <br>solvable(A) returns false
         <br> | Entering solvable(B)
          <br> | | Entering solvable(E)
          <br>  | | solvable(E) returns true 
            <br>| solvable(B) returns true
             <br>solvable(Root) returns true<br>
              true</p>
 <p><B>Trick #3: Never discard your debugging statements.</p></B>
 <p>Writing debugging statements is programming, too. Often it's as much work to debug the debugging statements as it is to debug the actual program. Once your program is working, why throw this code away? Obviously, you don't want to print out all this debugging information from a program you are ready to submit (or to turn over to your manager). You could comment out your debugging calls, but that can be a lot of work. What's more, in the above example, you would have to replace every return(yes(node)) with return(true), and every return(no(node)) with return false. With all these changes, you might introduce new bugs into your program. The simple solution is to make your debugging statements conditional. For example,</p>
 <fieldset style="color: #007EB4";><pre>static final boolean debugging = false;
   static void enter(BinaryTree node) {
     if (debugging) {
       System.out.println(indent + "Entering solvable(" + name(node) + ")");
       indent = indent + "| ";
     } 
    } 
    static boolean yes(BinaryTree node) {
       if (debugging) { 
        indent = indent.substring(3);
         System.out.println(indent + "solvable(" + name(node) + ") returns true");
         } 
         return true;
         }
          static boolean no(BinaryTree node) {
             if (debugging) {
               indent = indent.substring(3); 
               System.out.println(indent + "solvable(" + name(node) + ") returns false");
               } 
               return false;
               }</fieldset></pre>
 <p>In industry, actual programs often have multiple flags to control different aspects of debugging. Don't worry too much about making your code larger; modern compilers will notice that since the variable debugging is final, it can never be true, and the controlled code will be discarded.</p>
 <h2>Trick #4: Create an Exception.</h2>
 <p>If an Exception is thrown, you can get information about just where it happened by sending it the message printStackTrace(PrintStream). Since an Exception is an object like any other, you can create and throw your own Exceptions. However, Java programmers don't always realize that you can create an Exception without throwing it. For example, the following code</p>
 <fieldset style="color: #007EB4";><pre>new Exception("Checkpoint Charlie").printStackTrace(System.out);</pre></fieldset>
 <p>will print out a message something like this, and the program will then continue normally. That is, the above code just acts like a print statement.</p>
 <fieldset style="color: #007EB4";><pre>java.lang.Exception:
   Checkpoint Charlie at TreeSearch.
   solvable(TreeSearch.java:53) 
   at TreeSearch.solvable(TreeSearch.java:57)
    at TreeSearch.main(TreeSearch.java:72)
     at _SHELL38.run(_SHELL38.java:16) 
     at bluej.runtime.ExecServer.suspendExecution(Unknown Source)
    </pre></fieldset>
 <h2>Example: Cindy's Puzzle</h2>
 
 <p>I call the following puzzle "Cindy's puzzle" for historical reasons. You have some number n of black marbles and the same number of white marbles, and you have a playing board which consists simply of a line of 2n+1 spaces to put the marbles in. Start with the black marbles all at one end (say, the left), the white marbles all at the other end, and a free space in between.</p>
 <table>
  <tr>
  <th><img src="./images/black-ball.png"></th>
  <th><img src="./images/black-ball.png"></th>
 <th>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</th>
 <th><img src="./images/white-ball.png" ></th>
 <th><img src="./images/white-ball.png" ></th>
  </tr>
  </table>
  <p>The goal is to reverse the positions of the marbles:</p>
  <table>
  <tr>
  <th><img src="Screenshot (35).png"></th>
  <th><img src="./images/white-ball.png"></th>
  <th>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</th>
  <th><img src="./images/black-ball.png"></th>
  <th><img src="./images/black-ball.png"></th>
</tr>
</table>
<p><B>The black marbles can only move to the right, and the white marbles can only move to the left (no backing up). At each move, a marble can either:</p></B>
<ul type="disc">
  <li>Move one space ahead, if that space is clear, or</li>
  <li>Jump ahead over exactly one marble of the opposite color, if the space just beyond that marble is clear.</li>
  
</ul>
  
<p>For example, you could make the following sequence of moves:</p>
<div  style="display:flex ;">
  <h4 style="padding-left:250px;padding-right: 45px;">Starting position : &nbsp;&nbsp;&nbsp;</h4>
  <table style="background-color: #D8D8D8!important;">
  
      <th ><img src="./images/black-ball.png" alt=""></th>
      <th > <img src="./images/black-ball.png" alt=""></th>
      <th > &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;</th>
      <th ><img src="./images/white-ball.png" alt=""></th>
      <th ><img src="./images/white-ball.png" alt=""></th>
  </table><br>

</div><br>
<div  style="display:flex ;">
  <h4 style="padding-left:250px;padding-right: 45px;">Black moves ahead : </h4>
  <table style="background-color: #D8D8D8!important;">
  
      <th  style="background-color: #D8D8D8;"> <img src="./images/black-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;</th>
      <th style="background-color:#D8D8D8;"> <img src="./images/black-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"><img src="./images/white-ball.png" alt=""></th>
      <th style="background-color:#D8D8D8;"><img src="./images/white-ball.png" alt=""></th>
  </table><br>

</div><br>
<div  style="display:flex ;">
  <h4 style="padding-left:250px;padding-right: 45px;">White jumps : &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;&nbsp; &nbsp; </h4>
  <table style="background-color: #D8D8D8!important;">
  
      <th  style="background-color:#D8D8D8;"> <img src="./images/black-ball.png" alt=""></th>
      <th style="background-color:#D8D8D8;"><img src="./images/white-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"> <img src="./images/black-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;</th>
      <th style="background-color: #D8D8D8;"><img src="./images/white-ball.png" alt=""></th>
  </table><br>

</div><br>

<div  style="display:flex ;">
  <h4 style="padding-left:250px;padding-right: 45px;">Black moves ahead : </h4>
  <table  style="background-color: #D8D8D8;">
  
      <th  style="background-color: #D8D8D8;"> <img src="./images/black-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"><img src="./images/white-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"> &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;</th>
      <th style="background-color: #D8D8D8;"> <img src="./images/black-ball.png" alt=""></th>
      <th style="background-color: #D8D8D8;"><img src="./images/white-ball.png" alt=""></th>
      
  </table><br>

</div><br>
<div  style="display:flex ;">
  <h4 style="padding-left:250px;padding-right: 45px;">Black jumps :&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp; &nbsp; </h4>
  <table style="background-color: #D8D8D8!important;">
      <th > &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;</th>
      <th ><img src="./images/white-ball.png" alt=""></th>
      <th > <img src="./images/black-ball.png" alt=""></th>
      <th > <img src="./images/black-ball.png" alt=""></th>
      <th ><img src="./images/white-ball.png" alt=""></th>
  </table><br>

</div><br>
<div  style="display:flex ;">
  <h4 style="padding-left:250px;padding-right: 45px;">white moves ahead : </h4>
  <table style="background-color: #D8D8D8!important;" >
      <th > &nbsp; &nbsp; &nbsp;&nbsp; &nbsp; &nbsp;&nbsp;</th>
      <th ><img src="./images/white-ball.png" alt=""></th>
      <th > <img src="./images/black-ball.png" alt=""></th>
      <th > <img src="./images/black-ball.png" alt=""></th>
      <th ><img src="./images/white-ball.png" alt=""></th>
  </table><br>

</div>
<h4 style="padding-left:250px;padding-right: 45px;">Stuck!</h4>
<p>The backtracking method is named solvable and returns a boolean. In solvable we shall need to check whether we are at a leaf, which in this case means a position from which no further moves are possible. This isn't so easy.<br> 
  <br>Now to the program. The main program will initialize the board, and call a recursive backtracking routine to attempt to solve the puzzle. The backtracking routine will either succeed and print out a winning path, or it will fail, and the main program will have to print out the bad news. <br>
  <br>The backtracking method is named solvable and returns a boolean. In solvable we shall need to check whether we are at a leaf, which in this case means a position from which no further moves are possible. This isn't so easy. <br>
  <br> Each possible move will result in a new board position, and these new board positions are the children of the current board position. Hence to find the children of a node (that is, of a board position), we need only find the possible moves from that node. Remember that it is also highly desirable to find an ordering on these possible moves.<br>
  <br> Here it is time to stop and take thought. To make progress, we must analyze the game to some extent. Probably a number of approaches would work, and what follows is based on the way I worked it out. If you were to program this puzzle, you might find a different but equally valid approach.</p> <br>
  <br>First, notice that if a marble has a move, that move is unique: if it can move ahead one square, then it cannot jump. If it can jump, it cannot move ahead one square. This suggests that, to find the possible moves, we might assign numbers to the marbles, and check each marble in turn. When we have looked at all the marbles, we have looked at all the possible moves. This would require having a table to keep track of where each marble is, or else somehow "marking" each marble with its number and searching the board each time to find the marble we want. Neither alternative is very attractive.</p><br>
[19:45, 16/12/2022] +91 85018 67870: <br> Next, notice that for a given board position, each marble occupies a unique space. Hence, instead of talking about moving a particular marble, we can talk about moving the marble in a particular space. If a move is possible from a given space, then that must be the only move possible from that space, because if the marble in that space has a move, it is unique. There is a slight complication because not every space contains a marble, but at least the spaces (unlike the marbles) stay in one place.</p><br>

 <p><B>Now we have a simpler ordering of moves to use in our program. Just check, in order, the 2n+1 spaces of the board. For each space, either zero or one moves is possible. With this understanding, we can write a boolean method canMove(int[] board, …
  <fieldset style="color: #007EB4";><pre> 

boolean solvable(int[] board) {
  if (puzzlesoved(borad)) {
    return true
  }
  for (int position=0 ; position< BOARD_SIZE; position++) {
    if(canMove (board position)) {
      int[] newBoard= markMove(board,position);
      if(solvable(newBoard)){
        printBoard(newBoard);
        return true;
      }

    }
  }
  return false;
}
</pre></fieldset>
<br>


  <p style="color:gray;">
    Here is some output from the program


  </p>
  <font color="blue">16.</font>
  WHITE WHITE WHITE ____ BLACK BLACK BLACK
  <br>
  <font color="blue">15.</font>
  WHITE WHITE WHITE BLACK____  BLACK BLACK
  <br>
  font color="blue">14.</font>
  WHITE WHITE  ____ BLACK WHITE BLACK BLACK
  <br>
  <font color="blue">13.</font>
  WHITE_____ WHITE BLACK WHITE  BLACK BLACK
  <br>
  <font color="blue">12.</font>
  WHITE BLACK WHITE ___ WHITE  BLACK WHITE
  <br>
  <font color="blue">11.</font>
  WHITE BLACK WHITE BLACK WHITE ____ BLACK 
  <br>
  <font color="blue">10.</font>
  WHITE BLACK WHITE BLACK WHITE BLACK ____
  <br>
  <font color="blue">9.</font>
  WHITE BLACK WHITE BLACK  ____ BLACK WHITE 
  <br>
  <font color="blue">8.</font>
  WHITE BLACK ____ BLACK WHITE BLACK WHITE
  <br>
  <font color="blue">7.</font>
  ___  BLACK  WHITE BLACK WHITE BLACK WHITE
  <br>
  <font color="blue">6.</font>
  BLACK  ____  WHITE BLACK WHITE BLACK WHITE
  <br>
  <font color="blue">5.</font>
  BLACK  WHITE BLACK ___ K WHITE BLACK WHITE
  <br>
  <font color="blue">4.</font>
   BLACK  BLACK WHITE BLACK WHITE_____ WHITE
   <br>
   <font color="blue">3.</font>
  BLACK BLACK WHITE BLACK ____ WHITE WHITE
  <br>
  <font color="blue">2.</font>
   BLACK BLACK ____ BLACK WHITE WHITE WHITE
   <br>
   <font color="blue">1.</font>
  BLACK BLACK BLACK ____ WHITE WHITE WHITE
  <br>
  <p style="color:gray;">
  Notice that the solution is given in reverse order: BLACK start on out of the left and WHITE of the right, as in the <br>
  last line.I have addedd line numbers to the actual output of in order to emphasize the point.Backtracking always produce its <br>
  results (sequence of choices)in reverse order;it is up to you,the programmer;to reverse results again to get them in the reverse order.
  </p>



 
  



  

    
