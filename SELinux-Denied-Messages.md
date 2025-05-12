#SELinux Basics - Denied Messages Lab
Date: May 11, 2025
OBJECTIVE: Understand how SELinux blocks access and identify denial events using log files.

TOOLS USED: * OS: CentOS(Virtual Machine)
            * COMMANDS USED: getenforce, sestatus, setenforce 0(Permissive) & 1(Enforcing), sudo cat /var/log/audit/audit.log | less, sudo grep denied /var/log/audit/audit.log | less

STEPS COMPLETED:
                1. CHECK THE SELinux STATUS
                I wanted to check SELinux status & one way to do that was using the command "getenforce" # Output: Enforcing
                 Another way to check SELinux's status would be using the command "sestatus," which would show if SELinux is enforcing, permissive, or disabled on a larger scale. (You can see SELinux's status, mount, root directory, and current mode.)

  2. SWITCHING MODES: 
   After learning how to see SELinux status, I took time out to figure out how to change it. The command that I use to change the status is "setenforce 0" or "setenforce 1".
  setonforce 0 = Permissive, setonforce 1 = Enforcing. #For this lab, we wanted the status to be on Enforcing.

  3. PERMISSION DENIED:
   My next goal in the lab was to read the logs "/var/log/audit/audit.log". While testing my limits, going through each file, I got denied permission when I tried to access the file "audit". After struggling to understand what the problem could be, I learned that the file was owned by root, and as a regular user, I didn't have permission to read it.

 4. ANOTHER WAY TO ACCESS THE LOGS:
    I wanted to access the files, so I learned a new command that could give me access: "sudo cat /var/log/audit/audit.log | less." This command lets me get past because of the power of the command "sudo," and the command cat allows me to see the file. 
    Another command that showed me that the permissions that were denied gave me only two reasons for each denial was "sudo grep denied /var/log/audit/audit.log | less". 1. Missing type enforcement (TE) allows rule & 2. Was caused by: Unknown- would be allowed by active policy.

 5.  OUTCOME & KEY LEARNINGS:
I learned in this lab that SELinux  enforcing mode actively denies access based on policy.
Logs for denied events live in /var/log/audit/audit.log.
Sudo and grep are powerful tools for filtering and understanding these logs.
