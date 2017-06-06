PRELIMINARIES
a. This procedure has been varified to work on Ubuntu 12.10 Linux. 
b. There is a bug(?) in the kthesis class, which makes the pdf:s take a whole a4-page when using the electronic option. Therefore, don't use this option. 

How to externalize tikz-images using xelatex
1. First run xelatex -shell-escape with the options below. Tikz-mages in the pdf should be replaced with a text. 

%%%% Put this somewhere in your latex preamble %%%%
\usetikzlibrary{external}
\tikzset{external/system call={xelatex -shell-escape \tikzexternalcheckshellescape -halt-on-error -interaction=batchmode -jobname "\image" "\texsource"}}
\tikzexternalize[prefix=tikzfigures/, mode=list and make]
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

2. Run the command in the same folder as your LaTeX files: (Replace 8 below by the number of cores you wich to use)
sed -i 's/\^\^I/\t/g' main.makefile && make -j 8 -f main.makefile

3. Recompile the tex-file with xelatex -shell-escape. Images should now appear in the compiled pdf.
