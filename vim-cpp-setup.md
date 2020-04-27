# Setting up VIM for C++ development


## Using syntax highlighting

https://github.com/octol/vim-cpp-enhanced-highlight
(see [using-vim-packages.md](using-vim-packages.md) for installation
instructions)

## Creating ctags for UE4

Currently using the following to generate 2 tags files from the UE4 Source
```
ctags -R --sort=yes --c++-kinds=+p --fields=+iaS --extra=+q --language-force=C++ -f ue4runtime "${UNREALENGINE_HOME}/Engine/Source/Runtime"
ctags -R --sort=yes --c++-kinds=+p --fields=+iaS --extra=+q --language-force=C++ -f ue4developer "${UNREALENGINE_HOME}/Engine/Source/Developer"
```

## Setting up C++ code completion with ctags

* https://vim.fandom.com/wiki/C%2B%2B_code_completion 

Added to .vimrc

```
" add C++ tags
set tags+=~/.vim/tags/cpp
set tags+=~/.vim/tags/ue4runtime
set tags+=~/.vim/tags/ue4dev

" OmniCppComplete
let OmniCpp_NamespaceSearch = 1
let OmniCpp_GlobalScopeSearch = 1
let OmniCpp_ShowAccess = 1
let OmniCpp_ShowPrototypeInAbbr = 1 " show function parameters
let OmniCpp_MayCompleteDot = 1 " autocomplete after .
let OmniCpp_MayCompleteArrow = 1 " autocomplete after ->
let OmniCpp_MayCompleteScope = 1 " autocomplete after ::
let OmniCpp_DefaultNamespaces = ["std", "_GLIBCXX_STD"]
" automatically open and close the popup menu / preview window
au CursorMovedI,InsertLeave * if pumvisible() == 0|silent! pclose|endif
set completeopt=menuone,menu,longest,preview
```

## using ctags in vim

* use `:help tags` for help
* use `ctrl-]` to jump to first explanaition of a tag
* use `:ts` to list all matches
  * and then input the number
  * or just to `:ts <number>`
* use `:tags` to show the tag stack when jumping through multiple tags
* finally use `ctrl-t` twice to return to the main
