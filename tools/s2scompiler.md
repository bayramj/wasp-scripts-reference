S2SCompiler
A “Simba to Simba compiler” that compiles multiple scripts into a single one. This is a very basic script and won’t understand things like “IF” compiler directives.

input is the base file name you want to compile.

path is the path to input

ERASE_DIRECTIVE_REGEX is a regex for the lines you want this to ignore when “compiling” your script. This is because if you have multiple files including the same file, you will get stuck in a recursive loop. Should be easy to modify this to use simple strings instead of regex.

The final result will be placed along thing script with input or if input is in the same directory, it will be named:

input.Replace('.simba', '-compiled.simba')
