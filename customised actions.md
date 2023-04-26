Browsing Marketplace actions in the workflow editor:

In your repository, browse to the workflow file you want to edit.
In the upper right corner of the file view, to open the workflow editor click pen like structure
To the right of the editor, use the GitHub Marketplace sidebar to browse actions. Actions with the badge indicate GitHub has verified the creator of the action as a partner organization.

Adding an action to your workflow:

By refencing the workflow action we can add other actions tothe workflow.
Actions referenced can be viewed as dependencies in dependency graph of the repository containing workflows

Adding an action from GitHub Marketplace:

Navigate to the action you want to use in your workflow.
Click to view the full marketplace listing for the action.
Under "Installation",copy the workflow syntax.
Paste the syntax as a new step in your workflow.
If the action requires you to provide inputs, set them in your workflow



Adding an action from the same repository:

                      reference the action with either the ‌{owner}/{repo}@{ref} or ./path/to/dir syntax in your workflow file.

Adding an action from diferent repository:

                   reference the action with the {owner}/{repo}@{ref} syntax in your workflow file.

Referencing a container on Docker Hub:
 If an action is defined in a published docker container image on docker hub you must reference the action with the docker://{image}:{tag} syntax in your workflow file. 

Features of github actions:

Using variables in workflow:       
              GitHub Actions include default environment variables for each workflow run. If you need to use custom environment variables,
               you can set these in your YAML workflow file. 

Adding scripts to the workflow:
            You can use actions to run scripts and shell commands, which are then executed on the assigned runner. 
ex:
how an action can use the run keyword to execute npm install -g bats on the runner.

jobs:
example-job:
    steps:
      - run: npm install -g bats

Sharing data between jobs:
                   If your job generates files that you want to share with another job in the same workflow, or if you want to save the 
                   files for later reference, you can store them in GitHub as artifacts.
Artifacts: are the files created when you build and test the code.Artifact might include screenshots,test results,binary or package files. They can be used by another job.  All actions and workflows called within a run have write access to that run's artifacts.

Expressions

An expression can be any combination of literal values, references to a context, or functions. You can combine literals, context references, and functions using operators.
 
Expressions are commonly used with the conditional if keyword in a workflow file. When an if conditional is true, the step will run.

Syntax:
${{ <expression> }}

Literals:Data type 	Literal value

         boolean	     true or false
         null	          null
         number	     Any number format supported by JSON.
         string	    You don't need to enclose strings in ${{ and }}. However, if you do, you must use single quotes (') around the string. 
                       To use a literal single quote, escape the literal single quote using an additional single quote (''). Wrapping with 
                       double quotes (") will throw an error.

Operators:
( )	Logical grouping
[ ]	Index
.	Property de-reference
!	Not
<	Less than
<=	Less than or equal
>	Greater than
>=	Greater than or equal
==   Equal
!=	Not equal
&&	And
||	Or

If the types do not match, GitHub coerces the type to a number. GitHub casts data types to a number using these conversions:

Null 	0
Boolean	true returns 1 false returns 0
String	Parsed from any legal JSON number format, otherwise NaN. Note: empty string returns 0.
Array	NaN
Object	NaN


A comparison of one NaN to another NaN does not result in true.
GitHub ignores case when comparing strings.
Objects and arrays are only considered equal when they are the same instance.

Functions:
GitHub offers a set of built-in functions that you can use in expressions. Some functions cast values to a string to perform comparisons. GitHub casts data types to a string using these conversions:

Null	     ''
Boolean	'true' or 'false'
Number	Decimal format, exponential for large numbers
Array	Arrays are not converted to a string
Object	Objects are not converted to a string

Status check functions: checks the status of function as expression in if conditions

success:
Returns true when none of the previous steps have failed or been canceled.

always:
Causes the step to always execute, and returns true, even when canceled. The always expression is best used at the step level or on tasks that you expect to run even when a job is canceled. For example, you can use always to send logs even when a job is canceled.

cancelled:
       Returns true if the workflow was canceled.

failure:
    Returns true when any previous step of a job fails. If you have a chain of dependent jobs, failure() returns true if any ancestor job fails.

contains:
          Returns true if search contains item.
          If search is an array, this function returns true if the item is an element in the array.
          If search is a string, this function returns true if the item is a substring of search.
          This function is not case sensitive. Casts values to a string.

contains( search, item )


startsWith:
Returns true when searchString starts with searchValue. This function is not case sensitive. Casts values to a string.
syntax:
startsWith( searchString, searchValue )

Ex:  startsWith('Hello world', 'He') returns true

endsWith:
Returns true when searchString ends with searchValue. This function is not case sensitive. Casts values to a string.

syntax: endsWith( searchString, searchValue )

Ex:  endsWith('lucky','ky') returns true


format:
Replaces values in the string, with the variable replaceValueN. Variables in the string are specified using the {N} syntax, where N is an integer. You must specify at least one replaceValue and string. There is no maximum for the number of variables (replaceValueN) you can use. Escape curly braces using double braces.

syntax:  format( string, replaceValue0, replaceValue1, ..., replaceValueN)

Ex:      format('Hello {0} {1} {2}', 'Mona', 'the', 'Octocat') returns 'Hello Mona the Octocat'.


joins:
The value for array can be an array or a string. All values in array are concatenated into a string. If you provide optionalSeparator, it is inserted between the concatenated values. Otherwise, the default separator , is used. Casts values to a string.

Syntax:  join(array, optionalSeparater)

toJSON:
Returns a pretty-print JSON representation of value. You can use this function to debug the information provided in contexts.

Syntax: toJSON(value)


fromJSON:
Returns a JSON object or JSON data type for value. You can use this function to provide a JSON object as an evaluated expression or to convert environment variables from a string.

syntax:   fromJSON(value)


hashFiles:
Returns a single hash for the set of files that matches the path pattern. You can provide a single path pattern or multiple path patterns separated by commas. The path is relative to the GITHUB_WORKSPACE directory and can only include files inside of the GITHUB_WORKSPACE.
syntax:   hashFiles(path)



















































