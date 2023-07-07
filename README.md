# 42 Header Script for Vim

## Introduction

This script is designed to automatically add the 42 header to your files in Vim. The 42 header includes information such as the file name, author, creation date, and update date. It is commonly used in 42 school projects.

## Installation

To use the 42 header script in Vim, follow these steps:

1. Open your Vim configuration file, usually located at `~/.vimrc`.
2. Add the following code to the end of the file:

```vim
let g:auth = '42username'

function! Stdheader()
    let filename = expand('%:t')
    let width = 51 "desired width for variables  
    let filename_field = repeat(' ', width - strlen(filename))
    let au_fld = repeat(' ', width - 23 - strlen(g:auth))
    let date_fld = repeat(' ', width - 34 - strlen(g:auth))
    let st_t = strftime("%Y/%m/%d %H:%M:%S")

    let header = "/* ************************************************************************** */\n"
    let header .= "/*                                                                            */\n"
    let header .= "/*                                                        :::      ::::::::   */\n"
    let header .= "/*   " . filename . filename_field .                   ":+:      :+:    :+:   */\n"
    let header .= "/*                                                    +:+ +:+         +:+     */\n"
    let header .= "/*   By: " . g:auth . " <marvin@42.fr>" . au_fld  ."+#+  +:+       +#+        */\n"
    let header .= "/*                                                +#+#+#+#+#+   +#+           */\n"
    let header .= "/*   Created: " . st_t . " by " . g:auth . date_fld ." #+#    #+#             */\n"
    let header .= "/*   Updated: " . st_t . " by " . g:auth . date_fld ."###   ########.fr       */\n"
    let header .= "/*                                                                            */\n"
    let header .= "/* ************************************************************************** */\n"

    call setline(1, header . getline(1))
    %s/\%x00/\r/g
endfunction

" Set <F1> as leader key
let mapleader = "\<F1>"

" Map <leader> to generate 42 header
nnoremap <leader> :call Stdheader()<CR>

" Map :Stdheader to generate 42 header
command! Stdheader call Stdheader()


function! UpdateHeader()
    let filename = expand('%:t')
    let width = 51 "desired width for variables
    let filename_field = repeat(' ', width - strlen(filename))
    let au_fld = repeat(' ', width - 23 - strlen(g:auth))
    let date_fld = repeat(' ', width - 34 - strlen(g:auth))
    let md_t = strftime("%Y/%m/%d %H:%M:%S")

    " check if the header exists
    let line1 = getline(1)
    if line1 != "/* ************************************************************************** */"
        return
    endif
    let line2 = getline(2)
    if line2 != "/*                                                                            */"
        return
    endif
    let line3 = getline(3)
    if line3 != "/*                                                        :::      ::::::::   */"
        return
    endif

    " update the timestamp on line 9
    let line9 = getline(9)
    if match(line9, 'Updated: \d\d\d\d/\d\d/\d\d \d\d:\d\d:\d\d by ' . g:auth . '.*') == -1
        echo "Timestamp not found"
        return
    endif
    let line9 = substitute(line9, 'Updated: \d\d\d\d/\d\d/\d\d \d\d:\d\d:\d\d', 'Updated: ' . md_t, '')
    call setline(9, line9)
endfunction

" automatically update the header on save
autocmd BufWritePre * call UpdateHeader()
```

3. Replace `'42username'` with your actual 42 username.
4. Save the file and exit.

## Usage

Once you have added the script to your Vim configuration, you can use the following commands:

- Press `<leader>` (usually mapped to `<F1>`) to generate the 42 header at the top of the current file.
- Alternatively, you can use the command `:Stdheader` to generate the 42 header.

The script will also automatically update the timestamp in the header whenever you save the file.

## Acknowledgements

This script is inspired by the 42 school curriculum. Thanks to the 42 school for providing the opportunity to work on this project.

## License

This script is released under the MIT License. See the [LICENSE](LICENSE) file for more details.
