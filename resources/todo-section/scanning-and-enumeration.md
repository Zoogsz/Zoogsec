# Scanning and Enumeration

#### Useful NMAP one liner commands



<pre class="language-bash"><code class="lang-bash">nmap -T4 -p- -A -oN &#x3C;DumpFile> -iL &#x3C;targetsFile>

nmap -sS -Pn -sU -v &#x3C;IP> --open -oA &#x3C;dumpFile>

nmap -sS -p1-65535 -v -Pn -sV -iL hosts-live.txt -oA full-syn-svc
<strong>##further setup##
</strong>smb
grep '445/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-smb.txt
 
https
grep '443/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-ssl.txt
 
ssh
grep '22/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-ssh.txt
 
Telnet
grep '23/open/tcp//' ./nmap/s_u_live.gnmap | cut -d " " -f2 | sort -uV | tee -a ./nmap/hosts-telnet.txt
++common ports + vulns
</code></pre>
