# Rootkit-Hunter

<h2>Introduction to Rootkit Hunter</h2>

Rootkit Hunter is a Unix based open-source tool written in bash and pre-installed in some Unix distributions. It is used for scanning systems for potential rootkits or backdoors. This is done by comparing files in a system to known rootkits, searching for hidden files, detecing executables with strange permissions, and searching for suspicious strings in the kernel. 

<strong>What is a rootkit?</strong>

Rootkits are self hiding program that gain root access on a computer system. Rootkits usually come hidden inside of cracked programs, malicious drivers, or any other sort of unsuspecting program. Once downloaded onto a system they typically hook into the kernel to be able to evade detection. While not all rootkits are bad, most of them tend to be malicious. 

<hr>
<h2>Using Rootkit Hunter to detect rootkits</h2>

This demonstration will be going over how to install Rootkit Hunter, as well as how to use Rootkit Hunter to detect possible rootkits in a computer system. The goal of this demonstration is to expand the users knowledge of system vulnerability management, and detecting possible threats.

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

<em>Note: if running the command above provides the error: "Invalid SCRIPTWHITELIST configuration option: Non-existent pathname: /bin/which" or any other subsequent "Invalid SCRIPTWHITELIST" error, this can be fixed by going into the /etc/rkhunter.conf file and looking for "SCRIPTWHITELIST <pathname>" and commenting out that line. </em>
<hr>

![update](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/5cd28104-c0e3-447c-a667-72b5b7f8cf51)
<hr>

To start Rootkit Hunter use:
<code>rkhunter --check</code>

This command scans through all directories for anomalous files permissions, hidden files, and any files/executables that may match with known rootkits. This may take some time depending on how many files and directories there are.

![rkrun](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/6ae2d8e2-08d7-46c0-84ae-101b414be41d)

Once scanning is done, Rootkit Hunter will save all the information in a log file. To open this file run the command:
<code>nano /var/log/rkhunter.log</code>
<hr>

![nan](https://github.com/victorF29/Rootkit-Hunter/assets/145622790/fd258846-5825-4fd0-ab63-0fff9d57a6e3)
<hr>

After checking the logs of the previous scan, rootkit hunter may give you warnings for specific files or directories. Before removing or deleting any of these files, make sure to check first whether the file is genuinely malicious or just a false positive. Rootkit Hunter will sometimes pick up false positives that do not require any action.
