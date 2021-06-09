# r
r program launcher for cp/m 2.2, Inspired by TOPS-10

When I started using Mike Douglas' excellent CP/M 2.2 implementation for the Altair Hard Disk
on the Altair-Duino, I noted that the prompt had been patched, and the program launch had been
patched.

The program launch patch however failed if launching a program larger than one extent.
In other words, launching MBASIC.COM would cause a crash! Also, the search did not work
when running CP/NET!

I unpatched the BDOS, and wrote R.COM This looks at drive A, user 0 for all COM files.
If the COM file is not there, it opens A0:COMMAND.LBR and runs the command if found.

R.COM is slightly smaller than LRUN.COM (7 sectors). R.COM loads any program that the
CCP would load. It also supports small programs doing a "RET" back to CCP (like STAT.COM).
This is supported for both CCP and CP/NET 1.2. R.COM is aware of programs that stay
resident (like XSUB) and uses a bit less memory in that case because it no longer has
to protect the (already protected) CCP.

The COMMAND.LBR load facility was added because my drive A: was filling up! The minimum
file size was 4K, meaning that an average of 2K was being lost for each COM file.
Bundling into COMMAND.LBR and using LRUN seemed sensible. But, I don't want think
of launching with LRUN and launching without differently. I decided to incorporate
COMMAND.LBR search and run.

Do what you will with it -- I have been using this for months, and it appears ok.

Change requests are welcome.
