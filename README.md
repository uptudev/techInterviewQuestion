# techInterviewQuestion
This repo is here to document the different ways of handling the following prompt:

### Interview Question
```
Here we go, the last big question. Let's write the below function.

// Returns the shortest qualifier that uniquely identifies the node across the entire tree.
string GetShortestUniqueQualifier(CustomNode node);

Output: A qualifier formatted with the "Title" of the node and the necessary hierarchy represented like a path with "/".

Example 1:

    Root
        UserData
            Browser
            Word
            Private
                Word
        Windows
        Programs
            Notepad
            Word
            Browser
        Custom1
            Custom2
                Custom3


GetShortestUniqueQualifier(Root/Programs/Notepad) returns "Notepad"
GetShortestUniqueQualifier(Root/Programs/Browser) returns "Programs/Browser" (to distinguish it from "UserData/Browser")


Safe Assumptions which your code should take for granted:

    Titles never have a "/".
    
    The nodes that are passed in always are found somewhere in the tree (they aren't orphans).
    
    2 sibling nodes can not have the same name (just like 2 folders can't have the same name if they are at the same location).

Misc Notes

    You don't need to make any improvements to the main() boilerplate function, the main() function simply needs to exist to wrap the function you are building, so you won't be judge on the code in the main() function.
    The code you write for this quiz is expected to be better quality than the boilerplate code we left there.
    
    Comments are not required, to save you time, so use them only if really necessary to avoid confusion.
    
    We, of course, want the code you write for all of the questions to work correctly for many use cases, not only the example given.
    
    These are not trick questions and not intended to "show off" excessive code.
    
    Code as you would on the job to get the job done accurately, with stability, and quickly. This includes checking params if appropriate.
    
    Performance needs to be reasonable for production code, not ultra-optimized.
```

### Approach
Initially I had tried to devise a C# solution to better fit the job posting, however I had issues with my inability to debug effectively without a proper C# IDE installed, so I ported it to Java to bugfix and submit.
In the future, I may end up porting this to more languages as a side project, as the methods used should work across most languages.
I just simply had IntelliJ installed and ready to go, and installing VSCode et al. would have taken longer than just rewriting the function.

I had two main approaches to do this: 

#### DFS MaxDepth

Using a DFS, operating on all nodes where `node.Title == target.Title`; add words to the qualifiers of both until they become dissimilar, taking note of the iteration depth.
Take the max of all results and push the target qualifier with that depth to output.

#### HashSet Iteration

Initialize a `HashSet<String>`, then populate the HashSet with all possible qualifiers in the tree. Check to see if the `targetQualifier` substrings are in the HashSet, adding a level of context everytime it's found.

Now, while the DFS function seemed more efficient at first glance, I was unable to get desired behaviour out of it, due in part to the way the recursion was checking for uniqueness.
As such, I decided to go with the iterative solution to get the job done, as HashSets make this much easier.