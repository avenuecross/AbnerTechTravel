Keil:
生成bin文件<br>
fromelf –bin –output=xx.bin xx.axf<br>

生成反汇编文件<br>
fromelf –text -a -c –output=xx.txt xx.axf // Old version command<br>

Combined with keil compiler stupidity. What it does is that it combines project path + relative resource path.
So for example:
project path: projects/projectX/toolchain/keil5/projectX.uvprojx
src path is : projects/projectX/src/a/b/src.c
Then what is used internally by armcc is:
projects/projectX/toolchain/keil5/../../a/b/src.c

Solution for arm is to go to: Project->options->C/C++->Misc Controls and add "--reduce_paths".
