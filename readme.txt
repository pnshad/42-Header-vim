Hi guys, if you want to add the 42 header into your files on your personal machine,(the one that updated it's updated date everytime you usave it) you can add this code to your vimrc file


the file is located in 
~/.vimrc

you can do 
vim ~/.vimrc

and add this code to the end of the file

after adding the code to vimrc, you need to to change the '42username' to your current username

let g:auth = '42username'

