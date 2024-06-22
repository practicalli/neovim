# Quickfix

!!! WARNING "Initial draft - feedback welcome"

## quickfix mode


```vim title="Open quickfix in window"
:ccopen
```

Use ++"j"++ ++"k"++ to navigate the list or `:cc` and a number to jump to a result

```vim title="jump to the 7th result"
:cc 7
```


- ++"ctrl"++ and navigation key (hjkl) to move to quickfix window
- ++"q"++ closes the quickfix buffer

## Tools

- [qf.nvim](https://github.com/ten3roberts/qf.nvim) - Quickfix and location list management for Neovim
- [nvim-bqf](https://github.com/kevinhwang91/nvim-bqf) enhanced quickfix window


Quickfix is a mode to show results of another command

- a make compile task
- the results of a search
- lsp analysis errors

Quickfix buffer can be used to jump through the errors one by one.  Each error can be viewe and fix it in turn.

quickfix is used to find a list of positions in files.

- :vimgrep| finds pattern matches.

The 'errorformat' option should be set to match the error messages from your
compiler (see |errorformat| below).

							*quickfix-ID*
Each quickfix list has a unique identifier called the quickfix ID and this
number will not change within a Vim session. The |getqflist()| function can be
used to get the identifier assigned to a list. There is also a quickfix list
number which may change whenever more than ten lists are added to a quickfix
stack.

						*location-list* *E776*
A location list is a window-local quickfix list. You get one after commands
like `:lvimgrep`, `:lgrep`, `:lhelpgrep`, `:lmake`, etc., which create a
location list instead of a quickfix list as the corresponding `:vimgrep`,
`:grep`, `:helpgrep`, `:make` do.
						*location-list-file-window*
A location list is associated with a window and each window can have a
separate location list.  A location list can be associated with only one
window.  The location list is independent of the quickfix list.

When a window with a location list is split, the new window gets a copy of the
location list.  When there are no longer any references to a location list,
the location list is destroyed.

						*quickfix-changedtick*
Every quickfix and location list has a read-only changedtick variable that
tracks the total number of changes made to the list.  Every time the quickfix
list is modified, this count is incremented. This can be used to perform an
action only when the list has changed.  The |getqflist()| and |getloclist()|
functions can be used to query the current value of changedtick.  You cannot
change the changedtick variable.

The following quickfix commands can be used.  The location list commands are
similar to the quickfix commands, replacing the 'c' prefix in the quickfix
command with 'l'.

							*E924*
If the current window was closed by an |autocommand| while processing a
location list command, it will be aborted.

							*E925* *E926*
If the current quickfix or location list was changed by an |autocommand| while
processing a quickfix or location list command, it will be aborted.

							*:cc*
:cc[!] [nr]		Display error [nr].  If [nr] is omitted, the same
:[nr]cc[!]		error is displayed again.  Without [!] this doesn't
			work when jumping to another buffer, the current buffer
			has been changed, there is the only window for the
			buffer and both 'hidden' and 'autowrite' are off.
			When jumping to another buffer with [!] any changes to
			the current buffer are lost, unless 'hidden' is set or
			there is another window for this buffer.
			The 'switchbuf' settings are respected when jumping
			to a buffer.
			When used in the quickfix window the line number can
			be used, including "." for the current line and "$"
			for the last line.

							*:ll*
:ll[!] [nr]		Same as ":cc", except the location list for the
:[nr]ll[!]		current window is used instead of the quickfix list.

						*:cn* *:cne* *:cnext* *E553*
:[count]cn[ext][!]	Display the [count] next error in the list that
			includes a file name.  If there are no file names at
			all, go to the [count] next error.  See |:cc| for
			[!] and 'switchbuf'.

							*:lne* *:lnext*
:[count]lne[xt][!]	Same as ":cnext", except the location list for the
			current window is used instead of the quickfix list.

:[count]cN[ext][!]		*:cp* *:cprevious*  *:cprev* *:cN* *:cNext*
:[count]cp[revious][!]	Display the [count] previous error in the list that
			includes a file name.  If there are no file names at
			all, go to the [count] previous error.  See |:cc| for
			[!] and 'switchbuf'.


:[count]lN[ext][!]		*:lp* *:lprevious* *:lprev* *:lN* *:lNext*
:[count]lp[revious][!]	Same as ":cNext" and ":cprevious", except the location
			list for the current window is used instead of the
			quickfix list.

							*:cabo* *:cabove*
:[count]cabo[ve]	Go to the [count] error above the current line in the
			current buffer.  If [count] is omitted, then 1 is
			used.  If there are no errors, then an error message
			is displayed.  Assumes that the entries in a quickfix
			list are sorted by their buffer number and line
			number. If there are multiple errors on the same line,
			then only the first entry is used.  If [count] exceeds
			the number of entries above the current line, then the
			first error in the file is selected.

							*:lab* *:labove*
:[count]lab[ove]	Same as ":cabove", except the location list for the
			current window is used instead of the quickfix list.

							*:cbel* *:cbelow*
:[count]cbel[ow]	Go to the [count] error below the current line in the
			current buffer.  If [count] is omitted, then 1 is
			used.  If there are no errors, then an error message
			is displayed.  Assumes that the entries in a quickfix
			list are sorted by their buffer number and line
			number.  If there are multiple errors on the same
			line, then only the first entry is used.  If [count]
			exceeds the number of entries below the current line,
			then the last error in the file is selected.

							*:lbel* *:lbelow*
:[count]lbel[ow]	Same as ":cbelow", except the location list for the
			current window is used instead of the quickfix list.

							*:cbe* *:cbefore*
:[count]cbe[fore]	Go to the [count] error before the current cursor
			position in the current buffer.  If [count] is
			omitted, then 1 is used.  If there are no errors, then
			an error message is displayed.  Assumes that the
			entries in a quickfix list are sorted by their buffer,
			line and column numbers.  If [count] exceeds the
			number of entries before the current position, then
			the first error in the file is selected.

							*:lbe* *:lbefore*
:[count]lbe[fore]	Same as ":cbefore", except the location list for the
			current window is used instead of the quickfix list.

							*:caf* *:cafter*
:[count]caf[ter]	Go to the [count] error after the current cursor
			position in the current buffer.  If [count] is
			omitted, then 1 is used.  If there are no errors, then
			an error message is displayed.  Assumes that the
			entries in a quickfix list are sorted by their buffer,
			line and column numbers.  If [count] exceeds the
			number of entries after the current position, then
			the last error in the file is selected.

							*:laf* *:lafter*
:[count]laf[ter]	Same as ":cafter", except the location list for the
			current window is used instead of the quickfix list.

							*:cnf* *:cnfile*
:[count]cnf[ile][!]	Display the first error in the [count] next file in
			the list that includes a file name.  If there are no
			file names at all or if there is no next file, go to
			the [count] next error.  See |:cc| for [!] and
			'switchbuf'.

							*:lnf* *:lnfile*
:[count]lnf[ile][!]	Same as ":cnfile", except the location list for the
			current window is used instead of the quickfix list.

:[count]cNf[ile][!]			*:cpf* *:cpfile* *:cNf* *:cNfile*
:[count]cpf[ile][!]	Display the last error in the [count] previous file in
			the list that includes a file name.  If there are no
			file names at all or if there is no next file, go to
			the [count] previous error.  See |:cc| for [!] and
			'switchbuf'.


:[count]lNf[ile][!]			*:lpf* *:lpfile* *:lNf* *:lNfile*
:[count]lpf[ile][!]	Same as ":cNfile" and ":cpfile", except the location
			list for the current window is used instead of the
			quickfix list.

							*:crewind* *:cr*
:cr[ewind][!] [nr]	Display error [nr].  If [nr] is omitted, the FIRST
			error is displayed.  See |:cc|.

							*:lrewind* *:lr*
:lr[ewind][!] [nr]	Same as ":crewind", except the location list for the
			current window is used instead of the quickfix list.

							*:cfirst* *:cfir*
:cfir[st][!] [nr]	Same as ":crewind".

							*:lfirst* *:lfir*
:lfir[st][!] [nr]	Same as ":lrewind".

							*:clast* *:cla*
:cla[st][!] [nr]	Display error [nr].  If [nr] is omitted, the LAST
			error is displayed.  See |:cc|.

							*:llast* *:lla*
:lla[st][!] [nr]	Same as ":clast", except the location list for the
			current window is used instead of the quickfix list.

							*:cq* *:cquit*
:cq[uit][!]
:{N}cq[uit][!]
:cq[uit][!] {N}		Quit Vim with error code {N}.  {N} defaults to one.
			Useful when Vim is called from another program:
			e.g., a compiler will not compile the same file again,
			`git commit` will abort the committing process, `fc`
			(built-in for shells like bash and zsh) will not
			execute the command, etc.
			{N} can also be zero, in which case Vim exits
			normally.
			WARNING: All changes in files are lost.  It works like
			":qall!" |:qall|, except that Nvim exits non-zero or
			[count].

							*:cf* *:cfi* *:cfile*
:cf[ile][!] [errorfile]	Read the error file and jump to the first error.
			This is done automatically when Vim is started with
			the -q option.  You can use this command when you
			keep Vim running while compiling.  If you give the
			name of the errorfile, the 'errorfile' option will
			be set to [errorfile].  See |:cc| for [!].
			If the encoding of the error file differs from the
			'encoding' option, you can use the 'makeencoding'
			option to specify the encoding.

							*:lf* *:lfi* *:lfile*
:lf[ile][!] [errorfile]	Same as ":cfile", except the location list for the
			current window is used instead of the quickfix list.
			You can not use the -q command-line option to set
			the location list.


:cg[etfile] [errorfile]					*:cg* *:cgetfile*
			Read the error file.  Just like ":cfile" but don't
			jump to the first error.
			If the encoding of the error file differs from the
			'encoding' option, you can use the 'makeencoding'
			option to specify the encoding.


:lg[etfile] [errorfile]					*:lg* *:lge* *:lgetfile*
			Same as ":cgetfile", except the location list for the
			current window is used instead of the quickfix list.

							*:caddf* *:caddfile*
:caddf[ile] [errorfile]	Read the error file and add the errors from the
			errorfile to the current quickfix list. If a quickfix
			list is not present, then a new list is created.
			If the encoding of the error file differs from the
			'encoding' option, you can use the 'makeencoding'
			option to specify the encoding.

							*:laddf* *:laddfile*
:laddf[ile] [errorfile]	Same as ":caddfile", except the location list for the
			current window is used instead of the quickfix list.

						*:cb* *:cbuffer* *E681*
:cb[uffer][!] [bufnr]	Read the error list from the current buffer.
			When [bufnr] is given it must be the number of a
			loaded buffer.  That buffer will then be used instead
			of the current buffer.
			A range can be specified for the lines to be used.
			Otherwise all lines in the buffer are used.
			See |:cc| for [!].

						*:lb* *:lbuffer*
:lb[uffer][!] [bufnr]	Same as ":cbuffer", except the location list for the
			current window is used instead of the quickfix list.

						*:cgetb* *:cgetbuffer*
:cgetb[uffer] [bufnr]	Read the error list from the current buffer.  Just
			like ":cbuffer" but don't jump to the first error.

						*:lgetb* *:lgetbuffer*
:lgetb[uffer] [bufnr]	Same as ":cgetbuffer", except the location list for
			the current window is used instead of the quickfix
			list.

						*:cad* *:cadd* *:caddbuffer*
:cad[dbuffer] [bufnr]	Read the error list from the current buffer and add
			the errors to the current quickfix list.  If a
			quickfix list is not present, then a new list is
			created. Otherwise, same as ":cbuffer".

							*:laddb* *:laddbuffer*
:laddb[uffer] [bufnr]	Same as ":caddbuffer", except the location list for
			the current window is used instead of the quickfix
			list.

							*:cex* *:cexpr* *E777*
:cex[pr][!] {expr}	Create a quickfix list using the result of {expr} and
			jump to the first error.
			If {expr} is a String, then each newline terminated
			line in the String is processed using the global value
			of 'errorformat' and the result is added to the
			quickfix list.
			If {expr} is a List, then each String item in the list
			is processed and added to the quickfix list.  Non
			String items in the List are ignored.
			See |:cc| for [!].
			Examples:
				:cexpr system('grep -n xyz *')
				:cexpr getline(1, '$')

							*:lex* *:lexpr*
:lex[pr][!] {expr}	Same as |:cexpr|, except the location list for the
			current window is used instead of the quickfix list.

							*:cgete* *:cgetexpr*
:cgete[xpr] {expr}	Create a quickfix list using the result of {expr}.
			Just like |:cexpr|, but don't jump to the first error.

							*:lgete* *:lgetexpr*
:lgete[xpr] {expr}	Same as |:cgetexpr|, except the location list for the
			current window is used instead of the quickfix list.

							*:cadde* *:caddexpr*
:cadde[xpr] {expr}	Evaluate {expr} and add the resulting lines to the
			current quickfix list. If a quickfix list is not
			present, then a new list is created. The current
			cursor position will not be changed. See |:cexpr| for
			more information.
			Example:
    :g/mypattern/caddexpr expand("%") .. ":" .. line(".") ..  ":" .. getline(".")

						*:lad* *:addd* *:laddexpr*
:lad[dexpr] {expr}	Same as ":caddexpr", except the location list for the
			current window is used instead of the quickfix list.

							*:cl* *:clist*
:cl[ist] [from] [, [to]]
			List all errors that are valid |quickfix-valid|.
			If numbers [from] and/or [to] are given, the respective
			range of errors is listed.  A negative number counts
			from the last error backwards, -1 being the last error.
			The |:filter| command can be used to display only the
			quickfix entries matching a supplied pattern. The
			pattern is matched against the filename, module name,
			pattern and text of the entry.

:cl[ist] +{count}	List the current and next {count} valid errors.  This
			is similar to ":clist from from+count", where "from"
			is the current error position.

:cl[ist]! [from] [, [to]]
			List all errors.

:cl[ist]! +{count}	List the current and next {count} error lines.  This
			is useful to see unrecognized lines after the current
			one.  For example, if ":clist" shows:
        8384 testje.java:252: error: cannot find symbol
			Then using ":cl! +3" shows the reason:
        8384 testje.java:252: error: cannot find symbol
        8385:   ZexitCode = Fmainx();
        8386:               ^
        8387:   symbol:   method Fmainx()

:lli[st] [from] [, [to]]				*:lli* *:llist*
			Same as ":clist", except the location list for the
			current window is used instead of the quickfix list.

:lli[st]! [from] [, [to]]
			List all the entries in the location list for the
			current window.

If you insert or delete lines, mostly the correct error location is still
found because hidden marks are used.  Sometimes, when the mark has been
deleted for some reason, the message "line changed" is shown to warn you that
the error location may not be correct.  If you quit Vim and start again the
marks are lost and the error locations may not be correct anymore.

Two autocommands are available for running commands before and after a
quickfix command (':make', ':grep' and so on) is executed. See
|QuickFixCmdPre| and |QuickFixCmdPost| for details.

						*QuickFixCmdPost-example*
When 'encoding' differs from the locale, the error messages may have a
different encoding from what Vim is using.  To convert the messages you can
use this code:
	function QfMakeConv()
	   let qflist = getqflist()
	   for i in qflist
	      let i.text = iconv(i.text, "cp936", "utf-8")
	   endfor
	   call setqflist(qflist)
	endfunction

	au QuickfixCmdPost make call QfMakeConv()
Another option is using 'makeencoding'.

							*quickfix-title*
Every quickfix and location list has a title. By default the title is set to
the command that created the list. The |getqflist()| and |getloclist()|
functions can be used to get the title of a quickfix and a location list
respectively. The |setqflist()| and |setloclist()| functions can be used to
modify the title of a quickfix and location list respectively. Examples:
	call setqflist([], 'a', {'title' : 'Cmd output'})
	echo getqflist({'title' : 1})
	call setloclist(3, [], 'a', {'title' : 'Cmd output'})
	echo getloclist(3, {'title' : 1})

							*quickfix-index*
When you jump to a quickfix/location list entry using any of the quickfix
commands (e.g. |:cc|, |:cnext|, |:cprev|, etc.), that entry becomes the
currently selected entry. The index of the currently selected entry in a
quickfix/location list can be obtained using the getqflist()/getloclist()
functions. Examples:
	echo getqflist({'idx' : 0}).idx
	echo getqflist({'id' : qfid, 'idx' : 0}).idx
	echo getloclist(2, {'idx' : 0}).idx

For a new quickfix list, the first entry is selected and the index is 1.  Any
entry in any quickfix/location list can be set as the currently selected entry
using the setqflist() function. Examples:
	call setqflist([], 'a', {'idx' : 12})
	call setqflist([], 'a', {'id' : qfid, 'idx' : 7})
	call setloclist(1, [], 'a', {'idx' : 7})

							*quickfix-size*
You can get the number of entries (size) in a quickfix and a location list
using the |getqflist()| and |getloclist()| functions respectively. Examples:
	echo getqflist({'size' : 1})
	echo getloclist(5, {'size' : 1})

							*quickfix-context*
Any Vim type can be associated as a context with a quickfix or location list.
The |setqflist()| and the |setloclist()| functions can be used to associate a
context with a quickfix and a location list respectively. The |getqflist()|
and the |getloclist()| functions can be used to retrieve the context of a
quickfix and a location list respectively. This is useful for a Vim plugin
dealing with multiple quickfix/location lists.
Examples:

	let somectx = {'name' : 'Vim', 'type' : 'Editor'}
	call setqflist([], 'a', {'context' : somectx})
	echo getqflist({'context' : 1})

	let newctx = ['red', 'green', 'blue']
	call setloclist(2, [], 'a', {'id' : qfid, 'context' : newctx})
	echo getloclist(2, {'id' : qfid, 'context' : 1})

							*quickfix-parse*
You can parse a list of lines using 'errorformat' without creating or
modifying a quickfix list using the |getqflist()| function. Examples:
	echo getqflist({'lines' : ["F1:10:Line10", "F2:20:Line20"]})
	echo getqflist({'lines' : systemlist('grep -Hn quickfix *')})
This returns a dictionary where the "items" key contains the list of quickfix
entries parsed from lines. The following shows how to use a custom
'errorformat' to parse the lines without modifying the 'errorformat' option:
	echo getqflist({'efm' : '%f#%l#%m', 'lines' : ['F1#10#Line']})


EXECUTE A COMMAND IN ALL THE BUFFERS IN QUICKFIX OR LOCATION LIST:
							*:cdo*
:cdo[!] {cmd}		Execute {cmd} in each valid entry in the quickfix list.
			It works like doing this:
				:cfirst
				:{cmd}
				:cnext
				:{cmd}
				etc.
 			When the current file can't be |abandon|ed and the [!]
			is not present, the command fails.
			When going to the next entry fails execution stops.
			The last buffer (or where an error occurred) becomes
			the current buffer.
			{cmd} can contain '|' to concatenate several commands.

			Only valid entries in the quickfix list are used.
			A range can be used to select entries, e.g.:
				:10,$cdo cmd
 			To skip entries 1 to 9.

			Note: While this command is executing, the Syntax
			autocommand event is disabled by adding it to
			'eventignore'.  This considerably speeds up editing
			each buffer.
			Also see |:bufdo|, |:tabdo|, |:argdo|, |:windo|,
			|:ldo|, |:cfdo| and |:lfdo|.

							*:cfdo*
:cfdo[!] {cmd}		Execute {cmd} in each file in the quickfix list.
			It works like doing this:
				:cfirst
				:{cmd}
				:cnfile
				:{cmd}
				etc.
 			Otherwise it works the same as `:cdo`.

							*:ldo*
:ld[o][!] {cmd}		Execute {cmd} in each valid entry in the location list
			for the current window.
			It works like doing this:
				:lfirst
				:{cmd}
				:lnext
				:{cmd}
				etc.
 			Only valid entries in the location list are used.
			Otherwise it works the same as `:cdo`.

							*:lfdo*
:lfdo[!] {cmd}		Execute {cmd} in each file in the location list for
			the current window.
			It works like doing this:
				:lfirst
				:{cmd}
				:lnfile
				:{cmd}
				etc.
 			Otherwise it works the same as `:ldo`.

FILTERING A QUICKFIX OR LOCATION LIST:
				    *cfilter-plugin* *:Cfilter* *:Lfilter*
If you have too many entries in a quickfix list, you can use the cfilter
plugin to reduce the number of entries.  Load the plugin with:

    packadd cfilter

Then you can use the following commands to filter a quickfix/location list:

    :Cfilter[!] /{pat}/
    :Lfilter[!] /{pat}/

The |:Cfilter| command creates a new quickfix list from the entries matching
{pat} in the current quickfix list. {pat} is a Vim |regular-expression|
pattern. Both the file name and the text of the entries are matched against
{pat}. If the optional ! is supplied, then the entries not matching {pat} are
used. The pattern can be optionally enclosed using one of the following
characters: ', ", /. If the pattern is empty, then the last used search
pattern is used.

The |:Lfilter| command does the same as |:Cfilter| but operates on the current
location list.

The current quickfix/location list is not modified by these commands, so you
can go back to the unfiltered list using the |:colder|/|:lolder| command.

=============================================================================
2. The error window					*quickfix-window*

					    *:cope* *:copen* *w:quickfix_title*
:cope[n] [height]	Open a window to show the current list of errors.

			When [height] is given, the window becomes that high
			(if there is room).  When [height] is omitted the
			window is made ten lines high.

			If there already is a quickfix window, it will be made
			the current window.  It is not possible to open a
			second quickfix window.  If [height] is given the
			existing window will be resized to it.

							*quickfix-buffer*
			The window will contain a special buffer, with
			'buftype' equal to "quickfix".  Don't change this!
			The window will have the w:quickfix_title variable set
			which will indicate the command that produced the
			quickfix list. This can be used to compose a custom
			status line if the value of 'statusline' is adjusted
			properly. Whenever this buffer is modified by a
			quickfix command or function, the |b:changedtick|
			variable is incremented.  You can get the number of
			this buffer using the getqflist() and getloclist()
			functions by passing the "qfbufnr" item. For a
			location list, this buffer is wiped out when the
			location list is removed.

							*:lop* *:lopen*
:lop[en] [height]	Open a window to show the location list for the
			current window. Works only when the location list for
			the current window is present.  You can have more than
			one location window opened at a time.  Otherwise, it
			acts the same as ":copen".

							*:ccl* *:cclose*
:ccl[ose]		Close the quickfix window.

							*:lcl* *:lclose*
:lcl[ose]		Close the window showing the location list for the
			current window.

							*:cw* *:cwindow*
:cw[indow] [height]	Open the quickfix window when there are recognized
			errors.  If the window is already open and there are
			no recognized errors, close the window.

							*:lw* *:lwindow*
:lw[indow] [height]	Same as ":cwindow", except use the window showing the
			location list for the current window.

							*:cbo* *:cbottom*
:cbo[ttom]		Put the cursor in the last line of the quickfix window
			and scroll to make it visible.  This is useful for
			when errors are added by an asynchronous callback.
			Only call it once in a while if there are many
			updates to avoid a lot of redrawing.

							*:lbo* *:lbottom*
:lbo[ttom]		Same as ":cbottom", except use the window showing the
			location list for the current window.

Normally the quickfix window is at the bottom of the screen.  If there are
vertical splits, it's at the bottom of the rightmost column of windows.  To
make it always occupy the full width:
	:botright cwindow
You can move the window around with |window-moving| commands.
For example, to move it to the top: CTRL-W K
The 'winfixheight' option will be set, which means that the window will mostly
keep its height, ignoring 'winheight' and 'equalalways'.  You can change the
height manually (e.g., by dragging the status line above it with the mouse).

In the quickfix window, each line is one error.  The line number is equal to
the error number.  The current entry is highlighted with the QuickFixLine
highlighting.  You can change it to your liking, e.g.:
	:hi QuickFixLine ctermbg=Yellow guibg=Yellow

You can use ":.cc" to jump to the error under the cursor.
Hitting the <Enter> key or double-clicking the mouse on a line has the same
effect.  The file containing the error is opened in the window above the
quickfix window.  If there already is a window for that file, it is used
instead.  If the buffer in the used window has changed, and the error is in
another file, jumping to the error will fail.  You will first have to make
sure the window contains a buffer which can be abandoned.

When you select a file from the quickfix window, the following steps are used
to find a window to edit the file:

1. If a window displaying the selected file is present in the current tabpage
   (starting with the window before the quickfix window), then that window is
   used.
2. If the above step fails and if 'switchbuf' contains "usetab" and a window
   displaying the selected file is present in any one of the tabpages
   (starting with the first tabpage) then that window is used.
3. If the above step fails then a window in the current tabpage displaying a
   buffer with 'buftype' not set (starting with the window before the quickfix
   window) is used.
4. If the above step fails and if 'switchbuf' contains "uselast", then the
   previously accessed window is used.
5. If the above step fails then the window before the quickfix window is used.
   If there is no previous window, then the window after the quickfix window
   is used.
6. If the above step fails, then a new horizontally split window above the
   quickfix window is used.

					*CTRL-W_<Enter>* *CTRL-W_<CR>*
You can use CTRL-W <Enter> to open a new window and jump to the error there.

When the quickfix window has been filled, two autocommand events are
triggered.  First the 'filetype' option is set to "qf", which triggers the
FileType event (also see |qf.vim|).  Then the BufReadPost event is triggered,
using "quickfix" for the buffer name.  This can be used to perform some action
on the listed errors.  Example:
	au BufReadPost quickfix  setlocal modifiable
		\ | silent exe 'g/^/s//\=line(".") .. " "/'
		\ | setlocal nomodifiable
This prepends the line number to each line.  Note the use of "\=" in the
substitute string of the ":s" command, which is used to evaluate an
expression.
The BufWinEnter event is also triggered, again using "quickfix" for the buffer
name.

Note: When adding to an existing quickfix list the autocommand are not
triggered.

Note: Making changes in the quickfix window has no effect on the list of
errors.  'modifiable' is off to avoid making changes.  If you delete or insert
lines anyway, the relation between the text and the error number is messed up.
If you really want to do this, you could write the contents of the quickfix
window to a file and use ":cfile" to have it parsed and used as the new error
list.

						*location-list-window*
The location list window displays the entries in a location list.  When you
open a location list window, it is created below the current window and
displays the location list for the current window.  The location list window
is similar to the quickfix window, except that you can have more than one
location list window open at a time. When you use a location list command in
this window, the displayed location list is used.

When you select a file from the location list window, the following steps are
used to find a window to edit the file:

1. If a non-quickfix window associated with the location list is present in
   the current tabpage, then that window is used.
2. If the above step fails and if the file is already opened in another window
   in the current tabpage, then that window is used.
3. If the above step fails and 'switchbuf' contains "usetab" and if the file
   is opened in a window in any one of the tabpages, then that window is used.
4. If the above step fails then a window in the current tabpage showing a
   buffer with 'buftype' not set is used.
5. If the above step fails, then the file is edited in a new window.

In all of the above cases, if the location list for the selected window is not
yet set, then it is set to the location list displayed in the location list
window.

							*quickfix-window-ID*
You can use the |getqflist()| and |getloclist()| functions to obtain the
window ID of the quickfix window and location list window respectively (if
present).  Examples:
	echo getqflist({'winid' : 1}).winid
	echo getloclist(2, {'winid' : 1}).winid

							*getqflist-examples*
The |getqflist()| and |getloclist()| functions can be used to get the various
attributes of a quickfix and location list respectively. Some examples for
using these functions are below:

    " get the title of the current quickfix list
    :echo getqflist({'title' : 0}).title

    " get the identifier of the current quickfix list
    :let qfid = getqflist({'id' : 0}).id

    " get the identifier of the fourth quickfix list in the stack
    :let qfid = getqflist({'nr' : 4, 'id' : 0}).id

    " check whether a quickfix list with a specific identifier exists
    :if getqflist({'id' : qfid}).id == qfid

    " get the index of the current quickfix list in the stack
    :let qfnum = getqflist({'nr' : 0}).nr

    " get the items of a quickfix list specified by an identifier
    :echo getqflist({'id' : qfid, 'items' : 0}).items

    " get the number of entries in a quickfix list specified by an id
    :echo getqflist({'id' : qfid, 'size' : 0}).size

    " get the context of the third quickfix list in the stack
    :echo getqflist({'nr' : 3, 'context' : 0}).context

    " get the number of quickfix lists in the stack
    :echo getqflist({'nr' : '$'}).nr

    " get the number of times the current quickfix list is changed
    :echo getqflist({'changedtick' : 0}).changedtick

    " get the current entry in a quickfix list specified by an identifier
    :echo getqflist({'id' : qfid, 'idx' : 0}).idx

    " get all the quickfix list attributes using an identifier
    :echo getqflist({'id' : qfid, 'all' : 0})

    " parse text from a List of lines and return a quickfix list
    :let myList = ["a.java:10:L10", "b.java:20:L20"]
    :echo getqflist({'lines' : myList}).items

    " parse text using a custom 'efm' and return a quickfix list
    :echo getqflist({'lines' : ['a.c#10#Line 10'], 'efm':'%f#%l#%m'}).items

    " get the quickfix list window id
    :echo getqflist({'winid' : 0}).winid

    " get the quickfix list window buffer number
    :echo getqflist({'qfbufnr' : 0}).qfbufnr

    " get the context of the current location list
    :echo getloclist(0, {'context' : 0}).context

    " get the location list window id of the third window
    :echo getloclist(3, {'winid' : 0}).winid

    " get the location list window buffer number of the third window
    :echo getloclist(3, {'qfbufnr' : 0}).qfbufnr

    " get the file window id of a location list window (winnr: 4)
    :echo getloclist(4, {'filewinid' : 0}).filewinid

							*setqflist-examples*
The |setqflist()| and |setloclist()| functions can be used to set the various
attributes of a quickfix and location list respectively. Some examples for
using these functions are below:

    " create an empty quickfix list with a title and a context
    :let t = 'Search results'
    :let c = {'cmd' : 'grep'}
    :call setqflist([], ' ', {'title' : t, 'context' : c})

    " set the title of the current quickfix list
    :call setqflist([], 'a', {'title' : 'Mytitle'})

    " change the current entry in the list specified by an identifier
    :call setqflist([], 'a', {'id' : qfid, 'idx' : 10})

    " set the context of a quickfix list specified by an identifier
    :call setqflist([], 'a', {'id' : qfid, 'context' : {'val' : 100}})

    " create a new quickfix list from a command output
    :call setqflist([], ' ', {'lines' : systemlist('grep -Hn main *.c')})

    " parse text using a custom efm and add to a particular quickfix list
    :call setqflist([], 'a', {'id' : qfid,
		\ 'lines' : ["a.c#10#L10", "b.c#20#L20"], 'efm':'%f#%l#%m'})

    " add items to the quickfix list specified by an identifier
    :let newItems = [{'filename' : 'a.txt', 'lnum' : 10, 'text' : "Apple"},
		    \ {'filename' : 'b.txt', 'lnum' : 20, 'text' : "Orange"}]
    :call setqflist([], 'a', {'id' : qfid, 'items' : newItems})

    " empty a quickfix list specified by an identifier
    :call setqflist([], 'r', {'id' : qfid, 'items' : []})

    " free all the quickfix lists in the stack
    :call setqflist([], 'f')

    " set the title of the fourth quickfix list
    :call setqflist([], 'a', {'nr' : 4, 'title' : 'SomeTitle'})

    " create a new quickfix list at the end of the stack
    :call setqflist([], ' ', {'nr' : '$',
			\ 'lines' : systemlist('grep -Hn class *.java')})

    " create a new location list from a command output
    :call setloclist(0, [], ' ', {'lines' : systemlist('grep -Hn main *.c')})

    " replace the location list entries for the third window
    :call setloclist(3, [], 'r', {'items' : newItems})

=============================================================================
3. Using more than one list of errors			*quickfix-error-lists*

So far has been assumed that there is only one list of errors.  Actually the
ten last used lists are remembered.  When starting a new list, the previous
ones are automatically kept.  Two commands can be used to access older error
lists.  They set one of the existing error lists as the current one.

						*:colder* *:col* *E380*
:col[der] [count]	Go to older error list.  When [count] is given, do
			this [count] times.  When already at the oldest error
			list, an error message is given.

						*:lolder* *:lol*
:lol[der] [count]	Same as `:colder`, except use the location list for
			the current window instead of the quickfix list.

						*:cnewer* *:cnew* *E381*
:cnew[er] [count]	Go to newer error list.  When [count] is given, do
			this [count] times.  When already at the newest error
			list, an error message is given.

						*:lnewer* *:lnew*
:lnew[er] [count]	Same as `:cnewer`, except use the location list for
			the current window instead of the quickfix list.

						*:chistory* *:chi*
:[count]chi[story]	Show the list of error lists.  The current list is
			marked with ">".  The output looks like:
			  error list 1 of 3; 43 errors   :make
			> error list 2 of 3; 0 errors    :helpgrep tag
			  error list 3 of 3; 15 errors   :grep ex_help *.c

			When [count] is given, then the count'th quickfix
			list is made the current list. Example:
				" Make the 4th quickfix list current
				:4chistory

						*:lhistory* *:lhi*
:[count]lhi[story]	Show the list of location lists, otherwise like
			`:chistory`.

When adding a new error list, it becomes the current list.

When ":colder" has been used and ":make" or ":grep" is used to add a new error
list, one newer list is overwritten.  This is especially useful if you are
browsing with ":grep" |grep|.  If you want to keep the more recent error
lists, use ":cnewer 99" first.

To get the number of lists in the quickfix and location list stack, you can
use the |getqflist()| and |getloclist()| functions respectively with the list
number set to the special value '$'. Examples:
	echo getqflist({'nr' : '$'}).nr
	echo getloclist(3, {'nr' : '$'}).nr
To get the number of the current list in the stack:
	echo getqflist({'nr' : 0}).nr

=============================================================================
4. Using :make						*:make_makeprg*

							*:mak* *:make*
:mak[e][!] [arguments]	1. All relevant |QuickFixCmdPre| autocommands are
			   executed.
			2. If the 'autowrite' option is on, write any changed
			   buffers
			3. An errorfile name is made from 'makeef'.  If
			   'makeef' doesn't contain "##", and a file with this
			   name already exists, it is deleted.
			4. The program given with the 'makeprg' option is
			   started (default "make") with the optional
			   [arguments] and the output is saved in the
			   errorfile (for Unix it is also echoed on the
			   screen).
			5. The errorfile is read using 'errorformat'.
			6. All relevant |QuickFixCmdPost| autocommands are
			   executed.  See example below.
			7. If [!] is not given the first error is jumped to.
			8. The errorfile is deleted.
			9. You can now move through the errors with commands
			   like |:cnext| and |:cprevious|, see above.
			This command does not accept a comment, any "
			characters are considered part of the arguments.
			If the encoding of the program output differs from the
			'encoding' option, you can use the 'makeencoding'
			option to specify the encoding.

							*:lmak* *:lmake*
:lmak[e][!] [arguments]
			Same as ":make", except the location list for the
			current window is used instead of the quickfix list.

The ":make" command executes the command given with the 'makeprg' option.
This is done by passing the command to the shell given with the 'shell'
option.  This works almost like typing

	":!{makeprg} [arguments] {shellpipe} {errorfile}".

{makeprg} is the string given with the 'makeprg' option.  Any command can be
used, not just "make".  Characters '%' and '#' are expanded as usual on a
command-line.  You can use "%<" to insert the current file name without
extension, or "#<" to insert the alternate file name without extension, for
example:
   :set makeprg=make\ #<.o

[arguments] is anything that is typed after ":make".
{shellpipe} is the 'shellpipe' option.
{errorfile} is the 'makeef' option, with ## replaced to make it unique.

The placeholder "$*" can be used for the argument list in {makeprg} if the
command needs some additional characters after its arguments.  The $* is
replaced then by all arguments.  Example:
   :set makeprg=latex\ \\\\nonstopmode\ \\\\input\\{$*}
or simpler
   :let &mp = 'latex \\nonstopmode \\input\{$*}'
"$*" can be given multiple times, for example:
   :set makeprg=gcc\ -o\ $*\ $*

The 'shellpipe' option defaults to "2>&1| tee" for Win32.
This means that the output of the compiler is saved in a file and not shown on
the screen directly.  For Unix "| tee" is used.  The compiler output is shown
on the screen and saved in a file the same time.  Depending on the shell used
"|& tee" or "2>&1| tee" is the default, so stderr output will be included.

If 'shellpipe' is empty, the {errorfile} part will be omitted.  This is useful
for compilers that write to an errorfile themselves.


Using QuickFixCmdPost to fix the encoding

It may be that 'encoding' is set to an encoding that differs from the messages
your build program produces.  This example shows how to fix this after Vim has
read the error messages:

	function QfMakeConv()
	   let qflist = getqflist()
	   for i in qflist
	      let i.text = iconv(i.text, "cp936", "utf-8")
	   endfor
	   call setqflist(qflist)
	endfunction

	au QuickfixCmdPost make call QfMakeConv()

(Example by Faque Cheng)
Another option is using 'makeencoding'.
