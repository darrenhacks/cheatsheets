# nmap
## port statuses

+ **open**: A service is listening on the port.
+ **closed**: A port is accessible, but no service is listening on it.
+ **filtered**: The port cannot be reached. Either something is blocking Nmap from reaching the port or responses are blocked from coming back.
+ **unfiltered**: The port is accessible, but Nmap can't determine if it is open or closed. Only comes up in an ACK scan.
+ **open|filtered**: Nmap can't decide if the port is open or it is filtered.
+ **closed|filtered**: Nmap can't decide if the port is closed or filtered.

## scan types

|flag|description|
|---|---|
|-sT|Connect scan. This will do the full TCP handshake and send a RTS, ACK packet to close the connection. When you are not root, this is the default scan type. It is also the only scan type you can run when not root.|
|-sS|SYN scan. This will set a RST as soon as it gets the SYN, ACK response from the remote. This is the default scan type when run as root.|
|-sU|UDP scan. Sends a UDP packet. This relies on the remote not sending a response packet from closed ports.|
|-sN|NULL scan. Sends a packet with no TCP flags set. An open or filtered port will not send a response.|
|-sF|FIN scan. This has a similar effect in that an open or filtered port will not send a response.|
|-sX|Christmas scan. Set the FIN, PSH, and URG flags. It also has a similar effect in that an open or filtered port will not send a response.|
|-sM|Maimon scan. This one mostly won't work except in some BSD-based systems which will not send a response if the port is open.|
|-sA|ACK scan. This is more helpful in determining firewall rules than port status. The response to just sending an ACK should always be a RST. If the firewall is blocking this port, then you won't get anything back.|
|-sW|Window scan. Sends an ACK and reads the window field of the RST. In some systems, this can tell you if the port is open or not.|
|\--scanflags *xyz*|Custom scan. This allows you to set specific flags. Just put the list in, like `--scanflags ACKRSTFIN`.|


## other flags

|flag|description|
|---|---|
|-F|Fast scan. Only scan the most common 100 ports. Without this, Nmap will default to 1 through 1,000.|
|\--top-ports *x*|Will scan the *x* most common ports.|
|-p|Say which ports to scan. There are a lot of options like `-p-1000` for ports less than 1000, `-p1000-` for ports greater than 1000, `-p10-100` for ports 10 through 100, and `-p10,20,30` to only scan ports 10, 20, and 30.|
|-Pn|Don't ping the host before running the scan.|
|-r|Scans the ports in consecutive order rather than random order.|
|-T<0-5>|Controls the timing of the scan. 0 is the slowest where 5 is the fastest. 3 is the default.|
|-sV|Service detection. Try to identify the service running on the port and its version. This will force a full TCP handshake.|
|\--version-intensity *x*|Use this in conjunction with `-sV` to set the intensity with which it will do the scan. *X* should be between 0 and 9.|
|\--version-light|Same as `--version-intensity 2`.|
|\--version-all|Same as `--version-intensity 9`.|
|-O|Detect OS and version. This may or may not be accurate.|
|\--traceroute|Add a traceroute to the output.|
|\--min-rate *x*|Send at least *x* packets per second.|
|\--max-rate *x*|Send at most *x* packets per second.|
|\--min-parallelism *x*|Use at least *x* probes running at a time.|
|\--max-parallelism *x*|Use at most *x* probes running at a time.|
|-f, -ff|Split the data portion of the packet into 8 (`-f`) or 16 (`-ff`) bytes. This may help get around an Intrusion Detection System (IDS).|
|-D *x,y,z*|Sends decoy packets. *X, y, z* can be IP addresses, `RND` (pick a random one), or `ME` (the machine you're running on).|
|-S *IP*|Spoof an IP address. This will make the traffic look like it's coming from the machine whose IP address is *IP*. You'll need a way to capture the traffic on the other machine to make this useful.|
|-sI *IP*|Zombie scan. Similar to the above, it makes it look like traffic is coming from *IP*. In this case, though, you don't have direct access to *IP*, but you can probe it for an indication that the remote host under scan responded.|
|\--reason|How did Nmap come to its conclusion?|
|-v, -vv|Verbose or even more verbose output.|

## scripts
You can run a default set of scripts with `-sC` or `--script=default`. Other broad categories are:

|category|description|
|---|---|
|auth|Authentication related.|
|broadcast|Discover hosts with broadcast messages.|
|brute|Brute-force password guessing.|
|discovery|Retrieve whatever it can figure out.|
|dos|Denial of Service|
|exploit|Tries to exploit vulnerable services.|
|external|Run checks using a third-party service.|
|fuzzer|Run fuzzing attacks.|
|intrusive|More intrusive attacks.|
|malware|Run scans for backdoors.|
|safe|Run scripts that won't crash the remote.|
|version|Retrieve service versions.|
|vuln|Check for vulnerabilities.|

You can also run scripts by name.  They are found in the  `/usr/share/nmap/scripts` directory.

## saving output

You can save output in a format that looks basically like the command-line with `-oN <filename>`.

You can save output in a format that it is easier to use `grep` with by adding `-oG <filename>`.

You can save output in an XML format with `-oX <filename>`.

You can save all three with `-oA <filename>`. Not sure how the output looks.

There is a script kiddie format too, but it is not useful.
