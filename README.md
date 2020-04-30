This is a ctags file for extending Exuberant Ctags to accept latex.

## Generated Tags
Tags will be generated for:

DOCUMENT SECTIONS
----------------
* parts as PART *entry* 
* chapters as CHAP *entry* 
* sections as . *entry* 
* subsections .. *entry* 
* subsubsections ... *entry* 

* table of contents as TABLE OF CONTENTS
* frontmatter as FRONTMATTER
* mainmatter as MAINMATTER
* backmatter as BACKMATTER
* bibliography as BIBLIOGRAPHY

GRAPHICS AND LISTINGS
----------------
* includegraphics as GL *entry* 
* lstinputlisting as GL *entry* 

LABELS
----------------
* label as LABEL *entry* 
* reference as LABEL *entry* 
* pageref as LABEL *entry* 

DEFINITIONS
----------------
* math definitions as DEFINITION *entry* 
* math theorems as THEOREM *entry* 

COMMANDS
----------------
* \newcommand as NEW COMMAND *entry* 
* \renewcommand as RENEW COMMAND *entry* 
* \providecommand as PROVIDE COMMAND *entry* 
* \DeclareRobustCommand as DECLARE ROBUST COMMAND *entry* 
* \CheckCommand as CHECK COMMAND *entry* 

ENVIRONMENTS
----------------
* \newenvironment as NEW ENVIRONMENT *entry* 
* \renewenvironment as RENEW ENVIRONMENT *entry* 
 
## Special symbols and generated tags
The above generates the tags file that one would expect, however; the default ctags integration with vim does not like commands with special characters such as `\newcommand{@my@command}`. The ctags command will correctly add `@my@command` as type `NEW COMMAND` to the tags file, but vim will not autocomplete to it. As the use of the `@` symbol is convention in commands that the user of a class, style, or definition file is not suppsed to use (protecting the command), it is desired that these can be autocompleted since they are used in many of such files already. A further exercise is to investigate making this work as desired. 

The good news is twofold: 

1. You get a nice concise listing of all commands and definitions used in the creation of style, class, and definition files in addition to those in your tex files.
2. You can use text completion on any commands not including special characters.

## Using this ctags file with vim
To get this to work in vim, add the following to your vimrc:

```vim
let g:tagbar_type_plaintex = {
    \ 'ctagstype' : 'plaintex',
    \ 'kinds'     : [
        \ 's:sections',
        \ 'g:graphics:0:0',
        \ 'l:labels',
        \ 'r:refs:1:0',
        \ 'p:pagerefs:1:0',
        \ 'c:commands',
        \ 'e:environments'
    \ ],
    \ 'sort'    : 0,
\ }

augroup latex
    autocmd!
    autocmd BufRead,BufNewFile *.tex set filetype=tex
    autocmd BufNewFile,BufRead *.cls set filetype=tex
    autocmd BufNewFile,BufRead *.def set filetype=tex
augroup END

```

See: <https://stackoverflow.com/questions/26145505/using-vims-tagbar-plugin-for-latex-files>
