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
    " Code for generating the 42 header
endfunction

nnoremap <leader> :call Stdheader()<CR>
command! Stdheader call Stdheader()

function! UpdateHeader()
    " Code for updating the 42 header
endfunction

autocmd BufWritePre * call UpdateHeader()
```

3. Replace `'42username'` with your actual 42 username.
4. Save the file and exit.

## Usage

Once you have added the script to your Vim configuration, you can use the following commands:

- Press `<leader>` (usually mapped to `<F1>`) to generate the 42 header at the top of the current file.
- Alternatively, you can use the command `:Stdheader` to generate the 42 header.

The script will also automatically update the timestamp in the header whenever you save the file.

## Customization

If you want to customize the appearance of the 42 header, you can modify the code inside the `Stdheader` function. You can change the width, formatting, or add additional information to the header as per your requirements.

## Acknowledgements

This script is inspired by the 42 school curriculum. Thanks to the 42 school for providing the opportunity to work on this project.

## License

This script is released under the MIT License. See the [LICENSE](LICENSE) file for more details.
