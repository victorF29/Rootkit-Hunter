# Rootkit-Hunter

<h2>Introduction to Rootkit Hunter</h2>

Rootkit Hunter is a Unix based open-source tool written in bash and pre-installed in some Unix distributions. It is used for scanning systems for potential rootkits or backdoors. This is done by comparing files in a system to known rootkits, searching for hidden files, detecing executables with strange permissions, and searching for suspicious strings in the kernel. 

<strong>What is a rootkit?</strong>

Rootkits are self hiding program that gain root access on a computer system. Rootkits usually come hidden inside of cracked programs, malicious drivers, or any other sort of unsuspecting program. Once downloaded onto a system they typically hook into the kernel to be able to evade detection. While not all rootkits are bad, most of them tend to be malicious. 

<hr>
<h2>Using Rootkit Hunter to detect rootkits</h2>

This demonstration will be going over how to install Rootkit Hunter, as well as how to use Rootkit Hunter to detect possible rootkits in a computer system. The goal of this demonstration is to expand the users knowledge of system vulnerability management, system hardening, and detecting possible threats.

<strong>Installing Rootkit Hunter on Linux:</strong>

<em>Note: While these examples use Linux for the installation, the same steps apply to any Unix/Debian distribution. Just with slightly different commands.</em>

Use:
<code>sudo apt install rkhunter</code>

This will begin the installation for Rootkit Hunter (rkhunter).
<hr>

![rkdown](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/62650922-938d-44a7-8f5c-9178098a95d7)
<hr>

Once installed use: 
<code>rkhunter --update</code>

This will update rootkit hunter to the latest version.

<hr>

![update](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/5cd28104-c0e3-447c-a667-72b5b7f8cf51)
<hr>

To start Rootkit Hunter use:
<code>rkhunter --check</code>

This command scans through all directories for anomalous files permissions, hidden files, and any files/executables that may match with known rootkits. This may take some time depending on how many files and directories there are.
<hr>

![rkrun](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/6ae2d8e2-08d7-46c0-84ae-101b414be41d)
<hr>

Once scanning is done, Rootkit Hunter will save all the information in a log file. To open this file run the command:
<code>nano /var/log/rkhunter.log</code>

After checking the logs of the previous scan, rootkit hunter may give you warnings for specific files or directories. Before removing or deleting any of these files, make sure to check first whether the file is genuinely malicious or just a false positive. Rootkit Hunter will sometimes pick up false positives that do not require any action.
<hr>

![nan](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/fd258846-5825-4fd0-ab63-0fff9d57a6e3)
<hr>

To set up scheduled scans run:
<code>crontab -e</code>

After running the command it will ask which editor to use, this example will use nano (select 1) since it is more simple to use.

![crotab](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/9a5cad56-234d-4eec-9819-bdfc6198373a)
<hr>

At the bottom of the text page write in the command: 
<code>@daily /usr/bin/rkhunter --cronjob --update --quiet</code>

This command will set it so that Rootkit Hunter runs automatically everyday.
<hr>

<h2>Error fixes</h2>

<strong>"Invalid SCRIPTWHITELIST":</strong>
If running the command above provides the error: "Invalid SCRIPTWHITELIST configuration option: Non-existent pathname: /bin/which" or any other subsequent "Invalid SCRIPTWHITELIST" error, this can be fixed by going into the /etc/rkhunter.conf file and looking for "SCRIPTWHITELIST <pathname>" and commenting out that line.

<strong>Invalid WEB_CMD:</strong>
If running the command above provides the error: "Invalid WEB_CMD configuration option: Relative pathname: "/bin/false"" this can be fixed by going into the /etc/rkhunter.conf file and looking for and changing these 3 variables:

<em>MIRRORS_MODE=1 ---> MIRRORS_MODE=0</em>

<em>UPDATE_MIRRORS=0 ---> UPDATE_MIRRORS=1</em>

<em>WEB_CMD="/bin/false" ---> WEB_CMD=""</em>
<hr>

<h2>Concepts of this demonstration</h2>

This demonstration showed how to install and run Rootkit Hunter on a system. As well as showing how Rootkit Hunter can be used to harden a system, detect system vulnerabilities and threats, and system file analysis. Since Rootkit Hunter has the chance for false positives it is best when used along side other rootkit scanners.
