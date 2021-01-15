---
title: Shell
has_children: true
---

Write multi-line on terminal \(using Here Document format\):  
  `cat >  << EOL`  # Enter line 'EOL' to complete. Change leading '>' to '>>' for append.  

 Refresh terminal with applications from new packages  
  `source /etc/profile`

Unbork the terminal:  
  `reset`  
 Permutations:  
  Use `{1,2}` to apply both version 1 and version 2.  
   Generates all permutations for token  
   E.g:  
    `mkdir -p folder/{sub1,sub2}/{sub1,sub2,sub3}`  # `-p` creates parents. Creates 6 children.  
  Range:  
   `{1..100}`  
   E.g:  
    `echo {0..9}{0..9}`  # Count from 00 to 99  
 Emacs shortcuts (including command-line):  
  Clear screen:  
   `Ctrl-l`  
  Move cursor by word: `Alt-F`, `Alt-B`  
  Cut to end of line:  
   `Ctrl-k`
  Cut to beginning of line:  
   `Ctrl-u`  
  Cut previous word:  
   `Ctrl-w`  
  Paste:  
   `Ctrl-y`  
  Open command-line in `$EDITOR` (e.g. vim, useful for long command-line, multi-line):  
   Active command-line:  
    `Ctrl-x-e`  
   Previous command-line:  
    `fc`  
  Previous argument:  
   `alt-.`  
  Search history by substring:  
   `Ctrl-r`  # Repeat `Ctrl-R` to continue searching backwards for more results  
   `Ctrl-g` to exit without clearing entry  
  Exit:  
   `Ctrl-d`  

 Color command line  
   `| ccze -m ansi`  

 Set vi mode on command line  
  `set -o vi`  

 Shell reference last argument from previous command-line  
  `!$`  

 Prevent sleep and shutdown while command line is running  
  `systemd-inhibit`   

 Enable Bash tab completion for systemd, firewalld, nmcli, etc.  
  `yum install -y bash-completion`  

 `cmd2`  
  Framework for CLI that can be used interactively or remotely, keeps history, etc.  

 How to log command line output from commands that overwrite the screen, like top, curl, etc.?  

 Run command with \(SIGHUP\) signal after \(1 minute\) timeout:  
  `timeout -sHUP 1m`   

 Command-line interface  
  [https://www.codesynthesis.com/projects/cli/doc/guide/\#1](https://www.codesynthesis.com/projects/cli/doc/guide/#1)  
  [http://alexis.royer.free.fr/CLI/user-guide/cli-user-guide.html\#howto](http://alexis.royer.free.fr/CLI/user-guide/cli-user-guide.html#howto)  

 Rate-limit lines on shell:  
  `| pv -l -L <lines/s: integer> -q`

 Piping via text  
  Probably reason for slowness due to buffering  
  Use text for logging \(optionally\) from each process, but use messaging for pipeline

## Looping

Make full directory path: `mkdir -p <path>`  


Numeric range: `for i in {1..10}; do echo $i; done`

On listed files: `for i in $(ls ); do  $i; done`

pipe in arguments: `ls | xargs -I{} echo "hello {}"`

If number of files exceeds ARG\_MAX \(error 'Argument list too long'\), pipe from 'echo': `echo <glob, e.g. *.png> | xargs <command taking input as last argument>  
# e.g. mv -t takes input as last argument  
echo *.png | xargs mv -t <destination>`

## To Organize

Detach process from shell:  
  When starting:  
   `nohup  &`  
  Already running:  
   `disown -h %`  
  All processes in terminal, then exit:  
   `disown -a && exit`  

Parallel downloads (great for lots of small files):
	`parallel --gnu --argfile urlfile wget`

Search command line history
	`Ctrl-r`, enter search term. `Ctrl-r` to continue searching

Re-run command
	`!<starting text>`
	`!?<search text>?`

Find missing executables from saved list `sbin`:
	`LIST=sbin; cat $LIST | xargs which | cut -d '/' -f3 | diff $LIST - | sort --uniq | grep "^<" | cut -d ' ' -f2 > ${LIST}_missing`
	# TODO: Change cut column as needed. Would be better to cut on last slash.

Shell History:
	`$HISTFILE`

Temp directory:
	`cd $(mktemp -d)`

Shell
	`$0`, `$@`
	`set -ex`

Search in files recursively within a directory for text:
	`grep -rnw '/path/to/somewhere/' -e 'pattern'`

`less`
	next file
		`:n`
	previous file
		`:p`

echo with sudo (overcome permission denied when echoing with sudo)
	`sudo bash -c "echo <something> > <somewhere>"`

Is there a way to color code or otherwise obviously designate which computer I'm on via SSH in terminal? See bashrc.

Cut on whitespace:
  awk '{print $1}'

Here String
  <<< word
  <<< 'A quoted string'
  A word or quoted string is expanded and supplied to the command on its standard input.

Shell printf
  Allows formatting
  Unlike echo, can exit with error (upon failure)

cat with sudo
	sudo bash -c 'cat > <file>' << EOF
	<content>
	EOF

Stream (such as journalctl) without hanging
	grep --line-buffered
	sed -u

loop over lines in file, including last line (without trailing newline)
	while IFS="" read -r line || [ -n "$line" ]; do
		echo ${line}
	done < <file>

Bash:
  http://redsymbol.net/articles/unofficial-bash-strict-mode/

Shell:
	Exit on any failure:
		set +e
	Echo all commands:
		set +x

Text streams:
	Last word:
  	grep -oE '[^[:space:]]+$'
	Grep with surrounding lines:
		grep -B <lines-before> -A <lines-after> <search-regex>
  Filter stderr:
    http://www.burgerbum.com/stderr_pipe.html
    ---
    ( <command> 3>&1 1>&2 2>&3 | grep -v <regex> ) 3>&1 1>&2 2>&3
      Need to create another file descriptor for stdout, then shuffle them, filter, shuffle back

Tail until match:
	https://stackoverflow.com/questions/5024357/do-a-tail-f-until-matching-a-pattern
		sh -c 'tail -n +0 --pid=$$ -f <path to file> | { sed "/<text to match>/ q" && kill $$ ;}'

ls full paths:
	ls -d1 $PWD/*

Follow file:  
  `less +F`  
  Exit follow mode:  
   `ctrl-c`  
  Enter follow mode:  
   `F`  

Copy complete directory \(not just content\):  
  `cp -ar`    

 Check for file differences \(may check only matching files, not detect added or deleted files\)  
  `find . | xargs md5sum > /tmp/aaa`  
  `md5sum -c /tmp/aaa`  

 Copy directory to another  . Destination than contains source, not just its content.  
  `cp -ar . /data`  
 Check for file differences \(may check only matching files, not detect added or deleted files\)  
  `find . | xargs md5sum > /tmp/aaa`  
  `md5sum -c /tmp/aaa`  

