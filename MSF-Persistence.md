Meterpreter Service
a11y.text Meterpreter Service
Understanding the Metasploit Meterpreter
a11y.text Understanding the Metasploit Meterpreter
After going through all the hard work of exploiting a system, it’s often a good idea to leave yourself an easier way back into the system for later use. This way, if the service you initially exploited is down or patched, you can still gain access to the system. Metasploit has a Meterpreter script, persistence.rb, that will create a Meterpreter service that will be available to you even if the remote system is rebooted.

One word of warning here before we go any further. The persistent Meterpreter as shown here requires no authentication. This means that anyone that gains access to the port could access your back door! This is not a good thing if you are conducting a penetration test, as this could be a significant risk. In a real world situation, be sure to exercise the utmost caution and be sure to clean up after yourself when the engagement is done.

Once we’ve initially exploited the host, we run persistence with the -h switch to see which options are available:
